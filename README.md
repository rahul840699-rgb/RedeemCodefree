<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Scratch & Redeem – Premium</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif}
body{
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    background:linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    color:#fff;
}
.wrapper{
    width:100%;
    max-width:420px;
    padding:15px;
}
.ad{
    background:#020617;
    border:1px dashed #334155;
    border-radius:12px;
    padding:15px;
    text-align:center;
    font-size:13px;
    color:#94a3b8;
    margin-bottom:15px;
}
.container{
    background:#111827;
    padding:22px;
    border-radius:20px;
    box-shadow:0 25px 60px rgba(0,0,0,.45);
    text-align:center;
}
.logo{
    font-size:22px;
    font-weight:700;
}
.tagline{
    font-size:13px;
    color:#9ca3af;
    margin-bottom:15px;
}
.card{
    position:relative;
    width:100%;
    height:160px;
    border-radius:15px;
    overflow:hidden;
    background:linear-gradient(135deg,#fde68a,#f59e0b);
}
.code{
    position:absolute;
    inset:0;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:26px;
    font-weight:700;
    color:#111;
    letter-spacing:3px;
}
canvas{
    position:absolute;
    inset:0;
    cursor:pointer;
}
.info{
    margin:12px 0;
    font-size:13px;
    color:#9ca3af;
}
.actions{
    display:none;
    gap:10px;
    margin-top:10px;
}
.btn{
    flex:1;
    padding:11px;
    border:none;
    border-radius:10px;
    font-size:14px;
    font-weight:600;
    cursor:pointer;
    transition:.3s;
}
.copy{
    background:linear-gradient(135deg,#22c55e,#16a34a);
    color:#052e16;
}
.new{
    background:linear-gradient(135deg,#3b82f6,#2563eb);
    color:#fff;
}
.btn:hover{
    transform:translateY(-2px);
}
.footer{
    margin-top:14px;
    font-size:11px;
    color:#6b7280;
}
@media(min-width:768px){
    .wrapper{max-width:460px}
}
</style>
</head>

<body>

<div class="wrapper">

    <div class="ad">Ad Space (728×90 / 320×50)</div>

    <div class="container">
        <div class="logo">Premium Rewards</div>
        <div class="tagline">Scratch to reveal & copy your code</div>

        <div class="card">
            <div class="code" id="redeemCode">X7P9-AK2M-Q8Z</div>
            <canvas id="scratch"></canvas>
        </div>

        <div class="info">Scratch completely to unlock copy option</div>

        <div class="actions" id="actions">
            <button class="btn copy" onclick="copyCode()">Copy Code</button>
            <button class="btn new" onclick="resetScratch()">New Code</button>
        </div>

        <div class="footer">© 2026 Premium Redeem</div>
    </div>

    <div class="ad">Ad Space (Native / Rectangle)</div>

</div>

<script>
const canvas = document.getElementById("scratch");
const ctx = canvas.getContext("2d");
const card = document.querySelector(".card");
const actions = document.getElementById("actions");

function resizeCanvas(){
    canvas.width = card.offsetWidth;
    canvas.height = card.offsetHeight;
    ctx.globalCompositeOperation="source-over";
    ctx.fillStyle="#9ca3af";
    ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.globalCompositeOperation="destination-out";
    actions.style.display="none";
}
resizeCanvas();
window.addEventListener("resize",resizeCanvas);

let drawing=false;
let scratched=0;

canvas.addEventListener("mousedown",()=>drawing=true);
canvas.addEventListener("mouseup",()=>drawing=false);
canvas.addEventListener("mousemove",scratch);

canvas.addEventListener("touchstart",()=>drawing=true);
canvas.addEventListener("touchend",()=>drawing=false);
canvas.addEventListener("touchmove",scratch);

function scratch(e){
    if(!drawing) return;
    const rect=canvas.getBoundingClientRect();
    const x=(e.clientX||e.touches[0].clientX)-rect.left;
    const y=(e.clientY||e.touches[0].clientY)-rect.top;
    ctx.beginPath();
    ctx.arc(x,y,18,0,Math.PI*2);
    ctx.fill();
    scratched++;
    if(scratched>120){
        actions.style.display="flex";
    }
}

function copyCode(){
    const code=document.getElementById("redeemCode").innerText;
    navigator.clipboard.writeText(code);
    alert("Redeem code copied!");
}

function resetScratch(){
    const chars="ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
    let code="";
    for(let i=0;i<12;i++){
        code+=chars[Math.floor(Math.random()*chars.length)];
        if(i==3||i==7) code+="-";
    }
    document.getElementById("redeemCode").innerText=code;
    scratched=0;
    resizeCanvas();
}
</script>

</body>
</html>
