<html>
<head>
    <title>     
    </title>

</head>
<body id="ht">
<div class="black_background" id="black_background"> </div>
    <div class="menu_controls" style="text-align:center;">
        <!-- Main Menu -->
        <div id="start_menu" class="py-4 text-light">
            <p>Welcome to checkers!</p>
        </div>
        <!-- Game Over -->
        <div id="gameover_form" class="py-4 text-light">
            <p>Game Over, press the <span style="background-color: #d4ca1c; color: #000000">refresh</span> button to try again</p>
            <p><span style="background-color: #FFFFFF; color: #000000">Your username must have exactly 3 characters in order to log your score.</span></p>
            <form action="javascript:create_user()">
                <p><label>
                    Username for Player Red:
                    <input type="text" name="uidR" id="user1" placeholder="Must have 3 characters" required>
                </label></p>
                <p><label>
                    Username for Player Black:
                    <input type="text" name="uidB" id="user2" placeholder="Must have 3 characters" required>
                </label></p>
                <p><label>
                    Result for red:
                    <span name="resultR" id="resultR">Result displayed here</span>
                </label></p>
                <p><label>
                    Result for black:
                    <span name="resultB" id="resultB">Result displayed here</span>
                </label></p> -->
                <p>
                    <button onclick="alert('Your game has been posted!')">Submit</button>
                </p>
            </form>
        </div>

<div class="checker white_checker" style="display:none"> </div>
<div class="checker black_checker" style="display:none"> </div>
<div class="square" style="display: none" id ="ht"> </div>
    <div class="score" id="score">
        <br>
    </div>
<button id="exit_screen" onclick="exitResultScreen()">Exit</button>
<div class="table" id="table">
<!-- Creating the board-->
  <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>  
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>
    <div class="checker white_checker"> </div>  

  <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>
    <div class="checker black_checker"> </div>


  <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="clear_float"> </div>
    
  <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="clear_float"> </div>

  <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="clear_float"> </div>

  <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="clear_float"> </div>

  <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="clear_float"> </div>

  <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="clear_float"> </div>

  <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="clear_float"> </div>

  <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="square white_square"> </div>
    <div class="square black_square"> </div>
    <div class="clear_float"> </div>

</div>

<script>
//setting the variables
var square_class = document.getElementsByClassName("square");
var white_checker_class = document.getElementsByClassName("white_checker");
var black_checker_class = document.getElementsByClassName("black_checker");
var table = document.getElementById("table");
var score = document.getElementById("score");
var black_background = document.getElementById("black_background");
const exit_background = document.getElementById("exit_screen");
exit_background.style.display = "none";
var windowHeight = window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;  ;
var windowWidth =  window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;
var moveLength = 80 ;
var moveDeviation = 10;
var Dimension = 1;
var selectedPiece,selectedPieceindex;
var upRight,upLeft,downLeft,downRight;
var contor = 0 , gameOver = 0;
var bigScreen = 1;
var block = [];
var w_checker = [];
var b_checker = [];
var the_checker ;
var oneMove;
var anotherMove;
var mustAttack = false;
var multiplier = 1 
var tableLimit,reverse_tableLimit ,  moveUpLeft,moveUpRight, moveDownLeft,moveDownRight , tableLimitLeft, tableLimitRight;
const GAMEOVERFORM = document.getElementById("gameover_form");
GAMEOVERFORM.style.display = "none";
const result_red = document.getElementById("resultR");
const result_black = document.getElementById("resultB");
//start of game logic  
  getDimension();
    if(windowWidth > 640){
        moveLength = 80;
        moveDeviation = 10;
    }
    else{
        moveLength = 50;
        moveDeviation = 6;
    }
var square_p = function(square,index){
    this.id = square;
    this.occupied = false;
    this.pieceId = undefined;
    this.id.onclick = function() {
        makeMove(index);
    }
}
var checker = function(piece,color,square) {
    this.id = piece;
    this.color = color;
    this.king = false;
    this.occupied_square = square;
    this.alive = true;
    this.attack = false;
    if(square%8){
        this.coordX= square%8;
        this.coordY = Math.floor(square/8) + 1 ;
    }
    else{
        this.coordX = 8;
        this.coordY = square/8 ;
    }
    this.id.onclick = function  () {
        showMoves(piece);   
    }
}
checker.prototype.setCoord = function(X,Y){
    var x = (this.coordX - 1  ) * moveLength + moveDeviation;
    var y = (this.coordY - 1 ) * moveLength  + moveDeviation;
    this.id.style.top = y + 'px';
    this.id.style.left = x + 'px';
}
checker.prototype.changeCoord = function(X,Y){
    this.coordY +=Y;
    this.coordX += X;
}
checker.prototype.checkIfKing = function () {
    if(this.coordY == 8 && !this.king &&this.color == "white"){
        this.king = true;
        this.id.style.border = "4px solid #FFFF00";
    }
    if(this.coordY == 1 && !this.king &&this.color == "black"){
        this.king = true;
        this.id.style.border = "4px solid #FFFF00";
    }
}
for (var i = 1; i <=64; i++)
    block[i] =new square_p(square_class[i],i); 
for (var i = 1; i <= 4; i++){
    w_checker[i] = new checker(white_checker_class[i], "white", 2*i -1 );
    w_checker[i].setCoord(0,0);
    block[2*i - 1].occupied = true;
    block[2*i - 1].pieceId =w_checker[i];
}
for (var i = 5; i <= 8; i++){
    w_checker[i] = new checker(white_checker_class[i], "white", 2*i );
    w_checker[i].setCoord(0,0);
    block[2*i].occupied = true;
    block[2*i].pieceId = w_checker[i];
}
for (var i = 9; i <= 12; i++){
    w_checker[i] = new checker(white_checker_class[i], "white", 2*i - 1 );
    w_checker[i].setCoord(0,0);
    block[2*i - 1].occupied = true;
    block[2*i - 1].pieceId = w_checker[i];
}
for (var i = 1; i <= 4; i++){
    b_checker[i] = new checker(black_checker_class[i], "black", 56 + 2*i  );
    b_checker[i].setCoord(0,0);
    block[56 +  2*i ].occupied = true;
    block[56+  2*i ].pieceId =b_checker[i];
}
for (var i = 5; i <= 8; i++){
    b_checker[i] = new checker(black_checker_class[i], "black", 40 +  2*i - 1 );
    b_checker[i].setCoord(0,0);
    block[ 40 + 2*i - 1].occupied = true;
    block[ 40 + 2*i - 1].pieceId = b_checker[i];
}
for (var i = 9; i <= 12; i++){
    b_checker[i] = new checker(black_checker_class[i], "black", 24 + 2*i  );
    b_checker[i].setCoord(0,0);
    block[24 + 2*i ].occupied = true;
    block[24 + 2*i ].pieceId = b_checker[i];
}
the_checker = w_checker;
function showMoves (piece) {
    var match = false;
    mustAttack = false;
    if(selectedPiece){
            erase_roads(selectedPiece);
    }
    selectedPiece = piece;
    var i,j; // retain the queen index
    for ( j = 1; j <= 12; j++){
        if(the_checker[j].id == piece){
            i = j;
            selectedPieceindex = j;
            match = true;
        }
    }
    if(oneMove && !attackMoves(oneMove)){
        changeTurns(oneMove);
        oneMove = undefined;
        return false;
    }
    if(oneMove && oneMove != the_checker[i] ){
        return false;
    }
    if(!match) {
     return 0 ;
    }
    if(the_checker[i].color =="white"){
        tableLimit = 8;
        tableLimitRight = 1;
        tableLimitLeft = 8;
        moveUpRight = 7;
        moveUpLeft = 9;
        moveDownRight = - 9;
        moveDownLeft = -7;
    }
    else{
        tableLimit = 1;
        tableLimitRight = 8;
        tableLimitLeft = 1;
        moveUpRight = -7;
        moveUpLeft = -9;
        moveDownRight = 9;
        moveDownLeft = 7;
    }
        attackMoves(the_checker[i]); 
    if(!mustAttack){
      downLeft = checkMove( the_checker[i] , tableLimit , tableLimitRight , moveUpRight , downLeft);
        downRight = checkMove( the_checker[i] , tableLimit , tableLimitLeft , moveUpLeft , downRight);
        if(the_checker[i].king){
            upLeft = checkMove( the_checker[i] , reverse_tableLimit , tableLimitRight , moveDownRight , upLeft);
            upRight = checkMove( the_checker[i], reverse_tableLimit , tableLimitLeft , moveDownLeft, upRight)
        }
    }
    if(downLeft || downRight || upLeft || upRight){
            return true;
        }
    return false;   
}
function erase_roads(piece){
    if(downRight) block[downRight].id.style.background = "#BA7A3A";
    if(downLeft) block[downLeft].id.style.background = "#BA7A3A";
    if(upRight) block[upRight].id.style.background = "#BA7A3A";
    if(upLeft) block[upLeft].id.style.background = "#BA7A3A";
}   
function makeMove (index) {
    var isMove = false;
    if(!selectedPiece)
        return false;
    if(index != upLeft && index != upRight && index != downLeft && index != downRight){
        erase_roads(0);
        selectedPiece = undefined;
        return false;
    }
    if(the_checker[1].color=="white"){
        cpy_downRight = upRight;
        cpy_downLeft = upLeft;
        cpy_upLeft = downLeft;
        cpy_upRight = downRight;
    }
    else{
        cpy_downRight = upLeft;
        cpy_downLeft = upRight;
        cpy_upLeft = downRight;
        cpy_upRight = downLeft;
    }  
    if(mustAttack)  
        multiplier = 2;
    else
        multiplier = 1;
        if(index == cpy_upRight){
            isMove = true;      
            if(the_checker[1].color=="white"){
                executeMove( multiplier * 1, multiplier * 1, multiplier * 9 );
                if(mustAttack) eliminateCheck(index - 9);
            }
            else{
                executeMove( multiplier * 1, multiplier * -1, multiplier * -7);
                if(mustAttack) eliminateCheck( index + 7 );
            }
        }
        if(index == cpy_upLeft){
            isMove = true;
            if(the_checker[1].color=="white"){
                executeMove( multiplier * -1, multiplier * 1, multiplier * 7);
                if(mustAttack)  eliminateCheck(index - 7 );             
            }
            else{
                executeMove( multiplier * -1, multiplier * -1, multiplier * -9);
                if (mustAttack) eliminateCheck( index + 9 );
            }
        }
        if(the_checker[selectedPieceindex].king){
            if(index == cpy_downRight){
                isMove = true;
                if(the_checker[1].color=="white"){
                    executeMove( multiplier * 1, multiplier * -1, multiplier * -7);
                    if(mustAttack) eliminateCheck ( index  + 7) ;
                }
                else{
                    executeMove( multiplier * 1, multiplier * 1, multiplier * 9);
                    if(mustAttack) eliminateCheck ( index  - 9) ;
                }
            }
        if(index == cpy_downLeft){
            isMove = true;
                if(the_checker[1].color=="white"){
                    executeMove( multiplier * -1, multiplier * -1, multiplier * -9);
                    if(mustAttack) eliminateCheck ( index  + 9) ;
                }
                else{
                    executeMove( multiplier * -1, multiplier * 1, multiplier * 7);
                    if(mustAttack) eliminateCheck ( index  - 7) ;
                }
            }
        }
    erase_roads(0);
    the_checker[selectedPieceindex].checkIfKing();
    if (isMove) {
            anotherMove = undefined;
         if(mustAttack) {
                anotherMove = attackMoves(the_checker[selectedPieceindex]);
         }
        if (anotherMove){
            oneMove = the_checker[selectedPieceindex];
            showMoves(oneMove);
        }
        else{
            oneMove = undefined;
            changeTurns(the_checker[1]);
            gameOver = checkIfLost();
            if(gameOver) { setTimeout( declareWinner(),3000 ); return false};
            gameOver = checkForMoves();
            if(gameOver) { setTimeout( declareWinner() ,3000) ; return false};
        }
    }
}
function executeMove (X,Y,nSquare){
    the_checker[selectedPieceindex].changeCoord(X,Y); 
    the_checker[selectedPieceindex].setCoord(0,0);
    block[the_checker[selectedPieceindex].occupied_square].occupied = false;          
    block[the_checker[selectedPieceindex].occupied_square + nSquare].occupied = true;
    block[the_checker[selectedPieceindex].occupied_square + nSquare].pieceId =   block[the_checker[selectedPieceindex].occupied_square ].pieceId;
    block[the_checker[selectedPieceindex].occupied_square ].pieceId = undefined;     
    the_checker[selectedPieceindex].occupied_square += nSquare;
}
function checkMove(Apiece,tLimit,tLimit_Side,moveDirection,theDirection){
    if(Apiece.coordY != tLimit){
        if(Apiece.coordX != tLimit_Side && !block[ Apiece.occupied_square + moveDirection ].occupied){
            block[ Apiece.occupied_square + moveDirection ].id.style.background = "#704923";
            theDirection = Apiece.occupied_square + moveDirection;
        }
    else
            theDirection = undefined;
    }
    else
        theDirection = undefined;
    return theDirection;
}
function  checkAttack( check , X, Y , negX , negY, squareMove, direction){
    if(check.coordX * negX >=   X * negX && check.coordY *negY <= Y * negY && block[check.occupied_square + squareMove ].occupied && block[check.occupied_square + squareMove].pieceId.color != check.color && !block[check.occupied_square + squareMove * 2 ].occupied){
        mustAttack = true;
        direction = check.occupied_square +  squareMove*2 ;
        block[direction].id.style.background = "#704923";
        return direction ;
    }
    else
        direction =  undefined;
        return direction;
}
function eliminateCheck(indexx){
    if(indexx < 1 || indexx > 64)
        return  0;
    var x =block[ indexx ].pieceId ;
    x.alive =false;
    block[ indexx ].occupied = false;
    x.id.style.display  = "none";
}
function attackMoves(ckc){
        upRight = undefined;
        upLeft = undefined;
        downRight = undefined;
        downLeft = undefined;
    if(ckc.king ){
        if(ckc.color == "white"){
            upRight = checkAttack( ckc , 6, 3 , -1 , -1 , -7, upRight );
            upLeft = checkAttack( ckc, 3 , 3 , 1 , -1 , -9 , upLeft );
        }
        else{
            downLeft = checkAttack( ckc , 3, 6, 1 , 1 , 7 , downLeft );
            downRight = checkAttack( ckc , 6 , 6 , -1, 1 ,9 , downRight );      
        }
    }
    if(ckc.color == "white"){
        downLeft = checkAttack( ckc , 3, 6, 1 , 1 , 7 , downLeft );
        downRight = checkAttack( ckc , 6 , 6 , -1, 1 ,9 , downRight );
    }
    else{
        upRight = checkAttack( ckc , 6, 3 , -1 , -1 , -7, upRight );
        upLeft = checkAttack( ckc, 3 , 3 , 1 , -1 , -9 , upLeft );
    }
    if(ckc.color== "black" && (upRight || upLeft || downLeft || downRight ) ) {
        var p = upLeft;
        upLeft = downLeft;
        downLeft = p;
        p = upRight;
        upRight = downRight;
        downRight = p;
        p = downLeft ;
        downLeft = downRight;
        downRight = p;
        p = upRight ;
        upRight = upLeft;
        upLeft = p;
    }
    if(upLeft != undefined || upRight != undefined || downRight != undefined || downLeft != undefined){
        return true;
    }
    return false;
}
function changeTurns(ckc){
        if(ckc.color=="white")
    the_checker = b_checker;
else
    the_checker = w_checker;
 }
function checkIfLost(){
    var i;
    for(i = 1 ; i <= 12; i++)
        if(the_checker[i].alive)
            return false;
    return true;
}
function exitResultScreen(){
    black_background.style.display = "none";
    exit_background.style.display = "none";
    score.style.display = "none";
}
function  checkForMoves() {
    var i ;
    for(i = 1 ; i <= 12; i++)
        if (the_checker[i].alive && showMoves(the_checker[i].id)) {
            erase_roads(0);
            return false;
        }
    return true;
}
function declareWinner() {
    black_background.style.display = "inline";
    score.style.display = "block";
    exit_background.style.display = "inline";
    GAMEOVERFORM.style.display = "block";

if (the_checker[1].color == "white") {
    score.innerHTML = "Black wins";
    result_red.innerHTML = "Loss";
    result_black.innerHTML = "Win";
}

else {
    score.innerHTML = "Red wins";
    result_red.innerHTML = "Win";
    result_black.innerHTML = "Loss";
} 

}
function getDimension (){
    contor ++;
 windowHeight = window.innerHeight
    || document.documentElement.clientHeight
    || document.body.clientHeight;  ;
 windowWidth =  window.innerWidth
    || document.documentElement.clientWidth
    || document.body.clientWidth;
}
document.getElementsByTagName("BODY")[0].onresize = function(){
    getDimension();
    var cpy_bigScreen = bigScreen ;
if(windowWidth < 650){
        moveLength = 50;
        moveDeviation = 6; 
        if(bigScreen == 1) bigScreen = -1;
    }
if(windowWidth > 650){
        moveLength = 80;
        moveDeviation = 10; 
        if(bigScreen == -1) bigScreen = 1;
    }
    if(bigScreen !=cpy_bigScreen){
    for(var i = 1; i <= 12; i++){
        b_checker[i].setCoord(0,0);
        w_checker[i].setCoord(0,0);
    }
    }
}
//end of game logic
</script>
<style>
  body , html{
        transition: 1s ease-in-out;
        width: 100%;
        height : 100%;
        margin : 0 0;
        padding: 0  0;
}
.square{
    float: left;
    width: 80px;
    height: 80px;
}
.white_square{
    background-color:#F0D2B4;
}
.black_square{
    background-color :#BA7A3A;
}
.clear_float{
    clear: both;
}
.table{
    position: relative;
    width: 640px;
    height: 640px;
    margin: 0 auto;
}
.score{
    background-color: #ada61a;
    color: white;
    display: none;
    font-size: 45px;
    font-weight: 900;
    height:150px;
    border-radius: 10%;
    left: 0px;
    letter-spacing: 1px;
    margin : 0 auto;
    padding-top: 30px;
    overflow: hidden;
    position: absolute;
    right: 0px;
    text-align: center;
    top: 15%;
    width: 200px;
    z-index: 8;
    font-family: Calibri, Candara, Segoe, 'Segoe UI', Optima, Arial, sans-serif;
     -webkit-transition: 5s ease-in-out;
    -moz-transition: 5s ease-in-out;
  -o-transition: 5s ease-in-out;
  transition: 5s ease-in-out;
}
.checker{
    top:10px;
    left:10px;
    width: 54px;
    height: 54px;
    border-radius: 50%;
    position: absolute;
    border: 4px solid white;
    cursor: pointer;    
}
.white_checker{
    background: #CC0000;
 -webkit-transition: 0.3s ease-in-out;
    -moz-transition: 0.3s ease-in-out;
  -o-transition: 0.3s ease-in-out;
  transition: 0.3s ease-in-out;
}
.black_checker{
    background: #00001F;
 -webkit-transition: 0.3s ease-in-out;
    -moz-transition: 0.3s ease-in-out;
  -o-transition: 0.3s ease-in-out;
  transition: 0.3s ease-in-out;
}
.black_background{
    /* position: fixed; */
    overflow: hidden;
    position: absolute;
    width: 100%;
    height: 120%;
    background-color: black;
    opacity: 0.5;
    z-index:  8;
    display: none;
    float: left;
}
#exit_screen{
    z-index: 10;
    overflow: hidden;
    position: absolute;
    transform: translate(-50%, -750%);
    height: 40px;
    width: 100px;
}
@media only screen and (max-width : 640px){
    .table{
        width: 400px;
        height: 400px;  
    }
    .square{
        width: 50px;
        height: 50px;
    }
    .checker{
        width: 32px;
        height: 32px;
    }
}
</style>
</body>
</html>

<script>
  //const url = "http://localhost:8095/api/score"
  const url = "https://pythonalflask.tk/api/checkers"
  const create_fetch = url + '/addCheckersGame';
  // Load users on page entry
  function create_user(){
    const body = {
        uidB: document.getElementById("user2").value,
        resultB: result_black.innerHTML,
        uidR: document.getElementById("user1").value,
        resultR: result_red.innerHTML
    };
    const requestOptions = {
        method: 'POST',
        body: JSON.stringify(body),
        mode: 'cors',
        cache: 'default',
        //credentials: 'include',
        headers: {
            "content-type": "application/json",
            'Authorization': 'Bearer my-token',
        },
    };
    // URL for Create API
    // Fetch API call to the database to create a new user
    fetch(create_fetch, requestOptions)
      .then(response => {
        // trap error response from Web API
        if (response.status !== 200) {
          const errorMsg = 'Database create error: ' + response.status;
          console.log(errorMsg);
          return;
        }
        // response contains valid result
        response.json().then(data => {
            console.log(data);
        })
    })
  }
</script>

