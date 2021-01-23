# canvasの内容をファイル化する方法

`toDataURL`もあるがサーバに送るような場合は[toBlob](https://developer.mozilla.org/ja/docs/Web/API/HTMLCanvasElement/toBlob)を使う方が手っ取り早い。第1引数がコールバックで第2引数がファイル形式なのがちょっとわかりにくい。

```html
<html>
  <body>
    <canvas id="canvas"></canvas>
    <script>
      const canvas = document.getElementById('canvas')
      canvas.toBlob(blob => {
        // サーバに送る
      }, 'image/jpeg')
    </script>
  </body>
</html>
```

Promise使いたい人は以下のように関数を定義すればよい。

```js
function canvasToBlob(canvas, type, quality) {
  return new Promise((resolve, reject) => 
    // callbackとして直接resolveを渡してしまえばよい
    canvas.toBlob(resolve, type, quality)
  )
}

canvasToBlob(canvas, 'image/jpeg')
  .then(blob => {
    // サーバに送る
  })
```
