---
layout: page 
title: Snake Game
search_exclude: true
permalink: /games/snakegameplus/
description: Play the Snake Game with a friend or by yourself
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Two Player Snake Game</title>
    <style>
        canvas {
            background: #f0f0f0;
            display: block;
            margin: 0 auto;
            border: 1px solid #000;
        }
        #controls {
            text-align: center;
            margin-bottom: 10px;
        }
        button {
            margin: 5px;
        }
    </style>
</head>
<body>
    <div id="controls">
        <button id="humanButton">Opponent: Human</button>
        <button id="aiButton">Opponent: AI</button>
    </div>
    <canvas id="gameCanvas" width="600" height="400"></canvas>
    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scale = 20;
        const rows = canvas.height / scale;
        const cols = canvas.width / scale;

        let isAI = false; // Default opponent type is human

        let snake1 = { x: 2 * scale, y: 2 * scale, dx: scale, dy: 0, body: [], started: false, alive: true };
        let snake2 = { x: 10 * scale, y: 10 * scale, dx: 0, dy: -scale, body: [], started: false, alive: true };
        let apple = { x: Math.floor(Math.random() * cols) * scale, y: Math.floor(Math.random() * rows) * scale };

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Draw grid
            ctx.strokeStyle = '#ddd';
            for (let i = 0; i <= canvas.width; i += scale) {
                ctx.beginPath();
                ctx.moveTo(i, 0);
                ctx.lineTo(i, canvas.height);
                ctx.stroke();
            }
            for (let i = 0; i <= canvas.height; i += scale) {
                ctx.beginPath();
                ctx.moveTo(0, i);
                ctx.lineTo(canvas.width, i);
                ctx.stroke();
            }
            
            // Draw apple
            ctx.fillStyle = 'red';
            ctx.fillRect(apple.x, apple.y, scale, scale);
            
            // Draw snakes
            if (snake1.alive) drawSnake(snake1, 'green');
            if (snake2.alive) drawSnake(snake2, 'blue');
        }

        function drawSnake(snake, color) {
            ctx.fillStyle = color;
            snake.body.forEach(segment => ctx.fillRect(segment.x, segment.y, scale, scale));
            ctx.fillRect(snake.x, snake.y, scale, scale);
        }

        function update() {
            if (snake1.alive && snake1.started) moveSnake(snake1);
            if (snake2.alive && snake2.started) {
                if (isAI) aiMove(snake2);
                else moveSnake(snake2);
            }
            
            // Check for apple collision
            if (snake1.x === apple.x && snake1.y === apple.y) {
                snake1.body.push({ x: apple.x, y: apple.y });
                apple = { x: Math.floor(Math.random() * cols) * scale, y: Math.floor(Math.random() * rows) * scale };
            }
            
            if (snake2.x === apple.x && snake2.y === apple.y) {
                snake2.body.push({ x: apple.x, y: apple.y });
                apple = { x: Math.floor(Math.random() * cols) * scale, y: Math.floor(Math.random() * rows) * scale };
            }
            
            // Check for wall collision and collisions with the other snake
            if (!snake1.alive) respawn(snake1);
            if (!snake2.alive) respawn(snake2);

            if (collision(snake1, snake2) || collision(snake2, snake1)) {
                if (snake1.alive && snake2.alive) resetGame();
                else if (snake1.alive) respawn(snake1);
                else if (snake2.alive) respawn(snake2);
            }
        }

        function moveSnake(snake) {
            snake.x += snake.dx;
            snake.y += snake.dy;
            
            // Check for wall collision
            if (snake.x < 0 || snake.x >= canvas.width || snake.y < 0 || snake.y >= canvas.height) {
                snake.alive = false;
                return;
            }
            
            // Add new head
            snake.body.unshift({ x: snake.x, y: snake.y });
            
            // Remove tail
            snake.body.pop();
        }

        function aiMove(snake) {
            // AI that tries to move towards the apple
            const directions = [{dx: scale, dy: 0}, {dx: -scale, dy: 0}, {dx: 0, dy: scale}, {dx: 0, dy: -scale}];
            let bestMove = null;
            let minDistance = Infinity;

            for (const move of directions) {
                if (move.dx === -snake.dx && move.dy === -snake.dy) continue; // Avoid reverse direction
                const newX = snake.x + move.dx;
                const newY = snake.y + move.dy;
                const distance = Math.hypot(apple.x - newX, apple.y - newY);

                if (distance < minDistance) {
                    minDistance = distance;
                    bestMove = move;
                }
            }

            if (bestMove) {
                snake.dx = bestMove.dx;
                snake.dy = bestMove.dy;
                moveSnake(snake);
            }
        }

        function collision(snake1, snake2) {
            return snake2.body.some(segment => segment.x === snake1.x && segment.y === snake1.y);
        }

        function respawn(snake) {
            if (!snake.alive) {
                snake.x = Math.floor(Math.random() * cols) * scale;
                snake.y = Math.floor(Math.random() * rows) * scale;
                snake.body = [];
                snake.dx = scale;
                snake.dy = 0;
                snake.started = false;
                snake.alive = true;
            }
        }

        function resetGame() {
            snake1 = { x: 2 * scale, y: 2 * scale, dx: scale, dy: 0, body: [], started: false, alive: true };
            snake2 = { x: 10 * scale, y: 10 * scale, dx: 0, dy: -scale, body: [], started: false, alive: true };
            apple = { x: Math.floor(Math.random() * cols) * scale, y: Math.floor(Math.random() * rows) * scale };
        }

        function control(e) {
            switch(e.keyCode) {
                case 37: // Left arrow
                    if (snake1.dx === 0) { snake1.dx = -scale; snake1.dy = 0; }
                    snake1.started = true;
                    e.preventDefault(); // Prevent default arrow key action
                    break;
                case 38: // Up arrow
                    if (snake1.dy === 0) { snake1.dy = -scale; snake1.dx = 0; }
                    snake1.started = true;
                    e.preventDefault(); // Prevent default arrow key action
                    break;
                case 39: // Right arrow
                    if (snake1.dx === 0) { snake1.dx = scale; snake1.dy = 0; }
                    snake1.started = true;
                    e.preventDefault(); // Prevent default arrow key action
                    break;
                case 40: // Down arrow
                    if (snake1.dy === 0) { snake1.dy = scale; snake1.dx = 0; }
                    snake1.started = true;
                    e.preventDefault(); // Prevent default arrow key action
                    break;
                case 65: // A key (left for player 2)
                    if (snake2.dx === 0) { snake2.dx = -scale; snake2.dy = 0; }
                    snake2.started = true;
                    break;
                case 87: // W key (up for player 2)
                    if (snake2.dy === 0) { snake2.dy = -scale; snake2.dx = 0; }
                    snake2.started = true;
                    break;
                case 68: // D key (right for player 2)
                    if (snake2.dx === 0) { snake2.dx = scale; snake2.dy = 0; }
                    snake2.started = true;
                    break;
                case 83: // S key (down for player 2)
                    if (snake2.dy === 0) { snake2.dy = scale; snake2.dx = 0; }
                    snake2.started = true;
                    break;
            }
        }

        function selectOpponent(opponent) {
            if (opponent === 'human') {
                isAI = false;
                document.getElementById('humanButton').disabled = true;
                document.getElementById('aiButton').disabled = false;
            } else if (opponent === 'ai') {
                isAI = true;
                document.getElementById('humanButton').disabled = false;
                document.getElementById('aiButton').disabled = true;
            }
            resetGame(); // Reset the game when opponent type is changed
        }

        document.getElementById('humanButton').addEventListener('click', () => selectOpponent('human'));
        document.getElementById('aiButton').addEventListener('click', () => selectOpponent('ai'));

        document.addEventListener('keydown', control);

        function gameLoop() {
            update();
            draw();
            setTimeout(gameLoop, 100);
        }

        gameLoop();
    </script>
</body>