---
layout: page 
title: Snake Game
search_exclude: true
permalink: /games/snakegame/
description: Play the Snake Game with power-ups
---

Controls: Arrow Keys


Apples: Red Square


PowerUp: Yellow


<canvas id="snakeGame" width="400" height="400" style="border:1px solid black;"></canvas>
<button id="startButton" style="display:none;">Start Game</button>

<script>
      window.addEventListener("keydown", function(event) {
      if (["ArrowUp", "ArrowDown", "ArrowLeft", "ArrowRight"].includes(event.key)) {
        event.preventDefault(); // Prevents default scrolling behavior
      }
    });
  const canvas = document.getElementById("snakeGame");
  const ctx = canvas.getContext("2d");
  const box = 20;
  let snake, food, powerUp, direction, gameOver, game;
  let gameSpeed = 100; // Initial game speed

  const startButton = document.getElementById("startButton");
  startButton.addEventListener("click", startGame);

  document.addEventListener("keydown", setDirection);

  function startGame() {
    snake = [{ x: 9 * box, y: 10 * box }];
    food = {
      x: Math.floor(Math.random() * 20) * box,
      y: Math.floor(Math.random() * 20) * box
    };
    powerUp = null; // No power-up at the start
    direction = null;
    gameOver = false;
    gameSpeed = 100;
    startButton.style.display = "none";
    clearInterval(game); // Clear any existing game intervals
    game = setInterval(drawGame, gameSpeed);
    generatePowerUp(); // Generate a single power-up
  }

  function setDirection(event) {
    if (event.key === 'ArrowUp' && direction !== "DOWN") direction = "UP";
    else if (event.key === 'ArrowDown' && direction !== "UP") direction = "DOWN";
    else if (event.key === 'ArrowLeft' && direction !== "RIGHT") direction = "LEFT";
    else if (event.key === 'ArrowRight' && direction !== "LEFT") direction = "RIGHT";
  }

  function drawGame() {
    if (gameOver) {
      ctx.fillStyle = "black";
      ctx.font = "40px Arial";
      ctx.fillText("Game Over", 100, canvas.height / 2);
      clearInterval(game);
      startButton.style.display = "block";
      return;
    }

    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Draw snake
    for (let i = 0; i < snake.length; i++) {
      ctx.fillStyle = (i === 0) ? "green" : "lightgreen";
      ctx.fillRect(snake[i].x, snake[i].y, box, box);
    }

    // Draw food
    ctx.fillStyle = "red";
    ctx.fillRect(food.x, food.y, box, box);

    // Draw power-up if it exists
    if (powerUp) {
      ctx.fillStyle = "orange";
      ctx.fillRect(powerUp.x, powerUp.y, box, box);
    }

    // Move snake
    let snakeX = snake[0].x;
    let snakeY = snake[0].y;

    if (direction === "UP") snakeY -= box;
    if (direction === "DOWN") snakeY += box;
    if (direction === "LEFT") snakeX -= box;
    if (direction === "RIGHT") snakeX += box;

    // Snake eats food
    if (snakeX === food.x && snakeY === food.y) {
      food = {
        x: Math.floor(Math.random() * 20) * box,
        y: Math.floor(Math.random() * 20) * box
      };
    } else {
      snake.pop();
    }

    let newHead = { x: snakeX, y: snakeY };

    // Check for power-up collision
    if (powerUp && snakeX === powerUp.x && snakeY === powerUp.y) {
      growSnakeByThree();
      powerUp = null; // Remove the power-up after it is consumed
      setTimeout(generatePowerUp, Math.random() * 10000 + 5000); // Generate a new power-up after a delay
    }

    // Game over condition
    if (snakeX < 0 || snakeY < 0 || snakeX >= canvas.width || snakeY >= canvas.height || collision(newHead, snake)) {
      gameOver = true;
    }

    snake.unshift(newHead); // Add the new head to the front of the snake
  }

  function collision(head, array) {
    for (let i = 0; i < array.length; i++) {
      if (head.x === array[i].x && head.y === array[i].y) {
        return true;
      }
    }
    return false;
  }

  function generatePowerUp() {
    powerUp = {
      x: Math.floor(Math.random() * 20) * box,
      y: Math.floor(Math.random() * 20) * box
    };
  }

  function growSnakeByThree() {
    // Add three segments to the snake
    for (let i = 0; i < 3; i++) {
      snake.push({ x: snake[snake.length - 1].x, y: snake[snake.length - 1].y });
    }
  }

  // Start the game initially
  startGame();
</script>