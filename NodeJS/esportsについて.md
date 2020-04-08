書き方はいろいろある？

```js
// my-module.js
module.exports.hoge = 'hoge';
exports.fuga = 'fuga';
```
```js
//main.js
const myModule = require('./my-module');

console.log(myModule.hoge);
console.log(myModule.fuga);
console.log(myModule.macho);
```
```shell
// shell
$ node main.js
hoge
fuga
undefined
```

ほかにも、まとめて指定できたりもする。
```js
// my-module.js
module.exports = {
  hoge: 'hoge',
  fuga: 'fuga',
};
```
```js
//main.js
const myModule = require('./my-module');

console.log(myModule.hoge);
console.log(myModule.fuga);
console.log(myModule.macho);
```
```shell
// shell
$ node main.js
hoge
fuga
undefined
```

また、オブジェクトの代入時点で値が変わるので、代入以前にexportsした情報は失われる。
```js
// my-module.js
module.exports.hoge = 'hoge';
module.exports = {
  fuga: 'fuga',
};
```
```js
//main.js
const myModule = require('./my-module');

console.log(myModule.hoge);
console.log(myModule.fuga);
console.log(myModule.macho);
```
```shell
// shell
$ node main.js
undefined
fuga
undefined
```

まあそのへんの挙動は、`require`したオブジェクトの型が`object`だってのを見れば見当がつく。
```js
// my-module.js
module.exports.hoge = 'hoge';
module.exports = {
  fuga: 'fuga',
};
```
```js
//main.js
const myModule = require('./my-module');

console.log(typeof myModule);
```
```shell
// shell
$ node main.js
ogject
```

問題はこれ。  
exportsで代入ができない。
```js
// my-module.js
exports = {
  hoge: 'hoge',
  fuga: 'fuga',
};
```
```js
//main.js
const myModule = require('./my-module');

console.log(myModule.hoge);
console.log(myModule.fuga);
console.log(myModule.macho);
```
```shell
// shell
$ node main.js
undefined
undefined
undefined
```

「`exports`」 と 「`module.exports`」 の違いがよくわからない:sweat:  
いまのとこの挙動を見る限り、  
`exports`は、  
`exports.hoge = 'hoge'`はできるけど、  
`exports = { hoge: 'hoge' }`はできない。代入はできない。

ひとまず公式を見る :eyes:
https://nodejs.org/api/modules.html#modules_exports_shortcut

つまり、
`exports.f = ...`ってのは、  
`module.exports.f = ...`のショートカットであり、同じ処理が行われる。

`exports = { hoge: 'hoge' }`は、  
`exports`というローカル変数にオブジェクトリテラルを代入している。もちろんモジュール内の変数としては使えるけど、requireはできない。

納得！！:tada:
