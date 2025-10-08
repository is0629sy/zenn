---
title: "7-3. Webアプリ制作【JavaScript】"
---

## JavaScriptで動きをつけよう！

次は「動き（javascript）」をつけていきます！
以下のプロンプトをChatGPTに入力し、JavaScriptのコードを出力してもらいましょう。

>script.jsを出力してください。

![](/images/itboot2025/chatgpt-js-sanmoku.png)

送信すると、またまたコードの出力が始まります。

コードの出力が終了したら、お馴染みの「コピーする」を押してコピーします。

VSCodeに移り、最後は `script.js` に貼り付けます。

![](/images/itboot2025/vscode-js-sanmoku-1.png)

コードが貼り付けられていることを確認したら、**保存**しましょう。

「Go Live」で開いたWebページ再び戻ってみます。

![](/images/itboot2025/vscode-golive-test-sanmoku-3.png)

マス目をクリックすると⚪︎と×が交互に入力されることが確認できると思います。

最終的には勝敗や引き分けも判定してくれるはずです。

たった(?)これだけの入力で三目並べが完成します！

もしうまく動作しない場合は、以下のコードをコピーして貼り付けてみましょう！

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