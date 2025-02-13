<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <a href ="http://www.our quotes.com"></a>
  <title>Random Quote Generator</title>
  <style>
    body {
      font-family: 'Helvetica', Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background-color: #f0f0f0;
      position: relative;
      overflow: hidden;
      transition: background-color 0.5s ease;
    }

    .container {
      text-align: center;
      padding: 40px;
      border-radius: 15px;
      width: 90%;
      max-width: 600px;
      background-color: white;
      box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
      transition: box-shadow 0.3s ease;
    }

    .container:hover {
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
    }

    h1 {
      font-size: 32px;
      margin-bottom: 20px;
      color: #333;
    }

    .quote {
      font-size: 20px;
      margin: 30px 0;
      color: #555;
      font-style: italic;
      line-height: 1.6;
      transition: color 0.3s ease;
      position: relative;
    }

    button {
      padding: 12px 24px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 10px;
      font-size: 18px;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.3s ease;
    }

    button:hover {
      background-color: #45a049;
      transform: scale(1.1);
    }

    button:active {
      transform: scale(1);
    }

    /* Glitter particles styling */
    .glitter {
      position: absolute;
      border-radius: 50%;
      background-color: #fff;
      pointer-events: none;
      animation: glitter 1.5s ease-out infinite;
    }

    @keyframes glitter {
      0% {
        opacity: 1;
        transform: scale(1) translateY(0);
      }
      50% {
        opacity: 0.6;
        transform: scale(0.5) translateY(100px);
      }
      100% {
        opacity: 1;
        transform: scale(1) translateY(0);
      }
    }

    /* Snow effect */
    .snowflake {
      position: absolute;
      top: -10px;
      font-size: 20px;
      color: white;
      animation: snow 10s linear infinite;
    }

    @keyframes snow {
      0% {
        transform: translateY(0);
        opacity: 1;
      }
      100% {
        transform: translateY(100vh);
        opacity: 0;
      }
    }

    /* Fire effect */
    .fire {
      position: absolute;
      bottom: 10%;
      left: 50%;
      transform: translateX(-50%);
      width: 150px;
      height: 100px;
      background: linear-gradient(45deg, #ff5e62, #ff9966);
      border-radius: 50%;
      animation: fireAnimation 3s ease-in-out infinite;
      transition: transform 0.5s, background 1s ease-in-out;
    }

    @keyframes fireAnimation {
      0% {
        transform: translateX(-50%) scaleY(1);
        background: linear-gradient(45deg, #ff5e62, #ff9966);
      }
      50% {
        transform: translateX(-50%) scaleY(1.2);
        background: linear-gradient(45deg, #ff6347, #ff4500);
      }
      100% {
        transform: translateX(-50%) scaleY(1);
        background: linear-gradient(45deg, #ff5e62, #ff9966);
      }
    }

    /* Burn effect on the quote */
    .quote.burn {
      animation: burnQuote 3s forwards;
    }

    @keyframes burnQuote {
      0% {
        color: #555;
        filter: brightness(100%);
      }
      50% {
        color: #ff6347;
        filter: brightness(150%);
      }
      100% {
        color: transparent;
        filter: brightness(0%);
      }
    }

    /* Heart falling effect */
    .heart {
      position: absolute;
      font-size: 30px;
      color: red;
      animation: fall 5s linear forwards;
    }

    @keyframes fall {
      0% {
        opacity: 1;
        transform: translateY(0) rotate(0deg);
      }
      50% {
        opacity: 0.7;
        transform: translateY(50vh) rotate(180deg);
      }
      100% {
        opacity: 0;
        transform: translateY(100vh) rotate(360deg);
      }
    }

  </style>
</head>
<body>
  <div class="container">
    <h1>Random Quote Generator with Glitter, Snow, and Fire</h1>
    <p class="quote" id="quoteLabel">Click the button below to generate a quote!</p>
    <button onclick="generateQuote()">Generate Quote</button>
  </div>

  <!-- Snowflakes -->
  <div class="snowflake" style="left: 10%; animation-duration: 12s;"></div>
  <div class="snowflake" style="left: 20%; animation-duration: 15s;"></div>
  <div class="snowflake" style="left: 30%; animation-duration: 18s;"></div>
  <div class="snowflake" style="left: 40%; animation-duration: 22s;"></div>
  <div class="snowflake" style="left: 50%; animation-duration: 10s;"></div>
  <div class="snowflake" style="left: 60%; animation-duration: 14s;"></div>
  <div class="snowflake" style="left: 70%; animation-duration: 16s;"></div>
  <div class="snowflake" style="left: 80%; animation-duration: 12s;"></div>

  <!-- Fire Effect -->
  <div class="fire"></div>

  <script>
    // List of quotes
    const quotes = [
      "The only way to do great work is to love what you do. - Steve Jobs",
      "Life is 10% what happens to us and 90% how we react to it. - Charles R. Swindoll",
      "The purpose of life is not to be happy. It is to be useful, to be honorable, to be compassionate, to have it make some difference that you have lived and lived well. - Ralph Waldo Emerson",
      "In the end, we will remember not the words of our enemies, but the silence of our friends. - Martin Luther King Jr.",
      "Do not go where the path may lead, go instead where there is no path and leave a trail. - Ralph Waldo Emerson",
      "IMAGINATION LEADS THE WORLD",
      "Every autumn is a welcome of spring....... Siya"
    ];

    // Function to generate a random quote and change the background color
    function generateQuote() {
      // Select a random quote from the array
      const quote = quotes[Math.floor(Math.random() * quotes.length)];

      // Generate a random color
      const randomColor = `#${Math.floor(Math.random() * 16777215).toString(16)}`;

      // Add burning animation to the quote
      const quoteElement = document.getElementById("quoteLabel");
      quoteElement.classList.add("burn");

      // After the burning effect is complete, update the quote
      setTimeout(() => {
        quoteElement.textContent = quote;
        quoteElement.classList.remove("burn");
      }, 3000);

      // Update the background color
      document.body.style.backgroundColor = randomColor;

      // Add glitter particles
      createGlitterParticles(randomColor);

      // Trigger the heart falling effect
      createFallingHearts();
    }

    // Function to create glitter particles
    function createGlitterParticles(color) {
      const glitterCount = 30;
      const body = document.body;

      const existingGlitters = document.querySelectorAll('.glitter');
      existingGlitters.forEach(particle => particle.remove());

      for (let i = 0; i < glitterCount; i++) {
        const glitter = document.createElement('div');
        glitter.classList.add('glitter');
        glitter.style.width = `${Math.random() * 10 + 5}px`;
        glitter.style.height = glitter.style.width;
        glitter.style.backgroundColor = color;
        glitter.style.left = `${Math.random() * window.innerWidth}px`;
        glitter.style.top = `${Math.random() * window.innerHeight}px`;

        body.appendChild(glitter);
        glitter.style.animationDuration = `${Math.random() * 1.5 + 1}s`;
        glitter.style.animationDelay = `${Math.random() * 2}s`;
      }
    }

    // Function to create falling hearts
    function createFallingHearts() {
      const heartCount = 10; // Number of hearts
      const body = document.body;

      for (let i = 0; i < heartCount; i++) {
        const heart = document.createElement('div');
        heart.classList.add('heart');
        heart.textContent = '❤️';
        heart.style.left = `${Math.random() * window.innerWidth}px`; // Random position
        body.appendChild(heart);
      }
    }
  </script>
</body>
</html>
