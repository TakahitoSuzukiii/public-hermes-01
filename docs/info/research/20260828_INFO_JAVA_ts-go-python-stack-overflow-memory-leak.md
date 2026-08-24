作成日: 2026-08-28 / STATUS: INFO / TOPIC: JAVA

# TypeScript・Go・Python のスタックオーバーフローとメモリリーク

> 前回2本の学習ノート([スタックとヒープ](20260828_INFO_JAVA_stack-heap-primitive-reference-types.md)、[スタックオーバーフローとメモリリーク](20260828_INFO_JAVA_stack-overflow-and-memory-leak.md))の続編。TypeScript(JavaScript)・Go・Pythonの3言語について、ガベージコレクション(GC)方式の違いを軸に、スタックオーバーフロー・メモリリークの特徴と回避手法を整理する。

## 0. 結論(先出し) — 3言語のGC方式比較

| 言語 | GC方式 | 特徴 |
|---|---|---|
| **TypeScript(JS)** | マーク&スイープ方式(V8等) | 「どこからも辿れないオブジェクト」を定期的に検出して回収。循環参照があっても回収できる |
| **Go** | 並行マーク&スイープ方式 | GCによる自動回収に加え、goroutine(軽量スレッド)特有のリークに要注意 |
| **Python** | 参照カウント + 世代別GC(循環参照検出) | 基本は参照カウントで即座に回収、循環参照だけ別途GCが定期的に検出・回収 |

**共通の教訓**: どの言語もGCが「参照が切れたオブジェクト」を自動回収してくれるが、**「意図せず参照が残り続けているケース」だけはGCでは救えない**。これがメモリリークの本質。

## 1. TypeScript(JavaScript) 編

### 1-1. スタックオーバーフロー

- エラー名: `RangeError: Maximum call stack size exceeded`
- 原因は他言語と同様、**終了条件のない/深すぎる再帰呼び出し**
- 対策: 再帰をループ(反復処理)に書き換える、末尾再帰の活用(ただしJSエンジンによっては末尾呼び出し最適化が保証されない点に注意)

出典: [Qiita「JavaScriptにおける再帰とスタック制御」](https://qiita.com/CRUD5th/items/5a27063425510c8c13f1)

### 1-2. メモリリーク

JavaScriptのGC(マーク&スイープ方式)は循環参照があっても回収できる設計だが、それでも以下のパターンでリークが発生する。

1. **クロージャによる意図しない参照保持**: クロージャが外側のスコープの変数を掴んだままにしてしまい、本来不要になった大きなオブジェクトが解放されない
2. **DOMイベントリスナーの解除忘れ**: `addEventListener`したまま`removeEventListener`しないと、DOM要素への参照が残り続ける
3. **グローバル変数・キャッシュの肥大化**: グローバルスコープやキャッシュ用オブジェクトに要素を追加し続け、削除しない

出典: [Qiita「JavaScript の仕組み：メモリ管理+4つの共通のメモリリーク処理方法」](https://qiita.com/tkdn/items/ea4f034e0d661def244a)

### 1-3. 循環参照とその回避

JavaScriptのGC(マーク&スイープ)は「ルート(グローバルオブジェクト等)から辿れるかどうか」で判定するため、**AとBが互いを参照し合っていても、外部から誰も参照していなければ正しく回収される**。ただし、DOM要素とイベントリスナーのクロージャが絡む場合など、ルートから辿れる経路が意図せず残ってしまうケースは注意が必要。

**回避方法:**
- 不要になったイベントリスナーは明示的に解除する
- 大きなオブジェクトを長期間保持するクロージャは避ける、または使い終わったら参照をnullにする
- `WeakMap`/`WeakSet`を使う(キーが他から参照されなくなれば自動的にエントリも消える「弱い参照」)

## 2. Go 編

### 2-1. スタックオーバーフロー

Goのgoroutine(軽量スレッド)は、**開始時は小さいスタックサイズで始まり、必要に応じて動的に拡張される**という他言語にない特徴を持つ。そのため通常の再帰ではスタックオーバーフローは起きにくいが、**無限再帰や極端に深い再帰では最終的にクラッシュする**。

出典: [Qiita「Go の goroutine stack と g0 stack は何をしているのか」](https://qiita.com/yingtian0/items/cefc972ee461c121f05b)

**回避方法:**
- 再帰の終了条件を明確にする
- 深さが予測できない処理はループへ書き換える

### 2-2. メモリリーク(goroutineリーク)

Go特有の要注意ポイントが**「goroutineリーク」**。goroutine自体はGCの対象になるオブジェクトではなく、**終了せずに残り続けたgoroutineがメモリを圧迫し続ける**という現象。

**典型的な原因:**
1. **チャンネルの送受信がブロックしたまま終了しない**: 送信側・受信側のどちらかが待ち続け、goroutineが永久にブロックされる
2. **context(コンテキスト)によるキャンセル処理の未実装**: 処理を途中で止める仕組みがなく、不要になったgoroutineが動き続ける
3. **for-selectループの終了条件漏れ**: ループを抜ける条件が設計されていない

本番環境で秒間数百回呼ばれるWebサービスにこのパターンが混入すると、goroutineがメモリを食いつぶしOOM(Out of Memory)でプロセスがクラッシュする、という実例が複数報告されている。

出典: [Kawa Portfolio「Go言語のGoroutineリーク防止策とContext」](https://kawagame.com/blog/go-goroutine-channel-leak-prevention/)、[Zenn「goroutineリークで本番環境のメモリを食いつくしかけた話」](https://zenn.dev/y640/articles/goroutine-leak-blocking-channel)

**回避方法:**
- `context.Context`を使い、goroutineに明確なキャンセル・タイムアウトの仕組みを持たせる
- チャンネル操作には必ず`select`でタイムアウトやキャンセルのケースを用意する
- `runtime.NumGoroutine()`で起動中のgoroutine数を監視する、またはプロファイリングツール(Go 1.26以降は「Goroutine Leak Profiles」機能も追加)を活用する

出典: [Future Architect「Go 1.26リリース連載 Goroutine Leak Profiles」](https://future-architect.github.io/articles/20260128a/)

## 3. Python 編

### 3-1. スタックオーバーフロー

- エラー名: `RecursionError: maximum recursion depth exceeded`
- Pythonはデフォルトで**再帰の深さの上限が1000回程度**に設定されている(`sys.getrecursionlimit()`で確認可能)
- `sys.setrecursionlimit()`で上限を引き上げることは技術的に可能だが、**Pythonのインタプリタ自体のCスタックの制約もあるため、上限を上げすぎると別のクラッシュ(セグメンテーションフォルト等)を招くリスクがある**

出典: [Qiita「【Python】再帰のエラーを防ぐ」](https://qiita.com/hrel11/items/e0f0465d8d987b5ef67e)

**回避方法:**
- 再帰をループへ書き換える(Pythonは末尾再帰最適化を行わないため、深い再帰が必要な処理は特にループ推奨)
- `setrecursionlimit`で安易に上限を上げるのではなく、根本的にアルゴリズムを見直す

### 3-2. メモリリーク

Pythonのメモリ管理は**「参照カウント方式」が基本**。オブジェクトが参照される数をカウントし、0になった瞬間に即座にメモリを解放する。

しかし、**参照カウント方式だけでは循環参照(AがBを参照し、BもAを参照する)を解決できない**。AとBが互いを参照している場合、外部から誰も使っていなくても、互いのカウントが0にならず解放されない。

出典: [Qiita「Pythonのメモリ管理: ガベージコレクション、弱参照、循環参照の問題と解決策」](https://qiita.com/Tadataka_Takahashi/items/a5d9654bba38d4eb3686)

この問題に対処するため、Pythonには**世代別ガベージコレクション(GC)が別途搭載**されており、定期的に循環参照を持つオブジェクト群を検出し、参照されていないものをまとめて解放する。

出典: [nexunity.tech「【Python】メモリ管理 - ガベージコレクションについて」](https://nexunity.tech/post/python-memory-management/)

### 3-3. 循環参照とその回避(Pythonの具体例)

```python
import gc

class Node:
    def __init__(self, name):
        self.name = name
        self.next = None

node1 = Node("Node 1")
node2 = Node("Node 2")
node1.next = node2
node2.next = node1  # 循環参照が発生

del node1
del node2
# この時点では参照カウントが0にならないため、通常は解放されない
gc.collect()  # 明示的にGCを実行すると循環参照ごと回収される
```

**回避方法:**
- 循環参照が発生しうる構造(双方向リンクリスト、親子が互いを参照するツリー構造等)には、**`weakref`モジュールで弱い参照**を使う。弱い参照はカウントに影響を与えないため、循環参照そのものを作らずに済む
- `gc`モジュールで明示的にガベージコレクションを実行するAPIも用意されているが、根本対策は「循環参照を作らない設計」

出典: [emptypage.jp「__del__, gc, 循環参照, weakref」](https://emptypage.jp/notes/py-__del__-and-refcycle.html)

## 4. 3言語まとめ表

| 観点 | TypeScript(JS) | Go | Python |
|---|---|---|---|
| **スタックオーバーフローの主因** | 深い/無限の再帰呼び出し | 深い/無限の再帰呼び出し(goroutineは動的拡張スタックのため比較的発生しにくい) | 深い/無限の再帰呼び出し(デフォルト上限は約1000回と他言語より低め) |
| **メモリリークの主因** | クロージャの参照保持、イベントリスナー解除忘れ | goroutineリーク(ブロックしたまま終了しないgoroutine) | 循環参照(参照カウント方式の弱点) |
| **循環参照への耐性** | GC(マーク&スイープ)が自動対応 | (goroutine自体はGC対象ではなく別問題) | 参照カウントだけでは非対応。世代別GCが別途補完 |
| **弱い参照の仕組み** | `WeakMap`/`WeakSet` | (Goには直接的な弱参照の標準機構は薄い。設計で回避) | `weakref`モジュール |
| **回避の基本姿勢** | 参照のライフサイクルを意識し、不要な参照を明示的に切る | goroutineに必ず終了条件(context等)を持たせる | 循環参照が起きうる構造にはweakrefを使う |

## 5. スタックオーバーフロー・メモリリークを回避する共通のプログラミング手法

1. **再帰には必ず終了条件を設け、深さが不確定な処理はループに書き換える**(3言語共通)
2. **「使い終わったら手放す」を徹底する**: イベントリスナーの解除、goroutineの終了、循環参照を作らない設計など、言語ごとの「手放し方」を理解して実践する
3. **弱い参照の仕組みを活用する**: `WeakMap`(JS)、`weakref`(Python)など、GCの回収対象になりやすい参照方式を積極的に使う
4. **プロファイリング・監視を習慣化する**: メモリリークは即座に症状が出ないため、定期的にメモリ使用量やgoroutine数等をモニタリングする文化を持つ
5. **GC方式の違いを理解したうえで言語ごとの「弱点」を把握する**: 参照カウント方式(Python)は循環参照に弱い、goroutine(Go)は終了漏れに弱い、といった言語特性を踏まえて設計する

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。