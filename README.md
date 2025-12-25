# ❌⭕ Tic Tac Toe Game (HTML, CSS, JavaScript)

A simple **Tic Tac Toe game** created using **HTML, CSS, and JavaScript**.  
This project is beginner-friendly and demonstrates basic game logic, DOM manipulation, and user interaction.

---

## 📌 Project Description

Tic Tac Toe is a classic two-player game played on a 3×3 grid.  
Players take turns marking **X** or **O**.  
The first player to align three marks horizontally, vertically, or diagonally wins.

---

## 🛠️ Technologies Used

- HTML5
- CSS3
- JavaScript (Vanilla)

---

## 📂 Project Files & Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Tic Tac Toe</title>

    <!-- CSS CODE -->
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
        }

        h1 {
            margin-top: 20px;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            gap: 5px;
            justify-content: center;
            margin: 20px auto;
        }

        .cell {
            width: 100px;
            height: 100px;
            background-color: #ffffff;
            border: 2px solid #000;
            font-size: 2.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }

        .cell:hover {
            background-color: #e0e0e0;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <!-- HTML CODE -->
    <h1>Tic Tac Toe</h1>
    <p id="status">Player X's turn</p>

    <div class="board">
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
    </div>

    <button onclick="restartGame()">Restart Game</button>

    <!-- JAVASCRIPT CODE -->
    <script>
        const cells = document.querySelectorAll('.cell');
        const statusText = document.getElementById('status');

        let currentPlayer = 'X';
        let gameActive = true;

        const winningCombinations = [
            [0,1,2],
            [3,4,5],
            [6,7,8],
            [0,3,6],
            [1,4,7],
            [2,5,8],
            [0,4,8],
            [2,4,6]
        ];

        cells.forEach(cell => {
            cell.addEventListener('click', handleCellClick);
        });

        function handleCellClick() {
            if (this.textContent !== '' || !gameActive) return;

            this.textContent = currentPlayer;
            checkWinner();
        }

        function checkWinner() {
            let win = false;

            for (let combo of winningCombinations) {
                const [a, b, c] = combo;

                if (
                    cells[a].textContent &&
                    cells[a].textContent === cells[b].textContent &&
                    cells[a].textContent === cells[c].textContent
                ) {
                    win = true;
                    break;
                }
            }

            if (win) {
                statusText.textContent = `Player ${currentPlayer} wins`;
                gameActive = false;
                return;
            }

            if ([...cells].every(cell => cell.textContent !== '')) {
                statusText.textContent = "Game Draw";
                gameActive = false;
                return;
            }

            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            statusText.textContent = `Player ${currentPlayer}'s turn`;
        }

        function restartGame() {
            currentPlayer = 'X';
            gameActive = true;
            statusText.textContent = "Player X's turn";
            cells.forEach(cell => cell.textContent = '');
        }
    </script>

</body>
</html>

