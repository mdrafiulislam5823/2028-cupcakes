<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2048 Cupcakes - Premium Online Game | Play Now</title>
    <meta name="description" content="Experience the ultimate 2048 Cupcakes game with stunning visuals and professional design. Combine delicious cupcakes to create amazing treats. Free premium gaming experience.">
    <meta name="keywords" content="2048 cupcakes, premium cupcake game, professional 2048, cupcake puzzle, online gaming, dessert games, bakery games, casual gaming">
    <meta name="author" content="2048 Cupcakes Studio">
    <meta name="robots" content="index, follow">
    <meta property="og:title" content="2048 Cupcakes - Premium Online Game">
    <meta property="og:description" content="Experience professional 2048 gaming with stunning cupcake visuals. Free premium gaming experience.">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://unblockedgamesgplus.bitbucket.io/">
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="2048 Cupcakes - Premium Game">
    <meta name="twitter:description" content="Professional 2048 gaming with stunning visuals">
    <link rel="canonical" href="https://unblockedgamesgplus.bitbucket.io/">
    <meta name="theme-color" content="#ff4d94">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.7.0/p5.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            position: relative;
            overflow-x: hidden;
        }
        
        body::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="grain" width="100" height="100" patternUnits="userSpaceOnUse"><circle cx="50" cy="50" r="1" fill="white" opacity="0.1"/></pattern></defs><rect width="100" height="100" fill="url(%23grain)"/></svg>');
            pointer-events: none;
        }
        
        .game-wrapper {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 30px;
            padding: 40px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.15);
            max-width: 600px;
            width: 100%;
            position: relative;
            z-index: 1;
        }
        
        .header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .title {
            font-size: 56px;
            font-weight: 700;
            background: linear-gradient(45deg, #ff6b9d, #ff8fab);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
            text-shadow: 0 4px 8px rgba(255, 107, 157, 0.3);
        }
        
        .subtitle {
            font-size: 20px;
            color: #666;
            font-weight: 300;
            margin-bottom: 25px;
        }
        
        .score-board {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-bottom: 30px;
        }
        
        .score-item {
            background: linear-gradient(135deg, #ff6b9d, #ff8fab);
            color: white;
            padding: 20px 30px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 8px 20px rgba(255, 107, 157, 0.3);
            transition: transform 0.3s ease;
        }
        
        .score-item:hover {
            transform: translateY(-2px);
        }
        
        .score-label {
            font-size: 14px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 5px;
            opacity: 0.9;
        }
        
        .score-value {
            font-size: 28px;
            font-weight: 700;
        }
        
        .game-board {
            display: flex;
            justify-content: center;
            margin: 30px 0;
        }
        
        #gameCanvas {
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            background: white;
        }
        
        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 30px 0;
            flex-wrap: wrap;
        }
        
        .btn {
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            text-transform: uppercase;
            letter-spacing: 1px;
            min-width: 140px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }
        
        .btn-secondary {
            background: linear-gradient(135deg, #ff6b9d, #ff8fab);
            color: white;
        }
        
        .btn-accent {
            background: linear-gradient(135deg, #f093fb, #f5576c);
            color: white;
            animation: pulse 2s infinite;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
        }
        
        .instructions {
            text-align: center;
            color: #666;
            font-size: 16px;
            line-height: 1.6;
            max-width: 500px;
            margin: 0 auto;
        }
        
        /* Enhanced Modal Styles */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(10px);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }
        
        .modal-overlay.show {
            opacity: 1;
            visibility: visible;
        }
        
        .modal-content {
            background: white;
            border-radius: 30px;
            padding: 50px;
            text-align: center;
            max-width: 450px;
            margin: 20px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
            transform: scale(0.8);
            transition: transform 0.3s ease;
        }
        
        .modal-overlay.show .modal-content {
            transform: scale(1);
        }
        
        .modal-icon {
            font-size: 60px;
            margin-bottom: 20px;
        }
        
        .modal-title {
            font-size: 32px;
            font-weight: 700;
            background: linear-gradient(45deg, #ff6b9d, #ff8fab);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 15px;
        }
        
        .modal-subtitle {
            font-size: 18px;
            color: #666;
            line-height: 1.6;
            margin-bottom: 30px;
        }
        
        .modal-btn {
            padding: 18px 40px;
            font-size: 18px;
            font-weight: 600;
            border: none;
            border-radius: 50px;
            background: linear-gradient(135deg, #ff6b9d, #ff8fab);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 8px 20px rgba(255, 107, 157, 0.3);
            animation: pulse 2s infinite;
        }
        
        .close-modal {
            position: absolute;
            top: 20px;
            right: 25px;
            font-size: 28px;
            color: #999;
            cursor: pointer;
            transition: color 0.3s ease;
            background: none;
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .close-modal:hover {
            color: #ff6b9d;
            background: rgba(255, 107, 157, 0.1);
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }
        
        .bounce {
            animation: bounce 0.6s ease;
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            .game-wrapper {
                margin: 10px;
                padding: 25px;
            }
            
            .title {
                font-size: 42px;
            }
            
            .score-board {
                gap: 15px;
            }
            
            .score-item {
                padding: 15px 20px;
            }
            
            .controls {
                gap: 10px;
            }
            
            .btn {
                padding: 12px 25px;
                font-size: 14px;
                min-width: 120px;
            }
        }
    </style>
</head>
<body>
    <!-- Enhanced Popup Modal -->
    <div class="modal-overlay" id="welcomeModal">
        <div class="modal-content">
            <button class="close-modal" onclick="closeModal()">&times;</button>
            <div class="modal-icon">🎂</div>
            <div class="modal-title">Welcome to 2048 Cupcakes</div>
            <div class="modal-subtitle">
                Experience the most beautiful 2048 game ever created! <br>
                <strong>Premium Design • Stunning Visuals • Free Forever</strong>
            </div>
            <button class="modal-btn" onclick="redirectToGames()">Start Playing Now</button>
        </div>
    </div>

    <div class="game-wrapper">
        <div class="header">
            <h1 class="title">2048 Cupcakes</h1>
            <p class="subtitle">Master the art of cupcake fusion</p>
        </div>
        
        <div class="score-board">
            <div class="score-item">
                <div class="score-label">Score</div>
                <div class="score-value" id="score">0</div>
            </div>
            <div class="score-item">
                <div class="score-label">Best</div>
                <div class="score-value" id="best">0</div>
            </div>
        </div>
        
        <div class="game-board">
            <div id="gameCanvas"></div>
        </div>
        
        <div class="controls">
            <button class="btn btn-primary" onclick="resetGame()">New Game</button>
            <button class="btn btn-secondary" onclick="showRules()">How to Play</button>
            <button class="btn btn-accent" onclick="window.open('https://unblockedgamesgplus.bitbucket.io/', '_blank')">Play More Games</button>
        </div>
        
        <div class="instructions">
            Use arrow keys or WASD to move. Combine matching cupcakes to create new delicious treats. <br>
            <strong>Goal: Reach the Ultimate Rainbow Cupcake!</strong>
        </div>
    </div>

    <script>
        let grid;
        let score = 0;
        let best = 0;
        let gameOver = false;
        let tileSize = 100;
        let gridSize = 4;
        let gap = 10;
        
        // Cupcake types with colors and emojis
        const cupcakes = [
            { value: 2, emoji: '🧁', color: '#FFB6C1' },
            { value: 4, emoji: '🍰', color: '#FF69B4' },
            { value: 8, emoji: '🍪', color: '#FF1493' },
            { value: 16, emoji: '🍩', color: '#DC143C' },
            { value: 32, emoji: '🍦', color: '#8B0000' },
            { value: 64, emoji: '🧊', color: '#FF4500' },
            { value: 128, emoji: '🎂', color: '#FF8C00' },
            { value: 256, emoji: '🍭', color: '#FFD700' },
            { value: 512, emoji: '🍮', color: '#ADFF2F' },
            { value: 1024, emoji: '🍬', color: '#00FF00' },
            { value: 2048, emoji: '🌈', color: '#00FFFF' }
        ];

        function setup() {
            let canvas = createCanvas(4 * tileSize + 5 * gap, 4 * tileSize + 5 * gap);
            canvas.parent('gameCanvas');
            
            resetGame();
            
            // Load best score from localStorage
            if (localStorage.getItem('cupcake2048_best')) {
                best = parseInt(localStorage.getItem('cupcake2048_best'));
                document.getElementById('best').textContent = best;
            }
        }

        function resetGame() {
            grid = Array(gridSize).fill().map(() => Array(gridSize).fill(0));
            score = 0;
            gameOver = false;
            document.getElementById('score').textContent = score;
            
            // Add initial tiles
            addRandomTile();
            addRandomTile();
        }

        function addRandomTile() {
            let emptyCells = [];
            for (let i = 0; i < gridSize; i++) {
                for (let j = 0; j < gridSize; j++) {
                    if (grid[i][j] === 0) {
                        emptyCells.push({x: i, y: j});
                    }
                }
            }
            
            if (emptyCells.length > 0) {
                let cell = random(emptyCells);
                grid[cell.x][cell.y] = random() < 0.9 ? 2 : 4;
            }
        }

        function draw() {
            background(255, 240, 245);
            
            // Draw grid
            for (let i = 0; i < gridSize; i++) {
                for (let j = 0; j < gridSize; j++) {
                    let x = j * (tileSize + gap) + gap;
                    let y = i * (tileSize + gap) + gap;
                    
                    // Draw empty tile
                    fill(240, 240, 240);
                    stroke(200);
                    strokeWeight(2);
                    rect(x, y, tileSize, tileSize, 10);
                    
                    // Draw cupcake
                    if (grid[i][j] !== 0) {
                        let cupcake = cupcakes.find(c => c.value === grid[i][j]) || 
                                     cupcakes[cupcakes.length - 1];
                        
                        fill(cupcake.color);
                        noStroke();
                        rect(x, y, tileSize, tileSize, 10);
                        
                        // Draw emoji
                        textAlign(CENTER, CENTER);
                        textSize(grid[i][j] > 512 ? 40 : 50);
                        text(cupcake.emoji, x + tileSize/2, y + tileSize/2 - 10);
                        
                        // Draw value
                        fill(255);
                        textSize(grid[i][j] > 512 ? 16 : 20);
                        text(grid[i][j], x + tileSize/2, y + tileSize/2 + 20);
                    }
                }
            }
            
            // Game over message
            if (gameOver) {
                fill(0, 0, 0, 150);
                rect(0, 0, width, height);
                
                fill(255);
                textAlign(CENTER, CENTER);
                textSize(32);
                text("Game Over!", width/2, height/2 - 20);
                textSize(20);
                text("Press R to restart", width/2, height/2 + 20);
            }
        }

        function keyPressed() {
            if (gameOver && keyCode === 82) { // R key
                resetGame();
                return;
            }
            
            if (!gameOver) {
                let moved = false;
                
                if (keyCode === UP_ARROW || key === 'w' || key === 'W') {
                    moved = moveUp();
                } else if (keyCode === DOWN_ARROW || key === 's' || key === 'S') {
                    moved = moveDown();
                } else if (keyCode === LEFT_ARROW || key === 'a' || key === 'A') {
                    moved = moveLeft();
                } else if (keyCode === RIGHT_ARROW || key === 'd' || key === 'D') {
                    moved = moveRight();
                }
                
                if (moved) {
                    addRandomTile();
                    updateScore();
                    
                    if (checkGameOver()) {
                        gameOver = true;
                        if (score > best) {
                            best = score;
                            localStorage.setItem('cupcake2048_best', best);
                            document.getElementById('best').textContent = best;
                        }
                    }
                }
            }
        }

        function moveUp() {
            let moved = false;
            for (let j = 0; j < gridSize; j++) {
                for (let i = 1; i < gridSize; i++) {
                    if (grid[i][j] !== 0) {
                        let k = i;
                        while (k > 0 && grid[k-1][j] === 0) {
                            grid[k-1][j] = grid[k][j];
                            grid[k][j] = 0;
                            k--;
                            moved = true;
                        }
                        if (k > 0 && grid[k-1][j] === grid[k][j]) {
                            grid[k-1][j] *= 2;
                            score += grid[k-1][j];
                            grid[k][j] = 0;
                            moved = true;
                        }
                    }
                }
            }
            return moved;
        }

        function moveDown() {
            let moved = false;
            for (let j = 0; j < gridSize; j++) {
                for (let i = gridSize - 2; i >= 0; i--) {
                    if (grid[i][j] !== 0) {
                        let k = i;
                        while (k < gridSize - 1 && grid[k+1][j] === 0) {
                            grid[k+1][j] = grid[k][j];
                            grid[k][j] = 0;
                            k++;
                            moved = true;
                        }
                        if (k < gridSize - 1 && grid[k+1][j] === grid[k][j]) {
                            grid[k+1][j] *= 2;
                            score += grid[k+1][j];
                            grid[k][j] = 0;
                            moved = true;
                        }
                    }
                }
            }
            return moved;
        }

        function moveLeft() {
            let moved = false;
            for (let i = 0; i < gridSize; i++) {
                for (let j = 1; j < gridSize; j++) {
                    if (grid[i][j] !== 0) {
                        let k = j;
                        while (k > 0 && grid[i][k-1] === 0) {
                            grid[i][k-1] = grid[i][k];
                            grid[i][k] = 0;
                            k--;
                            moved = true;
                        }
                        if (k > 0 && grid[i][k-1] === grid[i][k]) {
                            grid[i][k-1] *= 2;
                            score += grid[i][k-1];
                            grid[i][k] = 0;
                            moved = true;
                        }
                    }
                }
            }
            return moved;
        }

        function moveRight() {
            let moved = false;
            for (let i = 0; i < gridSize; i++) {
                for (let j = gridSize - 2; j >= 0; j--) {
                    if (grid[i][j] !== 0) {
                        let k = j;
                        while (k < gridSize - 1 && grid[i][k+1] === 0) {
                            grid[i][k+1] = grid[i][k];
                            grid[i][k] = 0;
                            k++;
                            moved = true;
                        }
                        if (k < gridSize - 1 && grid[i][k+1] === grid[i][k]) {
                            grid[i][k+1] *= 2;
                            score += grid[i][k+1];
                            grid[i][k] = 0;
                            moved = true;
                        }
                    }
                }
            }
            return moved;
        }

        function updateScore() {
            document.getElementById('score').textContent = score;
        }

        function checkGameOver() {
            // Check for empty cells
            for (let i = 0; i < gridSize; i++) {
                for (let j = 0; j < gridSize; j++) {
                    if (grid[i][j] === 0) return false;
                }
            }
            
            // Check for possible merges
            for (let i = 0; i < gridSize; i++) {
                for (let j = 0; j < gridSize; j++) {
                    if (i < gridSize - 1 && grid[i][j] === grid[i+1][j]) return false;
                    if (j < gridSize - 1 && grid[i][j] === grid[i][j+1]) return false;
                }
            }
            
            return true;
        }

        function showRules() {
            alert(`🧁 2048 Cupcakes Rules:

• Use arrow keys or WASD to move cupcakes
• When two identical cupcakes touch, they merge into a new cupcake
• Each merge gives you points equal to the new cupcake's value
• Try to reach the ultimate Rainbow Cupcake (2048)!
• The game ends when no more moves are possible

Good luck! 🍰`);
        }

        // Modal Popup Functions
        function redirectToGames() {
            window.open('https://unblockedgamesgplus.bitbucket.io/', '_blank');
        }

        function closeModal() {
            document.getElementById('welcomeModal').style.display = 'none';
        }

        // Show modal on page load
        window.addEventListener('load', function() {
            setTimeout(function() {
                document.getElementById('welcomeModal').style.display = 'flex';
            }, 500);
        });

        // Close modal when clicking outside
        window.addEventListener('click', function(event) {
            const modal = document.getElementById('welcomeModal');
            if (event.target === modal) {
                closeModal();
            }
        });
    </script>
</body>
</html>