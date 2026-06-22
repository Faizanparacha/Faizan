[my tic toe.html](https://github.com/user-attachments/files/29209676/my.tic.toe.html)
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
  }

  h1 { margin-bottom: 5px; }

  #status {
    font-size: 20px;
    margin-bottom: 15px;
  }

  .row {
    display: flex;
    justify-content: center;
  }

  .box {
    background-color: white;
    width: 70px;
    height: 70px;
    border: 2px solid black;
    margin: 5px;
    font-size: 36px;
    font-weight: bold;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .box:hover {
    background-color: #f0f0f0;
  }

  #resetBtn {
    margin-top: 15px;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
  }
</style>
</head>
<body>

<h1>Tic Tac Toe</h1>
<div id="status">Player X's Turn</div>

<div class="row">
  <div class="box" onclick="handleClick(this, 0)"></div>
  <div class="box" onclick="handleClick(this, 1)"></div>
  <div class="box" onclick="handleClick(this, 2)"></div>
</div>
<div class="row">
  <div class="box" onclick="handleClick(this, 3)"></div>
  <div class="box" onclick="handleClick(this, 4)"></div>
  <div class="box" onclick="handleClick(this, 5)"></div>
</div>
<div class="row">
  <div class="box" onclick="handleClick(this, 6)"></div>
  <div class="box" onclick="handleClick(this, 7)"></div>
  <div class="box" onclick="handleClick(this, 8)"></div>
</div>

<button id="resetBtn" onclick="resetGame()">Restart Game</button>

<script>
  let board = ["", "", "", "", "", "", "", "", ""];
  let currentPlayer = "X";
  let gameOver = false;

  const winCombos = [
    [0,1,2], [3,4,5], [6,7,8], // rows
    [0,3,6], [1,4,7], [2,5,8], // columns
    [0,4,8], [2,4,6]           // diagonals
  ];

  function handleClick(cell, index) {
    if (gameOver || board[index] !== "") return;

    board[index] = currentPlayer;
    cell.textContent = currentPlayer;

    if (checkWinner()) {
      document.getElementById("status").textContent = "Player " + currentPlayer + " Wins! 🎉";
      gameOver = true;
      return;
    }

    if (board.every(cell => cell !== "")) {
      document.getElementById("status").textContent = "It's a Draw!";
      gameOver = true;
      return;
    }

    currentPlayer = currentPlayer === "X" ? "O" : "X";
    document.getElementById("status").textContent = "Player " + currentPlayer + "'s Turn";
  }

  function checkWinner() {
    return winCombos.some(combo =>
      board[combo[0]] !== "" &&
      board[combo[0]] === board[combo[1]] &&
      board[combo[1]] === board[combo[2]]
    );
  }

  function resetGame() {
    board = ["", "", "", "", "", "", "", "", ""];
    currentPlayer = "X";
    gameOver = false;
    document.querySelectorAll(".box").forEach(box => box.textContent = "");
    document.getElementById("status").textContent = "Player X's Turn";
  }
</script>

</body>
</html>

