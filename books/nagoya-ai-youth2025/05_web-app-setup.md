---
title: "5-1. 事前準備"
---

## ChatGPTに三目並べを作ってもらおう！ -事前準備-

ChatGPTにコードを出力してもらう前に、必要なファイルを準備しておきましょう。  

必要なファイルは

- index.html
- style.css
- script.js

の三つです。

今回はこの三つのファイルを使って、三目並べを作っていきましょう！

### 1. 新しいフォルダの作成

HTML,CSS,JSをまとめておくフォルダを作成します。  
今回はわかりやすいようにデスクトップに作成しておきましょう。

1. デスクトップ上で右クリックをし、Windowsでは `新規作成` > `フォルダー` 、Macでは `新規フォルダ` をクリック
![](/images/nagoya2025/desktop-newfolder.png)
2. 名前は `三目並べ` とします
![](/images/nagoya2025/desktop-newfolder-2.png)

### 2. HTML,CSS,JSファイルの作成

`三目並べ` フォルダが完成したら、そのフォルダをVSCodeで開きます
1. VSCodeを開き、左上の「ファイル」をクリックし、「フォルダーを開く…」をクリック
![](/images/nagoya2025/vscode-openfolder.png)
2. エクスプローラーやFinderが開いたら、その中から先ほど作成した `三目並べ` を選択し、「開く」をクリックするとVSCodeでフォルダの中身を見ることができます
![](/images/nagoya2025/vscode-openfolder-2.png)
3. 次に、左側に出ている `三目並べ` のファイル名の横にある `新しいファイル` をクリックし、 `index.html` と入力します
![](/images/nagoya2025/vscode-newfile.png)
![](/images/nagoya2025/vscode-setting-filename.png)
4. 同じ方法で `style.css` と `script.js` も作成します
![](/images/nagoya2025/vscode-setting-filename-2.png)


### 3.HTML,CSS,Javascriptを動かしてみよう！

#### 実際に書いてみる！

後述するコードを`index.html`, `style.css`,`script.js` に記載してそれぞれ動きを確認してみましょう！

##### HTML

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
    <div class="container">
      <h1 id="hello">はじめまして！</h1>
      <p>僕が好きなのはオールマイトです。</p>
      <span>デクも好きです。</span>
    </div>
  </body>
</html>
```

##### CSS

Cascading Style Sheets の略で、Web ページのスタイルを定義するために使用されます。
CSS を使用して、レイアウト、色、フォント、間隔などの視覚的なスタイルを指定します。

```css
.container {
  width: 100%;
}

h1 {
  color: red;
}
h1.active {
  color: blue;
}
```

##### JavaScript

JavaScript は、Web ページの動的な振る舞いを定義するために使用されるプログラミング言語です。
JavaScript を使用して、ユーザーとのインタラクション、アニメーション、データの操作などを行います。

```javascript
const hello = document.getElementById('hello');

hello.addEventListener('click', () => {
  hello.classList.toggle('active');
});
```

どうでしょうか？プログラムの役割のイメージは沸きましたか？

動きが確認出来たら上で書いたコードはこれから使わないので、各ファイルの中身は一旦消して、中身を空にしてください！

次の章でHTML、CSS、Javascriptを使用していよいよ「三目並べ」を作っていきます！