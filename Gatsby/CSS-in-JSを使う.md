# CSS-in-JSを使う
jsにstyleを記述する。  
scopeも限定されわかりやすく、パフォーマンスの向上と動的なスタイルの設定が望める。

## 「CSS-in-JS」と「CSSとJavaScriptが別れているとき」の違い
- Reactの思想である、全てがコンポーネントであるというものに合う
- スコープがコンポーネント内にとどまる
- JSの変数を使って動的にstyleを定義できる
- ライブラリによっては、キャッシュ、自動ベンダープレフィックスなど多くの便利機能を提供してくれる

ただし、外部ライブラリを使う必要がある

## 外部ライブラリ1. Emotion
テンプレートリテラルを使って、オブジェクトの形でcssが書ける。

### 準備
```shell
yarn add gatsby-plugin-emotion @emotion/core @emotion/styled
```

`gatsby-config.js`
```js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

### 例
`src/pages/index.js`
```jsx
import React from "react"
import styled from "@emotion/styled"
import { css } from "@emotion/core"

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const UserWrapper = styled.div`
  display: flex;
  align-items: center;
  margin-top: 0;
  margin-right: auto;
  margin-bottom: 12px;
  margin-left: auto;
  &:last-child {
    margin-bottom: 0;
  }
`

const Avatar = styled.img`
  flex-grow: 0;
  flex-shrink: 0;
  flex-basis: 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Description = styled.div`
  flex: 1;
  margin-left: 18px;
  padding: 12px;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const Excerpt = styled.p`
  margin: 0;
`
// Using css prop provides a concise and flexible API to style the components. //
const underline = css`
  text-decoration: underline;
`

const User = props => (
  <UserWrapper>
    <Avatar src={props.avatar} alt="" />
    <Description>
      <Username>{props.username}</Username>
      <Excerpt>{props.excerpt}</Excerpt>
    </Description>
  </UserWrapper>
)

export default () => (
  <Container>
    <h1 css={underline}>About Emotion</h1>
    <p>Emotion is uber cool</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
  </Container>
)
```

### Emotionを使って、globalにstyleを適用する
`src/components/layout.js`
```js
import React from "react"
import { Global, css } from "@emotion/core"
import styled from "@emotion/styled"

const Wrapper = styled("div")`
  border: 2px solid green;
  padding: 10px;
`

export default ({ children }) => (
  <Wrapper>
    <Global
      styles={css`
        div {
          background: red;
          color: white;
        }
      `}
    />
    {children}
  </Wrapper>
)
```
`src/pages/index.js`
```js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

## 外部ライブラリ2. Styled Components
### 準備
```shell
yarn add gatsby-plugin-styled-components styled-components babel-plugin-styled-components
```

`gatsby-config.js`
```js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

### 例
`src/pages/index.js`
```jsx
import React from "react"
import styled from "styled-components"

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const UserWrapper = styled.div`
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
  &:last-child {
    margin-bottom: 0;
  }
`

const Avatar = styled.img`
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Description = styled.div`
  flex: 1;
  margin-left: 18px;
  padding: 12px;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const Excerpt = styled.p`
  margin: 0;
`

const User = props => (
  <UserWrapper>
    <Avatar src={props.avatar} alt="" />
    <Description>
      <Username>{props.username}</Username>
      <Excerpt>{props.excerpt}</Excerpt>
    </Description>
  </UserWrapper>
)

export default () => (
  <Container>
    <h1>About Styled Components</h1>
    <p>Styled Components is cool</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
  </Container>
)
```
