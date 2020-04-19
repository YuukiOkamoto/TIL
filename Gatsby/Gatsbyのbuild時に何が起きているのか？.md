こちらのサイトが大変参考になりました！  
https://medium.com/eureka-engineering/how-gatsby-works-bec4349caa12

Gatsbyのbuild関数（packages/gatsby/src/commands/build.js）では大きく下記が順次実行されます。
1. bootstrap
2. onPreBuild
3. copyStaticDirectory
4. buildCSS
5. buildProductionBundle
6. buildHTML
7. onPostBuild


ビルド時にプラグインがデータ取得やスキーマ生成の処理を差し込めるフックポイントとしてGatsby Node APIというのがある。  
ほとんどは、bootstrapの中で実行される。

`gatsby-node.js`にフックさせたいAPIの名前で関数を書けば、ビルド時に実行してくれる。

