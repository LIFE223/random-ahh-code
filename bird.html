<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Flappy Bird Math Challenge</title>
  <style>
    /* Basic reset */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #e0f7fa;
      overflow: hidden;
    }

    #gameContainer {
      position: relative;
      width: 400px;
      height: 600px;
      margin: 40px auto;
      border: 2px solid #555;
      background-color: #a3d5ff;
    }

    /* Canvas styling */
    #gameCanvas {
      background: #70c5ce;
      display: block;
    }

    /* Overlay for start screen */
    #overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 2;
    }

    #startButton {
      padding: 15px 30px;
      font-size: 18px;
      background-color: #ffeb3b;
      border: none;
      cursor: pointer;
      border-radius: 8px;
    }

    /* Settings button at top right */
    #settingsButton {
      position: absolute;
      top: 10px;
      right: 10px;
      padding: 10px 15px;
      font-size: 14px;
      background-color: #ffffffcc;
      border: 1px solid #888;
      cursor: pointer;
      border-radius: 4px;
      z-index: 3;
    }

    /* Generic modal styles */
    .modal {
      display: none;
      position: fixed;
      z-index: 10;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      overflow: auto;
      background-color: rgba(0,0,0,0.6);
    }

    .modal-content {
      background-color: #fefefe;
      margin: 10% auto;
      padding: 20px;
      border: 1px solid #888;
      width: 300px;
      border-radius: 8px;
      text-align: center;
    }

    .close {
      color: #aaa;
      float: right;
      font-size: 28px;
      font-weight: bold;
      cursor: pointer;
    }
    
    .close:hover {
      color: black;
    }

    /* Spacing for modal inputs */
    label, select, input, button {
      margin: 10px 0;
      display: block;
      width: 100%;
    }

    input[type="text"] {
      padding: 8px;
      font-size: 16px;
    }

    button {
      padding: 10px;
      font-size: 16px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div id="gameContainer">
    <canvas id="gameCanvas" width="400" height="600"></canvas>
    <!-- Start overlay -->
    <div id="overlay">
      <button id="startButton">Start</button>
    </div>
    <!-- Settings button -->
    <button id="settingsButton">Settings</button>
  </div>

  <!-- Settings Modal -->
  <div id="settingsModal" class="modal">
    <div class="modal-content">
      <span class="close">&times;</span>
      <h2>Settings</h2>
      <label for="difficulty">Math Difficulty:</label>
      <select id="difficulty">
        <option value="1">Level 1 (± up to 10)</option>
        <option value="2">Level 2 (+, -, ×, ÷. Up to 100 for + & -; 10 for × & ÷)</option>
        <option value="3">Level 3 (+, -, ×, ÷. Up to 1000 for + & -; 100 for × & ÷)</option>
      </select>
      <label>Choose Bird Color:</label>
      <input type="radio" name="birdColor" value="red" checked> Red
      <input type="radio" name="birdColor" value="blue"> Blue
      <input type="radio" name="birdColor" value="yellow"> Yellow
      <button id="saveSettings">Save</button>
    </div>
  </div>

  <!-- Math Problem Modal (shown on collision) -->
  <div id="mathModal" class="modal">
    <div class="modal-content">
      <h2>Solve to Continue</h2>
      <p id="mathQuestion"></p>
      <input type="text" id="mathAnswer" placeholder="Your Answer">
      <button id="submitMath">Submit</button>
      <p id="mathFeedback" style="color: red;"></p>
    </div>
  </div>

  <script>
    // GET DOM elements
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");
    const startButton = document.getElementById("startButton");
    const overlay = document.getElementById("overlay");
    const settingsButton = document.getElementById("settingsButton");
    const settingsModal = document.getElementById("settingsModal");
    const closeSettings = document.querySelector("#settingsModal .close");
    const saveSettingsButton = document.getElementById("saveSettings");
    const mathModal = document.getElementById("mathModal");
    const mathQuestionElem = document.getElementById("mathQuestion");
    const mathAnswerInput = document.getElementById("mathAnswer");
    const submitMathButton = document.getElementById("submitMath");
    const mathFeedback = document.getElementById("mathFeedback");

    // Game settings
    let difficulty = 1;      // default difficulty level
    let birdColor = "red";   // default bird color

    // Game state variables
    let gameStarted = false;
    let gamePaused = false;
    let score = 0;
    let startTime;
    const maxGameTime = 30 * 60 * 1000; // 30 minutes in ms
    let animationFrameId;
    let lastPipeTime = 0;
    const pipeInterval = 1500;  // milliseconds between pipes

    // Bird properties
    let bird = {
      x: 80,
      y: canvas.height / 2,
      radius: 12,
      velocity: 0,
      gravity: 0.6,
      jumpStrength: -10
    };

    // Pipe properties and storage
    let pipes = [];
    const pipeWidth = 50;
    const pipeGap = 120;  // vertical gap between top & bottom pipes
    const pipeSpeed = 2;

    // Listen for key presses and clicks to make the bird jump
    document.addEventListener("keydown", function(e) {
      if (e.code === "Space" && gameStarted && !gamePaused) {
        bird.velocity = bird.jumpStrength;
      }
    });
    canvas.addEventListener("click", function() {
      if (gameStarted && !gamePaused) {
        bird.velocity = bird.jumpStrength;
      }
    });

    // Start game function
    function startGame() {
      gameStarted = true;
      gamePaused = false;
      overlay.style.display = "none";

      // Reset state
      bird.y = canvas.height / 2;
      bird.velocity = 0;
      pipes = [];
      score = 0;
      startTime = Date.now();
      lastPipeTime = Date.now();

      // Begin game loop
      gameLoop();
    }

    // Main game loop using requestAnimationFrame
    function gameLoop() {
      if (!gameStarted || gamePaused) return;

      const currentTime = Date.now();
      const elapsedTime = currentTime - startTime;

      // Automatically end game at 30 minutes
      if (elapsedTime > maxGameTime) {
        endGame("Time's up! Final Score: " + score);
        return;
      }

      // Clear canvas for the new frame
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // Update bird physics
      bird.velocity += bird.gravity;
      bird.y += bird.velocity;

      // Draw bird (a simple colored circle)
      ctx.beginPath();
      ctx.fillStyle = birdColor;
      ctx.arc(bird.x, bird.y, bird.radius, 0, Math.PI * 2);
      ctx.fill();

      // Generate new pipes at regular intervals
      if (currentTime - lastPipeTime > pipeInterval) {
        // Determine a random gap position
        const pipeTopHeight = Math.random() * (canvas.height - pipeGap - 100) + 50;
        pipes.push({
          x: canvas.width,
          top: pipeTopHeight,
          bottom: pipeTopHeight + pipeGap,
          scored: false
        });
        lastPipeTime = currentTime;
      }

      // Update and draw pipes
      for (let i = 0; i < pipes.length; i++) {
        const p = pipes[i];
        p.x -= pipeSpeed;

        // Draw top pipe
        ctx.fillStyle = "green";
        ctx.fillRect(p.x, 0, pipeWidth, p.top);
        // Draw bottom pipe
        ctx.fillRect(p.x, p.bottom, pipeWidth, canvas.height - p.bottom);

        // Increase score when the bird passes a pipe
        if (!p.scored && p.x + pipeWidth < bird.x) {
          score++;
          p.scored = true;
        }

        // Check for collision with pipes
        if (
          bird.x + bird.radius > p.x &&
          bird.x - bird.radius < p.x + pipeWidth &&
          (bird.y - bird.radius < p.top || bird.y + bird.radius > p.bottom)
        ) {
          triggerMathChallenge();
          return; // stop loop until answer is provided
        }
      }

      // Check if bird collides with the floor or ceiling
      if (bird.y + bird.radius >= canvas.height || bird.y - bird.radius <= 0) {
        triggerMathChallenge();
        return;
      }

      // Draw the current score
      ctx.fillStyle = "black";
      ctx.font = "20px Arial";
      ctx.fillText("Score: " + score, 10, 30);

      animationFrameId = requestAnimationFrame(gameLoop);
    }

    // End the game and show an alert
    function endGame(message) {
      gameStarted = false;
      gamePaused = true;
      cancelAnimationFrame(animationFrameId);
      alert(message);
      location.reload();
    }

    // When a collision is detected, pause and show math challenge modal
    let currentProblem; // Stores the current math problem for checking
    function triggerMathChallenge() {
      gamePaused = true;
      generateMathProblem();
      mathModal.style.display = "block";
    }

    // Generate a math problem based on the selected difficulty
    function generateMathProblem() {
      let num1, num2, operator, answer;
      
      if (parseInt(difficulty) === 1) {
        // Level 1: addition or subtraction up to 10
        num1 = Math.floor(Math.random() * 10) + 1;
        num2 = Math.floor(Math.random() * 10) + 1;
        operator = Math.random() < 0.5 ? "+" : "-";
        answer = operator === "+" ? num1 + num2 : num1 - num2;
      } else if (parseInt(difficulty) === 2) {
        // Level 2: either addition/subtraction (up to 100) or multiplication/division (up to 10)
        if (Math.random() < 0.5) {
          num1 = Math.floor(Math.random() * 100) + 1;
          num2 = Math.floor(Math.random() * 100) + 1;
          operator = Math.random() < 0.5 ? "+" : "-";
          answer = operator === "+" ? num1 + num2 : num1 - num2;
        } else {
          if (Math.random() < 0.5) {
            operator = "*";
            num1 = Math.floor(Math.random() * 10) + 1;
            num2 = Math.floor(Math.random() * 10) + 1;
            answer = num1 * num2;
          } else {
            operator = "/";
            num2 = Math.floor(Math.random() * 9) + 1;
            answer = Math.floor(Math.random() * 10) + 1;
            num1 = num2 * answer;
          }
        }
      } else if (parseInt(difficulty) === 3) {
        // Level 3: either addition/subtraction (up to 1000) or multiplication/division (up to 100)
        if (Math.random() < 0.5) {
          num1 = Math.floor(Math.random() * 1000) + 1;
          num2 = Math.floor(Math.random() * 1000) + 1;
          operator = Math.random() < 0.5 ? "+" : "-";
          answer = operator === "+" ? num1 + num2 : num1 - num2;
        } else {
          if (Math.random() < 0.5) {
            operator = "*";
            num1 = Math.floor(Math.random() * 100) + 1;
            num2 = Math.floor(Math.random() * 100) + 1;
            answer = num1 * num2;
          } else {
            operator = "/";
            num2 = Math.floor(Math.random() * 99) + 1;
            answer = Math.floor(Math.random() * 100) + 1;
            num1 = num2 * answer;
          }
        }
      }
      
      currentProblem = { num1, num2, operator, answer };
      mathQuestionElem.textContent = `What is ${num1} ${operator} ${num2}?`;
      mathAnswerInput.value = "";
      mathFeedback.textContent = "";
    }

    // Check the answer from the math modal
    submitMathButton.addEventListener("click", function() {
      const userAnswer = parseFloat(mathAnswerInput.value);
      if (userAnswer === currentProblem.answer) {
        mathModal.style.display = "none";
        // Reset the bird's position to avoid immediate re–collision
        bird.y = canvas.height / 2;
        bird.velocity = 0;
        gamePaused = false;
        gameLoop();
      } else {
        mathFeedback.textContent = "Incorrect answer. Try again.";
      }
    });

    // Settings Modal Event Handlers
    settingsButton.addEventListener("click", function() {
      settingsModal.style.display = "block";
    });
    
    closeSettings.addEventListener("click", function() {
      settingsModal.style.display = "none";
    });
    
    saveSettingsButton.addEventListener("click", function() {
      difficulty = document.getElementById("difficulty").value;
      const radios = document.getElementsByName("birdColor");
      for (let radio of radios) {
        if (radio.checked) {
          birdColor = radio.value;
          break;
        }
      }
      settingsModal.style.display = "none";
    });
    
    // Optional: Click outside modal to close the settings modal
    window.addEventListener("click", function(event) {
      if (event.target === settingsModal) {
        settingsModal.style.display = "none";
      }
      // Note: the math modal remains open until an answer is submitted.
    });

    // Start the game when the user clicks the Start button
    startButton.addEventListener("click", startGame);
  </script>
</body>
</html>
