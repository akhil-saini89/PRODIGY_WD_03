# PRODIGY_WD_03
A simple and interactive Tic-Tac-Toe game built with HTML, CSS, and JavaScript. This project allows two players to play against each other in the browser. It features a clean UI, smooth interactions, and game status updates.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tic Tac Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f4f4f4;
    }
    h1 {
      margin-top: 30px;
      color: #333;
    }
    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      gap: 5px;
      margin: 20px auto;
      width: 310px;
    }
    .cell {
      width: 100px;
      height: 100px;
      background-color: #fff;
      border: 2px solid #444;
      font-size: 2em;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }
    .cell:hover {
      background-color: #e0e0e0;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 1em;
      cursor: pointer;
    }
    #status {
      font-size: 1.2em;
      margin-top: 15px;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe</h1>
  <div class="board" id="board">
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
  <p id="status"></p>
  <button onclick="resetGame()">Restart Game</button>

  <script>
    let currentPlayer = "X";
    let gameBoard = ["", "", "", "", "", "", "", "", ""];
    let gameActive = true;

    const statusDisplay = document.getElementById("status");
    const cells = document.querySelectorAll(".cell");

    function handleCellClick(e) {
      const cell = e.target;
      const index = cell.getAttribute("data-index");

      if (gameBoard[index] !== "" || !gameActive) return;

      gameBoard[index] = currentPlayer;
      cell.textContent = currentPlayer;

      if (checkWinner()) {
        statusDisplay.textContent = `Player ${currentPlayer} wins!`;
        gameActive = false;
        return;
      }

      if (!gameBoard.includes("")) {
        statusDisplay.textContent = "It's a draw!";
        gameActive = false;
        return;
      }

      currentPlayer = currentPlayer === "X" ? "O" : "X";
      statusDisplay.textContent = `Player ${currentPlayer}'s turn`;
    }

    function checkWinner() {
      const winPatterns = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // cols
        [0, 4, 8], [2, 4, 6]             // diagonals
      ];

      return winPatterns.some(pattern => {
        const [a, b, c] = pattern;
        return gameBoard[a] && gameBoard[a] === gameBoard[b] && gameBoard[a] === gameBoard[c];
      });
    }

    function resetGame() {
      gameBoard = ["", "", "", "", "", "", "", "", ""];
      currentPlayer = "X";
      gameActive = true;
      statusDisplay.textContent = `Player ${currentPlayer}'s turn`;
      cells.forEach(cell => cell.textContent = "");
    }

    cells.forEach(cell => cell.addEventListener("click", handleCellClick));
    statusDisplay.textContent = `Player ${currentPlayer}'s turn`;
  </script>
</body>
</html>
