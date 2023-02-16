<style>
    html, body {
    background: #222;
    font-family: 'Press Start 2P', Arial, sans-serif;
    font-size: 16px;
    color: #eee;
    }

    #board {
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 600px;
    height: 400px;
    background: #222;
    border: 5px solid #eee;
    }

    #board::before {
    content: "";
    top: 0;
    left: 50%;
    height: 100%;
    width:0%;
    border-left: 5px dashed #eee;
    transform: translate(-50%, 0%);
    }

    .paddle {
    height: 80px;
    width:10px;
    background: #eee;
    }

    #paddle-1 {
    top: 160px;
    left: 20px;
    }

    #paddle-2 {
    top: 160px;
    right: 20px;
    }

    #ball {
    width: 10px;
    height: 10px;
    background: #eee;
    top: 190px;
    left: 40px;
    z-index: 1;
    }

    .score {
    font-size: 4rem;
    color: #aaa;
    transform: translate(-50%, 0%);
    top: 10px;
    }

    #score-1 {
    left: 250px;
    }

    #score-2 {
    left: 360px;
    }
</style>
<div id="board">
  <div class="paddle" id="paddle-1"></div>
  <div class="paddle" id="paddle-2"></div>
  <div id="ball"></div>
  <div class="score" id="score-1">0</div>
  <div class="score" id="score-2">0</div>
</div>
<script>
// get references to DOM elements
const board = document.getElementById('board');
const paddle1 = document.getElementById('paddle-1');
const paddle2 = document.getElementById('paddle-2');
const ball = document.getElementById('ball');
const score1 = document.getElementById('score-1');
const score2 = document.getElementById('score-2');
// initialize game variables
let ballX = 40;  // starting position of the ball on the x-axis
let ballY = 190; // starting position of the ball on the y-axis
let ballSpeedX = 5; // speed of the ball on the x-axis
let ballSpeedY = 5; // speed of the ball on the y-axis
let paddleSpeed = 10; // speed of the paddles
let scorePlayer1 = 0;
let scorePlayer2 = 0;
// define function to update the position of the paddles
function movePaddles() {
  // move paddle 1
  if (wPressed) {
    let paddle1Y = parseInt(window.getComputedStyle(paddle1).getPropertyValue('top'));
    if (paddle1Y - paddleSpeed >= 0) {
      paddle1.style.top = `${paddle1Y - paddleSpeed}px`;
    }
  }
  if (sPressed) {
    let paddle1Y = parseInt(window.getComputedStyle(paddle1).getPropertyValue('top'));
    if (paddle1Y + paddleSpeed <= board.offsetHeight - paddle1.offsetHeight) {
      paddle1.style.top = `${paddle1Y + paddleSpeed}px`;
    }
  }
  // move paddle 2
  if (upPressed) {
    let paddle2Y = parseInt(window.getComputedStyle(paddle2).getPropertyValue('top'));
    if (paddle2Y - paddleSpeed >= 0) {
      paddle2.style.top = `${paddle2Y - paddleSpeed}px`;
    }
  }
  if (downPressed) {
    let paddle2Y = parseInt(window.getComputedStyle(paddle2).getPropertyValue('top'));
    if (paddle2Y + paddleSpeed <= board.offsetHeight - paddle2.offsetHeight) {
      paddle2.style.top = `${paddle2Y + paddleSpeed}px`;
    }
  }
}
// define function to update the position of the ball
function moveBall() {
  // update position of ball
  ballX += ballSpeedX;
  ballY += ballSpeedY;
  ball.style.left = `${ballX}px`;
  ball.style.top = `${ballY}px`;
  // check for collision with top/bottom walls
  if (ballY < 0 || ballY > board.offsetHeight - ball.offsetHeight) {
    ballSpeedY = -ballSpeedY;
  }
  // check for collision with paddles
  let paddle1Y = parseInt(window.getComputedStyle(paddle1).getPropertyValue('top'));
  let paddle2Y = parseInt(window.getComputedStyle(paddle2).getPropertyValue('top'));
  let paddle1X = parseInt(window.getComputedStyle(paddle1).getPropertyValue('left')) + paddle1.offsetWidth;
  let paddle2X = parseInt(window.getComputedStyle(paddle2).getPropertyValue('left'));
  if (ballX < paddle1X && ballY > paddle1Y && ballY < paddle1Y + paddle1.offsetHeight) {
    ballSpeedX = -ballSpeedX;
  }
  if (ballX > paddle2X && ballY > paddle2Y && ballY < paddle2Y + paddle2.offsetHeight) {
    ballSpeedX = -ballSpeedX;
  // check for score and end game if a player reaches 10 points
  if (ballX < 0) {
    scorePlayer2++;
    score2.textContent = scorePlayer2;
    if (scorePlayer2 === 10) {
      alert('Player 2 wins!');
      scorePlayer1 = 0;
      score1.textContent = 0;
      scorePlayer2 = 0;
      score2.textContent = 0;
    }
    resetBall();
  }
  if (ballX > board.offsetWidth - ball.offsetWidth) {
    scorePlayer1++;
    score1.textContent = scorePlayer1;
    if (scorePlayer1 === 10) {
      alert('Player 1 wins!');
      scorePlayer1 = 0;
      score1.textContent = 0;
      scorePlayer2 = 0;
      score2.textContent = 0;
    }
    resetBall();
  }
}
// check for scoring
if (ballX < 0) {
// player 2 scores
scorePlayer2++;
score2.textContent = scorePlayer2;
resetBall();
}
if (ballX > board.offsetWidth - ball.offsetWidth) {
// player 1 scores
scorePlayer1++;
score1.textContent = scorePlayer1;
resetBall();
}
}
// define function to reset the ball to the center of the board
function resetBall() {
ballX = (board.offsetWidth - ball.offsetWidth) / 2;
ballY = (board.offsetHeight - ball.offsetHeight) / 2;
ballSpeedX = -ballSpeedX;
ball.style.left = `${ballX}px`;
ball.style.top = `${ballY}px`;
}
// add event listeners to detect when keys are pressed
let wPressed = false;
let sPressed = false;
let upPressed = false;
let downPressed = false;
document.addEventListener('keydown', function(event) {
if (event.code === 'KeyW') {
wPressed = true;
}
if (event.code === 'KeyS') {
sPressed = true;
}
if (event.code === 'ArrowUp') {
upPressed = true;
}
if (event.code === 'ArrowDown') {
downPressed = true;
}
});
document.addEventListener('keyup', function(event) {
if (event.code === 'KeyW') {
wPressed = false;
}
if (event.code === 'KeyS') {
sPressed = false;
}
if (event.code === 'ArrowUp') {
upPressed = false;
}
if (event.code === 'ArrowDown') {
downPressed = false;
}
});
// define game loop
function gameLoop() {
movePaddles();
moveBall();
}
// start game loop
setInterval(gameLoop, 20); // run game loop every 20 milliseconds
// check for ball going out of bounds and update score
function checkOutOfBounds() {
if (ballX < 0) {
scorePlayer2++;
score2.textContent = scorePlayer2;
resetBall();
}
if (ballX > board.offsetWidth - ball.offsetWidth) {
scorePlayer1++;
score1.textContent = scorePlayer1;
resetBall();
}
}
// reset ball to starting position
function resetBall() {
ballX = 40;
ballY = 190;
ballSpeedX = 5;
ballSpeedY = 5;
ball.style.left = `${ballX}px`;
ball.style.top = `${ballY}px`;
}
// define function to update game state
function update() {
movePaddles();
moveBall();
checkOutOfBounds();
}
// set up keyboard event listeners
let wPressed = false;
let sPressed = false;
let upPressed = false;
let downPressed = false;
document.addEventListener('keydown', function(event) {
if (event.code === 'KeyW') {
wPressed = true;
}
if (event.code === 'KeyS') {
sPressed = true;
}
if (event.code === 'ArrowUp') {
upPressed = true;
}
if (event.code === 'ArrowDown') {
downPressed = true;
}
});
document.addEventListener('keyup', function(event) {
if (event.code === 'KeyW') {
wPressed = false;
}
if (event.code === 'KeyS') {
sPressed = false;
}
if (event.code === 'ArrowUp') {
upPressed = false;
}
if (event.code === 'ArrowDown') {
downPressed = false;
}
});
// set up game loop
setInterval(update, 1000/60); // 60 fps
</script>
