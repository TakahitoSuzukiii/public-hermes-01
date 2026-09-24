# Rustに基底クラスがない理由と、DDD・クリーンアーキテクチャの実装方法

- **記録日:** 2026-09-19
- **位置づけ:** Rustシリーズ第7弾。トランザクション処理・エラーハンドリング比較に続き、オブジェクト指向設計(基底クラス・継承)とアーキテクチャパターン(DDD・クリーンアーキテクチャ)におけるRustの実装アプローチを整理する。

## 結論を先に:Rustには「クラスの継承」という概念自体が存在しない

Java・C++・Goなどオブジェクト指向的な言語には「基底クラス(親クラス)を継承して振る舞いを引き継ぐ」という仕組みがあるが、**Rustには"class"というキーワード自体が存在しない**。代わりに`struct`(データ構造)+`trait`(振る舞いの契約)という組み合わせで設計する。これは意図的な言語設計であり、「**継承より合成(composition over inheritance)**」というソフトウェア設計原則を、言語仕様レベルで強制した結果と言える。

## 1. 基底クラスの代替:`trait`(トレイト)

### Java(継承ベース)

```java
abstract class Animal {
    abstract String speak();
    void introduce() {
        System.out.println("私は" + speak() + "と鳴きます");
    }
}

class Dog extends Animal {
    String speak() { return "ワン"; }
}
```

Javaでは`Animal`という**基底クラスを継承**して`Dog`を定義する。共通の実装(`introduce`)は親クラスに書いておき、サブクラスはそれを引き継ぐ。

### Rust(トレイトベース)

```rust
trait Animal {
    fn speak(&self) -> String;
    
    // デフォルト実装(Javaの親クラスメソッドに相当)
    fn introduce(&self) {
        println!("私は{}と鳴きます", self.speak());
    }
}

struct Dog;

impl Animal for Dog {
    fn speak(&self) -> String {
        "ワン".to_string()
    }
}
```

**違いのポイント:**
- Rustの`Dog`は`struct`(データの入れ物)として定義され、`impl Animal for Dog`という形で**「`Dog`型は`Animal`トレイトの契約を満たす」ことを別途宣言**する
- **1つの型は複数のトレイトを自由に実装できる**(Javaの単一継承の制約がない)。GoのInterfaceに近い発想だが、Rustのトレイトは**デフォルト実装を持てる**点でGoのInterfaceより表現力が高い
- **データ(struct)と振る舞い(trait)が分離されている**ため、「継承階層をどう設計するか」という古典的なオブジェクト指向の悩み(いわゆる「ダイヤモンド継承問題」等)がそもそも発生しない

## 2. 「継承より合成」という設計原則をRustは言語仕様で強制する

オブジェクト指向設計の世界では、以前から**「継承(is-a関係)を多用すると、クラス階層が硬直化し変更に弱くなる。可能な限り合成(has-a関係、部品の組み合わせ)を使うべき」**という原則(composition over inheritance)が推奨されてきた。Java・C++・Goはこの原則を「推奨」として提示するに留まるが、**Rustは継承という選択肢自体を言語から排除する**ことで、設計者が自然に合成ベースの設計へ導かれるようになっている。

## 3. DDD(ドメイン駆動設計)のRustでの実装

DDDの戦術的パターン(値オブジェクト、エンティティ、集約、リポジトリ)は、**Rustの型システムと非常に相性が良い**と評価されている。

### 値オブジェクト(Value Object)の実装:newtypeパターン

```rust
// 単なる文字列ではなく、「メールアドレス」という意味を型で表現する
struct EmailAddress(String);

impl EmailAddress {
    fn new(raw: &str) -> Result<Self, ValidationError> {
        if raw.contains('@') {
            Ok(EmailAddress(raw.to_string()))
        } else {
            Err(ValidationError::InvalidEmail)
        }
    }
}
```

**newtypeパターン**(既存の型を1要素のタプル構造体でラップする手法)により、「バリデーション済みの値であることをコンストラクタで保証し、以後は型として区別する」というDDDの値オブジェクトの考え方を、実行時コストゼロで実現できる。一度`EmailAddress`型として生成された値は、**再検証なしに「正しいメールアドレスである」ことが型レベルで保証される**。

### 集約(Aggregate)とリポジトリ(Repository)

```rust
// ドメイン層:ビジネスルールを持つ集約
struct Order {
    id: OrderId,
    items: Vec<OrderItem>,
    status: OrderStatus,
}

impl Order {
    fn add_item(&mut self, item: OrderItem) -> Result<(), DomainError> {
        if self.status != OrderStatus::Draft {
            return Err(DomainError::CannotModifyConfirmedOrder);
        }
        self.items.push(item);
        Ok(())
    }
}

// リポジトリはtraitとして「契約」だけをドメイン層に定義し、
// 実装(DB接続等)はインフラ層に置く(依存性逆転の原則)
trait OrderRepository {
    async fn find_by_id(&self, id: OrderId) -> Result<Option<Order>, RepositoryError>;
    async fn save(&self, order: &Order) -> Result<(), RepositoryError>;
}
```

- リポジトリを**トレイトとして定義し、ドメイン層はその契約にのみ依存する**。実際のDB実装(PostgreSQL用、テスト用のインメモリ実装等)はこのトレイトを`impl`する形でインフラ層に配置する
- これは後述のクリーンアーキテクチャの「依存性逆転の原則」をRustのトレイトで自然に表現したもの

## 4. クリーンアーキテクチャのRustでの実装

クリーンアーキテクチャは、**ドメイン(業務ルール)を中心に置き、DBやWebフレームワークといった技術的な詳細を外側の層に追いやる**という設計原則。Rustでの実装例(Axum + SQLx + MySQLの構成)では、以下のような層分けがよく採用される。

| 層 | 役割 | Rustでの実装 |
|---|---|---|
| **ドメイン層** | ビジネスルール、エンティティ、値オブジェクト | `struct`+`impl`(外部ライブラリへの依存を持たない、最も独立した層) |
| **アプリケーション層** | ユースケース、リポジトリのtrait定義 | `trait OrderRepository`のような**契約(インターフェース)**の定義 |
| **インフラ層** | DB接続、外部API連携の実装 | `impl OrderRepository for SqlxOrderRepository`のような**具体的な実装** |
| **プレゼンテーション層** | HTTPハンドラ等 | Axum等のWebフレームワークのハンドラ関数 |

Rustでの実装記事(Qiita・Zenn等の実践記事)では、**「クリーンアーキテクチャで実装しようとして複雑化しすぎ、オニオンアーキテクチャ(層の数を減らしたバリエーション)に落ち着いた」という試行錯誤の記録も多く見られる**。これはRust固有の問題というより、**クリーンアーキテクチャ自体が小〜中規模プロジェクトにはオーバースペックになりがち**という、言語非依存の一般的な知見でもある。

## Rustならではの強み:モジュールシステムによる可視性制御

Rustの`mod`(モジュール)システムと`pub`(公開)キーワードの組み合わせにより、**「ドメイン層の内部実装を外部から直接触れないよう、コンパイラレベルで強制する」**ことができる。

```rust
mod domain {
    pub struct Order {
        id: OrderId,       // privateフィールド:外部から直接書き換え不可
        items: Vec<OrderItem>,
    }
    
    impl Order {
        pub fn add_item(&mut self, item: OrderItem) -> Result<(), DomainError> {
            // ここを通してのみ状態変更可能。ビジネスルールを必ず通過させられる
        }
    }
}
```

JavaやGoでも`private`修飾子で同様のことはできるが、Rustは**モジュール単位での可視性制御が言語仕様として一貫しており、「意図しない直接アクセス」をコンパイル時に防ぎやすい**という評価がある。

## まとめ表:オブジェクト指向設計パターンのRustでの表現

| Java/Goの概念 | Rustでの対応 |
|---|---|
| 基底クラス・継承(`extends`) | 存在しない。`trait`のデフォルト実装で部分的に代替 |
| インターフェース(`interface`) | `trait`(ただしデフォルト実装を持てる分、表現力が高い) |
| カプセル化(`private`) | モジュール(`mod`)+可視性修飾子(`pub`) |
| DDDの値オブジェクト | newtypeパターン(タプル構造体によるラップ) |
| DDDのリポジトリパターン | `trait`によるドメイン層⇔インフラ層の分離(依存性逆転) |
| クリーンアーキテクチャの層分離 | クレート(パッケージ)分割 or モジュール分割+`trait`境界 |

## 実務上の示唆

- Rustは「クラス継承」という選択肢を持たないことで、**設計者が自然と「合成」「トレイトによる契約」に基づく設計へ導かれる**言語である
- DDD・クリーンアーキテクチャといった「技術的な詳細からドメインを守る」ことを目的とした設計パターンとは、**所有権・トレイト・モジュールシステムという言語機能そのものが親和性が高い**
- 一方で、クリーンアーキテクチャの層を厳密に実装しすぎると複雑化しやすいのは言語共通の課題であり、**プロジェクト規模に応じてオニオンアーキテクチャ等の簡略版を選ぶ判断も実務ではよく行われている**

## 参考

- Qiita「Rustの型システムで実装するDDD戦術パターン実践ガイド」: <https://qiita.com/0h-n0/items/0ad6d1f3c9033745d233>
- GitHub「kuwana-kb/ddd-in-rust」(『ドメイン駆動設計入門』のRust実装): <https://github.com/kuwana-kb/ddd-in-rust>
- Zenn「DDDとクリーンアーキテクチャをはじめよう-Rust編」: <https://zenn.dev/poporo/articles/20251011_1_start_ddd_and_clean_architecture_rust>
- Qiita「Rust で DDD を実践しながら API サーバーを実装・構築した（つもり）」: <https://qiita.com/tsuchinoko0402/items/dda60c43dbe4e83e729d>

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
