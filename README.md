
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rumah Interaktif Responsif</title>
<style>
* {box-sizing:border-box; margin:0; padding:0;}
body {
    font-family: Arial, sans-serif;
    background: linear-gradient(#87ceeb,#fff);
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:flex-start;
    min-height:100vh;
}

header {
    background:#ff9800;
    color:white;
    padding:15px;
    width:100%;
    text-align:center;
}

.game-container {
    max-width:800px;
    width:95%;
    margin-top:20px;
    position:relative;
}

/* Rumah */
.house {
    width:100%;
    max-width:400px;
    margin:auto;
    position:relative;
}

/* Pondasi & dinding */
.foundation {height:50px; background:#8b5e3c; width:100%; border-radius:5px;}
.wall {height:200px; background:#f5deb3; width:100%; position:relative; top:-50px; border-radius:5px;}

/* Atap */
.roof {
    width:0; height:0;
    border-left:50% solid transparent;
    border-right:50% solid transparent;
    border-bottom:80px solid #b22222;
    position:relative;
    margin:auto;
}

/* Pintu & jendela */
.door {width:80px;height:120px;background:#654321; position:absolute; bottom:50px; left:50%; transform:translateX(-50%);}
.window {width:60px;height:60px;background:#87cefa; border:2px solid #000; position:absolute; cursor:pointer; border-radius:5px;}
.window1 {left:20%; top:50px;} .window2 {right:20%; top:50px;}
.window.open {background:#b0e0e6;}

/* Lampu jendela */
.light {width:15px;height:15px;background:yellow;border-radius:50%;position:absolute; top:55px; left:23%; display:none;}
.light2 {left:73%;}

/* Interior mini */
.interior {width:80%; height:150px; background:#eee; position:relative; margin:10px auto; border:1px solid #ccc; display:none; border-radius:5px; padding:10px;}
.interior h4 {text-align:center; margin-bottom:10px;}

/* Pohon */
.tree {width:20px; height:60px; background:#8b5e3c; border-radius:5px; display:inline-block; margin:0 20px; position:relative;}
.tree::after {content:""; width:50px; height:50px; background:green; border-radius:50%; position:absolute; top:-35px; left:-15px; animation:sway 3s infinite alternate;}
@keyframes sway {0%{transform:rotate(-5deg);}50%{transform:rotate(5deg);}100%{transform:rotate(-5deg);}}

/* Jalan */
.path {width:60px; height:120px; background:#ccc; margin:10px auto; border-radius:10px;}

/* NPC */
.npc {width:30px;height:30px;background:red;border-radius:50%;position:absolute; bottom:0; animation:walk 4s infinite alternate;}
@keyframes walk {0%{left:0;}100%{left:calc(100% - 30px);}}

/* Responsif */
@media(max-width:600px){
    .roof {border-left:45% solid transparent; border-right:45% solid transparent; border-bottom:60px solid #b22222;}
    .door {width:60px;height:90px;}
    .window {width:40px;height:40px;}
}
button {padding:10px 15px; margin:5px; font-size:16px; border:none; border-radius:8px; cursor:pointer; background:#4caf50; color:white;}
</style>
</head>
<body>

<header>
<h1>🏡 Rumah Interaktif Responsif</h1>
<p>Ilman & Epit membangun rumah</p>
</header>

<div class="game-container">

<div class="house">
    <div class="roof"></div>
    <div class="wall">
        <div class="door" id="door"></div>
        <div class="window window1" id="window1"></div>
        <div class="window window2" id="window2"></div>
        <div class="light" id="light1"></div>
        <div class="light light2" id="light2"></div>
    </div>
    <div class="foundation"></div>
</div>

<div class="interior" id="interior">
<h4>Ruang Tamu Mini</h4>
<p>Sofa, meja, dan karpet tersedia!</p>
</div>

<div class="trees">
<div class="tree"></div>
<div class="tree"></div>
</div>

<div class="path"></div>
<div class="npc" id="npc"></div>

<div>
<button onclick="toggleInterior()">🏠 Masuk Rumah</button>
<button onclick="toggleLights()">💡 Nyalakan Lampu</button>
</div>

</div>

<script>
// Jendela interaktif
document.getElementById('window1').onclick=function(){this.classList.toggle('open');}
document.getElementById('window2').onclick=function(){this.classList.toggle('open');}

// Toggle interior
function toggleInterior(){
    const interior=document.getElementById('interior');
    interior.style.display=interior.style.display==='block'?'none':'block';
}

// Toggle lampu
function toggleLights(){
    const l1=document.getElementById('light1');
    const l2=document.getElementById('light2');
    l1.style.display=l1.style.display==='block'?'none':'block';
    l2.style.display=l2.style.display==='block'?'none':'block';
}
</script>

</body>
</html>
