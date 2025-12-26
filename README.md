# ❌⭕ Tic Tac Toe Game (HTML, CSS, JavaScript)

A simple **Tic Tac Toe game** created using **HTML, CSS, and JavaScript**.  
This project is beginner-friendly and demonstrates basic game logic, DOM manipulation, and user interaction.

---

## 📌 Project Description

Tic Tac Toe is a classic two-player game played on a 3×3 grid.  
Players take turns marking **X** or **O**.  
The first player to align three marks horizontally, vertically, or diagonally wins.

---


![Alt text](https://github.com/ayesha1332/tic-tac-toe/blob/main/Tic%20Tac%20Toe%20Game.jpeg?raw=true)



## 🛠️ Technologies Used

- HTML5
- CSS3
- JavaScript (Vanilla)

---

## 📂 Project Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>✨ Tic Tac Toe ✨</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Orbitron', 'Arial Black', sans-serif;
            background: linear-gradient(135deg, #0c0c2e 0%, #1a1a3e 50%, #0c0c2e 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: white;
            overflow-x: hidden;
            padding: 20px;
            position: relative;
        }

        /* Neon glow animation */
        @keyframes neon-glow {
            0%, 100% {
                text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff, 0 0 30px #ff00ff, 0 0 40px #ff00ff;
            }
            50% {
                text-shadow: 0 0 20px #00ffff, 0 0 30px #00ffff, 0 0 40px #00ffff, 0 0 50px #00ffff;
            }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes board-glow {
            0%, 100% { box-shadow: 0 0 20px #ff00ff, 0 0 40px rgba(255, 0, 255, 0.3); }
            50% { box-shadow: 0 0 30px #00ffff, 0 0 50px rgba(0, 255, 255, 0.3); }
        }

        @keyframes flicker {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.8; }
        }

        .container {
            background: rgba(10, 10, 40, 0.8);
            backdrop-filter: blur(10px);
            border: 3px solid;
            border-image: linear-gradient(45deg, #ff00ff, #00ffff, #ffff00) 1;
            border-radius: 25px;
            padding: 40px;
            width: 100%;
            max-width: 800px;
            position: relative;
            z-index: 2;
            animation: board-glow 3s infinite alternate;
        }

        /* Background neon lines */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                linear-gradient(90deg, transparent 49%, rgba(255, 0, 255, 0.1) 50%, transparent 51%) 0 0 / 50px 50px,
                linear-gradient(0deg, transparent 49%, rgba(0, 255, 255, 0.1) 50%, transparent 51%) 0 0 / 50px 50px;
            z-index: 1;
            pointer-events: none;
            animation: flicker 4s infinite alternate;
        }

        h1 {
            font-size: 4.5rem;
            margin-bottom: 10px;
            text-align: center;
            background: linear-gradient(to right, #ff00ff, #00ffff, #ffff00);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-transform: uppercase;
            letter-spacing: 3px;
            animation: neon-glow 2s infinite alternate;
            text-shadow: 0 0 20px #ff00ff;
        }

        .subtitle {
            color: #a0a0ff;
            font-size: 1.3rem;
            text-align: center;
            margin-bottom: 30px;
            text-shadow: 0 0 10px #a0a0ff;
            font-weight: 300;
        }

        .game-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(0, 0, 0, 0.5);
            padding: 20px 30px;
            border-radius: 15px;
            margin-bottom: 40px;
            border: 2px solid;
            border-image: linear-gradient(45deg, #ff00ff, #00ffff) 1;
            animation: pulse 3s infinite alternate;
        }

        #status {
            font-size: 2rem;
            font-weight: bold;
            background: linear-gradient(to right, #ff00ff, #00ffff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 15px rgba(255, 0, 255, 0.5);
        }

        .score {
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .score-x {
            color: #ff00ff;
            text-shadow: 0 0 15px #ff00ff;
        }

        .score-o {
            color: #00ffff;
            text-shadow: 0 0 15px #00ffff;
        }

        .vs {
            color: #ffff00;
            font-weight: bold;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin: 0 auto 40px;
            max-width: 500px;
            background: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 20px;
            border: 3px solid;
            border-image: linear-gradient(45deg, #ffff00, #ff00ff) 1;
            animation: pulse 4s infinite alternate;
        }

        .cell {
            aspect-ratio: 1;
            background: rgba(20, 20, 60, 0.8);
            border: none;
            border-radius: 15px;
            font-size: 5rem;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .cell:hover {
            transform: scale(1.05);
            background: rgba(40, 40, 100, 0.9);
            box-shadow: 0 0 30px rgba(255, 255, 255, 0.3);
        }

        .cell::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, #ff00ff, #00ffff, #ffff00, #ff00ff);
            border-radius: 16px;
            z-index: -1;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .cell:hover::before {
            opacity: 1;
            animation: rotate 3s linear infinite;
        }

        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .cell.x {
            color: #ff00ff;
            text-shadow: 0 0 20px #ff00ff, 0 0 40px #ff00ff;
        }

        .cell.o {
            color: #00ffff;
            text-shadow: 0 0 20px #00ffff, 0 0 40px #00ffff;
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 25px;
            margin-top: 30px;
        }

        .neon-btn {
            padding: 18px 40px;
            font-size: 1.3rem;
            font-weight: bold;
            cursor: pointer;
            border: none;
            border-radius: 50px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-family: 'Orbitron', sans-serif;
        }

        .neon-btn::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, #ff00ff, #00ffff, #ffff00, #ff00ff);
            border-radius: 52px;
            z-index: -1;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .neon-btn:hover::before {
            opacity: 1;
            animation: rotate 3s linear infinite;
        }

        .neon-btn span {
            position: relative;
            z-index: 2;
        }

        #restartBtn {
            background: rgba(0, 0, 0, 0.8);
            color: #ffff00;
            box-shadow: 0 0 20px rgba(255, 255, 0, 0.3);
        }

        #restartBtn:hover {
            color: #ffffff;
            box-shadow: 0 0 30px rgba(255, 255, 0, 0.7);
            transform: translateY(-5px);
        }

        #resetScoreBtn {
            background: rgba(0, 0, 0, 0.8);
            color: #ff00ff;
            box-shadow: 0 0 20px rgba(255, 0, 255, 0.3);
        }

        #resetScoreBtn:hover {
            color: #ffffff;
            box-shadow: 0 0 30px rgba(255, 0, 255, 0.7);
            transform: translateY(-5px);
        }

        .winning-cell {
            animation: win-glow 1s infinite alternate;
        }

        @keyframes win-glow {
            0% {
                box-shadow: 0 0 20px #ffff00, 0 0 40px #ffff00, 0 0 60px #ffff00;
                transform: scale(1.1);
            }
            100% {
                box-shadow: 0 0 30px #ff00ff, 0 0 50px #ff00ff, 0 0 70px #ff00ff;
                transform: scale(1.15);
            }
        }

        .player-turn {
            display: flex;
            justify-content: center;
            gap: 40px;
            margin-bottom: 30px;
        }

        .player-indicator {
            padding: 15px 30px;
            border-radius: 15px;
            font-size: 1.5rem;
            font-weight: bold;
            text-transform: uppercase;
            transition: all 0.3s ease;
        }

        .player-x {
            background: rgba(255, 0, 255, 0.1);
            border: 2px solid #ff00ff;
            color: #ff00ff;
            text-shadow: 0 0 10px #ff00ff;
        }

        .player-o {
            background: rgba(0, 255, 255, 0.1);
            border: 2px solid #00ffff;
            color: #00ffff;
            text-shadow: 0 0 10px #00ffff;
        }

        .active-player {
            animation: pulse 1s infinite alternate;
            box-shadow: 0 0 30px currentColor;
            transform: scale(1.1);
        }

        .instructions {
            margin-top: 40px;
            padding: 25px;
            background: rgba(0, 0, 0, 0.6);
            border-radius: 15px;
            border: 2px solid;
            border-image: linear-gradient(45deg, #00ffff, #ffff00) 1;
            font-size: 1.1rem;
            line-height: 1.6;
        }

        .instructions h3 {
            color: #ffff00;
            margin-bottom: 15px;
            text-shadow: 0 0 10px #ffff00;
            font-size: 1.5rem;
        }

        .instructions p {
            margin-bottom: 10px;
            color: #a0a0ff;
        }

        .neon-border {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .neon-border::before {
            content: '';
            position: absolute;
            top: 10px;
            left: 10px;
            right: 10px;
            bottom: 10px;
            border: 2px solid;
            border-image: linear-gradient(45deg, #ff00ff, #00ffff, #ffff00, #ff00ff) 1;
            border-radius: 20px;
            animation: flicker 5s infinite alternate;
        }

        /* Floating particles */
        .particles {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            border-radius: 50%;
            background: #ff00ff;
            animation: float 15s infinite linear;
        }

        .particle:nth-child(2n) {
            background: #00ffff;
            animation-delay: -5s;
        }

        .particle:nth-child(3n) {
            background: #ffff00;
            animation-delay: -10s;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) rotate(360deg);
                opacity: 0;
            }
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 3rem;
            }
            
            .container {
                padding: 20px;
            }
            
            .cell {
                font-size: 3.5rem;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
            
            .neon-btn {
                width: 100%;
                max-width: 300px;
            }
            
            .player-turn {
                flex-direction: column;
                gap: 20px;
            }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
</head>
<body>
    <!-- Neon Border -->
    <div class="neon-border"></div>
    
    <!-- Floating Particles -->
    <div class="particles" id="particles"></div>

    <div class="container">
        <h1>TIC TAC TOE</h1>
        <p class="subtitle">Experience the vibrant colors of gaming</p>
        
        <!-- Player Indicators -->
        <div class="player-turn">
            <div class="player-indicator player-x" id="playerXIndicator">
                PLAYER X
                <div style="font-size: 2rem; margin-top: 5px;">✖</div>
            </div>
            <div class="player-indicator player-o" id="playerOIndicator">
                PLAYER O
                <div style="font-size: 2rem; margin-top: 5px;">◯</div>
            </div>
        </div>
        
        <!-- Game Info -->
        <div class="game-info">
            <div id="status">PLAYER X'S TURN</div>
            <div class="score">
                <span class="score-x" id="scoreX">0</span>
                <span class="vs">VS</span>
                <span class="score-o" id="scoreO">0</span>
            </div>
        </div>
        
        <!-- Game Board -->
        <div class="board">
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
        
        <!-- Controls -->
        <div class="controls">
            <button class="neon-btn" id="restartBtn">
                <span>RESTART GAME</span>
            </button>
            <button class="neon-btn" id="resetScoreBtn">
                <span>RESET SCORE</span>
            </button>
        </div>
        
        <!-- Instructions -->
        <div class="instructions">
            <h3>⚡ HOW TO PLAY ⚡</h3>
            <p>🎯 Players alternate placing X and O on the grid</p>
            <p>🏆 First to get 3 in a row WINS</p>
            <p>🔑 Press R to restart • ESC to reset score</p>
            <p>✨ Experience the vibrant glow!</p>
        </div>
    </div>

    <script>
        // Create floating particles
        function createParticles() {
            const particlesContainer = document.getElementById('particles');
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.classList.add('particle');
                particle.style.left = Math.random() * 100 + 'vw';
                particle.style.animationDuration = (Math.random() * 20 + 10) + 's';
                particle.style.width = particle.style.height = (Math.random() * 6 + 2) + 'px';
                particlesContainer.appendChild(particle);
            }
        }

        // Game elements
        const cells = document.querySelectorAll('.cell');
        const statusText = document.getElementById('status');
        const restartBtn = document.getElementById('restartBtn');
        const resetScoreBtn = document.getElementById('resetScoreBtn');
        const scoreXElement = document.getElementById('scoreX');
        const scoreOElement = document.getElementById('scoreO');
        const playerXIndicator = document.getElementById('playerXIndicator');
        const playerOIndicator = document.getElementById('playerOIndicator');
        
        // Game state
        let currentPlayer = 'X';
        let gameActive = true;
        let gameState = ['', '', '', '', '', '', '', '', ''];
        let scores = { X: 0, O: 0 };
        
        // Winning combinations
        const winningCombinations = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
            [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
            [0, 4, 8], [2, 4, 6]             // diagonals
        ];
        
        // Initialize
        createParticles();
        updatePlayerIndicators();
        
        // Add event listeners
        cells.forEach(cell => {
            cell.addEventListener('click', handleCellClick);
            // Add hover sound effect simulation
            cell.addEventListener('mouseenter', () => {
                if (gameActive && !cell.textContent) {
                    cell.style.transform = 'scale(1.1)';
                }
            });
            cell.addEventListener('mouseleave', () => {
                if (!cell.classList.contains('winning-cell')) {
                    cell.style.transform = 'scale(1)';
                }
            });
        });
        
        restartBtn.addEventListener('click', restartGame);
        resetScoreBtn.addEventListener('click', resetScore);
        
        // Handle cell click
        function handleCellClick(event) {
            const cell = event.target;
            const cellIndex = parseInt(cell.getAttribute('data-index'));
            
            if (gameState[cellIndex] !== '' || !gameActive) return;
            
            // Update game state
            gameState[cellIndex] = currentPlayer;
            cell.textContent = currentPlayer;
            cell.classList.add(currentPlayer.toLowerCase());
            
            // Add click effect
            cell.style.transform = 'scale(0.95)';
            setTimeout(() => {
                if (!cell.classList.contains('winning-cell')) {
                    cell.style.transform = 'scale(1)';
                }
            }, 150);
            
            // Check result
            checkResult();
        }
        
        // Check game result
        function checkResult() {
            let roundWon = false;
            let winningCombo = [];
            
            for (let combo of winningCombinations) {
                const [a, b, c] = combo;
                
                if (gameState[a] && gameState[a] === gameState[b] && gameState[a] === gameState[c]) {
                    roundWon = true;
                    winningCombo = combo;
                    break;
                }
            }
            
            if (roundWon) {
                // Win
                statusText.innerHTML = `🎉 <span style="color:${currentPlayer === 'X' ? '#ff00ff' : '#00ffff'}">PLAYER ${currentPlayer}</span> WINS! 🎉`;
                gameActive = false;
                
                // Update score
                scores[currentPlayer]++;
                updateScoreDisplay();
                
                // Highlight winning cells
                winningCombo.forEach(index => {
                    cells[index].classList.add('winning-cell');
                });
                
                // Create celebration effect
                createCelebration();
                return;
            }
            
            // Check for draw
            if (!gameState.includes('')) {
                statusText.innerHTML = '✨ GAME DRAW! ✨';
                gameActive = false;
                return;
            }
            
            // Continue game
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            statusText.innerHTML = `PLAYER <span style="color:${currentPlayer === 'X' ? '#ff00ff' : '#00ffff'}">${currentPlayer}</span>'S TURN`;
            updatePlayerIndicators();
        }
        
        // Update player indicators
        function updatePlayerIndicators() {
            if (currentPlayer === 'X') {
                playerXIndicator.classList.add('active-player');
                playerOIndicator.classList.remove('active-player');
            } else {
                playerOIndicator.classList.add('active-player');
                playerXIndicator.classList.remove('active-player');
            }
        }
        
        // Update score display
        function updateScoreDisplay() {
            scoreXElement.textContent = scores.X;
            scoreOElement.textContent = scores.O;
        }
        
        // Restart game
        function restartGame() {
            currentPlayer = 'X';
            gameActive = true;
            gameState = ['', '', '', '', '', '', '', '', ''];
            statusText.innerHTML = 'PLAYER <span style="color:#ff00ff">X</span>\'S TURN';
            
            // Clear cells
            cells.forEach(cell => {
                cell.textContent = '';
                cell.classList.remove('x', 'o', 'winning-cell');
                cell.style.transform = 'scale(1)';
            });
            
            updatePlayerIndicators();
        }
        
        // Reset score
        function resetScore() {
            scores = { X: 0, O: 0 };
            updateScoreDisplay();
            restartGame();
        }
        
        // Create celebration effect
        function createCelebration() {
            const container = document.querySelector('.container');
            const colors = ['#ff00ff', '#00ffff', '#ffff00'];
            
            for (let i = 0; i < 20; i++) {
                const confetti = document.createElement('div');
                confetti.style.position = 'absolute';
                confetti.style.width = '10px';
                confetti.style.height = '10px';
                confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.borderRadius = '50%';
                confetti.style.left = Math.random() * 100 + '%';
                confetti.style.top = '-20px';
                confetti.style.zIndex = '1000';
                confetti.style.boxShadow = `0 0 20px ${confetti.style.background}`;
                container.appendChild(confetti);
                
                // Animate confetti
                confetti.animate([
                    { transform: 'translateY(0) rotate(0deg)', opacity: 1 },
                    { transform: `translateY(${window.innerHeight}px) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                ], {
                    duration: Math.random() * 2000 + 1000,
                    easing: 'cubic-bezier(0.1, 0.8, 0.9, 0.1)'
                });
                
                // Remove after animation
                setTimeout(() => confetti.remove(), 3000);
            }
        }
        
        // Keyboard controls
        document.addEventListener('keydown', (event) => {
            if (event.key === 'r' || event.key === 'R') {
                restartBtn.style.transform = 'scale(0.95)';
                setTimeout(() => restartBtn.style.transform = 'scale(1)', 150);
                restartGame();
            }
            
            if (event.key === 'Escape') {
                resetScoreBtn.style.transform = 'scale(0.95)';
                setTimeout(() => resetScoreBtn.style.transform = 'scale(1)', 150);
                resetScore();
            }
        });
        
        // Add some random neon flicker to status
        setInterval(() => {
            if (gameActive) {
                statusText.style.textShadow = `0 0 ${15 + Math.random() * 10}px ${currentPlayer === 'X' ? '#ff00ff' : '#00ffff'}`;
            }
        }, 1000);
    </script>
</body>
</html>

