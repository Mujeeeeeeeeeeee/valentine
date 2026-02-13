<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For You ❤️</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:'Poppins',sans-serif;
}

body{
height:100vh;
overflow:hidden;
background:black;
display:flex;
justify-content:center;
align-items:center;
color:white;
text-align:center;
}

/* ⭐ STARRY SKY */
body::before{
content:"";
position:fixed;
width:100%;
height:100%;
background:url("https://www.transparenttextures.com/patterns/stardust.png");
animation:starsMove 120s linear infinite;
z-index:-2;
}

@keyframes starsMove{
from{background-position:0 0;}
to{background-position:10000px 5000px;}
}

/* glow nebula */
body::after{
content:"";
position:fixed;
width:200%;
height:200%;
background:radial-gradient(circle at 30% 40%, rgba(255,0,150,.15), transparent 40%),
radial-gradient(circle at 70% 60%, rgba(0,200,255,.12), transparent 40%);
animation:nebula 18s ease infinite alternate;
z-index:-1;
}

@keyframes nebula{
from{transform:translate(-5%,-5%);} 
to{transform:translate(5%,5%);} 
}

.card{
backdrop-filter: blur(18px);
background: rgba(255,255,255,0.08);
padding:35px;
border-radius:28px;
width:90%;
max-width:420px;
box-shadow:0 0 80px rgba(255,0,120,.25);
animation:fadeUp .9s ease;
}

@keyframes fadeUp{
from{opacity:0; transform:translateY(40px);} 
to{opacity:1; transform:translateY(0);} 
}

button{
border:none;
padding:14px 26px;
border-radius:30px;
font-size:18px;
cursor:pointer;
margin:10px;
transition:.25s;
}

.yes{
background:#00ffb7;
color:black;
font-weight:bold;
}

.no{
background:#ff4e8a;
color:white;
}

.hidden{display:none;}

/* 🎬 CINEMATIC INTRO */
#intro{
position:fixed;
width:100%;
height:100%;
background:black;
display:flex;
justify-content:center;
align-items:center;
flex-direction:column;
z-index:999;
animation:introFade 2.5s forwards;
animation-delay:3.2s;
}

#intro h1{
font-size:42px;
letter-spacing:4px;
animation:cinematicZoom 3s ease forwards;
}

@keyframes cinematicZoom{
from{transform:scale(1.8); opacity:0;} 
to{transform:scale(1); opacity:1;} 
}

@keyframes introFade{
to{opacity:0; visibility:hidden;} 
}

/* 📜 LOVE LETTER */
.letterWrapper{
perspective:1200px;
margin-top:20px;
}

.letter{
width:100%;
height:220px;
background:linear-gradient(135deg,#fff,#ffe6f0);
color:#333;
border-radius:14px;
padding:20px;
transform:rotateX(-90deg);
transform-origin:top;
transition:transform 1s;
box-shadow:0 20px 60px rgba(0,0,0,.35);
overflow:auto;
}

.letter.open{
transform:rotateX(0deg);
}

.openBtn{
background:#ffd166;
color:black;
font-weight:600;
}

</style>
</head>

<body>

<!-- CINEMATIC INTRO -->
<div id="intro">
<h1>For Someone Very Special...</h1>
</div>

<!-- PASSWORD -->
<div class="card" id="passwordScreen">
<h2>Enter Password 🔐</h2>
<p style="margin:10px 0;">(Hint: the day we met)</p>

<input id="pass" type="password"
style="padding:10px;border-radius:10px;border:none;margin-top:10px;width:70%;">

<br><br>

<button onclick="checkPass()">Enter</button>
</div>

<!-- COUNTDOWN -->
<div class="card hidden" id="countdownScreen">
<h2>Something magical unlocks in...</h2>
<h1 id="count" style="font-size:55px;margin-top:10px;"></h1>
</div>

<!-- MAIN -->
<div class="card hidden" id="main">
<h1>Will you be my Valentine? ❤️</h1>

<button class="yes" id="yes" onclick="accepted()">YES</button>
<button class="no" onclick="growYes()">No</button>

<div id="letterSection" class="hidden">

<button class="openBtn" onclick="openLetter()">Open Love Letter 💌</button>

<div class="letterWrapper">
<div class="letter" id="letter">

<h3>I have something to tell you...</h3>
<br>
<p>
Some people search their whole lives for a feeling that makes their world softer, brighter, and warmer.

Somehow… I found that feeling in you.

If you say yes today, it won't just make my day — it will become one of those memories we smile about years from now.

So… what do you say?
</p>

</div>
</div>

</div>

</div>

<script>

let size=18;

function checkPass(){

if(document.getElementById("pass").value==="130126"){
document.getElementById("passwordScreen").style.display="none";
startCountdown();
}else{
alert("Wrong password 🙂");
}
}

function startCountdown(){

document.getElementById("countdownScreen").classList.remove("hidden");

let time=5;

let timer=setInterval(()=>{
document.getElementById("count").innerHTML=time;

time--;

if(time<0){
clearInterval(timer);
document.getElementById("countdownScreen").style.display="none";
document.getElementById("main").classList.remove("hidden");
}

},1000);
}

function growYes(){

size+=18;

let yes=document.getElementById("yes");

yes.style.fontSize=size+"px";
yes.style.padding=(size/2)+"px";

if(size>160){
document.querySelector(".no").style.display="none";
}
}

function accepted(){

fetch("https://api.countapi.xyz/hit/YOUR-SITE/yesClicks");

document.getElementById("letterSection").classList.remove("hidden");
confetti();
}

function openLetter(){

document.getElementById("letter").classList.add("open");
}

function confetti(){

for(let i=0;i<120;i++){

let div=document.createElement("div");

div.style.position="absolute";
div.style.width="10px";
div.style.height="10px";
div.style.background="white";
div.style.top="-10px";
div.style.left=Math.random()*100+"%";

div.style.animation="fall 3s linear";

document.body.appendChild(div);

setTimeout(()=>div.remove(),3000);
}
}

</script>

<style>
@keyframes fall{
to{
transform:translateY(110vh) rotate(720deg);
opacity:0;
}
}
</style>

</body>
</html>
