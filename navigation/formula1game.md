---
layout: page 
title: Formula 1
search_exclude: true
permalink: /formulagame/
description: The Pinnacle of Motorsports
---

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>F1 Quiz Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f4f4f4;
    }

    .question-container {
      margin: 20px auto;
      width: 80%;
      background-color: #fff;
      padding: 20px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      border-radius: 10px;
    }

    .question {
      font-size: 24px;
      margin-bottom: 20px;
    }

    .options {
      list-style: none;
      padding: 0;
    }

    .options li {
      margin: 10px 0;
      background-color: #e1e1e1;
      padding: 10px;
      border-radius: 5px;
      cursor: pointer;
    }

    .options li:hover {
      background-color: #d1d1d1;
    }

    #timer, #score {
      margin: 20px 0;
      font-size: 18px;
    }

    #result {
      font-size: 36px; /* Increased font size */
      color: rgb(184, 45, 17); /* Changed color */
      margin-top: 20px;
    }

  </style>
</head>
<body>

<h1>F1 Quiz Game</h1>

<div id="game-container">
  <div id="timer">Time: 0s</div>
  <div id="score">Score: 0</div>

  <div class="question-container" id="question-container">
    <div class="question" id="question"></div>
    <img id="question-image" style="max-width: 100%; display: none;" alt="F1 Question Image">
    <ul class="options" id="options"></ul>
  </div>
</div>

<div id="result" style="display: none;"></div>

<script>
  const questions = [
    {
      text: "Who won the 2022 F1 World Championship?",
      options: ["Max Verstappen", "Lewis Hamilton", "Sebastian Vettel"],
      correct: 0
    },
    {
      text: "What team does this logo belong to?",
      image: "../images/Ferrari-Scuderia-Logo.png", 
      options: ["Ferrari", "Mercedes", "Red Bull"],
      correct: 0
    },
    {
      text: "In what year did Ayrton Senna win his first world title?",
      options: ["1988", "1990", "1994"],
      correct: 0
    },
    {
      text: "Identify this F1 car.",
      image: "../images/mcl36.jpg", 
      options: ["McLaren MCL36", "Ferrari F2004", "Red Bull RB16"],
      correct: 0
    },
    // New questions
    {
      text: "Which driver won the most races in the 2021 F1 season?",
      options: ["Max Verstappen", "Lewis Hamilton", "Valtteri Bottas"],
      correct: 0
    },
    {
      text: "What is the name of the F1 circuit located in Monaco?",
      options: ["Circuit de Monaco", "Circuit Gilles Villeneuve", "Silverstone Circuit"],
      correct: 0
    },
    {
      text: "Which team did Michael Schumacher drive for during his first World Championship win?",
      options: ["Benetton", "Ferrari", "Williams"],
      correct: 0
    },
    {
      text: "Which country hosts the Australian Grand Prix?",
      options: ["Australia", "New Zealand", "South Africa"],
      correct: 0
    },
    {
      text: "Who is known as 'The Professor' in F1?",
      options: ["Ayrton Senna", "Alain Prost", "Niki Lauda"],
      correct: 1
    },
    {
      text: "What is the maximum number of points a driver can earn in a single race as of 2024?",
      options: ["25", "30", "35"],
      correct: 0
    },
    {
      text: "Which F1 team has won the most Constructors' Championships?",
      options: ["Ferrari", "Mercedes", "Red Bull"],
      correct: 0
    },
    {
      text: "Who holds the record for the most consecutive wins in F1?",
      options: ["Sebastian Vettel", "Michael Schumacher", "Max Verstappen"],
      correct: 2
    },
    {
      text: "Which driver is known for his famous rivalry with Ayrton Senna?",
      options: ["Nelson Piquet", "Nigel Mansell", "Alain Prost"],
      correct: 2
    },
    {
      text: "Which drivers is known as 'The Rookie' of F1?",
      options: ["George Russel", "Fernando Alonso", "Kimi Antonelli"],
      correct: 1
    },
    {
      text: "Which race, along with the 24h Hours of Lemans and the Monaco GP, forms the Triple Crown of Motorsport?",
      options: ["Belgian GP", "Indianapolis 500", "Nürburgring 24 Hours"],
      correct: 1
    }
  ];

  let currentQuestion = 0;
  let score = 0;
  let timer = 0;
  let interval;
  let timerStarted = false;

  const questionContainer = document.getElementById('question-container');
  const questionText = document.getElementById('question');
  const questionImage = document.getElementById('question-image');
  const optionsList = document.getElementById('options');
  const result = document.getElementById('result');
  const scoreDisplay = document.getElementById('score');
  const timerDisplay = document.getElementById('timer');

  function loadQuestion() {
    const question = questions[currentQuestion];

    questionText.textContent = question.text || '';
    if (question.image) {
      questionImage.src = question.image;
      questionImage.style.display = 'block';
    } else {
      questionImage.style.display = 'none';
    }

    optionsList.innerHTML = '';
    question.options.forEach((option, index) => {
      const li = document.createElement('li');
      li.textContent = option;
      li.addEventListener('click', () => selectAnswer(index));
      optionsList.appendChild(li);
    });
  }

  function selectAnswer(selectedIndex) {
    const question = questions[currentQuestion];

    // Start the timer when the first question is answered
    if (!timerStarted) {
      startTimer();
      timerStarted = true;
    }

    if (selectedIndex === question.correct) {
      score++;
      scoreDisplay.textContent = `Score: ${score}`;
    }

    currentQuestion++;
    if (currentQuestion < questions.length) {
      loadQuestion();
    } else {
      endGame();
    }
  }

  function startTimer() {
    interval = setInterval(() => {
      timer++;
      timerDisplay.textContent = `Time: ${timer}s`;
    }, 1000);
  }

  function endGame() {
    clearInterval(interval);
    questionContainer.style.display = 'none';
    result.style.display = 'block';
    result.textContent = `Quiz Over! Final Score: ${score}, Time: ${timer}s`;
  }

  loadQuestion(); // Load the first question as soon as the page loads
</script>

</body>

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