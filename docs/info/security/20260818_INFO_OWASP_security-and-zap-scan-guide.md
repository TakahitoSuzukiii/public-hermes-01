# セキュリティ 学習・実装ガイド集

Webアプリケーション/クラウド/CI-CDにおけるセキュリティの基礎知識、脆弱性診断の考え方、OWASP公式チートシートの要点(日本語訳)、OWASP ZAPによる脆弱性スキャンの手順をまとめたものです。実装例のIP/アカウントID等は全てプレースホルダー化されています(元docsリポジトリの記述もプレースホルダーのみで実値の混入なし)。

## 脆弱性・脆弱性診断の基礎
- 脆弱性とは: コンピュータ・ソフトウェア・ネットワークが抱える弱点
- 脆弱性診断: セキュリティ要件充足の確認、弱点の有無を調べるテスト
- 参考: [脆弱性診断士スキルマッププロジェクト(OWASP Japan)](https://github.com/OWASP/www-chapter-japan/tree/master/skillmap_project), [Webシステム/Webアプリケーションセキュリティ要件書(OWASP Japan)](https://github.com/OWASP/www-chapter-japan/tree/master/secreq)
- Awesome: [Awesome Security](https://github.com/sbilly/awesome-security), [Awesome Web Security](https://github.com/qazbnm456/awesome-web-security), [android-security-awesome](https://github.com/ashishb/android-security-awesome)

## OWASPと診断手法
- 参考記事: [AWSにおける安全なWebアプリの作り方](https://dev.classmethod.jp/articles/awssummit-2021-aws-55/)、[Webアプリの脆弱性とセキュリティガイドライン(AWS PDF)](https://d1.awsstatic.com/events/jp/2021/summit-online/AWS-55_AWS_Summit_Online_2021_Developing-Secure-Web-Applications-on-AWS.pdf)、[SCA/SAST/DASTを使ったAWS DevSecOps CI/CDパイプライン構築](https://aws.amazon.com/jp/blogs/devops/building-end-to-end-aws-devsecops-ci-cd-pipeline-with-open-source-sca-sast-and-dast-tools/)、[ZAPping the OWASP Top 10(2021)](https://www.zaproxy.org/docs/guides/zapping-the-top-10-2021/)
- セキュリティテストの3分類:
  - **SAST**(静的アプリケーション解析/ソースコード診断): [Source Code Analysis Tools(OWASP)](https://owasp.org/www-community/Source_Code_Analysis_Tools#)
  - **DAST**(動的アプリケーション解析=OWASP ZAP等。類似ツール: Burp Suite, Nikto, Fiddler): [Vulnerability Scanning Tools(OWASP)](https://owasp.org/www-community/Vulnerability_Scanning_Tools)
  - **SCA**(ソフトウェアコンポジション解析、依存ライブラリの脆弱性調査)
- OWASP Cheat Sheet Series: [公式](https://cheatsheetseries.owasp.org/), [GitHub](https://github.com/OWASP/CheatSheetSeries)
- OWASP ZAP本体: [zaproxy(GitHub)](https://github.com/zaproxy/zaproxy)
- その他OWASP資料: [OWASP Serverless Top 10](https://owasp.org/www-project-serverless-top-10/), [OWASP Proactive Controls](https://owasp.org/www-project-proactive-controls/), [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)

## IPA・脆弱性識別子関連
- [安全なウェブサイトの作り方(IPA 改訂第7版)](https://www.ipa.go.jp/security/vuln/websecurity/about.html)
- [共通脆弱性タイプ一覧 CWE概説(IPA)](https://www.ipa.go.jp/security/vuln/scap/cwe.html)、[CWE公式(mitre)](https://cwe.mitre.org)、[JVN](https://jvn.jp/index.html)
- [共通脆弱性識別子 CVE概説(IPA)](https://www.ipa.go.jp/security/vuln/scap/cve.html)、[CVE公式](https://cve.mitre.org/)
- [共通脆弱性評価システム CVSS v3概説(IPA)](https://www.ipa.go.jp/security/vuln/scap/cvssv3.html)、[CVSS Calculator](https://github.com/cvssjs/cvssjs)
- [Google Hacking Database](https://www.exploit-db.com/google-hacking-database)

## 代表的な攻撃と対策の要点
- **WAF(Web Application Firewall)**: サイバー攻撃からWebアプリを守る対策。シグネチャ自動更新、Cookie保護、特定URL除外/IP拒否、ログ収集・レポート出力が主な機能。対策手法としてシグネチャ・スコアリング・AIが挙げられる。[解説記事](https://www.kagoya.jp/howto/engineer/itsystem/waf01/)
- **XSS(クロスサイトスクリプティング)**: フィッシング詐欺・セッションハイジャック・Cookie窃取・サイト改ざんにつながる。対策: 入力値制限、サニタイジング(エスケープ)、WAF設定。[解説記事](https://www.kagoya.jp/howto/it-glossary/security/xss/)
- **SQLインジェクション**: 対策の原則はプリペアドステートメントの使用(文字列を正しくマッピングし、不正なSQL文の生成を防ぐ)。[解説記事](https://www.kagoya.jp/howto/it-glossary/security/sql-injection/)
- **DoS/DDoS攻撃**: 攻撃対象サーバーに大量データを送りつけ負荷をかけサービス停止を狙う。[解説記事](https://www.kagoya.jp/howto/engineer/infosecurity/dos-ddos/)
- **Cookie/セッション管理**: [cookieとsessionについて](https://zenn.dev/airiswim/articles/3ea83df67edf5d)、[Cookie/SessionStorage/LocalStorage/IndexedDBまとめ](https://zenn.dev/tm35/articles/584ece2d771a4b)、[HTTP Cookieの使用(MDN)](https://developer.mozilla.org/ja/docs/Web/HTTP/Cookies)

## OWASP Cheat Sheet Series 要点(日本語訳・元docsリポジトリより)
以下は各チートシートの概要。詳細は公式(英語)またはリンク先を参照。

| チートシート | 要点 |
|---|---|
| [Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) | 認証(AuthN)は主張された身元をパスワード・指紋・トークン等の認証子で検証するプロセス。デジタルアイデンティティはオンライン取引における主体の一意な表現 |
| [Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) | 認可は「要求されたアクション/サービスが承認されているか」を検証するプロセスで認証とは異なる概念(NIST定義)。認証済みユーザーが全リソースにアクセスできるとは限らない |
| Authorization Testing Automation | 認可の実装はセキュリティ上最重要項目の一つ。機能追加/変更時に認可への影響評価を怠ることが問題の主因になりやすい |
| [CI/CD Security](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html) | CI/CDパイプラインは現代のSDLCの要だが攻撃対象にもなりやすく、パイプライン自体のセキュリティ対策が重要 |
| [Cloud Architecture Security](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Cloud_Architecture_Cheat_Sheet.html) | クラウドアーキテクチャ設計/レビュー時の必須セキュリティパターン。リスク分析・脅威モデリング・攻撃サーフェス評価が前提 |
| Database Security | SQL/NoSQLデータベースの安全な設定方法。バックエンドDBは他サーバーから分離し接続先ホストを最小化すべき |
| Error Handling | エラーハンドリングもセキュリティの一部。攻撃は偵察フェーズ(サーバー/フレームワーク/ライブラリのバージョン等の情報収集)から始まる |
| [Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html) | パスワード再設定機能はユーザー列挙攻撃等の脆弱性の温床になりやすい |
| HTTP Security Response Headers | 適切なHTTPレスポンスヘッダーはXSS・クリックジャッキング・情報漏えい対策として有効 |
| Microservices Security | マイクロサービスの認証・認可はAPIゲートウェイでの一元化(エッジレベル認可)が一般的だが、内部サービスへの直接接続を防ぐ相互認証等の緩和策も必要 |
| Mobile Application Security | モバイルアプリ特有のセキュリティ考慮点(アーキテクチャ・設計含む)への入門ガイド |
| [OAuth 2.0 Protocol](https://cheatsheetseries.owasp.org/cheatsheets/OAuth2_Cheat_Sheet.html) | OAuth2.0のベストプラクティス。APIの保護標準となりOpenID Connectのフェデレーテッドログインの基盤にもなっている |
| REST Security | RESTはRoy FieldingのPh.D論文由来のアーキテクチャスタイル。HTTP経由の通信で最も一般的に使われる |
| [SAML Security](https://cheatsheetseries.owasp.org/cheatsheets/SAML_Security_Cheat_Sheet.html) | SAMLは認可・認証情報交換のオープン標準。メッセージの機密性・整合性検証にはTLS1.2が一般的な解決策 |
| Secure Product Design | 製品設計段階からのセキュリティ組み込みに関するガイダンス |
| [Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html) | セッション管理の安全な実装方法 |
| Transaction Authorization | 取引の認可・多要素検証に関するガイダンス |
| [Vulnerability Disclosure](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerability_Disclosure_Cheat_Sheet.html) | 脆弱性の適切な開示プロセスに関するガイダンス |
| Web Service Security | Webサービス(SOAP/REST等)全般のセキュリティ対策 |
| Vulnerable Dependency Management | 依存ライブラリの脆弱性管理プロセス |
| DotNet Security | .NET/ASP.NET Core固有のセキュリティ対策集 |

※原文は英語。docsリポジトリには日本語訳版が保存されている(分量が大きいため詳細は割愛し要点のみ抜粋)。

## OWASP ZAPによる脆弱性スキャン運用手順(Docker/ECS Fargate版)

OWASP ZAPをDockerコンテナ化し、AWS ECS Fargate上でスキャンジョブとして実行する運用手順の記録。**すべてのアカウントID・URLはプレースホルダーであり実環境の値は含まれていません。**

### 参考記事
- [OWASP ZAPのテストをCI/CDに組み込む](https://qiita.com/kemmy-qei/items/ad9c5417eee71277c67f)
- [Docker版OWASP ZAPを動かしてみる](https://qiita.com/koujimatsuda11/items/83558cd62c20141ebdda)
- [OWASP ZAPの設定と使い方](https://qiita.com/sangi/items/ba7e3d39237045c9be36)
- [Docker版OWASP ZAPでWebアプリの簡易脆弱性診断](https://dev.classmethod.jp/articles/easy-vulnerability-diagnosis-of-web-app-with-owasp-zap-on-docker/)
- [侵入テスト(AWS公式)](https://aws.amazon.com/jp/security/penetration-testing/)

### 手順概要(v2: ECS Fargate運用)
1. **Dockerイメージ作成**: `owasp/zap2docker-stable`ベースにzap.conf・entrypoint.shを組み込み、ポート8090を公開
2. **entrypoint.sh**: `zap.sh -daemon`でZAPをデーモン起動→`zap-cli quick-scan`でスキャン実行→HTML形式でレポート出力(`report.html`)。本番運用時は`tail -f /dev/null`のデバッグ保持行を削除すること
3. **zap.conf**: APIアクセス許可アドレス(`api.addrs.addr.name`)、プロキシ設定、スパイダー設定(最大深度5・最大時間60分)、レポート出力設定を定義
4. **ECRへのpush**: `docker build` → `aws ecr create-repository` → `aws ecr get-login-password | docker login` → `docker tag` → `docker push`（コマンド内の`[account-id]`は実行時に自環境のアカウントIDへ置換する）
5. **AWSインフラ準備**: VPC・Subnet・IGW・ルートテーブル・ALB・セキュリティグループを個別作成(命名規則: `<プロジェクト名>-<用途>`)
6. **ECS Fargateタスク定義**: `executionRoleArn`にIAMロールARN(プレースホルダー`your-account-id`)を指定、コンテナ環境変数`TARGET_URL`でスキャン対象URLを渡す
7. **タスク登録・クラスター作成・サービス作成**: `aws ecs register-task-definition` → `aws ecs create-cluster` → `aws ecs create-service`

参考: [ECR/ECS/Fargateのコンテナ知識まとめ](https://qiita.com/nyandora/items/0fa064f8a4402939673b)、[ECS用コンテナイメージ作成(AWS公式)](https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/create-container-image.html#use-ecr)、[AWS Fargate環境構築手順](https://zenn.dev/ttani/articles/aws-fargate-setup)

### 手順概要(v1: docker-compose簡易運用)
- `docker-compose up -d` → `zap-baseline.py -t <対象URL> -g config_file -r report.html -w report.md` → `docker-compose down`
- オプション: `-c`(警告レベル設定ファイル)、`-m`(スパイダリング時間・分)、`-g`(デフォルト設定生成)、`-D`(パッシブスキャン待機秒数)、`-T`(起動〜スキャン完了の最大時間)
- 参考: [ZAP CLI](https://github.com/Grunny/zap-cli)、[Command Line(公式)](https://www.zaproxy.org/docs/desktop/cmdline/)、[Windows Docker環境構築](https://zenn.dev/felmy/articles/108c3c30ab7d86)

---
*出典: docsリポジトリ(TakahitoSuzukiii/docs) pages/50_security配下(owasp_cheat_sheet含む)、2026-08-18時点の内容を再構成。実装コード中のアカウントID・URL等は全てプレースホルダー(機密情報の混入なし)。*
