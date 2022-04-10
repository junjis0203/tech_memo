# insertAdjacentHTMLで追加してquerySelectorで取得する

Reactのビルド環境を用意するのが面倒な場合に「素のDOM」でページを構築することがあるのだが、イベントハンドラを設定したい場合は`createElement`で要素を作って`addEventListener`でイベントハンドラを設定したうえで`appendChild`しないといけないと思っていた。適当HTMLの場合はこれでもいいのだが、ちょっとレイアウトもまともにしようとBootstrapとか使いだすと個別に`createElement`するなんてやってられない。

`innerHTML`に代入したものを即取れないかなと試してみたらいけた。Cardのように一番外側の要素にも`class`を設定する場合は[insertAdjacentHTML](https://developer.mozilla.org/ja/docs/Web/API/Element/insertAdjacentHTML)で追加して（この瞬間に「画面に反映」されてしまうが）、`lastElementChild`使うのがより手間がない。この要素に対する[querySelector](https://developer.mozilla.org/ja/docs/Web/API/Element/querySelector)は今追加した要素（の階層）のみが検索範囲となる。

```html
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
  </head>
  <body>
    <div class="container">
      <div id="app"></div>
    </div>
    <script>
      const $app = document.getElementById("app")
      // サーバからデータを受け取ったとする
      const items = [
        {title: 'foo', contents: 'FOOFOOFOO!'},
        {title: 'bar', contents: 'BARBARBAR!'},
        {title: 'baz', contents: 'BAZBAZBAZ!'},
      ]
      for (const item of items) {
        // 複雑な構造も一度に設定可能
        $app.insertAdjacentHTML('beforeend', `
          <div class="card mb-3">
            <div class="card-header">
              ${item.title}
            </div>
            <div class="card-body">
              <p class="card-text">
                ${item.contents}
              </p>
              <button class="btn btn-primary">Click!</button>
            </div>
          </div>
        `)
        // 最後に追加した（上でinsertしている）子要素を取得
        const $div = $app.lastElementChild
        console.log($div)
        // 追加した要素の範囲で子要素を取得し、ハンドラを設定できる
        const button = $div.querySelector("button")
        button.addEventListener("click", function() {
          alert(item.contents)
        })
      }
    </script>
  </body>
</html>
```

まあ、めんどくさがらずに初めからReact環境作れというところではあるが。
