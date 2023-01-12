<!DOCTYPE html>
<html>

<head>
    <style>
        /* styles for the game board */
        #board {
            width: 400px;
            height: 400px;
            border: 1px solid black;
        }
        /* styles for each cell */
        .cell {
            width: 20px;
            height: 20px;
            border: 1px solid black;
        }
        /* styles for the snake */
        .snake {
            background-color: green;
        }
        /* styles for the food */
        .food {
            background-color: red;
        }
    </style>
</head>

<body>
    <div id="board"></div>
    <div id="score">Score: <span id="score-value">0</span></div>
    <script>
        // global variables
        const board = document.getElementById("board");
        const scoreValue = document.getElementById("score-value");
        let snake = [[2, 0], [1, 0], [0, 0]];
        let food = [3, 3];
        let direction = "right";
        let score = 0;
        // creates the game board
        function createBoard() {
            for (let i = 0; i < 20; i++) {
                for (let j = 0; j < 20; j++) {
                    let cell = document.createElement("div");
                    cell.classList.add("cell");
                    cell.setAttribute("id", i + "-" + j);
                    board.appendChild(cell);
                }
            }
        }
        // renders the snake and food on the board
        function render() {
            snake.forEach(([x, y]) => {
                let cell = document.getElementById(x + "-" + y);
                cell.classList.add("snake");
            });
            let foodCell = document.getElementById(food[0] + "-" + food[1]);
            foodCell.classList.add("food");
        }
        // moves the snake in the specified direction
        function move() {
            let head = snake[snake.length - 1];
            let newHead = [...head];
            switch (direction) {
                case "right":
                    newHead[1]++;
                    break;
                case "left":
                    newHead[1]--;
                    break;
                case "up":
                    newHead[0]--;
                    break;
                case "down":
                    newHead[0]++;
                    break;
            }
            snake.push(newHead);
            let tail = snake.shift();
            let tailCell = document.getElementById(tail[0] + "-" + tail[1]);
            tailCell.classList.remove("snake");
            }
            // check if the snake has collided with the food
            let snakeHead = snake[snake.length - 1];
            if (snakeHead[0] === food[0] && snakeHead[1] === food[1]) {
                food = generateFood();
                score++;
                score
                }
