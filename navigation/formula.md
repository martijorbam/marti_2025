---
layout: page 
title: Formula 1
search_exclude: true
permalink: /formula1/
description: The Pinnacle of Motorsports
---

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Move F1 Car</title>
  <style>
    body {
      margin: 0;
      background-color: #f0f0f0; /* Light gray background */
      position: relative; /* Allows absolute positioning within the body */
      height: 100vh; /* Full viewport height */
    }

    .car {
      position: fixed;
      top: 50%; /* Center vertically */
      left: 20%; 
      width: 100px; /* Adjust size as needed */
      transform: translate(-50%, -50%); /* Adjust positioning to center the image */
      transition: transform 0.1s; /* Smooth movement */
    }
  </style>
</head>
<body>

  <!-- F1 Car Image -->
  <img src="../images/test_f1-removebg-preview.png" alt="F1 Car" class="car" id="car">

  <script>
    const car = document.getElementById('car');
    let position = 0;

    function moveCar(event) {
      const step = 10; // Number of pixels to move per key press
      if (event.key === 'ArrowRight') {
        position += step;
      } else if (event.key === 'ArrowLeft') {
        position -= step;
      }
      car.style.transform = `translate(-50%, -50%) translateX(${position}px)`;
    }

    document.addEventListener('keydown', moveCar);
  </script>

</body>

As the highest class of international racing for single-seater formula racing cars, Formula 1 is the pinnacle of motorsport and the world’s most prestigious motor racing competition. There really is nothing like it.


It’s a team sport (it needs to be to change all 4 tyres on a car in under 2 seconds!), but the drivers are more like fighter pilots than sportspeople. Battling extreme g-forces, making daring decisions in the blink of an eye – and at 370km/h. To be the best, F1 drivers push themselves – and their incredibly innovative machines – to the very limit.


Drivers compete for the esteemed F1 Drivers’ Championship, while the teams fight for the F1 Constructors’ Championship and prize money based on their position at the end of the season.


Each race is known as a Grand Prix, and they’re held in incredible locations around the world. 2024 will feature a record-breaking number of Grand Prix events, with 24 races set to take place this season.

<head>
  <h2> My favourite drivers of all time </h2>
</head>
(I haven't been able so watch them all live since I wasn't born yet but I've watched video recordings of their past races and achievements)
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    .image-container {
      display: flex; 
      justify-content: space-around; 
    }

    .image-box {
      text-align: center;
    }

    .image-box img {
      width: 150px; 
      height: auto; 
      margin-bottom: 5px; 
    }

    .image-box p {
      font-size: 18px; 
      color: #333; 
    }
  </style>
</head>
<body>

  <div class="image-container">
    <div class="image-box">
      <img src="../images/michael_schumacher.webp" alt="Image 1">
      <p>Michael Schumacher</p>
    </div>
    <div class="image-box">
      <img src="../images/ayrton-senna-1.jpg" alt="Image 2">
      <p>Ayrton Senna</p>
    </div>
    <div class="image-box">
      <img src="../images/f1_1.jpg" alt="Image 3">
      <p>Fernando Alonso</p>
    </div>
  </div>

</body>

Source:
<a href="https://www.formula1.com/en/latest/article/drivers-teams-cars-circuits-and-more-everything-you-need-to-know-about.7iQfL3Rivf1comzdqV5jwc">What You Need to Know About F1</a>