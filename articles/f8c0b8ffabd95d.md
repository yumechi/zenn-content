---
title: "Github Apps による認証で private リポジトリから poetry install を行う方法"
emoji: "📚"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["python", "github", "poetry", "githubactions"]
published: false
---

仕事がらプライベートリポジトリで管理しているライブラリをインストールしてその次の動作を行う、ということがしたかったのですが、結構苦労したので記録を残しておきます。

Qiita, Zenn の両方に投稿予定です。

## 前提条件

- GitHub でプライベートリポジトリを管理している
- poetry を使っている
- GitHub Actions で CI/CD をしたい
- 秘密鍵での通信はしたくない

## リポジトリの関係性

命名に特に意味はありませんが、仮に出てきた場合に備えて一応書いておきます。

```mermaid
graph TB
    利用リポジトリ（use_konpeko_package） --> ライブラリパッケージ（konpeko_package）
```

## GitHub Actions でやりたいフロー

- actions/checkout でリポジトリを取得
- python のセットアップ
- GitHub Apps で認証トークンを取得
- 認証トークンに沿った URL パターンに変更し、poetry install を実行

このうち難しかったのが「GitHub Actions で認証トークンを取得」「認証トークンに沿った URL パターンに変更し、poetry install を実行」の２つでした。

## GitHub Actions で認証トークンを取得

Github Apps で認証トークンを取得するためには、以下のような手順が必要です。

- GitHub Apps を作成
    - 作成方法については既にいろいろな方が記事を書いているので省略します
        - 自分はこちらの記事がわかりやすかったです
            - [GitHub Apps + GitHub Actionsで必要なアクセス権限のみ付与した一時的なアクセストークンを発行する | DevelopersIO](https://dev.classmethod.jp/articles/getting-an-access-token-with-only-the-necessary-permissions-on-github-appsgithub-actions/)
            - [GitHub Apps経由で発行したtokenを用いて、GitHub Actionsで使う](https://zenn.dev/suzutan/articles/how-to-use-github-apps-token-in-github-actions)
    - 作成したら関連するリポジトリにインストールします


少し古い記事を参照すると tibdex/github-app-token を使った例が出てきますが、今は [actions/create-github-app-token](https://github.com/actions/create-github-app-token) というアクションが公式から提供されています。
tibdex/github-app-token で指定していたような使い方とほぼ変わりませんが、公式から出ているというのは信頼性が高いと思いますので、今回はこちらにしました。

## 参考になった記事

- [【R&D DevOps通信】Poetryでプライベートパッケージを扱う(GitHub, AWS CodeArtifact, GCP Artifact Registry) - Sansan Tech Blog](https://buildersbox.corp-sansan.com/entry/2022/08/22/110000)
- [GitHub Apps のトークンを使ってプライベートリポジトリにアクセスする](https://zenn.dev/farstep/articles/32751d92dd1452)



## ほかの方法

一応調べたものを載せておきます。

### 秘密鍵をコピーして使う方法

セキュリティ的なところで運用が難しいのではないか？ と思って今回は選択しませんでした。

- [GitHub Actionsでprivate repositoryのPythonライブラリを含むDockerイメージをビルドする #Python - Qiita](https://qiita.com/ninomiyt/items/b564f8a742e1bb18ce57)
- [GitHub Actions で private repository の node module をインストールする #Node.js - Qiita](https://qiita.com/couzie/items/33d837d6f0dc049155cd)

### Personal Token を使う方法

同じくセキュリティ的な懸念から運用が難しいのではないか？ と思って今回は選択しませんでした。

- [GitHub Actions でプライベートリポジトリを checkout する](https://zenn.dev/kou_pg_0131/articles/gh-actions-checkout-private-repo)