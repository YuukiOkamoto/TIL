`blog-post.js`
```js
import React from 'react';
import { graphql } from 'gatsby';

export default ({ data }) => {
  const post = data.markdownRemark;
  return (
    <div>
      <h1>{post.frontmatter.title}</h1>
      <section dangerouslySetInnerHTML={{ __html: post.html }} />
    </div>
  );
};
export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`;
```

この中の、graphqlの、`$slug`ってなに？  
変数？  
いつ代入されてる？
どんな値が代入されてる？

## GraphQLの変数について理解する。
まずこれ → `$slug`は変数  
https://graphql.org/learn/queries/#variables

queryとは別にJSONで定義する。  
例えばこんな感じ。
```json
{
  "slug": "/blog/muscle/"
}
```
このJSONデータをqueryでは変数に適用している。

## Gatsbyではいつ変数の値を定義していた？
上の例だと、  
`gatsby-node.js`ファイルの`creatPages`の中の処理の`createPage`に渡すオブジェクトの、  
`content`で指定する。
```js
createPage({
  path: node.frontmatter.slug || node.fields.slug,
  component: path.resolve(`./src/templates/blog-post.js`),
  context: {
    slug: node.fields.slug,
  },
});
```
https://www.gatsbyjs.org/docs/page-query/#how-to-add-query-variables-to-a-page-query
