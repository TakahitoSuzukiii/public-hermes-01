# 設計・アーキテクチャ 学習リンク集

API設計・データベース設計・機能設計・インフラ・ネットワーク・リファクタリング・要件定義・システム設計・テスト・UIデザインの各テーマについて、参考になる公式ドキュメント・記事・書籍情報をまとめています。実装コードや機密情報は含まれていません。

## API設計
- Awesome: [Awesome API](https://github.com/Kikobeats/awesome-api), [HTTP API Development Tools](https://github.com/yosriady/awesome-api-devtools), [Awesome REST](https://github.com/marmelab/awesome-rest), [Awesome gRPC](https://github.com/grpc-ecosystem/awesome-grpc), [awesome GraphQL](https://github.com/chentsulin/awesome-graphql), [awesome APISec](https://github.com/arainho/awesome-api-security), [Awesome Web Scraping](https://github.com/lorien/awesome-web-scraping), [API Security Checklist](https://github.com/shieldfy/API-Security-Checklist)
- ロードマップ: [API Security Best Practices](https://roadmap.sh/best-practices/api-security)
- 基本: [API設計まとめ](https://qiita.com/KNR109/items/d3b6aa8803c62238d990)、[gRPC・OpenAPI・RESTの使い分け(Google Cloud)](https://cloud.google.com/blog/products/api-management/understanding-grpc-openapi-and-rest-and-when-to-use-them?hl=en)、[WebAPI解説](https://techinfoofmicrosofttech.osscons.jp/index.php?WebAPI)
- 公開API集: [Public APIs](https://github.com/public-apis/public-apis)
- REST: [Representational State Transfer(wiki)](https://ja.wikipedia.org/wiki/Representational_State_Transfer)
- gRPC: [公式](https://grpc.io/docs/what-is-grpc/introduction/)、[さくらナレッジ解説](https://knowledge.sakura.ad.jp/24059/)（異なるマシン上のサービス間通信手法、Googleが自社利用していたものをOSS化、言語非依存で設計、Protocol Buffersでバイナリを効率的に扱う）、[gRPCと従来REST APIの比較](https://www.integrate.io/jp/blog/grpc-vs-rest-how-does-grpc-compare-with-traditional-rest-apis-ja/)、[AWSによる比較](https://aws.amazon.com/jp/compare/the-difference-between-grpc-and-rest/)、[4種類のサービスメソッド](https://www.xlsoft.com/jp/blog/blog/2022/05/25/post-29393-post-29393/)
- Protocol Buffers: [公式](https://protobuf.dev/)、[wiki](https://ja.wikipedia.org/wiki/Protocol_Buffers)、[gRPCとPBの関係](https://lab.mo-t.com/blog/protocol-buffers)
- GraphQL: [公式学習](https://graphql.org/learn/)、[GraphQLはいつ使うか・RESTとの比較](https://zenn.dev/saboyutaka/articles/e5515872871534)
- OpenAPI: [openapis.org](https://www.openapis.org/)、[swagger](https://swagger.io/)、[what-is-openapi](https://www.openapis.org/what-is-openapi)、[OpenAPIまとめ](https://qiita.com/KNR109/items/7e094dba6bcf37ed73cf)、[OpenAPIとは](https://www.aeyescan.jp/media/openapi)
- JWT: [JWT仕様](https://self-issued.info/docs/draft-ietf-oauth-json-web-token.html#Overview)
- 認証・認可: [Basic/Digest/Bearer/OAuth認証方式まとめ](https://architecting.hateblo.jp/entry/2020/03/27/130535)
- WebSocket: [WebSocket API(MDN)](https://developer.mozilla.org/ja/docs/Web/API/WebSockets_API)、[wiki](https://ja.wikipedia.org/wiki/WebSocket)
- 書籍: 「Webを支える技術」(山本陽平)、「Web API: The Good Parts」(水野貴明)

## データベース設計
- Awesome: [Awesome DB](https://github.com/numetriclabz/awesome-db), [Awesome Scalability](https://github.com/binhnguyennus/awesome-scalability), [Awesome MySQL](https://github.com/shlomi-noach/awesome-mysql), [Awesome Postgres](https://github.com/dhamaniasad/awesome-postgres), [Awesome NoSQL Guides](https://github.com/erictleung/awesome-nosql-guides), [Awesome MongoDB](https://github.com/ramnes/awesome-mongodb), [Awesome DynamoDB](https://github.com/alexdebrie/awesome-dynamodb), [Awesome Elasticsearch](https://github.com/dzharii/awesome-elasticsearch)
- ロードマップ: [Roadmap SQL](https://roadmap.sh/sql)
- DB選定: [サービスに適したDBを選ぶ方法](https://medium.com/wix-engineering/how-to-choose-the-right-30_database-for-your-service-97b1670c5632)、[ユースケース別の選び方](https://www.integrate.io/jp/blog/which-30_database-ja/)
- RDB書籍: 「プログラマのためのSQL」「達人に学ぶDB設計」「達人に学ぶSQL」「SQLアンチパターン」(Bill Karwin)
- 正規化: [MS公式解説](https://learn.microsoft.com/ja-jp/office/troubleshoot/access/30_database-normalization-description)
- 多対多: [中間テーブル解説](https://qiita.com/ramuneru/items/db43589551dd0c00fef9)
- CQRS: [CQRS Journey(MS)](https://learn.microsoft.com/en-us/previous-versions/msp-n-p/jj554200(v=pandp.10))、[CQRS完全に理解した](https://zenn.dev/shmi593/articles/c1baeb2d453929)、[CQSとCQRSの違い](https://qiita.com/hirodragon/items/6281df80661401f48731)
- CORS: [MDN解説](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS)
- ACID特性: [wiki](https://ja.wikipedia.org/wiki/ACID_(%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF%E7%A7%91%E5%AD%A6))、[Pythonでのトランザクション実装例](https://zenn.dev/yutabeee/articles/66eeff0ac1de36)
- レプリケーション: [構成可能なレプリケーショントポロジ3つ](https://nippondanji.blogspot.com/2011/04/mysql-dba273.html)（マスタースレーブ・マルチマスター・カスケードは可能、マルチソースは不可）、[READ COMMITTED分離レベルとSharding](https://nippondanji.blogspot.com/2009/03/mysql7.html)、[トランザクション分離レベルVSリード現象対応表](https://qiita.com/momotaro98/items/ad859ec2934ee98540fb)
- SQLアンチパターン: [簡単まとめ](https://zenn.dev/yukito0616/articles/00ccc30b58e458)
- MySQL: [チートシート](https://quickref.me/mysql.html)、[スロークエリログの使い方](https://gihyo.jp/dev/serial/01/mysql-road-construction-news/0007)、[EXPLAIN公式](https://dev.mysql.com/doc/refman/8.0/ja/explain.html)、[実行計画の処理](https://use-the-index-luke.com/ja/sql/explain-plan/mysql/operations)
- インデックス: [実行計画・統計情報入門](https://zenn.dev/mesi/articles/23808becb50b75)、[use-the-index-luke(日本語)](https://use-the-index-luke.com/ja)、[B-treeインデックス入門](https://qiita.com/kiyodori/items/f66a545a47dc59dd8839)、[MySQL外部キー制約とインデックス](https://tech.layerx.co.jp/entry/2022/01/31/093141)
- ページネーション: [シーク法によるアクセス(オフセット法との比較)](https://use-the-index-luke.com/ja/sql/partial-results/fetch-next-page#fig07_03) — シーク法はWHERE句が複雑になり任意ページ取得不可だが無限スクロールには適する
- PROFILE: [SHOW PROFILE公式](https://dev.mysql.com/doc/refman/8.0/ja/show-profile.html)
- Null: [GoでNULL許可カラムを扱う](https://zenn.dev/voicy/articles/9a7793c4818a60)、[sql.NullStringのJSON Marshalling](https://okamuuu.hatenablog.com/entry/2016/12/20/150339)
- Aurora: [Amazon Aurora特徴](https://aws.amazon.com/jp/rds/aurora/features/)、[Aurora PostgreSQLパーティショニング導入(検討編/実践編)](https://lab.mo-t.com/blog/introduce-table-partitioning-in-aurora-postgres)
- TiDB: [GitHub](https://github.com/pingcap/tidb)、[docker quick start](https://github.com/pingcap/tidb-docker-compose)
- NoSQL: [MongoDBスキーマ設計ベストプラクティス](https://www.mongodb.com/developer/products/mongodb/mongodb-schema-design-best-practices/)、[MongoDBパフォーマンスベストプラクティス](https://www.mongodb.com/basics/best-practices)
- N+1問題: [DataLoaderでGraphQLのN+1解決](https://tech.layerx.co.jp/entry/2022/06/13/120000)
- MongoDB: [wiki](https://ja.wikipedia.org/wiki/MongoDB)、[公式](https://www.mongodb.com/ja-jp)、[DynamoDBとの比較](https://www.mongodb.com/compare/mongodb-dynamodb)
- DynamoDB: [公式](https://aws.amazon.com/jp/dynamodb/)、[NoSQL設計ベストプラクティス](https://docs.aws.amazon.com/ja_jp/amazondynamodb/latest/developerguide/bp-general-nosql-design.html)、[DynamoDB vs MongoDBの違い7つ](https://www.integrate.io/blog/dynamodb-vs-mongodb-differences/)
- キャッシュ: [Memcached](https://aws.amazon.com/jp/memcached/)、[Redis](https://aws.amazon.com/jp/redis/)、[ElastiCache for Memcached](https://aws.amazon.com/jp/elasticache/memcached/)、[ElastiCache for Redis](https://aws.amazon.com/jp/elasticache/redis/)、[Redis vs Memcached](https://aws.amazon.com/jp/elasticache/redis-vs-memcached/)
- 全文検索: [Elasticsearch(AWS解説)](https://aws.amazon.com/jp/what-is/elasticsearch/)

## 機能設計
- アルゴリズム参考: [Twitter推薦アルゴリズム](https://github.com/twitter/the-algorithm)
- ストレージ管理: [Cookie(MDN)](https://developer.mozilla.org/ja/docs/Web/HTTP/Cookies)、[GDPR対応](https://b-risk.jp/blog/2022/02/gdpr/)
- ページネーション: [シーク法アクセス](https://use-the-index-luke.com/ja/sql/partial-results/fetch-next-page#fig07_03)、[カーソルページネーション実装事例](https://lab.mo-t.com/blog/cursor-pagination-implementation)
- 排他制御: [wiki](https://ja.wikipedia.org/wiki/%E6%8E%92%E4%BB%96%E5%88%B6%E5%BE%A1)、[mutex](https://ja.wikipedia.org/wiki/%E3%83%9F%E3%83%A5%E3%83%BC%E3%83%86%E3%83%83%E3%82%AF%E3%82%B9)、[セマフォ](https://ja.wikipedia.org/wiki/%E3%82%BB%E3%83%9E%E3%83%95%E3%82%A9)、[楽観/悲観ロックの基礎](https://zenn.dev/airiswim/articles/ebe313fb39a4c9)
  - ACID特性: 原子性・一貫性・独立性・耐久性の4要素
  - リード現象: ダーティリード(未コミットデータの読み取り)、ファジーリード(再実行で結果が変わる)、ファントムリード(結果件数が変わる)
  - ロック方式: 楽観ロック(バージョン管理、競合少ない・処理短時間向け)／悲観ロック(取得時ロック、競合多い・処理長時間向け)。デッドロックにも注意
- 認証・認可: [認可・権限管理の基礎概念](https://masatora.net/blogs/%E8%AA%8D%E5%8F%AF%E3%83%BB%E6%A8%A9%E9%99%90%E7%AE%A1%E7%90%86%E3%81%AE%E5%9F%BA%E7%A4%8E)、[ABAC(属性ベースアクセス制御)とは](https://www.okta.com/jp/blog/2020/09/attribute-based-access-control-abac/)
- OAuth2.0: [一番分かりやすい説明](https://qiita.com/TakahikoKawasaki/items/e37caf50776e00e733be)、[全フロー図解](https://qiita.com/TakahikoKawasaki/items/200951e5b5929f840a1f)
- SAML2.0: [SAML-tracer(Chrome拡張)](https://chromewebstore.google.com/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch)
- OpenID Connect: [一番分かりやすい説明](https://qiita.com/TakahikoKawasaki/items/498ca08bbfcc341691fe)
- JWT: [解説記事](https://qiita.com/TakahikoKawasaki/items/8f0e422c7edd2d220e06)
- 認可基盤: [Google Zanzibar](https://www.osohq.com/learn/google-zanzibar)、[認可アーキテクチャに関する考察](https://zenn.dev/she_techblog/articles/6eff1f28d107be)、[auth0](https://auth0.com/jp)、[freeeの権限管理基盤](https://developers.freee.co.jp/entry/authorization-management-microservice)
- 決済機能: [外部決済サービス利用時の脆弱ポイントと対策](https://dev.classmethod.jp/articles/devio2022-vulnerable-points-and-countermeasures-for-using-external-payment-services/)、[外部決済サービス利用の反省と改善](https://dev.classmethod.jp/articles/devio2021-introspection-and-improvement-of-development-with-external-payment-services/)、[ECサイト決済システム構築知見](https://dev.classmethod.jp/articles/developers-io-2020-connect-day5-payment-development-flow-with-e-commerce-site/)、[Stripe公式](https://stripe.com/docs/payments/payment-methods/overview?locale=ja-JP)
- リアルタイム通信: [双方向通信プロトコルまとめ](https://qiita.com/theFirstPenguin/items/55dd1daa9313f6b90e2f)
- メッセージング: [WebSocket(MDN)](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)、[WebPush](https://developer.mozilla.org/ja/docs/Web/API/Push_API)
- ビデオ通話: [WebRTC(MDN)](https://developer.mozilla.org/ja/docs/Web/API/WebRTC_API)、[WebRTC概要](https://zenn.dev/yuki_uchida/books/c0946d19352af5/viewer/0e7daa)
- 全文検索: [Amazon RDS for MySQLと全文検索](https://dev.classmethod.jp/articles/amazon-rds-for-mysql-fulltext-search/)、[Algolia×DynamoDB全文検索](https://dev.classmethod.jp/articles/algolia-dynamodb-search/)
- キャッシュ(フロント): [フロントエンドが知るべきキャッシュ](https://zenn.dev/kaa_a_zu/articles/f1430cf681b185)

## インフラ・DevOps
- Awesome: [Awesome Networking](https://github.com/clowwindy/Awesome-Networking), [Awesome Docker](https://github.com/veggiemonk/awesome-docker), [Awesome Kubernetes](https://github.com/ramitsurana/awesome-kubernetes), [Awesome Sysadmin](https://github.com/awesome-foss/awesome-sysadmin), [Ultimate DevSecOps library](https://github.com/sottlmarek/DevSecOps), [Awesome MLOps](https://github.com/visenger/awesome-mlops), [Awesome SRE](https://github.com/dastergon/awesome-sre), [Awesome CDK](https://github.com/kalaiser/awesome-cdk), [Awesome Nginx](https://github.com/agile6v/awesome-nginx)
- ロードマップ: [Roadmap Docker](https://roadmap.sh/docker), [Roadmap Kubernetes](https://roadmap.sh/kubernetes)
- 分散システム: [コンテナ・デザイン・パターン](https://qiita.com/MahoTakara/items/03fc0afe29379026c1f3)、[Kubernetesで学ぶ分散システムデザインパターン](https://qiita.com/reireias/items/85bcd0acc7f6982041c4)
- Ansible: [Red Hat公式チュートリアル](https://www.redhat.com/ja/topics/automation/learning-ansible-tutorial)、[Ansibleの使い方(Zenn)](https://zenn.dev/y_mrok/books/ansible-no-tsukaikata)
- Docker: [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)
- Kubernetes: [公式チュートリアル](https://kubernetes.io/ja/docs/tutorials/)、[徹底解説](https://zenn.dev/nameless_sn/articles/kubernetes-tutorial)
- CI/CD: [jenkins](https://www.jenkins.io)、[circle-ci解説](https://qiita.com/gold-kou/items/4c7e62434af455e977c2)、[GitOpsとArgoCD](https://circleci.com/ja/blog/gitops-argocd)
- ArgoCD: [公式](https://argo-cd.readthedocs.io/en/stable)、[導入設計とリリースフロー改善事例](https://techblog.zozo.com/entry/measure-argocd-introduction)
- 監視: [Prometheus](https://prometheus.io/)、[Grafana](https://grafana.com/)、[Datadog](https://docs.datadoghq.com/ja/)、[Sentry](https://docs.sentry.io/)、[Mackerel](https://ja.mackerel.io/)、[AWSにおけるObservabilityベストプラクティス](https://dev.classmethod.jp/articles/aws-summit-tokyo-best-practices-for-using-observability/)
- 書籍: 「Effective DevOps」「システム運用アンチパターン」「分散システムデザインパターン」(Brendan Burns)「マスタリングTCP/IP」シリーズ(入門/応用/セキュリティ/ルーティング編)

## ネットワーク
- OSI参照モデル: [wiki](https://ja.wikipedia.org/wiki/OSI%E5%8F%82%E7%85%A7%E3%83%A2%E3%83%87%E3%83%AB)
- HTTP: [リソースと仕様書(MDN)](https://developer.mozilla.org/ja/docs/Web/HTTP/Resources_and_specifications)、[TLS(wiki)](https://ja.wikipedia.org/wiki/Transport_Layer_Security)、[HTTP/2とHTTP/1.1の違い](https://www.kagoya.jp/howto/it-glossary/security/http-2/)、[HTTP/1.1〜HTTP/3の歩み](https://gihyo.jp/admin/serial/01/http3/0001)
- ロードバランシング: [レイヤ4ロードバランシング(nginx)](https://www.nginx.com/resources/glossary/layer-4-load-balancing/)、[レイヤ7ロードバランシング](https://www.nginx.com/resources/glossary/layer-7-load-balancing/)
- トラフィック: [基礎から学ぶネットワーク構築](https://atmarkit.itmedia.co.jp/ait/series/2575/)（1対多通信=ブロードキャスト/マルチキャスト、転送量はbyte/bit、帯域幅はbyte/s・bps）
- CDN: [CDNとは(図解)](https://www.kagoya.jp/howto/it-glossary/web/cdn/) — メリット: サーバ/ネットワーク負荷軽減、表示速度改善、SEO/CV率向上、DoS/DDoS耐性向上。デメリット: 古いコンテンツ表示リスク、キャッシュ事故、アクセスログ取得不可な場合あり
- スケーリング: スケールイン/アウト(サーバ台数増減、水平・垂直分割、シャーディング)、スケールアップ(高性能サーバへの変更)

## リファクタリング
- Awesome: [3 Rs of Software Architecture](https://github.com/ryanmcdermott/3rs-of-software-architecture), [useful coding style guides](https://github.com/NARKOZ/guides)
- リアーキテクチャ: [リファクタリング/リアーキテクティング/ビッグリライトの選択(技術的負債とダンスを4)](https://twop.agile.esm.co.jp/rafactoring-rearchitecting-bigrewrite-18549cd60004)
- 書籍: 「リーダブルコード」(Dustin Boswell)、「達人プログラマー」(David Thomas)、「Code Complete」(Steve McConnell)

## 要件定義・要求分析
- Awesome: [Awesome Technical Writing](https://github.com/BolajiAyodeji/awesome-technical-writing), [アーキテクチャ決定記録(ADR)](https://github.com/joelparkerhenderson/architecture-decision-record)
- ロードマップ: [フルスタック設計・アーキテクチャロードマップ](https://github.com/stemmlerjs/software-design-and-architecture-roadmap)
- ドキュメンテーション: C4モデル([C4-PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML))、ArchiMate([Archi](https://github.com/archimatetool/archi))
- 要件定義: [顧客も知らない真の要求を導き出す](https://www.ogis-ri.co.jp/otc/hiroba/technical/RequirementsAnalysis/)（概要→業務フロー→役割/クラス図/ER図→やりとり/API→非機能要件の順で整理）、[非機能要求とISO9126](https://www.ogis-ri.co.jp/otc/hiroba/technical/JavaPress_ISO9126/)
- メトリクス測定: [プロジェクト測定実践記](https://www.ogis-ri.co.jp/otc/hiroba/technical/ProjectAnalysis/ProjectAnalysis01.html)、[COSMIC法入門](https://www.ogis-ri.co.jp/otc/hiroba/technical/IntroCOSMIC/IntroCOSMICPart1Jun2010.html)
- ロバストネス分析: [実践ロバストネス分析](https://www.ogis-ri.co.jp/otc/hiroba/technical/RobustnessAnalysis/RA1/index.html)、[ロバストネス図活用事例](https://buildersbox.corp-sansan.com/entry/2022/02/28/110000)
- 狩野モデル(品質管理フレームワーク): 当たり前品質(不充足で不満)、一元的品質(充足で満足・不充足で不満)、魅力品質(充足で満足・不充足でも仕方ない)、無関心品質、逆品質。[wiki](https://ja.wikipedia.org/wiki/%E7%8B%A9%E9%87%8E%E3%83%A2%E3%83%87%E3%83%AB)
- 仕様書: [Google Design Docsから学ぶ設計](https://qiita.com/yoshii0110/items/32f93e0c8d24cb3207f7)、[Design Doc超入門](https://atmarkit.itmedia.co.jp/ait/articles/1606/21/news016.html)
- 書籍: 「要件最適アーキテクチャ戦略」(Vaughn Vernon)、「Googleのソフトウェアエンジニアリング」

## システム設計・アーキテクチャ
- Awesome: [Awesome Software Architecture](https://awesome-architecture.com/), [Awesome Design Patterns](https://github.com/DovAmir/awesome-design-patterns), [Awesome Microservices](https://github.com/mfornos/awesome-microservices), [Awesome Serverless](https://github.com/pmuens/awesome-serverless), [Awesome System Design](https://github.com/madd86/awesome-system-design), [Awesome DDD](https://github.com/heynickc/awesome-ddd)
- ロードマップ: [Roadmap System Design](https://roadmap.sh/system-design), [Roadmap Software Design Architecture](https://roadmap.sh/software-design-architecture), [Roadmap Backend](https://roadmap.sh/backend), [The System Design Primer](https://github.com/donnemartin/system-design-primer)
- サーバーレス: [サーバーレスブループリントのベストプラクティス(AWS)](https://aws.amazon.com/jp/blogs/infrastructure-and-automation/best-practices-for-accelerating-development-with-serverless-blueprints/)、[Lambdaで進化的アーキテクチャ](https://aws.amazon.com/jp/blogs/compute/developing-evolutionary-architecture-with-aws-lambda/)
- アーキテクチャパターン: 多層アーキテクチャ、古典DDD(3層構造、プレゼンテーション層はデータ層と直接通信しない)、MVC、レイヤードアーキテクチャ(古典DDD+ドメイン層)、ヘキサゴナル(ポート＆アダプター、2005年頃)、オニオン(2008年頃)、クリーン(2012年頃) — 本質的に類似し責務の区切り方が異なるとされる
- オブジェクト指向: 継承・カプセル化・ポリモーフィズム・抽象化の4大要素([まとめ](https://www.ogis-ri.co.jp/otc/hiroba/topic/oo.html))
- SOLID原則: [解説](https://qiita.com/baby-degu/items/d058a62f145235a0f007)
- Twelve-Factor App: [公式(日本語)](https://12factor.net/ja/)、[解説記事](https://developers.kddi.com/blog/2pcE20cmzJwt2wwov1QN5X)
- マイクロサービス: 書籍「ソフトウェアアーキテクチャの基礎」(Mark Richards)、「マイクロサービスパターン」(Chris Richardson)
- クリーンアーキテクチャ: [実装クリーンアーキテクチャ](https://qiita.com/nrslib/items/a5f902c4defc83bd46b8)、書籍「Clean Architecture」(Robert C. Martin)、[Go+CleanArchitecture再設計事例](https://tech.mirrativ.stream/entry/2020/11/30/142354)
- ヘキサゴナルアーキテクチャ: [解説記事](https://qiita.com/cocoa-maemae/items/b08c4cf95d47e314e2dc)
- デザインパターン: [DESIGN PATTERNS QUICK REFERENCE](http://www.mcdonaldland.info/2007/11/28/40/)、[デザインパターンINDEX](https://www.techscore.com/tech/DesignPattern/)、書籍「Java言語で学ぶデザインパターン入門」「Head Firstデザインパターン」。サーキットブレーカーパターン: [解説](https://fujiyamaegg.com/tech-microservices-circuitbreaker/)、[AWS Step Functionsでの実装](https://dev.classmethod.jp/articles/aws-step-functions-circuit-breaker-pattern/)
- ドメイン駆動設計(DDD): [Martin Fowler](https://martinfowler.com/tags/domain%20driven%20design.html)、[DDDのエッセンス](https://www.ogis-ri.co.jp/otc/hiroba/technical/DDDEssence/index.html)、書籍「エリック・エヴァンスのドメイン駆動設計」「実践ドメイン駆動設計」「ドメイン駆動設計入門」(成瀬允宣)。[戦術的DDDをGoで実現(entity編/Value Object編)](https://tech.yappli.io/entry/2022/07/12/)
- ユースケース駆動開発: 書籍「ユースケース駆動開発実践ガイド」
- モジュラーモノリス: [Modular Monolith with DDD](https://github.com/kgrzybek/modular-monolith-with-ddd)、[考察記事](https://qiita.com/YasuhiroKimesawa/items/1b1f8a7c004388d71388)
- データ指向設計: 書籍「データ指向アプリケーションデザイン」(Martin Kleppmann)
- ディレクトリ構成: [Frontend Development bookmarks](https://github.com/dypsilon/frontend-dev-bookmarks)、[React Project Structure Best Practices](https://www.devaradise.com/react-project-folder-structure)
- 整合性パターン: [System Design Primer該当項](https://github.com/donnemartin/system-design-primer/tree/master?tab=readme-ov-file#consistency-patterns)

## テスト
- Awesome: [Awesome Testing](https://github.com/TheJambo/awesome-testing), [Awesome Test Automation](https://github.com/atinfo/awesome-test-automation), [Awesome Penetration Testing](https://github.com/enaqx/awesome-pentest), [Awesome-tdd](https://github.com/unicodeveloper/awesome-tdd)
- ロードマップ: [QA Engineer](https://roadmap.sh/qa)
- TDD/BDD: [いまさら聞けないTDD/BDD超入門](https://atmarkit.itmedia.co.jp/ait/series/1431/)（動作検証スタイルのデトロイト派とTDDを組み合わせたものがBDD）、[TDD(wiki)](https://ja.wikipedia.org/wiki/%E3%83%86%E3%82%B9%E3%83%88%E9%A7%86%E5%8B%95%E9%96%8B%E7%99%BA)、[BDD(wiki)](https://ja.wikipedia.org/wiki/%E3%83%93%E3%83%98%E3%82%A4%E3%83%93%E3%82%A2%E9%A7%86%E5%8B%95%E9%96%8B%E7%99%BA)
- テストツール: [JEST](https://jestjs.io/ja)、[RSpec](https://rspec.info)、[Mocha](https://mochajs.org/)（[MochaとChaiの使い方](https://qiita.com/y_hokkey/items/f73ea6b3d5f6902396b6)）
- ペアワイズ法: [テスト工数削減とPairwiser](https://qiita.com/y_hokkey/items/0a433ba25a5c5587d4ad)
- 負荷テスト/ベンチマーク: [Load testing(wiki)](https://en.wikipedia.org/wiki/Load_testing)、[gobench](https://github.com/cmpxchg16/gobench)
- リグレッションテスト: [Awesome Visual Regression Testing](https://github.com/mojoaxel/awesome-regression-testing)
- モンキーテスト/ファジング: [Awesome Fuzzing](https://github.com/cpuu/awesome-fuzzing)、[fuzzer-test-suite](https://github.com/google/fuzzer-test-suite)、[rest-api-fuzz-testing](https://github.com/microsoft/rest-api-fuzz-testing)
- 書籍: 「テスト駆動開発」(Kent Beck)

## UIデザイン
- Awesome: [Awesome Design Principles](https://github.com/robinstickel/awesome-design-principles), [Awesome Design](https://github.com/gztchan/awesome-design), [Awesome-UI](https://github.com/kevindeasis/awesome-ui)
- ロードマップ: [UX Design](https://roadmap.sh/ux-design)
- ガイド: [design-resources-for-developers](https://github.com/bradtraversy/design-resources-for-developers)、[Awesome Login pages](https://github.com/LoginRadius/awesome-login-pages)
- Material Design: [Material Design 3](https://m3.material.io/)、[material-theme-builder](https://material-foundation.github.io/material-theme-builder/)

---
*出典: docsリポジトリ(TakahitoSuzukiii/docs) pages/20_design配下、2026-08-18時点の内容を再構成。*
