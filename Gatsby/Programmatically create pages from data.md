## 概要
Gatsbyは、他の静的サイトジェネレーターと違って、ファイルからページを作るだけじゃない。

ビルド時にGraphQLを使って取得したデータをページにマッピングできる！


筋肉 （マッピングって具体的に何ができるんや！？）
 
以下の2つのGatsby APIを使う
- `onCreateNode`
- `createPages`

ベストな使い方は、関数をexportsする。 

## ページにスラッグをつける

ルートディレクトリに以下ファイルを作る。  
`gatsby-node.js`
```js
exports.onCreateNode = ({ node }) => {
  console.log(node.internal.type);
};
```
`onCreateNode`は、nodeが作られるたびに呼ばれる。
例えば、development serverをrestartしてみると、、、
```shell
●yarn develop
yarn develop
yarn run v1.22.4
warning ../package.json: No license field
$ gatsby develop
success open and validate gatsby-configs - 0.023s
success load plugins - 0.348s
success onPreInit - 0.004s
info One or more of your plugins have changed since the last time you ran Gatsby. As
a precaution, we're deleting your site's cache to ensure there's no stale data.
success initialize cache - 0.022s
success copy gatsby files - 0.047s
success onPreBootstrap - 0.016s
success createSchemaCustomization - 0.005s
SitePage
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
SitePlugin
Site
SiteBuildMetadata
Directory
Directory
Directory
Directory
File
File
File
File
File
File
MarkdownRemark
File
MarkdownRemark
success source and transform nodes - 0.152s
success building schema - 0.177s
success createPages - 0.001s
SitePage
SitePage
SitePage
SitePage
success createPagesStatefully - 0.074s
success onPreExtractQueries - 0.002s
success update schema - 0.040s
success extract queries from components - 0.150s
success write out requires - 0.012s
success write out redirect data - 0.001s
success onPostBootstrap - 0.001s
⠀
info bootstrap finished - 4.123 s
⠀
success run queries - 0.069s - 5/5 72.19/s
⠀
You can now view gatsby-starter-hello-world in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
⠀
success Building development bundle - 2.548s
success Re-building development bundle - 0.048s


———————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————
4 pages                                                                                  Success                                                                                 gatsby-starter-hello-world
```
consoleにいっぱい出力されてる。
→ nodeが作られるたびに`onCreateNode`が呼ばれている。

また、こうすることで、  
`gatsby-node.js`
```js
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    const fileNode = getNode(node.parent);
    console.log(`\n`, fileNode.relativePath);
  }
};
```
markdownファイルのnodeを作るときだけ、パスを出力する。

こんなかんじ↓
```shell
yarn develop
yarn run v1.22.4
warning ../package.json: No license field
$ gatsby develop
success open and validate gatsby-configs - 0.017s
success load plugins - 0.179s
success onPreInit - 0.004s
info One or more of your plugins have changed since the last time you ran Gatsby. As
a precaution, we're deleting your site's cache to ensure there's no stale data.
success initialize cache - 0.018s
success copy gatsby files - 0.032s
success onPreBootstrap - 0.011s
success createSchemaCustomization - 0.004s

 pages/pandas-and-bananas.md

 pages/sweet-pandas-eating-sweets.md
success source and transform nodes - 0.062s
success building schema - 0.177s
success createPages - 0.002s
success createPagesStatefully - 0.046s
success onPreExtractQueries - 0.001s
success update schema - 0.022s
success extract queries from components - 0.153s
success write out requires - 0.025s
success write out redirect data - 0.003s
success onPostBootstrap - 0.001s
⠀
info bootstrap finished - 2.373 s
⠀
success run queries - 0.078s - 5/5 64.08/s
⠀
You can now view gatsby-starter-hello-world in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
⠀
success Building development bundle - 2.057s
success Re-building development bundle - 0.048s


———————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————
4 pages                                                                                  Success                                                                                 gatsby-starter-hello-world
```

これで、pathを含めたファイル名を取得できる🙌

けど、  
欲しいのはslugで、  
`pages/pandas-and-bananas.md`ではなく、  
`/pandas-and-bananas/`

パス付きファイル名からスラッグを生成したい。
ロジックが複雑になることもあるから、`gatsby-source-filesystem`プラグインが提供している関数の、`createFilePath`を使う！

`gatsby-node.js`
```js
const { createFilePath } = require(`gatsby-source-filesystem`)
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(createFilePath({ node, getNode, basePath: `pages` }))
  }
}
```

slugを出力できた！🎉
```shell
yarn develop
yarn run v1.22.4
warning ../package.json: No license field
$ gatsby develop
success open and validate gatsby-configs - 0.018s
success load plugins - 0.187s
success onPreInit - 0.003s
info One or more of your plugins have changed since the last time you ran Gatsby. As
a precaution, we're deleting your site's cache to ensure there's no stale data.
success initialize cache - 0.017s
success copy gatsby files - 0.033s
success onPreBootstrap - 0.011s
success createSchemaCustomization - 0.005s
/pandas-and-bananas/
/sweet-pandas-eating-sweets/
success source and transform nodes - 0.067s
success building schema - 0.184s
success createPages - 0.002s
success createPagesStatefully - 0.054s
success onPreExtractQueries - 0.002s
success update schema - 0.046s
success extract queries from components - 0.209s
success write out requires - 0.014s
success write out redirect data - 0.002s
success onPostBootstrap - 0.001s
⠀
info bootstrap finished - 2.453 s
⠀
success run queries - 0.081s - 5/5 61.83/s
⠀
You can now view gatsby-starter-hello-world in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
⠀
success Building development bundle - 2.135s
success Re-building development bundle - 0.046s


———————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————
4 pages                                                                                  Success                                                                                 gatsby-starter-hello-world
```

レディーパーフェクトリー！準備は完全に！

さっそく、`MarkdownRemark`ノードに、slugを追加する。

`createNodeField`を使う。
これは、他のプラグインで作ったnodeにfieldを追加できる！
追加したfieldはあとでGraphQLで取得できる！


`gatsby-node.js`
```js
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions;
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: 'pages' });
    createNodeField({
      node,
      name: 'slug',
      value: slug,
    });
  }
};
```

GraphQLで確認してみる！

[![Image from Gyazo](https://i.gyazo.com/08a7b5e8ad4646311cb7cd541b00bdb5.png)](https://gyazo.com/08a7b5e8ad4646311cb7cd541b00bdb5)

できた🎉

