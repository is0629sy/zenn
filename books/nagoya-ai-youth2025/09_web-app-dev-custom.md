---
title: "カスタマイズ"
---

ここまでで、シンプルな三目並べができましたね。

もしうまく動作していない人がいたら、以下のコードをコピーして貼り付けましょう！

:::details index.html
```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>三目並べ</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>三目並べ</h1>
  <div id="game">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>
  <div id="message"></div>
  <button id="restart">リスタート</button>

  <script src="script.js"></script>
</body>
</html>
```
:::

:::details style.css
```css
body {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f0f0f0;
  margin: 0;
  padding: 40px;
}

h1 {
  margin-bottom: 20px;
}

#game {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 5px;
  justify-content: center;
  margin: 0 auto 20px;
}

.cell {
  width: 100px;
  height: 100px;
  background-color: white;
  border: 2px solid #333;
  font-size: 2.5em;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background-color 0.2s;
}

.cell:hover {
  background-color: #e0e0e0;
}

#message {
  font-size: 1.2em;
  margin-bottom: 20px;
  min-height: 1.5em;
}

#restart {
  padding: 10px 20px;
  font-size: 1em;
  cursor: pointer;
}
```
:::

:::details script.js
```js
const cells = document.querySelectorAll('.cell');
const message = document.getElementById('message');
const restartButton = document.getElementById('restart');

let board = ['', '', '', '', '', '', '', '', ''];
let currentPlayer = '○';
let isGameOver = false;

function handleClick(e) {
  const index = e.target.dataset.index;

  if (board[index] !== '' || isGameOver) return;

  board[index] = currentPlayer;
  e.target.textContent = currentPlayer;

  if (checkWinner()) {
    message.textContent = `${currentPlayer} の勝ち！`;
    isGameOver = true;
    return;
  }

  if (board.every(cell => cell !== '')) {
    message.textContent = '引き分け！';
    isGameOver = true;
    return;
  }

  currentPlayer = currentPlayer === '○' ? '×' : '○';
  message.textContent = `${currentPlayer} の番`;
}

function checkWinner() {
  const winPatterns = [
    [0,1,2], [3,4,5], [6,7,8], // 横
    [0,3,6], [1,4,7], [2,5,8], // 縦
    [0,4,8], [2,4,6]           // 斜め
  ];

  return winPatterns.some(pattern => {
    const [a, b, c] = pattern;
    return board[a] && board[a] === board[b] && board[a] === board[c];
  });
}

function restartGame() {
  board = ['', '', '', '', '', '', '', '', ''];
  isGameOver = false;
  currentPlayer = '○';
  message.textContent = `${currentPlayer} の番`;
  cells.forEach(cell => cell.textContent = '');
}

cells.forEach(cell => cell.addEventListener('click', handleClick));
restartButton.addEventListener('click', restartGame);

// 初期メッセージ
message.textContent = `${currentPlayer} の番`;
```
:::

<br />
では次に、今まで内容をもとに三目並べをカスタマイズしていきましょう！

ChatGPTの使い方を理解し、自分でカスタマイズを進められそうな人はそのまま作業に移っていただいて構いません。

この先は自由にカスタマイズしてもらいますが、例としては以下のようなものがあります。

- 初級編
  1. 勝利した列をハイライト表示する
  2. 先攻後攻の選択
  3. 盤面の色やフォントなどのデザイン変更
- 中級編
  1. ⚪︎と×それぞれの勝利数をカウントするスコアボード
  2. 対戦履歴の表示
- 上級編
  1. コンピュータ対戦機能

今回はこれらの中でも例として勝利した列をハイライト表示する機能を追加してみましょう。  
もちろん、この他に追加したい機能がある方は、そちらに取り組んでいただいて大丈夫です。

今までと同じチャットで、以下のプロンプトを入力します。

>勝利した列をハイライト表示するようにしてください
今まで出力したコードも含めて全て出力してください

![](/images/nagoya2025/chatgpt-arrange-sanmoku.png)

場合によってChatGPTは変更部分だけのコードを出力してくれることがあります。  
現段階では変更部分だけを出してもらってもわからない！ということになると思うので、「今まで出力したコードも含めて全て出力してください」と入力しておきましょう。

コードの出力が完了したら、これまでと同じようにコピーしてそれぞれのファイルに貼り付け、保存します。

保存が完了したら、ブラウザで見てみましょう！

![](/images/nagoya2025/vscode-golive-test-sanmoku-4.png)

どちらかが勝利すると、その列がハイライト表示されるようになりました！

実際に確認してみて、

- ⚪︎や×が小さくて見づらい
- もっと他の機能がほしい
- 盤面をもっと広げたい

など気づいた点ややってみたいことをリストアップしてみてChatGPTに改善依頼をすることも面白いかもしれませんね！