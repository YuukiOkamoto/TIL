Typography.jsとは、

## 準備
```shell
yarn add gatsby-plugin-typography react-typography typography
```

`gatsby-config.js`
```js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

## 例
pathToConfigModuleに指定したpathのファイル（`src/utils/typography.js`）
```js
import Typography from 'typography';

const typography = new Typography({
  baseFontSize: '18px',
  baseLineHeight: 1.666,
  headerFontFamily: [
    'Avenir Next',
    'Helvetica Neue',
    'Segoe UI',
    'Helvetica',
    'Arial',
    'sans-serif',
  ],
  bodyFontFamily: ['Georgia', 'serif'],
});

export default typography;
```

## テーマを使ってみる
```shell
yarn add typography-theme-funston
```

`src/utils/typography.js`
```diff
import Typography from "typography";
+ import funstonTheme from 'typography-theme-funston'
const typography = new Typography(
- {
-     baseFontSize: '18px',
-     baseLineHeight: 1.666,
-     headerFontFamily: ['Avenir Next', 'Helvetica Neue', 'Segoe UI', 'Helvetica', 'Arial', 'sans-serif'],
-     bodyFontFamily: ['Georgia', 'serif'],
- },
+ funstonTheme
);

export default typography;
```
