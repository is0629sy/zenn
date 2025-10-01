---
title: "5-1. HTMLの基礎"
---

HTML（HyperText Markup Language）は、Web ページの構造を定義するために使用されるマークアップ言語です。
HTML を使用して、見出し、段落、リンク、画像などの要素をページに追加します。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="./style.css" />
    <script type="module" src="./script.js"></script>
  </head>

  <body>
    <div>
      <h1 id="hello">はじめまして！</h1>
      <p>僕の趣味はギターを弾くことです。</p>
      <span>ダーツも好きです。</span>
    </div>
  </body>
</html>
```
上記のコードをコピーし、`index.html`へ張り付け、どのような画面が表示されるか確認してみましょう！
教材のコードの右上にある「コピーする」を押してコピーします。

コピーができたらVSCodeに移り、 `index.html` に貼り付けます。  
Windowsでは `Ctrl+V` 、Macでは `⌘+V` で貼り付けることができます。

出力されたコードが全て貼り付けられていればOK！
コードの追加、削除、書き換えがあると、画面上部のファイル名の横に白丸が付きます。  

![](/images/itboot2025/vscode-save-html.png)



変更があったら、Windowsでは `Ctrl+S` 、Macでは `⌘+S` で**必ず保存**しておきましょう。

保存が完了したら、画面右下に小さく出ている `Go Live` をクリックしてブラウザで開いてみましょう。

![](/images/itboot2025/vscode-golive.png)