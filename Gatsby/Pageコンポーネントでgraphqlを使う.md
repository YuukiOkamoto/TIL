## Prerequisites
- Gatsbyではbuild時にページを生成する際GraphQLを使ってデータを取得する。
- `src/pages/xxx.js`というファイルが有れば、 このファイルが`default`でexportするJSXでページを作り、`/xxx/`というpathのurlでアクセスできるようになる

## データを準備する
今回は手っ取り早く、  
最も簡単でポピュラーな、`siteMetadata`を設定する。
`gatsby-config.js`
```js
module.exports = {
  siteMetadata: {
    title: '筋トレたのしいいいいいいいいいいいいいい',
    description: `今日も筋トレ明日も筋トレ明後日も筋トレいつでも筋トレ…`,
    author: `macho`,
  },
}
```

## Pageコンポーネントで呼び出してみる
`src/pages/macho.js`
```js
import React from 'react';
import { graphql } from 'gatsby';

export default ({ data }) => {
  <h1>{data.site.siteMetadata.title}</h1>;
  <p>{data.site.siteMetadata.description}</p>;
};

export const query = graphql`
  query {
    site {
      siteMetadata {
        title
        description
      }
    }
  }
`;
```
Point、決まりごととして覚えておくべきは、
- Pageコンポーネントで`query`という変数をexportすると、graphqlが実行される
- それによって得られたデータは、`data`という名前でpropsに付与される
