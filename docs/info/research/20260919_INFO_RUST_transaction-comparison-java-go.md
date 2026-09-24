作成日: 2026-09-19 / STATUS: INFO / TOPIC: RUST

# Rust・Java・Go:DBトランザクション処理の書き方比較

- **記録日:** 2026-09-19
- **位置づけ:** Rustシリーズ第5弾。2026-09-24に回答した「Rust決済機能でのトランザクション処理」を踏まえ、一般的な言語(Java・Go)との具体的な書き方の違いを整理する。

## 結論を先に:トランザクション処理は「できる/できない」ではなく「安全性の担保のされ方」が違う

Rust・Java・Goのいずれも、RDBMS(PostgreSQL/MySQL等のトランザクション機能を持つデータベース)に対してcommit/rollbackを伴うトランザクション処理を記述できる。ただし、**「commit/rollbackし忘れをどう防ぐか」という設計思想が言語ごとに大きく異なる**。

| 言語 | 主なライブラリ | commit/rollback忘れ防止の仕組み |
|---|---|---|
| **Rust** | sqlx、Diesel、SeaORM | **所有権システム**:トランザクションオブジェクトがスコープを抜けるとき、明示的commitがなければ`Drop`で自動rollback |
| **Java** | JDBC、Spring `@Transactional` | try-with-resources、AOP(アスペクト指向プログラミング)によるアノテーションベースの自動管理 |
| **Go** | `database/sql`、sqlx(Go版) | `defer tx.Rollback()`を明示的に書く**開発者の規律**に依存 |

## 1. Go:`database/sql`のトランザクション

Goの標準ライブラリ`database/sql`は、トランザクションを`*sql.Tx`という値として扱う、シンプルで明示的なスタイル。

```go
tx, err := db.Begin()
if err != nil {
    return err
}
defer tx.Rollback() // 呼ばれてもcommit済みなら何もしない(安全)

_, err = tx.Exec("UPDATE accounts SET balance = balance - ? WHERE id = ?", amount, fromID)
if err != nil {
    return err // ここでreturnすると、上のdeferでRollbackが実行される
}

_, err = tx.Exec("UPDATE accounts SET balance = balance + ? WHERE id = ?", amount, toID)
if err != nil {
    return err
}

return tx.Commit()
```

**特徴:**
- `defer tx.Rollback()`という**イディオム(お作法)を必ず書く**ことで安全性を確保する。書き忘れても文法エラーにはならない(=**言語機能としての強制力はない**)
- `tx.Rollback()`は、既に`tx.Commit()`が呼ばれた後に実行されても「トランザクションは既に終了しています」というエラーを返すだけで、実害はない設計になっている
- Goは複数戻り値(`err error`)を前提とした言語設計のため、`if err != nil`を都度書く必要がある。冗長だが、エラーの発生箇所が一目で分かる

## 2. Java:JDBCとSpringの`@Transactional`

### 素のJDBC(Java Database Connectivity)

```java
Connection conn = dataSource.getConnection();
try {
    conn.setAutoCommit(false);
    
    PreparedStatement stmt1 = conn.prepareStatement(
        "UPDATE accounts SET balance = balance - ? WHERE id = ?");
    stmt1.setBigDecimal(1, amount);
    stmt1.setLong(2, fromId);
    stmt1.executeUpdate();
    
    PreparedStatement stmt2 = conn.prepareStatement(
        "UPDATE accounts SET balance = balance + ? WHERE id = ?");
    stmt2.setBigDecimal(1, amount);
    stmt2.setLong(2, toId);
    stmt2.executeUpdate();
    
    conn.commit();
} catch (SQLException e) {
    conn.rollback(); // catchブロックで明示的にrollbackを書く必要がある
    throw e;
} finally {
    conn.close();
}
```

素のJDBCは**例外(Exception)を使ったtry-catch-finally**が基本形。Goと同様に、rollbackの呼び出し忘れは**文法上検知されない**(実行時のバグとして初めて顕在化する)。

### Spring Frameworkの`@Transactional`(実務での主流)

```java
@Service
public class TransferService {

    @Transactional
    public void transfer(Long fromId, Long toId, BigDecimal amount) {
        accountRepository.withdraw(fromId, amount);
        accountRepository.deposit(toId, amount);
        // メソッドが正常終了すればcommit、
        // 実行時例外(RuntimeException)が投げられれば自動rollback
    }
}
```

**特徴:**
- **AOP(アスペクト指向プログラミング)**という仕組みで、メソッドの前後に「トランザクション開始」「commit/rollback」の処理を**アノテーション1つで自動的に織り込む**
- 開発者はビジネスロジックだけを書けばよく、commit/rollbackのコード自体が視界から消える(=書き忘れが原理的に起こらない)
- 一方で、**「どのタイミングで実際にcommit/rollbackされるか」がコードを見ただけでは分かりにくくなる**というトレードオフがある(チェック例外か実行時例外かでrollbackされるかどうかが変わる、自己呼び出し[self-invocation]ではAOPが効かない、等の「Spring `@Transactional`の落とし穴」は非常によく話題になる)

## 3. Rust:所有権システムによる構造的な安全性

```rust
let mut tx = pool.begin().await?;

sqlx::query("UPDATE accounts SET balance = balance - $1 WHERE id = $2")
    .bind(amount)
    .bind(from_id)
    .execute(&mut *tx)
    .await?; // エラー時は?演算子で即座にreturn

sqlx::query("UPDATE accounts SET balance = balance + $1 WHERE id = $2")
    .bind(amount)
    .bind(to_id)
    .execute(&mut *tx)
    .await?;

tx.commit().await?; // 明示的にcommitしない限り、
                     // txがスコープを抜ける瞬間にDropトレイトが発動しrollbackされる
```

**特徴:**
- `tx`(トランザクションオブジェクト)は**所有権を持つ1つの値**として扱われる
- 関数の途中で`?`演算子によりエラーが発生して早期リターンしても、Rustは**スコープを抜ける全ての値に対して`Drop`(後始末処理)を自動的に呼ぶ**という言語仕様上の保証があるため、`tx`のDrop実装が自動的にrollbackを実行する
- つまり、**Go/Javaのように「rollbackを書き忘れる」というミスそのものが、言語の型システムと所有権規則によって構造的に起こりえない**
- これはGoの`defer tx.Rollback()`(開発者の規律に依存)やJavaの素のtry-catch(同上)とは異なり、**「安全側に倒れる」ことがコンパイラ・ランタイムによって保証される**という点が本質的な違い

## まとめ表:3言語の設計思想の違い

| 観点 | Go | Java(素のJDBC) | Java(Spring) | Rust |
|---|---|---|---|---|
| 安全性の担保 | 開発者の規律(`defer`) | 開発者の規律(try-catch) | フレームワークの自動化(AOP) | **言語機能(所有権・Drop)による強制** |
| コードの見た目 | 明示的・冗長 | 明示的・冗長 | 宣言的・簡潔(アノテーション) | 明示的だが安全性は自動保証 |
| 書き忘れ時の挙動 | コンパイルは通る、実行時バグ | コンパイルは通る、実行時バグ | 原理的に起こりにくい | **コンパイル時に構造上防がれる** |
| デバッグのしやすさ | 挙動が読みやすい | 挙動が読みやすい | 「実際いつcommitされるか」が読みにくい場合がある | 挙動が読みやすい、かつ安全 |

## 実務上の示唆

- **Go/Java(素のJDBC)**:シンプルで挙動は追いやすいが、**「rollbackを書き忘れる」という典型的な人為ミスのクラスが常に存在**する。コードレビューやLintツールでの検出に頼る必要がある
- **Java(Spring)**:書き忘れは減るが、**「実際どのタイミングでcommit/rollbackされるか」の見通しがフレームワークの規約に依存**するため、`@Transactional`の伝播設定(`Propagation`)やロールバック対象例外の設定を正しく理解していないと、逆に「rollbackされると思っていたのにcommitされていた」という別種のバグを生みやすい
- **Rust**:上記いずれの問題も、**言語のコア機能である所有権・借用・Dropによって構造的に排除**される。決済処理のような「commit/rollbackの取り違えが金銭的損失に直結する」領域では、この保証の強さがRust採用の大きな動機になりうる

## 参考

- Zenn「Rust アプリケーションにおける実践的トランザクション設計」: <https://zenn.dev/poi2/articles/68e3d158a6d4b9>
- Zenn「Rust | SQLx で transaction & commit / rollbackを実装する」: <https://zenn.dev/collabostyle/articles/ec055835386e77>
- スクールオブウェブ「Go実践 #4 DB連携 — database/sqlとトランザクション」: <https://schoolofweb.net/ja/posts/go-practice-4-database/>

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
