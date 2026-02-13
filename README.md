<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>For You ❤️</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family: 'Poppins', sans-serif;
}

body{
height:100vh;
overflow:hidden;
background: linear-gradient(270deg,#ff4e8a,#ff99ac,#ffd1dc,#ff4e8a);
background-size:800% 800%;
animation: gradient 12s ease infinite;
display:flex;
justify-content:center;
align-items:center;
color:white;
text-align:center;
}

@keyframes gradient{
0%{background-position:0% 50%;}
50%{background-position:100% 50%;}
100%{background-position:0% 50%;}
}

.card{
backdrop-filter: blur(20px);
background: rgba(255,255,255,0.12);
padding:35px;
border-radius:25px;
width:90%;
max-width:420px;
box-shadow:0 0 60px rgba(255,0,100,.4);
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
background:#00ff9d;
color:black;
font-weight:bold;
}

.no{
background:#ff4e8a;
color:white;
}

.gift{
font-size:55px;
cursor:pointer;
transition:.3s;
}

.gift:hover{
transform:scale(1.3);
}

.hidden{
display:none;
}

iframe{
margin-top:20px;
border-radius:12px;
}

</style>
</head>

<body>

<!-- PASSWORD SCREEN -->

<div class="card" id="passwordScreen">
<h2>Enter Password 🔐</h2>
<p style="margin:10px 0;">(Hint: the day we met)</p>

<input id="pass"
type="password"
style="padding:10px;border-radius:10px;border:none;margin-top:10px;">

<br><br>

<button onclick="checkPass()">Enter</button>
</div>

<!-- COUNTDOWN -->

<div class="card hidden" id="countdownScreen">
<h2>Something special unlocks in...</h2>
<h1 id="count" style="font-size:55px;margin-top:10px;"></h1>
</div>

<!-- MAIN QUESTION -->

<div class="card hidden" id="main">
<h1>Will you be my Valentine? ❤️</h1>

<button class="yes" id="yes"
onclick="accepted()">YES</button>

<button class="no"
onclick="growYes()">No</button>

<div id="gifts" class="hidden">
<h2 style="margin-top:20px;">Pick a gift 🎁</h2>

<span class="gift" onclick="openGift('song')">🎧</span>
<span class="gift" onclick="openGift('choco')">🍫</span>
<span class="gift" onclick="openGift('msg')">💌</span>

<div id="song" class="hidden">
<iframe src="https://open.spotify.com/embed/track/2iRN7kWwHNtuzO6Q0VDoOR"
width="100%" height="152"></iframe>
</div>

</div>
</div>

<script>

let size=18;

function checkPass(){

if(document.getElementById("pass").value==="2204"){ // CHANGE THIS
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

document.getElementById("gifts").classList.remove("hidden");

confetti();
}

function openGift(type){

if(type==="song"){
document.getElementById("song").classList.remove("hidden");
}

if(type==="choco"){
alert("Chocolate coupon redeemed 🍫");
}

if(type==="msg"){
alert(`In your eyes, I have found a home where my soul finally feels at rest... I love you more than words could ever express.`);
}
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
