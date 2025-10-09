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
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>シンプル三目並べ</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <main class="app">
    <header class="app-header">
      <h1>三目並べ (Tic-Tac-Toe)</h1>
      <p class="lead">プレイヤーは交互にマスをクリックして○と×を置き、縦・横・斜めに3つ並べた方が勝ちです。</p>
    </header>

    <!-- ステータス表示 -->
    <section class="status">
      <div id="turn">次の手: <strong id="current-player">◯</strong></div>
      <div id="message" aria-live="polite"></div>
    </section>

    <!-- 盤面 -->
    <section class="board-wrap" aria-label="三目並べの盤面">
      <div id="board" class="board" role="grid" aria-label="3x3 ボード">
        <!-- 9つのセルを button で作る（キーボード操作・アクセシビリティ対応） -->
        <button class="cell" data-index="0" role="gridcell" aria-label="セル 1"></button>
        <button class="cell" data-index="1" role="gridcell" aria-label="セル 2"></button>
        <button class="cell" data-index="2" role="gridcell" aria-label="セル 3"></button>

        <button class="cell" data-index="3" role="gridcell" aria-label="セル 4"></button>
        <button class="cell" data-index="4" role="gridcell" aria-label="セル 5"></button>
        <button class="cell" data-index="5" role="gridcell" aria-label="セル 6"></button>

        <button class="cell" data-index="6" role="gridcell" aria-label="セル 7"></button>
        <button class="cell" data-index="7" role="gridcell" aria-label="セル 8"></button>
        <button class="cell" data-index="8" role="gridcell" aria-label="セル 9"></button>
      </div>
    </section>

    <!-- コントロール -->
    <section class="controls">
      <button id="restart" class="btn">リセット</button>
      <button id="change-first" class="btn">先手を変更</button>
      <div class="note">先手は ◯ / × を交互に切り替えられます。</div>
    </section>

    <footer class="footer">
      <small>簡易版 — index.html / style.css / script.js で動作します。</small>
    </footer>
  </main>

  <script src="script.js" defer></script>
</body>
</html>
```
:::

:::details style.css
```css
/* -----------------------------
   シンプル三目並べ style.css
----------------------------- */

body {
  font-family: "Segoe UI", "Hiragino Kaku Gothic ProN", "Meiryo", sans-serif;
  background: #f4f6f8;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.app {
  text-align: center;
  background: #fff;
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  width: 320px;
  max-width: 90vw;
}

.app-header h1 {
  margin: 0 0 0.5rem;
  font-size: 1.6rem;
  color: #333;
}

.lead {
  font-size: 0.9rem;
  color: #555;
  margin-bottom: 1.5rem;
}

.status {
  margin-bottom: 1rem;
  font-size: 1.1rem;
  color: #222;
}

#message {
  margin-top: 0.5rem;
  color: #0077cc;
  font-weight: bold;
}

.board-wrap {
  display: flex;
  justify-content: center;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 90px);
  grid-template-rows: repeat(3, 90px);
  gap: 6px;
}

.cell {
  width: 90px;
  height: 90px;
  background: #f9f9f9;
  border: 2px solid #ccc;
  font-size: 2.5rem;
  font-weight: bold;
  color: #333;
  cursor: pointer;
  transition: background 0.2s, transform 0.1s;
  border-radius: 8px;
}

.cell:hover {
  background: #e8f0ff;
  transform: scale(1.03);
}

.cell:disabled {
  cursor: default;
  background: #eee;
  color: #888;
}

.controls {
  margin-top: 1.5rem;
}

.btn {
  background: #0077cc;
  color: white;
  border: none;
  padding: 0.6rem 1.2rem;
  font-size: 1rem;
  border-radius: 8px;
  margin: 0.3rem;
  cursor: pointer;
  transition: background 0.2s, transform 0.1s;
}

.btn:hover {
  background: #005fa3;
}

.btn:active {
  transform: scale(0.97);
}

.note {
  font-size: 0.8rem;
  color: #666;
  margin-top: 0.5rem;
}

.footer {
  margin-top: 2rem;
  font-size: 0.75rem;
  color: #aaa;
}
```
:::

:::details script.js
```js
// -----------------------------
// シンプル三目並べ script.js
// -----------------------------

const cells = document.querySelectorAll(".cell");
const currentPlayerSpan = document.getElementById("current-player");
const messageDiv = document.getElementById("message");
const restartBtn = document.getElementById("restart");
const changeFirstBtn = document.getElementById("change-first");

let board = Array(9).fill(null);
let currentPlayer = "◯";
let gameOver = false;
let firstPlayer = "◯";

const winPatterns = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6],
];

// セルをクリックしたときの処理
cells.forEach((cell) => {
  cell.addEventListener("click", () => handleClick(cell));
});

function handleClick(cell) {
  const index = cell.dataset.index;

  if (board[index] || gameOver) return;

  board[index] = currentPlayer;
  cell.textContent = currentPlayer;
  cell.disabled = true;

  if (checkWinner(currentPlayer)) {
    messageDiv.textContent = `🎉 ${currentPlayer} の勝ち！`;
    gameOver = true;
    return;
  }

  if (board.every((v) => v !== null)) {
    messageDiv.textContent = "引き分けです。";
    gameOver = true;
    return;
  }

  currentPlayer = currentPlayer === "◯" ? "×" : "◯";
  currentPlayerSpan.textContent = currentPlayer;
}

// 勝利判定
function checkWinner(player) {
  return winPatterns.some((pattern) => {
    return pattern.every((index) => board[index] === player);
  });
}

// ゲームをリセット
restartBtn.addEventListener("click", resetGame);
function resetGame() {
  board = Array(9).fill(null);
  cells.forEach((cell) => {
    cell.textContent = "";
    cell.disabled = false;
  });
  messageDiv.textContent = "";
  currentPlayer = firstPlayer;
  currentPlayerSpan.textContent = currentPlayer;
  gameOver = false;
}

// 先手を切り替える
changeFirstBtn.addEventListener("click", () => {
  firstPlayer = firstPlayer === "◯" ? "×" : "◯";
  messageDiv.textContent = `次のゲームは ${firstPlayer} が先手です。`;
});
```
:::