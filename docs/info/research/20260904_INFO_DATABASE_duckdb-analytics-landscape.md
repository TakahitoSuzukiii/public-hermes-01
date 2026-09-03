# DuckDBに類似・関連する分析基盤・DB群の全体マップ

作成日: 2026-09-04 / STATUS: INFO / TOPIC: DATABASE

> きっかけ: AWSによるDuckLabs（DuckDB開発元）買収のニュースから、類似・関連する分析基盤の全体像を整理した。

---

## 全体マップ:分析基盤の分類

分析系ツールは大きく3つの軸で分かれる。

1. **どこで動くか**（ローカル埋め込み型 / サーバー型 / クラウド型）
2. **何のデータを扱うか**（構造化データの集計・分析 / ログ・時系列 / 生データの変換）
3. **OLTP（日々のトランザクション処理）かOLAP（分析・集計処理）か**

DuckDBは「**ローカル埋め込み型のOLAP（分析）データベース**」というカテゴリの代表格である。

---

## 1. DuckDBと同じ「ローカル埋め込み型OLAP」カテゴリ

| ツール | 特徴 |
|---|---|
| **SQLite** | 実は**OLTP（トランザクション処理）寄り**。DuckDBとよく比較されるが、SQLiteは「行指向」（1レコードずつ処理）でトランザクション処理・小規模アプリのDBに強く、DuckDBは「列指向」（列ごとにまとめて処理）で大量データの集計・分析に強い、という設計思想が根本的に違う。「アプリの裏側のDB＝SQLite」「分析・レポート＝DuckDB」という住み分け。 |
| **Polars** | Rust製のデータフレームライブラリ（PythonのPandasの後継的存在）。DBというよりデータ処理ライブラリだが、DuckDBと同じ「列指向・高速・ローカル完結」という思想を共有し、しばしば組み合わせて使われる。 |
| **ClickHouse (Local)** | 通常はサーバー型だが、ローカル実行モードもあり、DuckDBと近い立ち位置で比較されることが増えている。 |
| **MotherDuck** | DuckDBをクラウド上でホスティングするサービス。「ローカルで書いたDuckDBのクエリを、そのままクラウドの大規模データにも使える」という橋渡し役。DuckLabsとは別会社だが、DuckDBのコミュニティでは常にセットで語られる存在。 |

## 2. サーバー型・クラウド型のOLAP（データウェアハウス）

DuckDBが代替・補完する対象として語られることが多い、より大規模な分析基盤:

| ツール | 特徴 |
|---|---|
| **Snowflake** | クラウド型データウェアハウスの代表格。エンタープライズで広く使われる。 |
| **Amazon Redshift** | AWSのデータウェアハウス。 |
| **Google BigQuery** | Google Cloudのサーバーレス型データウェアハウス。 |
| **Databricks** | 「レイクハウス」というデータレイク＋DWHの統合型。Apache Sparkがベース。 |
| **ClickHouse** | ロシア発、超高速なOLAP DB。ログ分析・リアルタイム分析に強い。 |

**DuckDBとの関係:** これらは「大規模・複数人でのクラウド分析基盤」であるのに対し、DuckDBは「手元のPCで、サーバーやクラウド課金なしに、数百万〜数億行レベルのデータを高速分析できる」という**軽量・低コストな代替**として台頭してきた。

## 3. Splunkと同じ「ログ・時系列分析」カテゴリ

Splunkはやや毛色が違い、**ログデータの収集・検索・可視化**に特化したツール。

| ツール | 特徴 |
|---|---|
| **Splunk** | ログの取り込み・検索・アラート・ダッシュボードまで一気通貫。エンタープライズで根強い人気だが高コスト。 |
| **Elastic Stack (ELK)** | Elasticsearch + Logstash + Kibanaの組み合わせ。Splunkの主要なOSS代替として使われる。 |
| **Grafana + Loki** | 軽量なログ・メトリクス可視化スタック。Prometheusと組み合わせて監視基盤として使われることも多い。 |
| **Datadog** | SaaS型の統合監視・ログ分析（APM・インフラ監視も含む）。 |

**DuckDBとの関係:** DuckDBはログ分析専用ではないが、「CSVやParquetファイルに溜めたログを、Splunkのような専用基盤を用意せずSQLでサクッと分析したい」という軽量なユースケースでは、DuckDBが代替として使われることもある。

## 4. ETL（データ変換・パイプライン）

ETL（Extract＝抽出・Transform＝変換・Load＝読み込み）は、上記のDB・分析基盤にデータを流し込む「配管工事」の部分。

| ツール | 特徴 |
|---|---|
| **dbt (data build tool)** | SQLベースでデータ変換パイプラインを定義する、今最も人気のツール。Snowflake/BigQuery/DuckDB等と組み合わせて使われる。 |
| **Apache Airflow** | データパイプラインのスケジューリング・依存関係管理の定番。 |
| **Fivetran / Airbyte** | 各種SaaS（Salesforce, Stripe等）からデータを自動で抽出・同期するツール。Airbyteはオープンソース。 |
| **AWS Glue** | AWSのマネージドETLサービス。 |

---

## まとめると

| 役割 | 代表例 |
|---|---|
| アプリの裏側DB（トランザクション） | SQLite, PostgreSQL, MySQL |
| **ローカル分析（DuckDBのカテゴリ）** | **DuckDB**, Polars |
| クラウド型データウェアハウス | Snowflake, BigQuery, Redshift, Databricks |
| ログ・監視分析 | Splunk, Elastic Stack, Datadog |
| データの配管（ETL） | dbt, Airflow, Fivetran, AWS Glue |

DuckLabsの買収は、この中でも**「ローカル分析ツールをクラウド大手（AWS）が取り込む」**という動き、つまり表の1番目と2番目の境界線をAWSが埋めにきた、という位置づけになる。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
