作成日: 2026-10-25 / STATUS: INFO / TOPIC: HN

# Hacker News 週間キャッチアップ（2026-10-18〜2026-10-25）

Hacker News（HN: 海外のエンジニア向けニュース投稿・議論サイト）の過去7日の上位20件です。Algolia公式Search APIで取得。要約はタイトルと公開メタ情報に基づく簡易版で、記事本文は精読していません。

## 今週のポイント

- **セキュリティ**: PHPの重大脆弱性(#3,#7,#15,#18)と、eMudhra認証局の鍵問題・事業撤退(#5,#6,#10)が議論の中心。iPhone・Switch 2の攻略報告も。
- **AI**: DeepSeek向け推論基盤(#1)、Kimi K3.1(#9)、Voxtral 3(#16)、WhatsAppの隠しAI指示(#17)。
- **開発ツール**: Docker考察(#13)。
- Rust/Go/TypeScript/Pythonは上位20件に明確な話題なし（キーワード判定でRust等に分類された記事も、実際には別内容のものがあります）。

## 上位20件

### 1. DeepInfer: High-performance inference framework for DeepSeek models
- 要点: DeepSeek系モデル向けの高性能な推論（学習済みAIに回答を生成させる処理）フレームワークの公開。
- ポイント: 2347 / コメント: 891 / 分類: ai, devtools
- 元記事: https://github.com/deepseek-ai/DeepInfer
- HN議論: https://news.ycombinator.com/item?id=50163277

### 2. Local Wikipedia: Wikipedia, but only for things a half hour walk from you
- 要点: 自宅から徒歩30分圏内の事柄だけを載せる「ローカル版Wikipedia」という試み。
- ポイント: 1635 / コメント: 251 / 分類: その他
- 元記事: https://edjefferson.com/localwiki/
- HN議論: https://news.ycombinator.com/item?id=50202285

### 3. Security advisory: Critical remote code execution vulnerabilities, update now
- 要点: PHPの重大なリモートコード実行（RCE: 外部から任意のプログラムを実行される）脆弱性の勧告。早急な更新が呼びかけられた。
- ポイント: 1558 / コメント: 659 / 分類: security
- 元記事: https://www.php.net/archive/2026.php#2026-10-21-5
- HN議論: https://news.ycombinator.com/item?id=50172041

### 4. Quad9 to exit France
- 要点: DNSサービスQuad9がフランスからの撤退を発表。
- ポイント: 1367 / コメント: 475 / 分類: その他
- 元記事: https://quad9.net/news/blog/au-revoir-france/
- HN議論: https://news.ycombinator.com/item?id=50195959

### 5. eMudhra intermediate CA compromise
- 要点: インドの認証局eMudhraの中間CA（証明書を発行する中間の認証局）が侵害された件の報告。
- ポイント: 1281 / コメント: 504 / 分類: その他
- 元記事: https://emudhra.we-have-a-problem.com/
- HN議論: https://news.ycombinator.com/item?id=50166579

### 6. eMudhra to exit global SSL/TLS certificate business
- 要点: eMudhraが世界向けSSL/TLS証明書事業から撤退すると発表。#5・#10の問題を受けた動きとみられる。
- ポイント: 1152 / コメント: 745 / 分類: その他
- 元記事: https://emudhra.com/en/press-release/emudhra-to-exit-global-ssl-tls-certificate-business
- HN議論: https://news.ycombinator.com/item?id=50195110

### 7. PHP 8.2.35
- 要点: PHP 8.2系のリリース。セキュリティ更新(#3)と同時期のもの。
- ポイント: 1106 / コメント: 578 / 分類: その他
- 元記事: https://github.com/php/php-src/releases/tag/php-8.2.35
- HN議論: https://news.ycombinator.com/item?id=50180873

### 8. Today, we hacked what we'd set out to hack: the iPhone
- 要点: 研究チームがiPhoneのハッキングに成功したと報告するブログ。
- ポイント: 1091 / コメント: 708 / 分類: その他
- 元記事: https://blog.calif.io/p/iphone
- HN議論: https://news.ycombinator.com/item?id=50211474

### 9. Kimi K3.1 Pro and K3.1 Pro Highspeed
- 要点: Kimi K3.1 Pro と高速版のAIモデル発表。
- ポイント: 1070 / コメント: 665 / 分類: ai
- 元記事: https://www.kimi.ai/blog/kimi-k3-1-pro
- HN議論: https://news.ycombinator.com/item?id=50212065

### 10. Eight Bits of Trust: eMudhra's CA keys cracked in milliseconds
- 要点: eMudhraのCA鍵がごく短時間で解読できてしまう問題の技術解説（鍵の強度不足）。
- ポイント: 952 / コメント: 461 / 分類: rust
- 元記事: https://scotthelme.co.uk/eight-bits-of-trust-emudhras-ca-keys-cracked-in-milliseconds/
- HN議論: https://news.ycombinator.com/item?id=50177916

### 11. Show HN: SimCity, but with Permits
- 要点: 都市建設ゲーム「SimCity」に建築許可（Permits）の仕組みを持ち込んだ Show HN（作品紹介）。
- ポイント: 938 / コメント: 425 / 分類: ai
- 元記事: https://permit.petercai.com/
- HN議論: https://news.ycombinator.com/item?id=50170593

### 12. Apple Music 404 Not Found
- 要点: 存在しないURLのApple Musicの404ページが話題に。
- ポイント: 926 / コメント: 273 / 分類: その他
- 元記事: https://music.apple.com/this-url-doesnt-exist
- HN議論: https://news.ycombinator.com/item?id=50207910

### 13. Docker is weird
- 要点: Dockerの「変な」挙動・設計への考察ブログ。
- ポイント: 866 / コメント: 366 / 分類: devtools
- 元記事: https://codeandcake.dev/posts/2026-10-22-docker-is-weird
- HN議論: https://news.ycombinator.com/item?id=50202681

### 14. Jailbreaking the Switch 2
- 要点: 任天堂Switch 2のジェイルブレイク（機器の制限解除）に関する技術ブログ。
- ポイント: 833 / コメント: 306 / 分類: ai
- 元記事: https://pepsipu.com/blog/2026-10-switch2-jailbreak-ns2jb/
- HN議論: https://news.ycombinator.com/item?id=50192536

### 15. Today's PHP security release, and how we're strengthening security
- 要点: PHP財団によるセキュリティリリース解説と、今後のセキュリティ強化策。
- ポイント: 815 / コメント: 402 / 分類: security
- 元記事: https://thephp.foundation/blog/2026/10/21/todays-php-security-release-and-how-were-strengthening-php-security/
- HN議論: https://news.ycombinator.com/item?id=50182987

### 16. Voxtral 3
- 要点: Mistral AIの音声モデル Voxtral 3 の発表。
- ポイント: 769 / コメント: 201 / 分類: ai
- 元記事: https://mistral.ai/news/voxtral-3/
- HN議論: https://news.ycombinator.com/item?id=50168396

### 17. WhatsApp's help pages hid LLM instructions: dont recommend a regulator
- 要点: WhatsAppのヘルプページに、AIに「規制当局を勧めるな」と指示する隠し文があったとの指摘。
- ポイント: 743 / コメント: 221 / 分類: ai
- 元記事: https://redact.dev/blog/whatsapp-help-pages-hidden-ai-instructions
- HN議論: https://news.ycombinator.com/item?id=50159341

### 18. Tell HN: I unknowingly broke the PHP RCE embargo. I am sorry
- 要点: PHPのRCE情報の公開解禁前（エンバーゴ）に、意図せず情報を漏らしてしまったとの投稿者による謝罪。
- ポイント: 738 / コメント: 266 / 分類: その他
- 元記事: https://news.ycombinator.com/item?id=50193416
- HN議論: https://news.ycombinator.com/item?id=50193416

### 19. EA is shutting down BioWare
- 要点: EAがゲーム開発会社BioWareを閉鎖するとの報道。
- ポイント: 705 / コメント: 477 / 分類: その他
- 元記事: https://www.theverge.com/games/1015647/ea-is-shutting-down-bioware
- HN議論: https://news.ycombinator.com/item?id=50184586

### 20. Meta ordered to pay $25B penalty in New Mexico Cambridge Analytica case
- 要点: MetaにニューメキシコでのCambridge Analytica事件で約250億ドルの制裁金命令との報道。
- ポイント: 697 / コメント: 428 / 分類: その他
- 元記事: https://www.cnbc.com/2026/10/21/meta-new-mexico-cambridge-analytica-penalty.html
- HN議論: https://news.ycombinator.com/item?id=50184820

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
