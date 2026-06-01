# latihan-soal
https://web-ujian-bahasa-indonesia.vercel.app
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Game Membangun Rumah 2D</title>

<style>
    body{
        margin:0;
        overflow:hidden;
        font-family:Arial;
        background:#87CEEB;
    }

    canvas{
        display:block;
        background:#87CEEB;
    }

    #ui{
        position:absolute;
        top:10px;
        left:10px;
        background:white;
        padding:10px;
        border-radius:10px;
        box-shadow:0 0 10px rgba(0,0,0,0.3);
    }

    button{
        margin:5px;
        padding:10px;
        border:none;
        background:#3498db;
        color:white;
        border-radius:5px;
        cursor:pointer;
    }

    button:hover{
        background:#2980b9;
    }
</style>
</head>
<body>

<div id="ui">
    <h3>🏠 Game Bangun Rumah 2D</h3>

    <button onclick="pilihBangunan('rumah')">Rumah</button>
    <button onclick="pilihBangunan('apartemen')">Apartemen</button>
    <button onclick="pilihBangunan('toko')">Toko</button>
    <button onclick="pilihBangunan('gedung')">Gedung</button>
    <button onclick="pilihBangunan('pohon')">Pohon</button>

    <p>Klik area game untuk membangun</p>
</div>

<canvas id="game"></canvas>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let bangunanDipilih = "rumah";

let objects = [];

function pilihBangunan(nama){
    bangunanDipilih = nama;
}

canvas.addEventListener("click", function(e){

    const rect = canvas.getBoundingClientRect();

    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;

    objects.push({
        type: bangunanDipilih,
        x: x,
        y: y
    });

});

function gambarTanah(){
    ctx.fillStyle = "#27ae60";
    ctx.fillRect(0, canvas.height - 150, canvas.width, 150);
}

function gambarRumah(x,y){

    // rumah
    ctx.fillStyle = "#e67e22";
    ctx.fillRect(x, y, 80, 60);

    // atap
    ctx.fillStyle = "#c0392b";
    ctx.beginPath();
    ctx.moveTo(x - 10, y);
    ctx.lineTo(x + 40, y - 40);
    ctx.lineTo(x + 90, y);
    ctx.closePath();
    ctx.fill();

    // pintu
    ctx.fillStyle = "#6e2c00";
    ctx.fillRect(x + 30, y + 30, 20, 30);
}

function gambarApartemen(x,y){

    ctx.fillStyle = "#7f8c8d";
    ctx.fillRect(x, y, 80, 140);

    ctx.fillStyle = "#ecf0f1";

    for(let i=0;i<4;i++){
        for(let j=0;j<3;j++){
            ctx.fillRect(x + 10 + j*20, y + 10 + i*30, 12, 18);
        }
    }
}

function gambarToko(x,y){

    ctx.fillStyle = "#f1c40f";
    ctx.fillRect(x, y, 100, 60);

    ctx.fillStyle = "#e74c3c";
    ctx.fillRect(x, y - 20, 100, 20);

    ctx.fillStyle = "black";
    ctx.font = "16px Arial";
    ctx.fillText("TOKO", x + 25, y + 15);
}

function gambarGedung(x,y){

    ctx.fillStyle = "#34495e";
    ctx.fillRect(x, y, 100, 220);

    ctx.fillStyle = "#f1c40f";

    for(let i=0;i<6;i++){
        for(let j=0;j<3;j++){
            ctx.fillRect(x + 15 + j*25, y + 10 + i*35, 15, 20);
        }
    }
}

function gambarPohon(x,y){

    // batang
    ctx.fillStyle = "#8e5a2b";
    ctx.fillRect(x + 10, y + 30, 20, 50);

    // daun
    ctx.fillStyle = "#2ecc71";
    ctx.beginPath();
    ctx.arc(x + 20, y + 20, 35, 0, Math.PI * 2);
    ctx.fill();
}

function update(){

    ctx.clearRect(0,0,canvas.width,canvas.height);

    gambarTanah();

    for(let obj of objects){

        if(obj.type === "rumah"){
            gambarRumah(obj.x, obj.y);
        }

        if(obj.type === "apartemen"){
            gambarApartemen(obj.x, obj.y);
        }

        if(obj.type === "toko"){
            gambarToko(obj.x, obj.y);
        }

        if(obj.type === "gedung"){
            gambarGedung(obj.x, obj.y);
        }

        if(obj.type === "pohon"){
            gambarPohon(obj.x, obj.y);
        }
    }

    requestAnimationFrame(update);
}

update();

window.addEventListener("resize", ()=>{

    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

});

</script>

</body>
</html>