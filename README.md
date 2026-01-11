
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ultimate 3D Mini Rumah Interaktif</title>
<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(#87ceeb,#ffffff);
    overflow: hidden;
    text-align: center;
    perspective: 1200px;
}

header {
    background: #ff9800;
    color: white;
    padding: 15px;
}

.game-container {
    max-width: 900px;
    margin: auto;
    padding: 20px;
}

.turn { font-weight:bold; font-size:18px; margin-top:10px; }

/* Scene 3D rumah */
.house-scene {
    width: 400px;
    height: 400px;
    margin: 30px auto;
    position: relative;
    transform-style: preserve-3d;
    cursor: grab;
}

.house-container {
    width: 100%;
    height: 100%;
    position: relative;
    transform-style: preserve-3d;
    transition: transform 0.5s;
}

/* Pondasi */
.foundation { width:200px;height:40px;background:#8b5e3c;bottom:0;left:100px;position:absolute; }

/* Dinding 3D */
.wall { width:200px;height:150px;background:#f5deb3;bottom:40px;position:absolute; transform-origin:bottom; }
.wall-front { transform:rotateY(0deg) translateZ(100px); left:100px; }
.wall-back { transform:rotateY(180deg) translateZ(100px); left:100px; }
.wall-left { width:200px;height:150px;transform:rotateY(-90deg) translateZ(100px); left:0; bottom:40px; }
.wall-right { width:200px;height:150px;transform:rotateY(90deg) translateZ(100px); left:300px; bottom:40px; }

/* Atap */
.roof { width:0;height:0;border-left:120px solid transparent;border-right:120px solid transparent;border-bottom:80px solid #b22222;left:80px;bottom:190px;position:absolute; }

/* Ventilasi */
.vent { width:20px;height:10px;background:#333; left:170px; bottom:200px; position:absolute; }

/* Pintu & Jendela */
.door { width:50px;height:70px;background:#654321; left:175px; bottom:40px; position:absolute; }
.window1,.window2 { width:50px;height:50px;background:#87cefa; border:2px solid #000; cursor:pointer; position:absolute; }
.window1 { left:120px; bottom:100px; } .window2 { left:230px; bottom:100px; }
.window-open { transform: translateX(20px); transition:transform 0.5s; }

/* Lampu berbeda di jendela */
.light1,.light2 { width:10px;height:10px;border-radius:50%;background:yellow; position:absolute; left:135px; bottom:115px; opacity:0; }
.light2 { left:245px; }

/* Interior mini */
.interior { width:160px;height:120px;background:#eee; left:120px; bottom:40px; position:absolute; border:1px solid #ccc; display:none; }

/* Karakter mini */
.npc { width:20px;height:20px;background:red; border-radius:50%; position:absolute; bottom:40px; left:50px; animation:walk 5s infinite alternate; }
@keyframes walk { 0% { left:50px;} 100% { left:330px;} }

/* Pohon bergoyang */
.tree { position:absolute;width:20px;height:50px;background:#8b5e3c; bottom:0;border-radius:5px; animation:sway 3s infinite alternate; }
.tree::after { content:"";position:absolute;width:40px;height:40px;background:green;border-radius:50%;top:-35px;left:-10px; }
@keyframes sway {0%{transform:rotate(-5deg);}50%{transform:rotate(5deg);}100%{transform:rotate(-5deg);}}

/* Jalan mini */
.path { position:absolute;width:50px;height:120px;background:#ccc; bottom:0; left:175px; border-radius:10px; }

/* Hujan & Salju */
.rain,.snow { position:absolute;width:100%;height:100%;top:0;left:0;pointer-events:none; }
.drop { position:absolute;width:2px;height:10px;background:#0cf; animation:fall 1s linear infinite; }
.snowflake { position:absolute;width:5px;height:5px;background:white;border-radius:50%;animation:snowFall 3s linear infinite;}
@keyframes fall{0%{top:-10px;}100%{top:100%;}}
@keyframes snowFall{0%{top:-10px;}100%{top:100%;}}

button{padding:10px 15px;margin:5px;font-size:16px;border:none;border-radius:8px;cursor:pointer;background:#4caf50;color:white;}
.color-picker{margin:10px 0;}
</style>
</head>
<body>

<header>
<h1>🏡 Ultimate 3D Mini Rumah Interaktif</h1>
<p>Ilman & Epit membangun rumah</p>
</header>

<div class="game-container">
<div class="turn" id="turnText">Giliran: Ilman</div>

<div class="house-scene" id="houseScene">
<div class="house-container" id="houseContainer">
<div class="house-part foundation" id="foundation"></div>
<div class="house-part wall wall-front" id="wallFront"></div>
<div class="house-part wall wall-back" id="wallBack"></div>
<div class="house-part wall wall-left" id="wallLeft"></div>
<div class="house-part wall wall-right" id="wallRight"></div>
<div class="house-part roof" id="roof"></div>
<div class="house-part vent" id="vent"></div>
<div class="house-part door" id="door"></div>
<div class="house-part window1" id="window1"></div>
<div class="house-part window2" id="window2"></div>
<div class="house-part light1" id="light1"></div>
<div class="house-part light2" id="light2"></div>
<div class="house-part interior" id="interior"></div>
<div class="house-part tree" id="tree1" style="left:-40px;"></div>
<div class="house-part tree" id="tree2" style="left:350px;"></div>
<div class="house-part path" id="path"></div>
<div class="npc" id="npc"></div>
</div>
</div>

<div id="buttonsContainer">
<h3>Pilih bagian rumah:</h3>
<button onclick="build('foundation')">🔨 Pondasi</button>
<button onclick="build('wallFront')">🧱 Dinding Depan</button>
<button onclick="build('wallBack')">🧱 Dinding Belakang</button>
<button onclick="build('wallLeft')">🧱 Dinding Kiri</button>
<button onclick="build('wallRight')">🧱 Dinding Kanan</button>
<button onclick="build('roof')">🏠 Atap</button>
<button onclick="build('vent')">🌀 Ventilasi</button>
<button onclick="build('door')">🚪 Pintu</button>
<button onclick="build('window1')">🪟 Jendela 1</button>
<button onclick="build('window2')">🪟 Jendela 2</button>
<button onclick="build('tree1')">🌳 Pohon Kiri</button>
<button onclick="build('tree2')">🌳 Pohon Kanan</button>
<button onclick="build('path')">🛤 Jalan</button>
<button onclick="toggleInterior()">🏠 Masuk Rumah</button>
<button onclick="toggleLights()">💡 Nyalakan Lampu</button>
<button onclick="toggleRain()">🌧️ Hujan</button>
<button onclick="toggleSnow()">❄️ Salju</button>
</div>

<h3 id="status">Mulai bangun rumah!</h3>
</div>

<footer>🎮 Dibuat oleh <b>Ilman</b> & <b>Epit</b> | © 2026 Ilman Game Studio</footer>

<audio id="sound"><source src="https://www.soundjay.com/buttons/sounds/button-16.mp3" type="audio/mpeg"></audio>

<script>
const sound=document.getElementById('sound');
const turnText=document.getElementById('turnText');
const statusText=document.getElementById('status');
let currentTurn='Ilman';
let house=document.getElementById('houseContainer');

// Drag rotation
let isDragging=false, prevX=0, rotY=0;
document.getElementById("houseScene").addEventListener('mousedown', e=>{isDragging=true; prevX=e.clientX;});
document.addEventListener('mouseup', ()=>isDragging=false);
document.addEventListener('mousemove', e=>{
    if(!isDragging) return;
    let deltaX=e.clientX-prevX;
    rotY += deltaX*0.5;
    house.style.transform=`rotateY(${rotY}deg) rotateX(20deg)`;
    prevX=e.clientX;
});

// Build function
function build(id){
    const part=document.getElementById(id);
    if(part.style.opacity==1) return;
    part.style.display='block'; part.style.opacity=0;
    setTimeout(()=>part.style.opacity=1,50);

    if(id==='window1'||id==='window2'){ part.onclick=()=>part.classList.toggle('window-open'); }
    sound.play();
    statusText.innerText=`${currentTurn} membangun ${id}!`;
    currentTurn=currentTurn==='Ilman'?'Epit':'Ilman';
    turnText.innerText=`Giliran: ${currentTurn}`;
}

// Toggle interior
function toggleInterior(){
    let interior=document.getElementById('interior');
    interior.style.display=interior.style.display==='block'?'none':'block';
}

// Toggle lights
function toggleLights(){
    let l1=document.getElementById('light1');
    let l2=document.getElementById('light2');
    l1.style.opacity=l1.style.opacity==1?0:1;
    l2.style.opacity=l2.style.opacity==1?0:1;
}

// Hujan
let raining=false;
function toggleRain(){
    if(raining){document.querySelectorAll('.rain').forEach(e=>e.remove()); raining=false; return;}
    raining=true;
    for(let i=0;i<100;i++){
        let drop=document.createElement('div');
        drop.className='drop rain';
        drop.style.left=Math.random()*window.innerWidth+'px';
        drop.style.animationDuration=(0.5+Math.random()*0.5)+'s';
        document.body.appendChild(drop);
    }
}

// Salju
let snowing=false;
function toggleSnow(){
    if(snowing){document.querySelectorAll('.snowflake').forEach(e=>e.remove()); snowing=false; return;}
    snowing=true;
    for(let i=0;i<100;i++){
        let flake=document.createElement('div');
        flake.className='snowflake snow';
        flake.style.left=Math.random()*window.innerWidth+'px';
        flake.style.animationDuration=(2+Math.random()*2)+'s';
        document.body.appendChild(flake);
    }
}
</script>

</body>
</html>
