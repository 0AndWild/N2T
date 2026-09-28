# N2T — New To This

![N2T — New To This: Just enough knowledge for your next quest.](assets/n2t-banner.png)

<p align="center">
  <a href="README.md">English</a> | <a href="README.ko.md" lang="ko">한국어</a> | <a href="README.ja.md" lang="ja">日本語</a> | <a href="README.zh-CN.md" lang="zh-CN">简体中文</a>
</p>

[![License: MIT](https://img.shields.io/badge/license-MIT-22c55e?style=flat-square)](LICENSE)
![Agent Skill](https://img.shields.io/badge/Agent-Skill-8b5cf6?style=flat-square)

> Every expert was a newbie once. You don't need to learn everything. Just enough knowledge for your next quest.

専門家も、かつてはニュービーでした。あらゆる分野を知り尽くすことはできませんし、新しいことを始めるたびに、その道の専門家になる必要もありません。

ただ、AIにうまく仕事を任せるには、作りたいものについての基礎知識が必要です。何を頼むのか、どんな条件を伝えるのか、できあがったものが意図どおりか。その判断には、分野の知識が役立ちます。

N2Tは、その最初の一歩を支えるために作りました。**すべてを学ぶのではなく、いま取り組むことに必要な分だけ理解する。** 初めて触れる概念や用語を調べ、画像・動画・実例とともにHTMLガイドにまとめる、オープンソースのAIスキルです。

たとえばAIで動画を編集するなら、編集技術を一からすべて覚える必要はありません。カット、ディゾルブ、マッチカットの違いや、それぞれが与える印象を知るだけでも、「自然につないで」より具体的に希望を伝えられます。

## ガイドでわかること

- 最初に押さえておきたい知識と、よく使われる用語
- 実務での使われ方と、勘違いしやすい点
- どこに注目すればよいかがわかる参考資料と出典
- 次に取り組むことと、今は知らなくても困らないこと

ガイドはHTMLファイルとして保存されます。専用アプリは不要で、ブラウザーでそのまま読めます。

必要になったときに、その作業について聞くだけで使えます。学習記録や定期通知の設定は必要ありません。本文はオフラインでも読めます。外部の画像や動画、リンク先の閲覧には、インターネット接続が必要な場合があります。

## 気になるカードから読む

上部に今回のクエスト、その下に**最初に知っておきたいこと・次に学ぶこと・後でよいこと**をカードで並べます。カードを開くと、短い説明と関連する画像・動画・サイトをモーダルで確認できます。プレビューで操作できない場合は、HTMLファイルをダウンロードしてブラウザーで開いてください。

## どう聞けばいい？

次の依頼文で作成したガイドです。

```text
$n2t I’m editing a video with AI, but I don’t know much about transitions—what should I know to describe the effects I want?
```

### できあがったガイド

<table>
  <tr>
    <td width="33%" align="center"><a href="assets/examples/n2t-gallery-main.jpg"><img src="assets/examples/n2t-gallery-main.jpg" alt="概念ギャラリー" width="100%"></a><br><sub>概念ギャラリー</sub></td>
    <td width="33%" align="center"><a href="assets/examples/n2t-cross-dissolve-detail.jpg"><img src="assets/examples/n2t-cross-dissolve-detail.jpg" alt="概念の詳しい説明" width="100%"></a><br><sub>概念の詳しい説明</sub></td>
    <td width="33%" align="center"><a href="assets/examples/n2t-ai-prompt-example.jpg"><img src="assets/examples/n2t-ai-prompt-example.jpg" alt="AIへの依頼例と参考資料" width="100%"></a><br><sub>AIへの依頼例と参考資料</sub></td>
  </tr>
</table>

スクリーンショット内の参考画像: [A2o dissolve — grm_wnr](https://commons.wikimedia.org/wiki/File:A2o_dissolve.ogv), [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

## 参考資料の選び方

- **画像：** 理解に役立つ参考画像をモーダル内に表示し、出典と注目する点を添えます。独自に作った説明図とは区別し、表示できる画像が見つからなければ理由を明記します。
- **動画：** 必要な内容を無料で視聴できると確認した動画だけを紹介します。有料講座、契約や購入が必要な動画、無料かどうか確認できない動画は含めません。
- **Webサイト：** 公式資料や実際のサービスを優先し、今回の作業にどう役立つかを説明します。

画像の表示を確認し、読み込めない場合も出典への案内を残すようにしています。検索やブラウザーでの検証ができない環境では、確認できなかった点を明記します。

## Skills CLIでインストール

[Node.jsとnpm](https://nodejs.org/en/download)が入っていれば、以下のコマンドですぐにインストールできます。[Skills CLI](https://github.com/vercel-labs/skills)は`npx`で実行するため、事前にインストールする必要はありません。

ターミナルで次のコマンドを実行し、画面の案内に従って利用するツールを選んでください。

```sh
npx skills add 0AndWild/N2T
```

インストール前にスキルの一覧を確認するには：

```sh
npx skills add 0AndWild/N2T --list
```

CodexとClaude Codeの両方にまとめてインストールするには：

```sh
npx skills add 0AndWild/N2T --skill n2t --agent codex claude-code
```

複数のプロジェクトで使う場合は、同じコマンドに`--global`を付けてください。

Claude Desktopの通常のチャットでは、別途インストールが必要です。`skills/n2t`フォルダー全体をZIPにして、Skills設定でアップロードし、有効にしてください。ZIP内には`n2t/SKILL.md`と関連ファイルを含めます。[Claude公式のSkillsガイド](https://support.claude.com/en/articles/12512180-use-skills-in-claude)も参照してください。

スキルの動作は`skills/n2t/SKILL.md`で定義しています。HTMLガイドの書き方は`references/html-guide.md`にまとめています。

CLIの導入方法やインストール先を指定する方法は、[詳しいセットアップ手順](docs/USAGE.ja.md)をご覧ください。

## 使い方

会話の中で作業を説明済みなら、`$n2t 今の作業に必要な知識を教えて`と短く頼んでも使えます。背景を繰り返したり、概念の名前を先に調べたりする必要はありません。

ガイドを保存するフォルダーでCodexを起動します。`--search`を付けると、Webで最新の情報を検索できます。

```sh
codex --search
```

起動したら、**Codexのチャット欄**で次のように依頼します。

```text
$n2t AIで動画を編集したいのですが、場面の切り替え方に詳しくありません。カット、ディゾルブ、マッチカットの違いと使いどころを教えてください。AIに希望の切り替えを伝える例文や、参考画像、無料で見られる動画も含めて、日本語のHTMLガイドにまとめてください。
```

Claude Codeを使う場合は、作業フォルダーで起動します：

```sh
claude
```

**Claude Codeのチャット欄**では、`/n2t`に続けて依頼します。

```text
/n2t AIで動画を編集したいのですが、場面の切り替え方に詳しくありません。カット、ディゾルブ、マッチカットの違いと使いどころを教えてください。AIに希望の切り替えを伝える例文や、参考画像、無料で見られる動画も含めて、日本語のHTMLガイドにまとめてください。
```

`$n2t`と`/n2t`は、CodexやClaude Codeを起動した後、チャット欄に入力します。何をしたいか、どこまで知っているか、何語で読みたいかも伝えると、必要な内容に絞ったガイドになります。

別の分野でも、同じように依頼できます。

```text
物流の管理画面を作っています。入庫・出庫・在庫・リードタイムが実際の業務でどう関わるのか、画面設計に必要な範囲で教えてください。ガイドはoutputs/logistics-guide.htmlに保存してください。
```

テーマだけでは必要な知識を絞れないときは、N2Tが作業の目的を確認します。参考資料は理解に役立つものを選び、内容を確認できなかった場合は、その旨を明記します。

### できあがったガイドを読む

保存先を指定しない場合、現在のワークスペースの`outputs/n2t-<quest-slug>.html`に保存します。実行環境に成果物の保存規則があれば、その規則を優先します。完了メッセージのリンク、またはHTMLファイルをブラウザーで開いてください。

## 更新とトラブルシューティング

更新、削除、その他のインストール方法は、[インストールとトラブルシューティング](docs/USAGE.ja.md)を参照してください。

## リポジトリ構成

```text
N2T/
├── README.md
├── README.ko.md
├── README.ja.md
├── README.zh-CN.md
├── docs/
└── skills/
    └── n2t/
        ├── SKILL.md                 # 両エージェント共通の実行指示
        ├── agents/
        │   └── openai.yaml          # Codexの表示情報
        ├── assets/
        │   └── gallery-guide.html
        └── references/
            └── html-guide.md        # HTMLガイドの作成基準
```

`agents/openai.yaml`はCodex用の追加メタデータです。Claude Codeは同じ`SKILL.md`と参照文書を使用し、処理はCodex専用ツールに依存しません。

インストール手順は、2026-09-28に確認した公式ドキュメントに基づいています。利用するツールや権限によって、調べられる資料やガイドの内容は変わります。

## ライセンス

[MIT](LICENSE) — 自由に使用・改変・配布できます。
