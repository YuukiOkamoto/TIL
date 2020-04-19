`gatsby-source-filesystem`で内部ファイルのデータを取得し、  
`gatsby-transformer-remark`でmarkdown形式の文字列をHTML形式にパースし、  
`gatsby-node.js`で`createPages`を実装して、build時の処理に割り込みページの追加を伝え、  
`createPages`のactionの`createPage`でどんなページを追加するか実装する。  
すると、[node](https://www.gatsbyjs.org/docs/node-interface/)に追加される。  
追加されたnodeを必要な場所でGraphQLを使って取得する。  
