<!-- <!DOCTYPE html> -->
<html>
<head>
  <meta charset="UTF-8">
  <title>Pong Game</title>
  <style>
    #pong-container {
      position: absolute;
      left: 50%;
      transform: translate(-50%, +60%);
      width: 600px;
      height: 400px;
    }
    canvas {
      width: 100%;
      height: 100%;
      background: #222;
      border: 5px solid #eee;
    }
    canvas:focus{
      outline: none;
    }
    .score {
      font-size: 4rem;
      color: #aaa;
      position: absolute;
      top: 10px;
    }
    #score1 {
      left: 150px;
    }
    #score2 {
      left: 450px;
    }
    #start_game_button {
      height: 40px;
      width: 100px;
    }
    .player_number{
      font-size: 2rem;
      /* background-color: #02fa51d7; */
      color: #968796;
    }
    #player2{
      transform: translate(+40%, -1000%);
    }
    #player1{
      transform: translate(-35%, -1100%);
    }
  </style>
</head>
<body>
  <div class="container bg-secondary" style="text-align:center;">
        <!-- Main Menu -->
        <div id="start_menu" class="py-4 text-light">
            <p>Welcome to Pong, press <span style="background-color: #d4ca1c; color: #000000">start</span> to begin</p>
            <button id="start_game_button" onclick="gameLoop()">Start</button>
        </div>
        <!-- Game Over -->
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press the <span style="background-color: #d4ca1c; color: #000000">refresh</span> button to try again</p>
            <p><span style="background-color: #FFFFFF; color: #000000">Your username must have exactly 3 characters in order to log your score.</span></p>
            <form action="javascript:create_user()">
                <p><label>
                    Username for Player 1:
                    <input type="text" name="user1" id="user1" placeholder="Must have 3 characters" required>
                </label></p>
                <p><label>
                    Username for Player 2:
                    <input type="text" name="user2" id="user2" placeholder="Must have 3 characters" required>
                </label></p>
                <p><label>
                    Score for Player 1:
                    <span name="scoring_1" id="scoring_1">0</span>
                </label></p>
                <p><label>
                    Score for Player 2:
                    <span name="scoring_2" id="scoring_2">0</span>
                </label></p>
                <p><label>
                    Result:
                    <span name="gameResult" id="gameResult">Result is displayed here.</span>
                </label></p>
                <!-- <p><label>
                    Date of Score:
                    <span type="date" name="dos" id="dos"></span>
                </label></p> -->
                <p>
                    <button onclick="alert('Your score has been posted!')">Submit</button>
                </p>
            </form>
            <!-- <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a> -->
        </div>
        <!-- Play Screen -->
        <div id="empty-space"></div>
        <div id="pong-container" style="text-align:center;">
          <canvas id="canvas"></canvas>
          <div class="player_number" id="player2">Player 2</div>
          <div class="player_number" id="player1">Player 1</div>
          <div class="score" id="score1">0</div>
          <div class="score" id="score2">0</div>
          <!-- <button id="restartButton">Restart Game</button> -->
        </div>
  </div>

<script>
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');
  const ballSize = 5;
  const PONG_GAMEOVER = document.getElementById("gameover");
  const PONG_START = document.getElementById("start_menu");
  // const button_new_game = document.getElementById("new_game");
  // Set the canvas width and height
  canvas.width = 600;
  canvas.height = 400;
  PONG_GAMEOVER.style.display= "none";
  PONG_START.style.display="block";
  // Set the initial ball position and velocity
  let ballX, ballY, ballSpeedX, ballSpeedY;
  resetBall();

  // let gameState = 0;

  // Set the initial paddle positions
  let paddle1Y = canvas.height / 2 - 40;
  let paddle2Y = canvas.height / 2 - 40;

  // Set the paddle dimensions
  const paddleWidth = 10;
  const paddleHeight = 80;

  // Set the initial scores
  let scorePlayer1 = 0;
  let scorePlayer2 = 0;

  // Define the score limit
  const scoreLimit = 5;

  // Get the game result
  const gameRes = document.getElementById('gameResult');
  // Get the score elements
  const score1 = document.getElementById('score1');
  const score2 = document.getElementById('score2');
  const score1_display = document.getElementById('scoring_1');
  const score2_display = document.getElementById('scoring_2');
  // Restart
  // const restartButton = document.getElementById('restartButton');
  // restartButton.addEventListener('click', restart);

  // function gameStart() {
  //   if(gameState ===0){
  //     gameLoop();
  //   }else{
  //     PONG_GAMEOVER.style.display= "block";
  //     resetBallNoSpeed();
  //   }
  // }

  // Draw the paddles and ball on the canvas
  function drawPaddlesAndBall() {
    // Clear the canvas
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    // Draw the paddles
    ctx.fillStyle = '#fff';
    ctx.fillRect(0 + 10, paddle1Y, paddleWidth, paddleHeight);
    ctx.fillRect(canvas.width - paddleWidth - 10, paddle2Y, paddleWidth, paddleHeight);

    // Draw the ball
    ctx.beginPath();
    ctx.fillStyle = '#fff';
    ctx.arc(ballX, ballY, ballSize, 0, Math.PI * 2);
    ctx.fill();
  }


  // Update the ball position and check for collisions
  function moveBall() {
    ballX += ballSpeedX;
    ballY += ballSpeedY;
    // Check for collisions with the top and bottom walls
    if (ballY - ballSize < 0 || ballY + ballSize > canvas.height) {
      ballSpeedY = -ballSpeedY;
    }
    // Check for collisions with the paddles
    if (ballX - ballSize < paddleWidth + 10 && ballY > paddle1Y && ballY < paddle1Y + paddleHeight) {
      ballSpeedX = -ballSpeedX;
      let deltaY = ballY - (paddle1Y + paddleHeight / 2);
      ballSpeedY = deltaY * 0.35;
    } else if (ballX + ballSize > canvas.width - paddleWidth - 10 && ballY > paddle2Y && ballY < paddle2Y + paddleHeight) {
      ballSpeedX = -ballSpeedX;
      let deltaY = ballY - (paddle2Y + paddleHeight / 2);
      ballSpeedY = deltaY * 0.35;
    }

    // Check for a goal scored by player 1
    if (ballX - ballSize < 0) {
      scorePlayer2 = scorePlayer2 + 1;
      resetBall();
    }

    // Check for a goal scored by player 2
    if (ballX + ballSize > canvas.width) {
      scorePlayer1 = scorePlayer1 + 1;
      resetBall();
    }
  }

  // Reset the ball to the center of the canvas
  function resetBall() {
    ballX = canvas.width / 2;
    ballY = canvas.height / 2;
    ballSpeedX = Math.random() < 0.5 ? -5 : 5;
    ballSpeedY = Math.random() * 4 - 2;
  }
  function resetBallNoSpeed() {
    ballX = canvas.width / 2;
    ballY = canvas.height / 2;
  }

  // Update the paddle positions based on the user input
  function movePaddles() {
    // Move the first paddle (player 1)
    if (wPressed) {
    paddle1Y -= 5;
    } else if (sPressed) {
    paddle1Y += 5;
    }
    // Move the second paddle (player 2)
    if (upPressed) {
      paddle2Y -= 5;
    } else if (downPressed) {
      paddle2Y += 5;
    }

    // Make sure the paddles don't move off the screen
    if (paddle1Y < 0) {
      paddle1Y = 0;
    } else if (paddle1Y + paddleHeight > canvas.height) {
      paddle1Y = canvas.height - paddleHeight;
    }

    if (paddle2Y < 0) {
      paddle2Y = 0;
    } else if (paddle2Y + paddleHeight > canvas.height) {
      paddle2Y = canvas.height - paddleHeight;
    }
  }

  // Main game loop
  function gameLoop() {
    // PONG_GAMEOVER.style.display= "none";
    // gameStart();
    drawPaddlesAndBall();
    moveBall();
    movePaddles();
    scoreTracker();
    checkGameEnd();
    // // Update the score display
    // score1.textContent = scorePlayer1;
    // score2.textContent = scorePlayer2;
    requestAnimationFrame(gameLoop);
    // console.log(score1);
    // console.log(score2);
  }

  // Detect user input
  let wPressed = false;
  let sPressed = false;
  let upPressed = false;
  let downPressed = false;

  document.addEventListener('keydown', (event) => {
  if (event.key === 'w') {
  wPressed = true;
  } else if (event.key === 's') {
  sPressed = true;
  } else if (event.key === 'ArrowUp') {
  upPressed = true;
  } else if (event.key === 'ArrowDown') {
  downPressed = true;
  }
  });

  document.addEventListener('keyup', (event) => {
  if (event.key === 'w') {
  wPressed = false;
  } else if (event.key === 's') {
  sPressed = false;resetBallNoSpeed
  } else if (event.key === 'ArrowUp') {
  upPressed = false;
  } else if (event.key === 'ArrowDown') {
  downPressed = false;
  }
  });



  function restart() {
    // Reset the scores
    scorePlayer1 = 0;
    scorePlayer2 = 0;

    // Reset the ball and paddles
    resetBallNoSpeed();
    paddle1Y = canvas.height / 2 - 40;
    paddle2Y = canvas.height / 2 - 40;
  }

  // Check for the game end
  function checkGameEnd() {
    // Check if player 1 has won
    if (scorePlayer1 >= scoreLimit) {
      PONG_GAMEOVER.style.display= "block";
      PONG_START.style.display="none";
      gameRes.innerHTML = "Player 1 wins!";
      requestAnimationFrame();
      // gameState = 1;
    }
    // Check if player 2 has won
    if (scorePlayer2 == scoreLimit) {
      PONG_GAMEOVER.style.display= "block";
      PONG_START.style.display="none";
      gameRes.innerHTML = "Player 2 wins!";
      requestAnimationFrame();
      // gameState = 1;
    }
    }
    
    function scoreTracker(){
      score1.innerHTML = String(scorePlayer1);
      score2.innerHTML = String(scorePlayer2);
      score1_display.innerHTML = String(scorePlayer1);
      score2_display.innerHTML = String(scorePlayer2);
    }
    
</script>

</body>
</html> 
