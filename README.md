<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>DG MODZ</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial}
body{background:#000;color:#fff}

/* LOGIN */
#login{
position:fixed;
top:50%;left:50%;
transform:translate(-50%,-50%);
width:320px;
background:#0a0a0a;
border:2px solid #ff0000;
border-radius:14px;
padding:20px;
box-shadow:0 0 25px #ff0000;
}
#login h1{text-align:center;color:#ff0000}
#login input{
width:100%;
padding:10px;
margin:10px 0;
background:#000;
border:1px solid #ff0000;
color:#fff;
}
#login button{
width:100%;
padding:10px;
background:#ff0000;
border:none;
color:#fff;
font-weight:bold;
}

/* MENU */
#menu{
position:fixed;
top:70px;left:20px;
width:320px;
background:#050505;
border-radius:12px;
border:2px solid #ff0000;
box-shadow:0 0 30px #ff0000;
display:none;
}

/* HEADER */
#header{
background:#d10000;
padding:10px;
text-align:center;
font-weight:bold;
}

/* TABS */
#tabs{display:flex;background:#b00000}
.tab{
flex:1;
padding:8px;
text-align:center;
font-size:13px;
cursor:pointer;
}
.tab.active{background:#ff0000}

/* CONTENT */
.content{display:none;padding:12px}
.content.active{display:block}

/* OPTIONS */
.row{
display:flex;
justify-content:space-between;
align-items:center;
margin:10px 0;
}

/* TOGGLE */
.toggle{
width:40px;height:20px;
background:#333;
border-radius:20px;
position:relative;
cursor:pointer;
}
.toggle::after{
content:"";
width:16px;height:16px;
background:red;
border-radius:50%;
position:absolute;
top:2px;left:2px;
transition:.2s;
}
.toggle.on{background:#0a0}
.toggle.on::after{
left:22px;
background:#0f0;
}

/* RANGE */
input[type=range]{width:100%}

/* FOOTER */
.footer{
text-align:center;
padding:8px;
color:#00ff66;
border-top:1px solid #400;
}

/* MINIMIZAR */
.minBtn{
width:100%;
padding:6px;
background:#eee;
border:none;
margin-top:8px;
font-weight:bold;
}

/* BOTÃO ABRIR */
#open{
position:fixed;
bottom:20px;right:20px;
width:55px;height:55px;
border-radius:50%;
background:red;
color:#fff;
font-size:22px;
border:none;
box-shadow:0 0 15px red;
display:none;
}

/* BOLINHA */
#bubble{
position:fixed;
width:56px;height:56px;
border-radius:50%;
background:radial-gradient(circle,#c084ff,#5b00cc);
display:none;
align-items:center;
justify-content:center;
font-weight:bold;
color:#fff;
box-shadow:0 0 20px #c084ff;
animation:glow 1.5s infinite alternate;
cursor:pointer;
z-index:9999;
user-select:none;
}
@keyframes glow{
from{box-shadow:0 0 10px #a96bff}
to{box-shadow:0 0 30px #e1c2ff}
}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="login">
<h1>DG MODZ</h1>
<input id="keyInput" placeholder="Digite sua KEY">
<button onclick="loginKey()">ENTRAR</button>
</div>

<!-- BOTÃO MENU -->
<button id="open" onclick="toggleMenu()">≡</button>

<!-- MENU -->
<div id="menu">
<div id="header">DG MODZ • FREE FIRE</div>

<div id="tabs">
<div class="tab active" onclick="openTab(0)">AIM</div>
<div class="tab" onclick="openTab(1)">ESP</div>
<div class="tab" onclick="openTab(2)">MISC</div>
<div class="tab" onclick="openTab(3)">SUP</div>
<div class="tab" onclick="openTab(4)">INFO</div>
</div>

<div class="content active">
<div class="row"><span>Aimbot</span><div class="toggle" onclick="tg(this)"></div></div>
<label>FOV</label>
<input type="range" min="0" max="360">
</div>

<div class="content">
<div class="row"><span>ESP Line</span><div class="toggle" onclick="tg(this)"></div></div>
<div class="row"><span>ESP Box</span><div class="toggle" onclick="tg(this)"></div></div>
</div>

<div class="content">
<div class="row"><span>No Recoil</span><div class="toggle" onclick="tg(this)"></div></div>
<div class="row"><span>Teleport 8m</span><div class="toggle" onclick="tg(this)"></div></div>
</div>

<div class="content">
<p>Suporte em breve</p>
</div>

<div class="content">
<p>DG MODZ</p>
<p>Status: ATIVO</p>
</div>

<button class="minBtn" onclick="minimize()">MINIMIZAR</button>
<div class="footer">STATUS: ACTIVE</div>
</div>

<!-- BOLINHA -->
<div id="bubble"
ontouchstart="startDrag(event)"
onmousedown="startDrag(event)"
onclick="restore()">DG</div>

<script>
/* KEY PADRÃO */
if(!localStorage.getItem("dg_keys")){
localStorage.setItem("dg_keys",JSON.stringify([
{code:"DG-123",expire:Date.now()+30*86400000}
]));
}

/* LOGIN */
function loginKey(){
let keys=JSON.parse(localStorage.getItem("dg_keys"));
let k=keys.find(x=>x.code===keyInput.value);
if(!k) return alert("KEY inválida");
if(Date.now()>k.expire) return alert("KEY expirada");

login.style.display="none";
open.style.display="block";
}

/* MENU */
function toggleMenu(){
menu.style.display=menu.style.display==="block"?"none":"block";
}

/* TABS */
function openTab(i){
document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
document.querySelectorAll('.content').forEach(c=>c.classList.remove('active'));
document.querySelectorAll('.tab')[i].classList.add('active');
document.querySelectorAll('.content')[i].classList.add('active');
}

/* TOGGLE */
function tg(el){el.classList.toggle("on")}

/* MINIMIZAR */
function minimize(){
menu.style.display="none";
bubble.style.display="flex";
}

/* RESTORE */
function restore(){
bubble.style.display="none";
menu.style.display="block";
}

/* BOLINHA DRAG + MAGNET */
let drag=false,ox=0,oy=0;
const saved=JSON.parse(localStorage.getItem("dg_bubble"));
if(saved){
bubble.style.left=saved.x+"px";
bubble.style.top=saved.y+"px";
}else{
bubble.style.right="20px";
bubble.style.bottom="90px";
}

function startDrag(e){
drag=true;
const ev=e.touches?e.touches[0]:e;
ox=ev.clientX-bubble.offsetLeft;
oy=ev.clientY-bubble.offsetTop;
document.onmousemove=move;
document.ontouchmove=move;
document.onmouseup=end;
document.ontouchend=end;
}

function move(e){
if(!drag)return;
const ev=e.touches?e.touches[0]:e;
bubble.style.left=(ev.clientX-ox)+"px";
bubble.style.top=(ev.clientY-oy)+"px";
bubble.style.right="auto";
bubble.style.bottom="auto";
}

function end(){
drag=false;
let x=bubble.offsetLeft;
let y=bubble.offsetTop;
const w=innerWidth;
const h=innerHeight;

x = x < w/2 ? 6 : w - bubble.offsetWidth - 6;
y = Math.max(6, Math.min(y, h - bubble.offsetHeight - 6));

bubble.style.left=x+"px";
bubble.style.top=y+"px";

localStorage.setItem("dg_bubble",JSON.stringify({x,y}));
}
</script>

</body>
</html>
