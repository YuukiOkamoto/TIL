# CSS Modulesを使って、コンポーネントスコープのstyle
メリット：スコープが限定的だから、他のコンポーネントで使っているstyleと名前の衝突がおこらない！

## example
`src/components/container.module.css`
```css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```
`src/components/container.js`
```js
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <section className={containerStyles.container}>{children}</section>
)
```
こんな感じの、動的なcss名でhtmlにレンダーされる。  
`container-module--container--3MbgH`


