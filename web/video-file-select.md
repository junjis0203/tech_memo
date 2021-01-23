# ローカルの動画ファイルを選択してページで再生する方法

[Media Source Extensions](https://developer.mozilla.org/ja/docs/Web/API/Media_Source_Extensions_API)というものがある。これが[URL.createObjectURLを拡張している](https://developer.mozilla.org/ja/docs/Web/API/Media_Source_Extensions_API#extensions_to_other_interfaces)ので普通にURLを作成して`video.src`に指定できる。

```html
<html>
  <body>
    <div>
      <input type="file" id="file" accept="video/*">
    </div>
    <div>
      <video controls id="video">
    </div>
    <script>
      const fileSelector = document.getElementById('file')
      fileSelector.addEventListener('change', () => {
        const file = fileSelector.files[0]
        const video = document.getElementById('video')
        video.src = URL.createObjectURL(file)
      })
    </script>
  </body>
</html>
```
