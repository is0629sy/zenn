---
title: "【Tips集】自由制作の参考に！"
---

ここでは、自由制作の時間に役立つ「Webサイトに機能を追加するためのヒント」を紹介します。
少しの工夫で、見た目も使い勝手もぐっと良くなります！

---

## 画像を挿入しよう

### 画像の準備と保存場所

画像ファイルは、HTMLファイルと同じフォルダ内に **「images」フォルダ** を作り、その中に入れておくのがおすすめです。

```
project-folder/
├── index.html
└── images/
    └── sample.jpg
```

### HTMLで画像を表示する

画像を表示するには、`<img>`タグを使います。

```html
<img src="images/sample.jpg" alt="サンプル画像" width="300">
```

* **src**：画像ファイルのパス
* **alt**：画像が表示されない場合の代替テキスト
* **width / height**：画像のサイズ（px単位）

---

## Google Fontsを使って文字をおしゃれにしよう

### Google Fontsとは？

[Google Fonts](https://fonts.google.com/) は、無料で使えるおしゃれなフォントを提供しているサービスです。
日本語や英語のフォントがたくさんあり、サイトの雰囲気を変えることができます。

### フォントの導入手順

1. [Google Fonts](https://fonts.google.com/) にアクセス
2. 好きなフォントを選ぶ（例：「Roboto」）
3. 「Get font」→「@import」タブをクリック
4. 指示通りにコードをコピーし、HTMLの`<head>`内に貼り付けます。

```html
<head>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Roboto', sans-serif;
    }
  </style>
</head>
```

これでページ全体の文字が指定したフォントになります！

![](/images/itboot2025/tips-google-fonts.png)

---

## Google Mapsを埋め込もう

### Google Mapの表示方法

自分の好きな場所の地図をページに埋め込むことができます。

1. [Googleマップ](https://www.google.com/maps) を開く
2. 表示したい場所を検索
3. 「共有」→「地図を埋め込む」をクリック
4. 表示されたHTMLコードをコピーして、貼り付けます。

```html
<h2>美唄駅の地図</h2>
<iframe 
  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2913.747...（省略）"
  width="400"
  height="300"
  style="border:0;"
  allowfullscreen=""
  loading="lazy">
</iframe>
```

地図の大きさを変えたいときは、`width`や`height`を調整しましょう。

![](/images/itboot2025/tips-googlemap.png)

---

## 簡単なAPIを使ってみよう（名言API）

### APIとは？

**API**とは、「他のサービスの情報を呼び出す仕組み」です。
たとえば、名言をランダムで取得して表示することもできます。

### コード例（名言API）

```html
<h2>名言を表示するアプリ</h2>
<button onclick="getQuote()">名言を表示</button>
<p id="quote"></p>

<script>
  async function getQuote() {
    const res = await fetch("https://api.quotable.io/random");
    const data = await res.json();
    document.getElementById("quote").innerText = data.content;
  }
</script>
```

ボタンを押すたびに、世界中の名言がランダムで表示されます。
ChatGPTに「このAPIを使って背景も変えるようにしたい」などと相談すると、さらに発展できます！

![](/images/itboot2025/tips-api.png)

---

## 💡 まとめ

| 項目           | できること      | 難易度 |
| ------------ | ---------- | --- |
| 画像の挿入        | ページに写真を追加  | ★☆☆ |
| Google Fonts | 文字をおしゃれにする | ★☆☆ |
| Google Maps  | 地図を埋め込む    | ★★☆ |
| API          | データを外部から取得 | ★★★ |

どれも少しのコードで大きく変化が出るテクニックです。
「これを応用したい！」と思ったら、ChatGPTに相談してみましょう！