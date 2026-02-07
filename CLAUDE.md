# Zenn Content Repository

Zenn（https://zenn.dev）の記事・本を管理するリポジトリ。

## パッケージマネージャー

pnpm を使用。

```bash
pnpm install    # 依存関係のインストール
pnpm update     # パッケージの更新
pnpm audit      # 脆弱性チェック
```

## Linter

textlint を使用して日本語の文章校正を行う。

```bash
pnpm run lint:article   # articles/ 内の記事をチェック
pnpm run fix:articles   # 自動修正
```

### 有効なルール

- preset-ja-technical-writing: 技術文書向けルール
- preset-ja-spacing: スペース関連ルール
- spellcheck-tech-word: 技術用語スペルチェック
- no-mix-dearu-desumasu: ですます/である調の混在チェック
- prh: 表記揺れチェック（prh.yaml）

## ディレクトリ構造

```
.
├── articles/          # Zenn 記事（Markdown）
├── books/             # Zenn 本
├── .devcontainer/     # Dev Container 設定
├── .textlintrc        # textlint 設定
├── prh.yaml           # 表記揺れルール
├── package.json
└── pnpm-lock.yaml
```
