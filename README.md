# game-JS
this is simon game Javascript
Javascript Code
//-----------------
let gameSeq = [];
let userSeq = [];

let btns = ["chocolate","green","yellow","teal"];

let started = false;
let level = 0;

let h2 = document.querySelector("h2");

document.addEventListener("keypress",function(){
    if(started == false){
        console.log("game is started");
        started = true;

        levelUp();
    }
})

function btnFlash(btn){
    btn.classList.add("flash");
    setTimeout(function(){
        btn.classList.remove("flash");
    },500);
}
function userFlash(btn){
    btn.classList.add("userflash");
    setTimeout(function(){
        btn.classList.remove("userflash");
    },250);

}
function levelUp(){
    userSeq = [];
    level++;
    h2.innerText = `level${level}`;

    let randIdx = Math.floor(Math.random()*3);
    let randColor = btns[randIdx];
    let randBtn = document.querySelector(`.${randColor}`);
    gameSeq.push(randColor);
    console.log(gameSeq);
    btnFlash(randBtn);
}
function checkAns(idx){
   if (userSeq[idx]===gameSeq[idx]){
        if(userSeq.length == gameSeq.length){
            setTimeout(levelUp,1000);
        }
    }else {
        h2.innerHTML = `Game Over! Your Score is <b>${level}</b>. <br> Press any key to restart the game`;
        document.querySelector("body").style.backgroundColor = "red";
        setTimeout(function(){
            document.querySelector("body").style.backgroundColor = "white";
        }, 200);
        reset();
    }
}

function btnPress(){
    let btn = this;
    btnFlash(btn);

    userColor = btn.getAttribute("id");
    userSeq.push(userColor);

    checkAns(userSeq.length-1);
}
let allBtns = document.querySelectorAll(".btn");
for(btn of allBtns){
    btn.addEventListener("click",btnPress);
}
function reset(){
    started = false;
    gameSeq = [];
    userSeq = [];
    level = 0;
}
-----JS end here------
Html Code start here
//-------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simon Says Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Simon Says Game</h1>
    <h2>Press Any Key to start the game</h2>
    <div class="btn-container">
        <div class="line-one">
            <div class="btn chocolate" type="button" id="chocolate"></div>
            <div class="btn green"type="button" id="green"></div>
        </div>
        <div class="line-two">
            <div class="btn yellow"type="button" id="yellow"></div>
            <div class="btn teal"type="button" id="teal"></div>
        </div>
    </div>
    <script src="app.js"></script>
</body>
</html>
-----HTML Code ends here---------------------
CSS code start here
//------------------------------------------
body{
    text-align: center;
}
.btn{
    height: 200px;
    width: 200px;
    border-radius: 20%;
    border: 10px solid black;
    margin: 1.5rem;
}
.btn-container{
    display: flex;
    justify-content: center;
}
.chocolate{
    background-color: chocolate;
}
.green{
    background-color: green;
}
.yellow{
    background-color: yellow;
}
.teal{
    background-color: teal;
}

.flash{
    background-color: whitesmoke;
}
.userflash{
    background-color: orangered;
}
----CSS code end here------------------
