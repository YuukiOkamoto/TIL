gatsbyのプラグインには3種類ある。
- Functional Plugins
- Source Plugins
- Transformaer Plugins

## Functional Plugins
機能の追加だったり、TS, Sassなどのサポートを追加してWebpackを拡張する。

例えば、  
- [gatsby-plugin-catch-links](gatsbyjs.org/packages/gatsby-plugin-catch-links/?=link#gatsby-plugin-catch-links)  
[`gatsby-link`](https://www.gatsbyjs.org/docs/gatsby-link/)を使っていない遷移を、  
割り込んで`gatsby-link`の[navigate](https://www.gatsbyjs.org/docs/gatsby-link/#how-to-use-the-navigate-helper-function)の動作に乗せる。  
そうすることで、SPAの雰囲気を壊さない。
`gatsby-link`を使ってない遷移は例えばこんなもの↓  
mdファイル内でのリンクだったり、WYSIWYGエディターで書いて生成されてた`<a>` タグ。
- [gatsby-plugin-react-helmet](https://www.gatsbyjs.org/packages/gatsby-plugin-react-helmet/)  
`head`タグの変更を可能にする[react-helmet](https://github.com/nfl/react-helmet)を使って、  
静的なHTMLを生成できるようになる。

## Source Plugins
GraphQLで取得する`nodes`に追加する、データを取得する。  
データは例えばサイト内のファイルだったり、外部のAPIだったりDBだったり。

例えば、  
- [gatsby-source-filesystem](https://www.gatsbyjs.org/packages/gatsby-source-filesystem/)  
ファイルからデータを取得
- [gatsby-source-twitter](https://www.gatsbyjs.org/packages/gatsby-source-twitter/?=source%20twitter)  
Twitter APIを使用してデータを取得
- [gatsby-source-mongodb](https://www.gatsbyjs.org/packages/gatsby-source-mongodb/?=source%20mongo)  
MongoDBからデータを取得

## Transformer plugins
Source Pluginsで取得したデータで、Gatsbyがそのままでは扱えない形式のものを扱えるようにする。

例えば、
- [gatsby-transformer-remark
](https://www.gatsbyjs.org/packages/gatsby-transformer-remark/)  
Markdown → HTML
- [gatsby-transformer-json](https://www.gatsbyjs.org/packages/gatsby-transformer-json/?=transformer)  
JSON形式の文字列 → JavaScriptのobject
