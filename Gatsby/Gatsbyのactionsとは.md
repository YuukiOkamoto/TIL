例えば、  
Gatsby Node APIsの、 [`onCreateNode`](https://www.gatsbyjs.org/docs/node-apis/#onCreateNode)では、引数のオブジェクトは`actions`をもつ。
```js
exports.onCreateNode = ({ node, actions }) => {
  const { createNode, createNodeField } = actions
  // Transform the new node here and create a new node or
  // create a new node field.
}
```
この`actions`ってなに？？

まずはじめに公式ドキュメントはこちら。  
https://www.gatsbyjs.org/docs/actions/

冒頭の説明によると、  
Gatsbyでは内部でReduxが使われていて、  
Reduxの[`bindActionCreators`](https://redux.js.org/api/bindactioncreators/)でバインドされたアクションと同じようなものが渡されるみたい。

Reduxわからんから辛い。。

Reduxのドキュメント見てみる。
