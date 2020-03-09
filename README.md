# Next.js + microCMS

Next.js の getStaticProps と getStaticPaths を使って microCMS のデータを取得して、静的にビルドするサンプル。

# バージョン

- Next.js 9.2.3-canary.16
- React 16.13.0
- ReactDOM 16.13.0

# 始め方

```
$ yarn install
```

.env.sample をコピー

```
$ cp .env.sample .env
```

## 開発サーバーの立ち上げ

microCMS で取得し API キーとエンドポイントを env ファイルに記述。

```
API_KEY=xxxxx
ENDPOINT=https://your.microcms.io/api/v1/

```

アプリケーションの立ち上げ

```
$ yarn dev
```

## SSG

```
$ yarn export
```

# ポイント

## getStaticProps

静的なファイルを事前に生成する API。

ビルド時に実行させる。クライアントサイドでは実行されず、必ずサーバーサイドで実行される。

```
export async function getStaticProps() {
  const key = {
    headers: {'X-API-KEY': process.env.api_key},
  };

  const res = await axios.get(process.env.endpoint, key);

  const data = await res.data.contents;

  return {
    props: {
      blogs: data,
    },
  };
}
```

## getStaticPaths

Dynamic Routes 利用時にも静的なファイルを生成する API。

ファイルに[]をつけるとダイナミックルーティングになる。そのファイル内で getStaticPaths を使うことで、ダイナミックルーティングを活用して、静的なファイルを生成できる。

```
export async function getStaticPaths() {
  const key = {
    headers: {'X-API-KEY': process.env.API_KEY},
  };

  const res = await axios.get(process.env.endpoint, key);
  const repos = await res.data.contents;
  const paths = repos.map(repo => `/blogs/${repo.id}`);
  return {paths, fallback: false};
}
```

# 参考

https://qiita.com/matamatanot/items/1735984f40540b8bdf91