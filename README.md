
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Game Bangun Rumah Interaktif - Ilman & Epit</title>
<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(#87ceeb, #ffffff);
    text-align: center;
}

header {
    background: #ff9800;
    color: white;
    padding: 15px;
}

.game-container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
}

.house {
    margin: 20px auto;
    width: 220px;
    height: 220px;
    position: relative;
    border-radius: 12px;
    background: #eee;
    overflow: hidden;
    border: 2px solid #555;
}

.part {
    position: absolute;
    display: none;
    opacity: 0;
    transition: all 0.5s ease;
}

.foundation { bottom: 0; width: 100%; height: 40px; background: #795548; }
.walls { bottom: 40px; width: 100%; height: 100px; background: #ffc107; }
.roof { top: -60px; width: 0; height: 0; border-left: 110px solid transparent; border-right: 110px solid transparent; border-bottom: 90px solid #f44336; }

.extra1 { top: 20px; left: 20px; width: 40px; height: 40px; background: #4caf50; border-radius: 6px; }
.extra2 { top: 20px; right: 20px; width: 40px; height: 40px; background: #2196f3; border-radius: 6px; }
.extra3 { bottom: 60px; left: 20px; width: 40px; height: 40px; background: #9c27b0; border-radius: 6px; }
.extra4 { bottom: 60px; right: 20px; width: 40px; height: 40px; background: #ffeb3b; border-radius: 6px; }
.extra6 { top: 80px; left: 80px; width: 40px; height: 40px; background: #ff5722; border-radius: 6px; }
.extra7 { top: 80px; right: 80px; width: 40px; height: 40px; background: #00bcd4; border-radius: 6px; }

button {
    padding: 10px 15px;
    margin: 5px;
    font-size: 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    background: #4caf50;
    color: white;
}

button:disabled { background: #aaa; }

footer { margin-top: 20px; font-size: 14px; color: #555; }

.house-epit { margin-top: 40px; border: 2px dashed #f44336; }

.turn {
    font-weight: bold;
    font-size: 18px;
    color: #333;
    margin-top: 10px;
}
</style>
</head>
<body>

<header>
    <h1>🏠 Game Bangun Rumah Interaktif</h1>
    <p>Ilman & Epit membangun rumah bersama</p>
</header>

<div class="game-container">
    <div class="turn" id="turnText">Giliran: Ilman</div>

    <h2>Rumah Ilman</h2>
    <div class="house" id="houseIlman">
        <div class="part foundation" id="foundation"></div>
        <div class="part walls" id="walls"></div>
        <div class="part roof" id="roof"></div>
        <div class="part extra1" id="extra1"></div>
        <div class="part extra2" id="extra2"></div>
        <div class="part extra3" id="extra3"></div>
        <div class="part extra4" id="extra4"></div>
        <div class="part extra6" id="extra6"></div>
        <div class="part extra7" id="extra7"></div>
    </div>

    <h2>Rumah Epit</h2>
    <div class="house house-epit" id="houseEpit">
        <div class="part foundation" id="foundationEpit"></div>
        <div class="part walls" id="wallsEpit"></div>
        <div class="part roof" id="roofEpit"></div>
    </div>

    <div id="buttonsContainer">
        <h3>Pilih bagian rumah:</h3>
        <button onclick="build('Ilman','foundation')">🔨 Pondasi Ilman</button>
        <button onclick="build('Ilman','walls')">🧱 Dinding Ilman</button>
        <button onclick="build('Ilman','roof')">🏠 Atap Ilman</button>
        <button onclick="build('Ilman','extra1')">🌳 Bagian 1</button>
        <button onclick="build('Ilman','extra2')">🌳 Bagian 2</button>
        <button onclick="build('Ilman','extra3')">🌳 Bagian 3</button>
        <button onclick="build('Ilman','extra4')">🌳 Bagian 4</button>
        <button onclick="build('Ilman','extra6')">🌳 Bagian 6</button>
        <button onclick="build('Ilman','extra7')">🌳 Bagian 7</button>

        <button onclick="build('Epit','foundationEpit')">🔨 Pondasi Epit</button>
        <button onclick="build('Epit','wallsEpit')">🧱 Dinding Epit</button>
        <button onclick="build('Epit','roofEpit')">🏠 Atap Epit</button>
    </div>

    <h3 id="status">Mulai bangun rumah!</h3>
</div>

<footer>
    🎮 Dibuat oleh <b>Ilman</b> & <b>Epit</b> <br>
    © 2026 Ilman Game Studio
</footer>

<audio id="sound">
    <source src="https://www.soundjay.com/buttons/sounds/button-16.mp3" type="audio/mpeg">
</audio>

<script>
const sound = document.getElementById("sound");
const statusText = document.getElementById("status");
const turnText = document.getElementById("turnText");

let currentTurn = 'Ilman'; // mulai dengan Ilman

function build(player, id) {
    if(player !== currentTurn){
        alert(`Sekarang giliran ${currentTurn}!`);
        return;
    }

    const part = document.getElementById(id);
    if(part.style.display === 'block') return;

    part.style.display = 'block';
    setTimeout(()=>part.style.opacity = 1,50);
    sound.play();

    statusText.innerText = `${player} membangun ${id}!`;

    // Ganti giliran
    currentTurn = (currentTurn === 'Ilman') ? 'Epit' : 'Ilman';
    turnText.innerText = `Giliran: ${currentTurn}`;
}
</script>

</body>
</html>
