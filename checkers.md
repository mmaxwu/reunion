<div class="s-panel">
  <div id="board" class="board">
  </div>
  <div class="s-ui">
    <button name="btnnextmove">Next move</button>
    <button name="btnreset">Reset</button>
    <label>
      <input type="checkbox" name="autoplay">
      <span>Autoplay</span>
    </label>
    <hr>
    <label>
      "AI" level
      <select name="selectailevel">
        <option value="3" selected>Beginner</option>
        <option value="6">Intermediate</option>
        <option value="8">Expert</option>
        <option value="9">Mr. Slow</option>
      </select>
    </label>
    <label>
      History
      <select name="selecthistory" multiple>
      </select>
    </label>
  </div>
</div>

<style>

  html {
    font-size: 16px;
  }
  html,
  body,
  div {
    margin: 0;
    padding: 0;
  }
  body {
    width: 100%;
    text-align: center;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: center;
  }
  .board {
    display: block;
    position: relative;
    margin: 1rem;
    padding: 1rem;
    width: 250px;
    height: 250px;
    background: #fff;
    white-space: normal;
    font-family: monospace;
    box-sizing: border-box;
    font-size: 0;
  }
  .s-panel {
    display: flex;
    justify-content: flex-start;
    align-items: stretch;
    width: 100%;
    height: 100%;
  }
  .s-ui {
    display: block;
    background: #808080;
    width: 300px;
    height: auto;
    margin: 1rem 0;
    padding: 1rem;
    box-sizing: border-box;
  }
  .s-ui button {
    display: inline-block;
    width: 100%;
    box-sizing: border-box;
    margin: 0 auto 0.6rem;
    padding: 0.5rem 1.5rem;
    font-size: 1.5rem;
    cursor: pointer;
  }
  .s-ui select {
    display: inline-block;
    width: 100%;
    box-sizing: border-box;
    margin: 0 auto 0.6rem;
    padding: 0.5rem 1.5rem;
    font-size: 1.5rem;
    cursor: pointer;
  }
  .s-ui select option {
    font-size: 1rem;
  }
  label {
    display: block;
    position: relative;
    width: 100%;
    margin: 0.5rem auto;
    height: auto;
    padding: 0;
    font-size: 1.75rem;
    text-align: left;
    
    > span {
      padding-left: .5rem;
    }
  }
  label input[type="checkbox"] {
    position: relative;
    display: inline-block;
    width: 20px;
    height: 20px;
    background: rgb(255, 255, 255);
  }

  .piece {
    display: inline-block;
    position: relative;
    border: 1px solid #fff;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .piece.possible-move {
    border: 4px solid #00ff00;
    cursor: pointer;
  }
  /*.piece.empty { background: rgb(127,127,127); }*/
  .piece.light {
    background: rgb(247, 220, 220);
  }
  .piece.dark {
    background: rgb(130, 79, 79);  
  }
  .piece.man::after {
    content: "";
    display: block;
    margin: 0 auto; 
    padding: 0;
    width: 30%;
    height: 30%;
    background: rgba(196, 65, 65, .5);
    border-radius: 50%;
    position: absolute;
    left: 50%;
    top: 50%;  
    transform: translateX(-50%) translateY(-50%);
    z-index: 2;
  }
  .piece.king::after {
    content: "K";
    display: block;
    margin: 0 auto;
    padding: 0;
    width: auto;
    height: auto;
    color: #fff;
    font-size: 16px;
    font-weight: 600;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translateX(-50%) translateY(-50%);
    z-index: 2;
  }
  .piece.black {
  }
  .piece.black::before {
    content: "";
    display: block;
    margin: 0 auto;
    padding: 0;
    width: 80%;
    height: 80%;
    border-radius: 50%;
    background: rgb(25, 25, 25);
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translateX(-50%) translateY(-50%);
    z-index: 1;
  }
  .piece.black.king::after {
    color: #fff;
  }
  .piece.red {
  }
  .piece.red::before {
    content: "";
    display: block;
    margin: 0 auto;
    padding: 0;
    width: 80%;
    height: 80%;
    border-radius: 50%;
    background: rgb(235, 235, 235);
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translateX(-50%) translateY(-50%);
    z-index: 1;
  }
  .piece.red.king::after {
    color: #FF0000;
  }
  .piece.half-highlight {
    border-color: rgb(117, 247, 167);
    background-color: rgb(48, 156, 40);
  }
  .piece.highlight {
    border-color: rgb(165, 255, 199);
    background-color: rgb(113, 251, 103);
  }
  hr {
    display: block;
    width: 100%; height: 1px;
    background: rgba(0,0,0,.2);
    border: none;
    margin: 1rem auto .75rem;
  } 
  select {
    width: 100%; height: auto;
    padding: .25rem 0; 
    margin: 1rem auto 1rem;
    
    option {
      padding: .5rem .5rem;
      font-size: 1rem;
    } 
  }
  select[multiple] {
    max-height: 200px;
    
    option {
      padding: .5rem .5rem;
      font-size: 1rem;
    }
  }
</style>
<script>
/**
 * A simple implementation of the game Checkers. 
 *
 * I wanted to test my ability to write such primitive logic from scratch. 
 * Used alpha-beta pruning optimization for the classic minimax algorithm. 
 * Didn't check all possible cases so there may be bugs.
 *
 * @version 0.2.5
 * @author Denis Khakimov <denisdude@gmail.com>
 */ 

const BASE = 8;
const root = document.getElementById("board");
let MINIMAX_DEPTH = 3;
const PAUSE_BEFORE_CPU_MOVE = 750
let AUTOPLAY = false
let board = null;
let currentMoves = [];
let history = [];
let currentPlayer = null;

const init = (event) => {
  currentPlayer = Player.Red;
  updateUI();
  reset();
};
document.addEventListener("DOMContentLoaded", init);

// UI -- begin
const updateUI = () => {
  if (currentPlayer == Player.Red) btnnextmove.setAttribute("disabled", true);
  else if (currentPlayer == Player.Black)
    btnnextmove.removeAttribute("disabled");
  
  // update history select
  selecthistory.innerHTML = ''
  const options = history.map((item, index) => {
    const option = document.createElement('option');
    option.value = index;
    option.innerHTML = `Step ${index + 1}`;
    return option;
  });
  options.reverse().forEach((option) => {
    selecthistory.appendChild(option);
  });
};
// We need to hangle all the clicks on the page.
document.addEventListener("click", (event) => {
  const target = event.target;

  // finish the move
  if (
    target.tagName == "SPAN" &&
    target.classList.contains("highlight") &&
    target.classList.contains("empty")
  ) {
    let index = target.getAttribute("data-move-index");
    const move = currentMoves[index];
    history.push({ player: currentPlayer, move, board: new Board([...board.state], currentPlayer, BASE) });
    board = board.move(move);
    render(root, board);

    detectWinner();

    currentPlayer = Player.opposite(currentPlayer);
    showPossibleMoves();
    updateUI();
    
    // click autoplay button after player's move
    if (AUTOPLAY) {
      setTimeout(() => {
        btnnextmove.click();
      }, 500); // immediate computer's move looks frightening, so I added a pause
    }

    return;
  }

  // start the move
  if (
    target.tagName == "SPAN" &&
    target.classList.contains("piece") &&
    (target.classList.contains("man") || target.classList.contains("king"))
  ) {
    // remove highlighting
    const cells = document.querySelectorAll(".piece");
    cells.forEach((el) => {
      el.classList.remove("highlight", "half-highlight");
      el.removeAttribute("data-move-index");
    }, this);
    // add highlight to the selected cell
    target.classList.add("highlight");

    let x = parseInt(target.getAttribute("data-x"));
    let y = parseInt(target.getAttribute("data-y"));
    const moves = possibleMoves(board.index(x, y));
    currentMoves = [];
    highlightMoves(moves);

    return;
  }
});
// next computer's move button
const btnnextmove = document.querySelector("button[name=btnnextmove]");
btnnextmove.addEventListener("click", (e) => {
  btnnextmove.setAttribute('disabled', true);
  const move = bestMove(board, currentPlayer, MINIMAX_DEPTH);
  
  highlightMoves([move]); // show computer's move
  
  setTimeout(() => {
    history.push({ player: currentPlayer, move, board: new Board([...board.state], currentPlayer, BASE) });
    board = board.move(move);
    render(root, board);

    detectWinner();

    currentPlayer = Player.opposite(currentPlayer);
    showPossibleMoves();
    updateUI();
  }, PAUSE_BEFORE_CPU_MOVE);
});
// reset button
const btnreset = document.querySelector("button[name=btnreset]");
btnreset.addEventListener("click", (e) => {
  reset();
});
// autoplay checkbox
const autoplay = document.querySelector('input[name=autoplay]')
autoplay.addEventListener('change', (e) => {
  AUTOPLAY = e.target.checked;
});
// load a step from the history
const selecthistory = document.querySelector('select[name=selecthistory]')
selecthistory.addEventListener('change', (e) => {
  const moveIndex = parseInt(e.target.value);
  const state = history[moveIndex];
  // history = history.slice(0, moveIndex);
  board = state.board;
  currentPlayer = state.player;
  if (currentPlayer == Player.Black) {
    btnnextmove.removeAttribute("disabled");
    btnnextmove.click();
  }
  render(root, board);
});
// level of "AI"
const selectailevel = document.querySelector('select[name=selectailevel]');
selectailevel.addEventListener('change', (e) => {
  MINIMAX_DEPTH = parseInt(e.target.value);
  //reset();
});

// UI -- end

const reset = () => {
  currentPlayer = Player.Red;
  board = new Board(new Array(BASE * BASE).fill(Piece.Empty), currentPlayer, BASE);

  board.set(1, 0, Piece.BlackMan);
  board.set(3, 0, Piece.BlackMan);
  board.set(5, 0, Piece.BlackMan);
  board.set(7, 0, Piece.BlackMan);
  board.set(0, 1, Piece.BlackMan);
  board.set(2, 1, Piece.BlackMan);
  board.set(4, 1, Piece.BlackMan);
  board.set(6, 1, Piece.BlackMan);
  board.set(1, 2, Piece.BlackMan);
  board.set(3, 2, Piece.BlackMan);
  board.set(5, 2, Piece.BlackMan);
  board.set(7, 2, Piece.BlackMan);

  board.set(0, 5, Piece.RedMan);
  board.set(2, 5, Piece.RedMan);
  board.set(4, 5, Piece.RedMan);
  board.set(6, 5, Piece.RedMan);
  board.set(1, 6, Piece.RedMan);
  board.set(3, 6, Piece.RedMan);
  board.set(5, 6, Piece.RedMan);
  board.set(7, 6, Piece.RedMan);
  board.set(0, 7, Piece.RedMan);
  board.set(2, 7, Piece.RedMan);
  board.set(4, 7, Piece.RedMan);
  board.set(6, 7, Piece.RedMan);

  render(root, board);
  showPossibleMoves();
};
const detectWinner = () => {
  if (board.isWin(Player.Red)) {
    alert("Player wins!");
    reset();
    return 1;
  }
  if (board.isWin(Player.Black)) {
    alert("Computer wins!");
    reset();
    return -1;
  }
  if (board.isDraw()) {
    alert("Draw!");
    return 0;
  }
};

// Useful functions -- begin
Array.prototype.shuffle = function () {
  const A = [...this];  
  for (let i = 0; i < A.length / 2; i++) {
    const index = i + Math.floor(Math.random() * (A.length - 1 - i));
    let temp = A[i];
    A[i] = A[index];
    A[index] = temp;
  }
  return A;
};
// Improved minimax.
function alphaBeta(board, player, max, depth, alpha = -Infinity, beta = Infinity) {
  // base case
  if (board.isWin(player) || board.isWin(Player.opposite(player)) || depth == 0)
    return board.evaluate(player);

  // recursive case
  if (max) {
    // maximizing
    let moves = board.possibleMoves(player);
    moves = moves.shuffle(); // a little bit randomness
    for (let move of moves) {
      let result = alphaBeta(board.move(move), player, false, depth - 1, alpha, beta);
      alpha = Math.max(result, alpha);
      if (beta <= alpha) break;
    }
    return alpha;
  } else {
    // minimizing
    let moves = board.possibleMoves(Player.opposite(player));
    moves = moves.shuffle(); // a little bit randomness
    for (let move of moves) {
      let result = alphaBeta(board.move(move), player, true, depth - 1, alpha, beta);
      beta = Math.min(result, beta);
      if (beta <= alpha) break;
    }
    return beta;
  }
}
// Returns the best move.
const bestMove = (board, player, depth) => {
  let bestSum = -Infinity;
  let bestMoveSoFar = new Move(null, null, null);
  const moves = board.possibleMoves(player);
  if (moves.length == 0) detectWinner();
  for (let move of moves) {
    let result = alphaBeta(board.move(move), player, false, depth);
    if (result > bestSum) {
      bestSum = result;
      bestMoveSoFar = move;
    }
  }
  return bestMoveSoFar;
};
// Highlights the moves.
const highlightMoves = (moves) => {
  const highlight = (x, y, index, className) => {
    const cell = document.querySelector(`.piece[data-x="${x}"][data-y="${y}"]`);
    if (cell) {
      cell.classList.add(className);
      cell.setAttribute("data-move-index", index);
    }
  };
  for (let i = 0; i < moves.length; i++) {
    const move = moves[i];
    currentMoves.push(move);
    highlight(...board.pos(move.from), i, "half-highlight");
    highlight(...board.pos(move.to), i, "highlight");
    for (let j = 0; j < move.children.length - 1; j++)
      highlight(...board.pos(move.children[j].to), -1, "half-highlight");
  }
};
const showPossibleMoves = () => {
  const moves = board.possibleMoves(currentPlayer);
  
  // remove highlighting
  const cells = document.querySelectorAll(".piece.possible-move");
  cells.forEach((el) => {
    el.classList.remove("possible-move");
  }, this);
  
  // highlight possible moves
  for (let i = 0; i < moves.length; i++) {
    const [x, y] = board.pos(moves[i].from)
    const cell = document.querySelector(`.piece[data-x="${x}"][data-y="${y}"]`);
    if (cell)
      cell.classList.add('possible-move');
  }
}
// Useful functions -- end

// Game functions -- begin
const possibleMoves = (position) => {
  const moves = board.possibleMoves(currentPlayer);
  return moves.filter((move) => move.from == position);
};
// Render the game board.
const render = (root, board) => {
  const html = [];

  for (let y = 0; y < board.base; y++) {
    for (let x = 0; x < board.base; x++) {
      const piece = board.get(x, y);
      const span = document.createElement("span");
      span.setAttribute("data-x", x);
      span.setAttribute("data-y", y);
      span.style.width = `${100 / board.base - 0.1}%`;
      span.style.height = `${100 / board.base - 0.1}%`;
      span.classList.add("piece");
      if ((x + y + 2) % 2 == 0) span.classList.add("light");
      else span.classList.add("dark");
      // type
      if (piece == Piece.Empty) span.classList.add("empty");
      else if (piece == Piece.RedMan) span.classList.add("man", "red");
      else if (piece == Piece.RedKing) span.classList.add("king", "red");
      else if (piece == Piece.BlackMan) span.classList.add("man", "black");
      else if (piece == Piece.BlackKing) span.classList.add("king", "black");
      else span.classList.add("empty");
      html.push(span);
    }
  }

  root.innerHTML = "";
  html.map((element) => {
    root.appendChild(element);
  });
};
// Game functions -- end

// Classes -- begin
/**
 * One cell of the game board.
 */
class Piece {
  static Empty = 0;
  static RedMan = 1;
  static BlackMan = 2;
  static RedKing = 3;
  static BlackKing = 4;

  static opposite(type) {
    if (type == Piece.RedMan) return Piece.BlackMan;
    else if (type == Piece.BlackMan) return Piece.RedMan;
    else if (type == Piece.RedKing) return Piece.BlackKing;
    else if (type == Piece.BlackKing) return Piece.RedKing;
    else return Piece.Empty;
  }
  static dir(type) {
    if ([Piece.RedKing, Piece.BlackKing].includes(type)) return [1, -1];
    else if (type == Piece.RedMan) return [-1];
    else if (type == Piece.BlackMan) return [1];
    else return [];
  }
  static value(type) {
    if ([Piece.RedKing, Piece.BlackKing].includes(type)) return 10;
    else if ([Piece.RedMan, Piece.BlackMan].includes(type)) return 3;
    else return 0;
  }
}

/**
 * Represents a player.
 */
class Player {
  static Red = 1;
  static Black = 2;

  static opposite(type) {
    if (type == Player.Red) return Player.Black;
    else if (type == Player.Black) return Player.Red;
    else return null;
  }
  static byPiece(type) {
    if ([Piece.RedMan, Piece.RedKing].includes(type)) return Player.Red;
    else if ([Piece.BlackMan, Piece.BlackKing].includes(type))
      return Player.Black;
    else return null;
  }
}

/**
 * Contains parameters of a move.
 */
class Move {
  constructor(from, to, piece) {
    this.from = from;
    this.to = to;
    this.piece = piece;
    this.children = [];
    this.eaten = [];
  }
}

/**
 * Represents the board of the game.
 */
class Board {
  static BASE = 8;

  constructor(state, player, base = Board.BASE) {
    this.state = state;
    this.player = player;
    this.base = base;
  }
  // Returns the index for the position.
  index(x, y) {
    return x + this.base * y;
  }
  // static version of index().
  static index(x, y) {
    return x + Board.BASE * y;
  }
  // Returns the position by index.
  pos(index) {
    return [
      index % this.base, // x
      Math.floor(index / this.base) // y
    ];
  }
  // static version of pos().
  static pos(index) {
    return [
      index % Board.BASE, // x
      Math.floor(index / Board.BASE) // y
    ];
  }
  // getter
  get(x, y) {
    return this.state[this.index(x, y)];
  }
  // setter
  set(x, y, piece) {
    this.state[this.index(x, y)] = piece;
  }
  // Returns an array of possible moves for current player.
  possibleMoves(player = this.player) {
    const moves = [];

    // eating moves
    for (let x = 0; x < this.base; x++)
      for (let y = 0; y < this.base; y++)
        if (Player.byPiece(this.get(x, y)) == player)
          moves.push(...this._possibleEatingMoves(x, y, Piece.dir(this.get(x, y)), player));

    // If there are eating moves, then we don't need simple moves
    // beacuse capturing is mandatory in most official rules.
    if (moves.length > 0) return moves;

    // simple moves
    for (let x = 0; x < this.base; x++)
      for (let y = 0; y < this.base; y++)
        if (Player.byPiece(this.get(x, y)) == player)
          moves.push(...this._possibleSimpleMoves(x, y, Piece.dir(this.get(x, y))));

    return moves;
  }
  // Returns an array with possible simple moves.
  _possibleSimpleMoves(x, y, dir) {
    const moves = [];

    // go through all allowwed directions
    for (let d = 0; d < dir.length; d++) {
      // left cell
      if (x > 0 && y + dir[d] >= 0 && y + dir[d] < this.base 
          && this.get(x - 1, y + dir[d]) == Piece.Empty
      ) {
        moves.push(
          new Move(this.index(x, y), this.index(x - 1, y + dir[d], this.get(x, y)))
        );
      }
      // right cell
      if (x < this.base - 1 && y + dir[d] >= 0 && y + dir[d] < this.base 
          && this.get(x + 1, y + dir[d]) == Piece.Empty
      ) {
        moves.push(
          new Move(this.index(x, y), this.index(x + 1, y + dir[d], this.get(x, y)))
        );
      }
    }

    return moves;
  }
  // Returns an array with possible eating moves.
  _possibleEatingMoves(x, y, dir, player) {
    const moves = [];
    const piece = this.get(x, y);
    const h_dir = [1, -1];

    for (let hd = 0; hd < h_dir.length; hd++) {
      // go through all allowed directions
      for (let d = 0; d < dir.length; d++) {
        // checks
        if (
          x + h_dir[hd] * 2 >= 0 && x + h_dir[hd] * 2 < this.base 
          && y + dir[d] * 2 >= 0 && y + dir[d] * 2 < this.base 
          && Player.byPiece(this.get(x + h_dir[hd], y + dir[d])) == Player.opposite(player) 
          && this.get(x + h_dir[hd] * 2, y + dir[d] * 2) == Piece.Empty
        ) {
          const state = [...this.state];

          // remove an eaten piece
          state[this.index(x + h_dir[hd], y + dir[d])] = Piece.Empty;
          // set player's piece to a new position
          state[this.index(x + h_dir[hd] * 2, y + dir[d] * 2)] = piece;

          const board = new Board(state, player, this.base);
          const innerMoves = board._possibleEatingMoves(x + h_dir[hd] * 2, y + dir[d] * 2, dir, player);

          if (innerMoves.length > 0) {
            for (let i = 0; i < innerMoves.length; i++) {
              let from = this.index(x, y);
              let to = this.index(x + h_dir[hd] * 2, y + dir[d] * 2);
              const move = new Move(from, to, piece);
              move.eaten = [this.index(x + h_dir[hd], y + dir[d])];

              const realMove = new Move(
                from,
                innerMoves[i].children.length
                  ? innerMoves[i].children[innerMoves[i].children.length - 1].to
                  : innerMoves[i].to,
                piece
              );
              realMove.children = [...innerMoves[i].children];
              realMove.children.splice(0, 0, move);
              realMove.eaten = [...innerMoves[i].eaten];
              realMove.eaten.splice(0, 0, this.index(x + h_dir[hd], y + dir[d]));

              moves.push(realMove);
            }
          } else {
            // innerMoves.length <= 0
            const move = new Move(this.index(x, y), this.index(x + h_dir[hd] * 2, y + dir[d] * 2), piece);
            move.children.push(move);
            move.eaten = [this.index(x + h_dir[hd], y + dir[d])];
            moves.push(move);
          }
        }
      }
    }

    return moves;
  }
  // How many player's pieces are there on the board?
  piecesCounter(player = this.player) {
    let number = 0;

    for (let i = 0; i < this.state.length; i++)
      if (Player.byPiece(this.state[i]) == player) number++;

    return number;
  }
  // Does the player win?
  isWin(player = this.player) {
    const enemyPieces = this.piecesCounter(Player.opposite(player));
    if (enemyPieces == 0) return true;

    const playerPieces = this.piecesCounter(player);
    const moves = this.possibleMoves(player);
    if (moves.length == 0 && playerPieces > enemyPieces) return true;

    return false;
  }
  // Is is a draw?
  isDraw() {
    const playerPieces = this.piecesCounter(this.player);
    const enemyPieces = this.piecesCounter(Player.opposite(this.player));
    return playerPieces == 1 && enemyPieces == 1;
  }
  // Evaluate the situation on the board.
  boardValue(player = this.player) {
    let value = 0;

    for (let y = 0; y < this.base; y++) {
      for (let x = 0; x < this.base; x++) {
        if (Player.byPiece(this.get(x, y)) == player) {
          let v_dir = Piece.dir(this.get(x, y));
          let moveScore = 0;
          if (v_dir.length == 1) {
            moveScore += (1 - v_dir[0]) * (this.base - 1) / 2 + v_dir[0] * y;
          }
          value += Piece.value(this.get(x, y)) + moveScore / this.base;
        }
      }
    }

    return value;
  }
  // Returns some value for the current board.
  evaluate(player = this.player) {
    if (this.isWin(player)) return 1000;
    else if (this.isWin(Player.opposite(player))) return -1000;

    let playerValue = this.boardValue(player);
    let opponentValue = this.boardValue(Player.opposite(player));

    return playerValue - opponentValue;
  }
  // Makes every lucky Man a King!
  doKings() {
    // black
    let blackY = this.base - 1;
    for (let x = 0; x < this.base; x++)
      if (this.get(x, blackY) == Piece.BlackMan)
        this.set(x, blackY, Piece.BlackKing);
    // red
    let redY = 0;
    for (let x = 0; x < this.base; x++)
      if (this.get(x, redY) == Piece.RedMan)
        this.set(x, redY, Piece.RedKing);
  }
  // Performs a move and returns the resulting board.
  move(move) {
    let state = [...this.state];
    let piece = state[move.from];

    // check eaten pieces
    if (move.eaten.length > 0)
      for (let i = 0; i < move.eaten.length; i++)
        state[move.eaten[i]] = Piece.Empty;

    state[move.to] = piece; // move the piece
    state[move.from] = Piece.Empty; // clear the old cell

    const board = new Board(state, Player.opposite(this.player), this.base);
    board.doKings();
    return board;
  }
}
// Classes -- end
</script>