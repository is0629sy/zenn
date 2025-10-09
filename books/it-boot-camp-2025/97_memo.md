---
title: "教材作成時のメモ"
---

カスタマイズ全部やった後の最終形

COM戦できなくなった

:::details index.html
```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>4x4 三目並べ（紙吹雪＆音声ガイド付き）</title>
  <link rel="stylesheet" href="style.css" />
  <!-- party.js CDN -->
  <script src="https://cdn.jsdelivr.net/npm/party-js@latest/bundle/party.min.js"></script>
</head>
<body>
  <main class="app">
    <header class="app-header">
      <h1 class="title-logo">🎊 4×4 三目並べ (Tic-Tac-Toe 4x4)</h1>
      <p class="lead">プレイヤー名を入力し、CPU対戦・難易度・テーマを選べます。</p>
    </header>

    <!-- プレイヤー名入力 -->
    <section class="player-input">
      <label>
        プレイヤー名:
        <input type="text" id="player-name-input" placeholder="あなたの名前を入力" />
      </label>
      <button id="set-name" class="btn">名前を設定</button>
      <div id="player-name-display"></div>
    </section>

    <!-- ステータス -->
    <section class="status">
      <div id="turn">次の手: <strong id="current-player">◯</strong></div>
      <div id="message" aria-live="polite"></div>
    </section>

    <!-- 盤面 -->
    <section class="board-wrap" aria-label="4x4盤面">
      <div id="board" class="board" role="grid" aria-label="4x4 ボード">
        <!-- 16マス -->
        <button class="cell" data-index="0"></button>
        <button class="cell" data-index="1"></button>
        <button class="cell" data-index="2"></button>
        <button class="cell" data-index="3"></button>
        <button class="cell" data-index="4"></button>
        <button class="cell" data-index="5"></button>
        <button class="cell" data-index="6"></button>
        <button class="cell" data-index="7"></button>
        <button class="cell" data-index="8"></button>
        <button class="cell" data-index="9"></button>
        <button class="cell" data-index="10"></button>
        <button class="cell" data-index="11"></button>
        <button class="cell" data-index="12"></button>
        <button class="cell" data-index="13"></button>
        <button class="cell" data-index="14"></button>
        <button class="cell" data-index="15"></button>
      </div>
    </section>

    <!-- コントロール -->
    <section class="controls">
      <button id="restart" class="btn">リセット</button>
      <button id="change-first" class="btn">先手を変更</button>
      <button id="toggle-theme" class="btn">テーマ切り替え</button>
      <button id="toggle-cpu" class="btn">CPU対戦: OFF</button>
      <select id="difficulty" class="btn">
        <option value="easy">難易度: かんたん</option>
        <option value="medium">難易度: ふつう</option>
        <option value="hard" selected>難易度: つよい</option>
      </select>
      <div class="note">CPU対戦をONにすると × がコンピュータになります。</div>
    </section>

    <footer class="footer">
      <small>🎉 4×4 三目並べ — HTML / CSS / JS + party.js</small>
    </footer>
  </main>

  <!-- 効果音 -->
  <audio id="click-sound" src="https://actions.google.com/sounds/v1/cartoon/wood_plank_flicks.ogg" preload="auto"></audio>

  <script src="script.js" defer></script>
</body>
</html>
```
:::

:::details style.css
```css
:root {
  --bg-color: #f4f6f8;
  --app-bg: #fff;
  --text-color: #222;
  --accent-color: #0077cc;
  --cell-bg: #f9f9f9;
  --cell-border: #ccc;
  --cell-hover: #e8f0ff;
  --win-bg: #ffe082;
  --win-border: #ffb300;
  --win-text: #d32f2f;
}

body.dark {
  --bg-color: #1e1f23;
  --app-bg: #2c2e33;
  --text-color: #eaeaea;
  --accent-color: #66ccff;
  --cell-bg: #3a3d42;
  --cell-border: #555;
  --cell-hover: #4b5158;
  --win-bg: #444a56;
  --win-border: #66ccff;
  --win-text: #ffe082;
}

body {
  font-family: "Segoe UI", "Hiragino Kaku Gothic ProN", "Meiryo", sans-serif;
  background: var(--bg-color);
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  color: var(--text-color);
  margin: 0;
  transition: background 0.3s, color 0.3s;
}

.app {
  background: var(--app-bg);
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  width: 360px;
  text-align: center;
}

.title-logo {
  color: var(--accent-color);
  transition: transform 0.25s ease, text-shadow 0.25s ease;
}
.title-logo:hover {
  transform: translateY(-4px) scale(1.08);
  text-shadow: 0 6px 14px rgba(0,0,0,0.3);
}

.board {
  display: grid;
  grid-template-columns: repeat(4, 70px);
  grid-gap: 6px;
  justify-content: center;
  margin: 1rem auto;
}
.cell {
  width: 70px;
  height: 70px;
  background: var(--cell-bg);
  border: 2px solid var(--cell-border);
  font-size: 2rem;
  font-weight: bold;
  color: var(--text-color);
  cursor: pointer;
  border-radius: 8px;
  transition: background 0.2s, transform 0.1s;
}
.cell:hover {
  background: var(--cell-hover);
  transform: scale(1.05);
}
.cell.win {
  background: var(--win-bg) !important;
  border-color: var(--win-border);
  color: var(--win-text);
}

.btn {
  background: var(--accent-color);
  color: white;
  border: none;
  padding: 0.6rem 1rem;
  border-radius: 8px;
  margin: 0.3rem;
  cursor: pointer;
}
.btn:hover { filter: brightness(0.9); }

.note {
  font-size: 0.8rem;
  opacity: 0.8;
  margin-top: 0.5rem;
}
```
:::

:::details script.js
```js
const cells = document.querySelectorAll(".cell");
const currentPlayerSpan = document.getElementById("current-player");
const messageDiv = document.getElementById("message");
const restartBtn = document.getElementById("restart");
const changeFirstBtn = document.getElementById("change-first");
const toggleThemeBtn = document.getElementById("toggle-theme");
const toggleCpuBtn = document.getElementById("toggle-cpu");
const difficultySelect = document.getElementById("difficulty");
const playerNameInput = document.getElementById("player-name-input");
const setNameBtn = document.getElementById("set-name");
const playerNameDisplay = document.getElementById("player-name-display");
const clickSound = document.getElementById("click-sound");

let board = Array(16).fill(null);
let currentPlayer = "◯";
let firstPlayer = "◯";
let gameOver = false;
let cpuEnabled = false;
let darkMode = false;
let difficulty = "hard";
let playerName = "プレイヤー";

// 勝利パターン（4x4）
const winPatterns = [];
for (let r = 0; r < 4; r++) winPatterns.push([r*4, r*4+1, r*4+2, r*4+3]);
for (let c = 0; c < 4; c++) winPatterns.push([c, c+4, c+8, c+12]);
winPatterns.push([0,5,10,15]);
winPatterns.push([3,6,9,12]);

// イベント設定
cells.forEach(cell => cell.addEventListener("click", () => handleClick(cell)));
restartBtn.addEventListener("click", resetGame);
changeFirstBtn.addEventListener("click", changeFirst);
toggleThemeBtn.addEventListener("click", toggleTheme);
toggleCpuBtn.addEventListener("click", toggleCPU);
difficultySelect.addEventListener("change", e => difficulty = e.target.value);
setNameBtn.addEventListener("click", setPlayerName);

function setPlayerName() {
  const name = playerNameInput.value.trim();
  if (name) {
    playerName = name;
    playerNameDisplay.textContent = `ようこそ、${playerName} さん！`;
  } else {
    playerNameDisplay.textContent = "";
  }
}

function speak(text) {
  const utter = new SpeechSynthesisUtterance(text);
  utter.lang = "ja-JP";
  speechSynthesis.speak(utter);
}

function handleClick(cell) {
  const index = cell.dataset.index;
  if (board[index] || gameOver) return;

  clickSound.currentTime = 0;
  clickSound.play();

  makeMove(index, currentPlayer);
  if (checkGameEnd()) return;

  currentPlayer = currentPlayer === "◯" ? "×" : "◯";
  currentPlayerSpan.textContent = currentPlayer;

  if (cpuEnabled && currentPlayer === "×") {
    setTimeout(cpuMove, 500);
  }
}

function makeMove(index, player) {
  board[index] = player;
  cells[index].textContent = player;
  cells[index].disabled = true;
}

function checkGameEnd() {
  const winner = getWinner();
  if (winner) {
    highlightWin(winner.pattern);
    const winnerName = winner.player === "◯" ? playerName : "コンピュータ";
    messageDiv.textContent = `🎉 ${winnerName} の勝ち！`;
    speak(`${winnerName} の勝ちです`);
    gameOver = true;
    // 紙吹雪
    party.confetti(document.body, {
      count: party.variation.range(80, 120),
      spread: 90,
      size: party.variation.range(0.6, 1.2)
    });
    return true;
  }
  if (board.every(v => v)) {
    messageDiv.textContent = "引き分けです。";
    speak("引き分けです");
    gameOver = true;
    return true;
  }
  return false;
}

function getWinner() {
  for (const p of winPatterns) {
    const [a,b,c,d] = p;
    if (board[a] && board[a]===board[b] && board[a]===board[c] && board[a]===board[d])
      return { player: board[a], pattern: p };
  }
  return null;
}

function highlightWin(pattern) {
  pattern.forEach(i => cells[i].classList.add("win"));
}

function cpuMove() {
  if (gameOver) return;
  let index;
  if (difficulty === "easy") {
    const empty = board.map((v,i)=>v?null:i).filter(v=>v!==null);
    index = empty[Math.floor(Math.random()*empty.length)];
  } else if (difficulty === "medium") {
    if (Math.random() < 0.5) {
      index = getBestMove();
    } else {
      const empty = board.map((v,i)=>v?null:i).filter(v=>v!==null);
      index = empty[Math.floor(Math.random()*empty.length)];
    }
  } else {
    index = getBestMove();
  }

  makeMove(index, "×");
  clickSound.currentTime = 0;
  clickSound.play();

  checkGameEnd();
  if (!gameOver) {
    currentPlayer = "◯";
    currentPlayerSpan.textContent = currentPlayer;
  }
}

// --- ミニマックス（4x4対応） ---
function getBestMove() {
  let bestScore = -Infinity;
  let move;
  for (let i = 0; i < 16; i++) {
    if (!board[i]) {
      board[i] = "×";
      const score = minimax(board, 0, false);
      board[i] = null;
      if (score > bestScore) {
        bestScore = score;
        move = i;
      }
    }
  }
  return move;
}

function minimax(state, depth, isMax) {
  const result = staticWinner(state);
  if (result === "×") return 10 - depth;
  if (result === "◯") return depth - 10;
  if (state.every(v=>v)) return 0;

  if (isMax) {
    let best = -Infinity;
    for (let i=0;i<16;i++){
      if(!state[i]){
        state[i]="×";
        best=Math.max(best,minimax(state,depth+1,false));
        state[i]=null;
      }
    }
    return best;
  } else {
    let best = Infinity;
    for (let i=0;i<16;i++){
      if(!state[i]){
        state[i]="◯";
        best=Math.min(best,minimax(state,depth+1,true));
        state[i]=null;
      }
    }
    return best;
  }
}

function staticWinner(b) {
  for (const [a,b1,c,d] of winPatterns) {
    if (b[a] && b[a]===b[b1] && b[a]===b[c] && b[a]===b[d]) return b[a];
  }
  return null;
}

function resetGame() {
  board = Array(16).fill(null);
  cells.forEach(c=>{
    c.textContent="";
    c.disabled=false;
    c.classList.remove("win");
  });
  messageDiv.textContent="";
  currentPlayer=firstPlayer;
  currentPlayerSpan.textContent=currentPlayer;
  gameOver=false;

  if(cpuEnabled && currentPlayer==="×"){
    setTimeout(cpuMove,500);
  }
}

function changeFirst(){
  firstPlayer=firstPlayer==="◯"?"×":"◯";
  messageDiv.textContent=`次のゲームは ${firstPlayer} が先手です。`;
}

function toggleTheme(){
  darkMode=!darkMode;
  document.body.classList.toggle("dark",darkMode);
  toggleThemeBtn.textContent=darkMode?"ライトテーマ":"ダークテーマ";
}

function toggleCPU(){
  cpuEnabled=!cpuEnabled;
  toggleCpuBtn.textContent=cpuEnabled?"CPU対戦: ON":"CPU対戦: OFF";
  messageDiv.textContent=cpuEnabled
    ?"CPU対戦モードをONにしました。×がコンピュータになります。"
    :"CPU対戦モードをOFFにしました。";
  resetGame();
}
```
:::