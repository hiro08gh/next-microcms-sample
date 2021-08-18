# Next.js + microCMS

Next.jsのgetStaticPropsとgetStaticPaths を使ってmicroCMSのデータを取得して、静的にビルドするサンプル。

## バージョン

- Next.js 11.1.0
- React 17.0.1
- ReactDOM 17.0.1

## コンテンツモデル
まず最初にmicroCMS側でコンテンツモデルを作成する必要があります。

API名 - ブログ

エンドポイント - blogs

### APIスキーマ
- title -> テキストフィールド

# 始め方

```
$ yarn install
```

.env.development.localを作成。

```
$ touch .env.development.local
```

## 開発サーバーの立ち上げ

microCMSで取得しAPIキーとエンドポイントをenvファイルに記述。

```
API_KEY=xxxxx
ENDPOINT=https://your.microcms.io/api/v1
```

アプリケーションの立ち上げ

```
$ yarn dev
```

## SSG

```
$ yarn export
```
