---
title: "5-3. JavaScriptの基礎"
---

## JavaScriptとは？

JavaScript は、Web ページの動的な振る舞いを定義するために使用されるプログラミング言語です。
JavaScript を使用して、ユーザーとのインタラクション、アニメーション、データの操作などを行います。

```javascript
const hello = document.getElementById('hello');

hello.addEventListener('click', () => {
  hello.classList.toggle('active');
});
```
上記のコードをコピーし、`script.js`へ張り付けましょう。

貼り付けが完了したら、おなじみになりつつある**保存**をしておきましょう！

そして、表示されるページにどのような動きが加わるか確認してみましょう！

![](/images/itboot2025/golive-js.png)

どうでしょうか？プログラムの役割のイメージは沸きましたか？

いよいよ次の章から、HTML、CSS、Javascriptを使用していよいよ「三目並べ」を作っていきます！