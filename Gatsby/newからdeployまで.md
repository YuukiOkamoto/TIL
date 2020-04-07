## starterを使って始める
```shell
gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]
```
[starter ドキュメント](https://www.gatsbyjs.org/docs/starters/)  
[sterter library](https://www.gatsbyjs.org/starters/?v=2)  
[starterのカスタマイズ](https://www.gatsbyjs.org/docs/modifying-a-starter)  
[starter? or plugin? or theme? どれを使う？](https://www.gatsbyjs.org/static/a39b81ed6da34191bcae5ae27b987fcf/17602/plugin-starter-theme-flowchart.png)  

## localhostで立ち上げる
```shell
gatsby develop
```
または、`package.json`に、以下の記載があるので、
```package.json
{
  "scripts": {
    "develop": "gatsby develop",
  }
}
```
これでもいける
```shell
yarn run develop
```

## deployする
[Surge](http://surge.sh/)が推奨されるので使ってみる。

### インストール
```shell
yarn global surge
```
（公式ではnpmで書かれていたが、[yarn公式サイトのnpmからの移行](https://classic.yarnpkg.com/ja/docs/migrating-from-npm/)を参考に、yarnでインストールした。

### buildする
```shell
gatsby build
```
または、`package.json`に、以下の記載があるので、
```package.json
{
  "scripts": {
    "build": "gatsby build",
  }
}
```
これでもいける
```shell
yarn run build
```

すると、  
`/public/`以下に静的はhtml, css, jsファイルが生成されるので、これをデプロイしていく

## deployする
```shell
surge public/
```
または、`package.json`に、以下の記載を**追加すると**、
```package.json
{
  "scripts": {
    "deploy": "surge public/",
  }
}
```
これでもいける
```shell
yarn run deploy
```

結果は、
```shell
●yarn run deploy                                                                                                                                                                                      【 master 】
yarn run v1.22.4
$ surge public/

   Running as yuuki.okamoto.it.fitness@gmail.com (Student)

        project: public/
         domain: hellish-sense.surge.sh
         upload: [====================] 100% eta: 0.0s (15 files, 932680 bytes)
            CDN: [====================] 100%

             IP: 45.55.110.124

   Success! - Published to hellish-sense.surge.sh

✨  Done in 7.50s.
```
hellish-sense.surge.sh を開いてみると？  
🎉  
[![Image from Gyazo](https://i.gyazo.com/b532819561b4797ce5608a12f45a642e.png)](https://gyazo.com/b532819561b4797ce5608a12f45a642e)
