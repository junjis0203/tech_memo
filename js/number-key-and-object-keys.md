# 数値キーとObject.keys

オブジェクトのプロパティ名（キー）一覧を取得したい場合、[Object.keys](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)が使えるが**数値で設定したキーも文字列で返される**点に注意。

```js
> o = {}; o[1] = 2; o[2] = 3
> Object.keys(o)
[ '1', '2' ]
```

そもそも`o[1]`と書いた場合でもプロパティは**文字列に変換されて**処理される。

```js
> o[1]
2
> o['1']
2
```

該当する仕様は以下のあたり。

https://262.ecma-international.org/6.0/#sec-property-accessors-runtime-semantics-evaluation  
https://262.ecma-international.org/6.0/#sec-topropertykey
