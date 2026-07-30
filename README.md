# AI Agent Tips

Claude CodeやCodexなどのAIエージェントを業務で使う中で見つけた、ちょっと便利な設定・工夫をまとめたサイトです。

## 公開URL

GitHub Pagesでホスティングしています：
`https://aoyama-webrider.github.io/ai-agent-tips/`

## 構成

```
ai-agent-tips/
├── index.html        # Tips一覧のトップページ
├── timestamp/        # IDE内Claude Codeのチャットに日時を表示するTips
│   └── index.html
├── sound/            # Claude Codeの完了・許可待ちを音で知らせるTips
│   └── index.html
├── codex/            # Claude CodeからCodexを呼び出して使うTips
│   └── index.html
├── ide-codex/        # VS CodeにCodexパネルを追加するTips
│   └── index.html
├── review-strategy/  # タスクの重さでAIのレビュー方法を使い分けるTips
│   └── index.html
└── README.md
```

## Tipsの追加方法

1. ルート直下に新しいフォルダを作る（例: `git-branch/`）
2. その中に `index.html` を置く（既存記事をコピーして中身を差し替えるのが早い）
3. ルートの `index.html` の `tips-grid` に新しいカードを追加（あわせて `tips published` の件数と `Last updated` も更新）
4. コミット・プッシュ → GitHub Pagesが自動更新

### 記事を書くときの約束

- 本文の段落は句点改行（1文1行）にする。`<br>` を句点の後ろに入れる。箇条書き・表・コードブロックはそのまま
- 文章の途中に部分的な太字（`<strong>`）を入れない
- `<head>` に `<meta name="robots" content="noindex, nofollow">` と `og:type` / `og:title` / `og:description` / `og:url` を入れる
- 想定環境は「OS/エディタ ＋ 使うツール ＋ 必要なアカウント」の順で書く。前提になるもの（Node.jsのバージョン、管理者権限など）は本文の途中ではなくここに出す
- 表は `<div class="table-wrap">` で包み、`<th scope="col">` を付ける
- コールアウトの背景に色やグラデーションは敷かない。種類は左ボーダーと見出しの色だけで示す
- `text-transform: uppercase` は使わない（コマンド名や ChatGPT の表記が崩れる）
- `.article-content p` が詳細度で勝つので、段落に別のクラス（`.where` `.prompt` `.callout-title` など）を当てるときは `.article-content .xxx` と書く
- アンカーのidは `<section>` に付ける。オフセットは `.article-content section { scroll-margin-top }` が持っている
- 記事末尾は「関連するTips（内部リンク）」と「参考リンク（外部の一次情報）」の2節に分ける
- 手順の場所ラベルは、コマンドを打つ手順は「実行場所」、GUIを操作する手順は「操作場所」

### 技術的な内容を書くときの注意

- フックのコマンドは既定でbashに渡される（WindowsでもGit Bashがあればbash経由）。`$` を含むPowerShellを1行で書くと変数が空になるので、`.ps1` ファイルに出すか、JSON内で `\\$` と書く
- 日本語を含む `.ps1` はUTF-8 BOM付きで保存する
- 外部サービスの仕様（プラン、モデル、コマンド一覧）は公式ドキュメントを開いて確認する。ローカルの拡張機能やプラグインの説明文は古いことがある
- OpenAIのドキュメントは `developers.openai.com/codex/*` から `learn.chatgpt.com/docs/*` へ移っている

## ローカルでの確認

`index.html` をブラウザで直接開けばOK。サーバ不要。

## 書く予定のネタ（サイトには出さない）

以前はトップページに「ストック中」として出していたが、書く前のものを公開しても読者の役に立たないため、ここで管理する。

- Gitブランチの自動通知（`UserPromptSubmit` フックでブランチ名を注入する応用）
- カスタムスキルの設計（`.claude/skills/` で自分用のワークフローを作る）
- MCP活用パターン（外部サービスとの接続をどこまで許すか）
- 許可プロンプトを減らす設定（`permissions.allow` の設計方針）
- グローバル `CLAUDE.md` とプロジェクト `CLAUDE.md` の書き分け

## 検索エンジン対策

全ページの `<head>` に `<meta name="robots" content="noindex, nofollow">` を入れている。

`robots.txt` は置いていない。このサイトは `aoyama-webrider.github.io/ai-agent-tips/` というサブディレクトリ配置のため、置いても `/ai-agent-tips/robots.txt` になり、ドメイン直下しか読まないクローラーには無視される。記事を追加するときも、メタタグの記述を忘れないこと。

## 対象読者

- IDE（VS Code・Cursorなど）やターミナルでClaude Codeを使い始めている人
- フックや設定ファイルのカスタマイズに興味がある人

## ライセンス

技術的な内容は自由に参考にしてください。誤りの指摘や改善案歓迎です。
