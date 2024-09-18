---
layout: page 
title: Formula1 Quiz
search_exclude: true
permalink: /games/formulagame/
description: How much do you know about F1?
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