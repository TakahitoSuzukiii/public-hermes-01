作成日: 2026-09-19 / STATUS: INFO / TOPIC: RUST

# Rust・Java・Go:エラーハンドリングとResult型の違い

- **記録日:** 2026-09-19
- **位置づけ:** Rustシリーズ第6弾。トランザクション処理比較記事の関連テーマとして、エラー処理の設計思想の違いを整理する。

## 結論を先に:3つの異なる「エラーの表現方法」

| 言語 | エラーの表現 | 「エラー処理を忘れた」場合の挙動 |
|---|---|---|
| **Java** | 例外(Exception)、特に**検査例外(checked exception)** | チェック例外はコンパイルエラーで検出される(型シグネチャに明記必須) |
| **Go** | 戻り値としての`error`型(多値戻り値の一部) | **コンパイルは通る**。`err`を無視しても文法上問題ない |
| **Rust** | `Result<T, E>`型(列挙型、値そのもの) | **コンパイルエラーになりうる**(`#[must_use]`属性により、戻り値を無視すると警告/エラー) |

## 1. Java:検査例外(checked exception)と非検査例外(unchecked exception)

Javaの大きな特徴は、**例外を「検査例外」と「非検査例外」の2種類に分けている**こと。

```java
// 検査例外(checked exception):メソッドのシグネチャに throws を明記する義務がある
public void readFile(String path) throws IOException {
    FileInputStream fis = new FileInputStream(path); // FileNotFoundExceptionはIOExceptionのサブクラス
    // ...
}

// 呼び出し側は、catchするかthrowsで再宣言するかを強制される(コンパイルエラーで検出)
public void process() {
    try {
        readFile("data.txt");
    } catch (IOException e) {
        // 対処必須
    }
}
```

- **検査例外**:`IOException`など。コンパイラが「この例外は処理されているか」を検査するため、対処法を明示しないとコンパイルが通らない。「プログラムの外側で起こりうる、想定内のエラー」(ファイルが見つからない等)に使われる
- **非検査例外**:`RuntimeException`とそのサブクラス(`NullPointerException`、`IllegalArgumentException`等)。コンパイラは検査しない。「プログラミングミスに起因する、本来起きてはいけないエラー」に使われる
- Javaコミュニティでは、**検査例外が「呼び出し元に例外処理の実装を強制する割に、大量の定型的なtry-catchを生む」として賛否が分かれ続けてきた**という歴史的経緯がある(Spring等のフレームワークは非検査例外を好む傾向がある)

## 2. Go:多値戻り値としての`error`

Goには例外機構(try-catchに相当するもの)が存在しない。代わりに、**関数の戻り値の最後に`error`型を追加する**という規約でエラーを表現する。

```go
func readFile(path string) ([]byte, error) {
    data, err := os.ReadFile(path)
    if err != nil {
        return nil, err
    }
    return data, nil
}

// 呼び出し側
data, err := readFile("data.txt")
if err != nil {
    // ここで対処
    log.Fatal(err)
}
```

**特徴:**
- `error`は単なるインターフェース型の値であり、**「無視しても文法上は合法」**(`data, _ := readFile("data.txt")`のように握りつぶせてしまう)
- この「握りつぶしのしやすさ」は、Goコミュニティ内でも長年の論争テーマ。`errcheck`のようなLintツールで検出する運用がデファクトスタンダードになっている
- `errors.Is`/`errors.As`によるエラーのラップ・アンラップ(Go 1.13以降)で、エラーの原因を階層的にたどれるようになっている

```go
if errors.Is(err, ErrOutOfTea) {
    // 特定のエラー(センチネルエラー)にマッチするか判定
}
```

## 3. Rust:`Result<T, E>`という「値」としてのエラー

Rustにも`panic!`(プログラムを異常終了させる仕組み)はあるが、**通常の回復可能なエラーは`Result<T, E>`という列挙型(enum)の値として表現**する。

```rust
fn read_file(path: &str) -> Result<String, std::io::Error> {
    let content = std::fs::read_to_string(path)?; // ?演算子でエラーを早期リターン
    Ok(content)
}

// 呼び出し側:matchによる網羅的な分岐
match read_file("data.txt") {
    Ok(content) => println!("{}", content),
    Err(e) => eprintln!("エラー: {}", e),
}
```

**特徴:**

1. **`Result`は"ただの値"であり、特別な制御構文(try-catch)を必要としない。** `Ok(T)`(成功時の値)か`Err(E)`(失敗時の値)のどちらかを持つ、ただの列挙型
2. **`#[must_use]`属性により、戻り値の`Result`を握りつぶすとコンパイラが警告(多くのプロジェクトでは警告をエラー扱いに設定)を出す。** Goの「エラーを無視しても合法」とは対照的に、**「無視したこと」自体が検出可能**
3. **`?`演算子**が、Goの`if err != nil { return err }`という定型コードを1文字で表現する糖衣構文になっている。ネストが深くならず、かつエラーの伝播漏れが起きない
4. **例外という概念自体が存在しない。** Javaの「検査例外か非検査例外か」という区別自体がなく、**全てのエラーは型シグネチャ(戻り値の型)に現れる**ため、「このメソッドがどんなエラーを投げうるか」を型だけで確認できる(Javaの検査例外に近い厳格さを、例外機構なしで実現している)

### `Option<T>`:「値がないかもしれない」もRustでは型で表現

RustはNull参照(JavaのNullPointerException、Goのnil参照)による実行時エラーを防ぐため、**「値が存在しないかもしれない」という状態も`Option<T>`という型で明示**する。

```rust
fn find_user(id: u64) -> Option<User> {
    // 見つかればSome(user)、見つからなければNoneを返す
}

match find_user(42) {
    Some(user) => println!("{}", user.name),
    None => println!("ユーザーが見つかりません"),
}
```

JavaやGoでは「nullを返すかもしれない関数」であることが**型シグネチャだけでは分からない**(ドキュメントやコード内コメントに頼るしかない)のに対し、Rustでは**戻り値の型自体が`Option<User>`であることで、呼び出し側は必ずNoneのケースを考慮せざるを得ない**という違いがある。

## まとめ表:3言語のエラーハンドリング設計思想

| 観点 | Java | Go | Rust |
|---|---|---|---|
| 表現方法 | 例外(検査/非検査) | 多値戻り値の`error` | `Result<T, E>` / `Option<T>`という値 |
| 処理忘れの検出 | 検査例外はコンパイル時に検出、非検査例外は検出されない | **検出されない**(規約・Lintに依存) | **`#[must_use]`でコンパイラが検出** |
| コードの制御フロー | try-catchによる中断・ジャンプ | 直線的(`if err != nil`の連続) | 直線的+`?`演算子による簡潔な伝播 |
| null安全性 | Optional<T>は存在するが強制力は限定的 | nilは通常のポインタ値、実行時パニックの温床 | `Option<T>`により、nullそのものが型システム上存在しない |
| エラーの階層化 | 例外チェーン(`cause`) | `errors.Is`/`errors.As`によるラップ | `?`演算子+`From`トレイトによる型変換、`thiserror`/`anyhow`クレート |

## 実務上の示唆

- **Go**は最もシンプルだが、**「エラーを握りつぶせてしまう」構造的な弱さ**があり、Lintツールでの補完が実質必須
- **Java**は検査例外という「コンパイラによる強制」を持つ稀有な言語だが、**その強制力自体が「定型的なtry-catchの氾濫」という副作用を生み**、多くの実務プロジェクトでは非検査例外中心の設計に倒れがち
- **Rust**は、**「エラー処理を強制する」という目的をJavaの検査例外に近い厳密さで実現しつつ、例外機構という特別な制御フローを持たず、ただの値として統一的に扱う**という点で、両言語の課題を構造的に解決したデザインになっている。`?`演算子による簡潔さも相まって、「安全性」と「書きやすさ」を両立させている点が評価されている

## 参考

- Baeldung「Checked and Unchecked Exceptions in Java」: <https://www.baeldung.com/java-checked-unchecked-exceptions>
- Go by Example「Errors」: <https://gobyexample.com/errors>
- Rust公式ドキュメント: Result型・Option型・`?`演算子に関する解説(The Rust Programming Language)

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
