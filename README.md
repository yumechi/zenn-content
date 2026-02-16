# zenn-content

[Zenn](https://zenn.dev) の記事・本を管理するリポジトリです。

## セットアップ

```bash
pnpm install
```

## 記事の作成・管理

```bash
npx zenn new:article        # 新しい記事を作成
npx zenn new:article --slug my-article --title "タイトル" --type tech --emoji 🔥
npx zenn new:book           # 新しい本を作成
npx zenn preview            # プレビューサーバーを起動（http://localhost:8000）
```

## 文章校正（textlint）

```bash
pnpm run lint:article       # articles/ 内の記事をチェック
pnpm run fix:articles       # 自動修正
```

## 参考リンク

- [Zenn CLIの導入手順](https://zenn.dev/zenn/articles/install-zenn-cli)
- [Zenn CLIで記事・本を管理する方法](https://zenn.dev/zenn/articles/zenn-cli-guide)
- [Zennのコンテンツ作成ガイド](https://zenn.dev/zenn/articles/editor-guide)
- [ZennのMarkdown記法一覧](https://zenn.dev/zenn/articles/markdown-guide)

## ライセンス

このリポジトリの記事は [MIT License](./LICENSE) の下で公開されています。
