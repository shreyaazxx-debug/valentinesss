<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valentine 💗</title>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:'Poppins',sans-serif;
}
body{
  background:#ffc0d9;
  overflow:hidden;
  text-align:center;
}
.page{
  display:none;
  width:100vw;
  height:100vh;
  padding:20px;
  position:absolute;
  inset:0;
  justify-content:center;
  align-items:center;
  flex-direction:column;
}
.show{display:flex}

h1,h2,p{color:#b30059}

button{
  padding:12px 24px;
  font-size:16px;
  border:none;
  border-radius:30px;
  background:#ff4da6;
  color:white;
  margin:10px;
  cursor:pointer;
}
.secondary{background:#ff99cc}

/* YES / NO */
#btnRow{
  display:flex;
  gap:24px;
  margin-top:20px;
}
#noBtn{position:relative}

/* FALLING HEARTS */
.heart{
  position:fixed;
  top:-10px;
  font-size:22px;
  animation:fall linear infinite;
}
@keyframes fall{
  to{transform:translateY(110vh)}
}

/* GIFTS */
.gifts{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:20px;
}
.gift{
  height:110px;
  background:#ff66b2;
  border-radius:16px;
  display:flex;
  align-items:center;
  justify-content:center;
  font-size:42px;
  cursor:pointer;
}

/* IMAGE VIEW */
#giftImg{
  max-width:95%;
  max-height:70vh;
  border-radius:18px;
}

/* NAV */
.photoNav{
  display:flex;
  gap:20px;
  margin-top:15px;
}

/* SONG PAGE */
#bigHeart{
  font-size:120px;
  animation:pulse 1.5s infinite;
  margin:20px 0;
}
@keyframes pulse{
  0%{transform:scale(1)}
  50%{transform:scale(1.2)}
  100%{transform:scale(1)}
}

iframe{
  border:none;
  width:100%;
  max-width:420px;
  height:80px;
  background:transparent;
}

/* FADE */
.fadeOut{animation:fade 3s forwards}
@keyframes fade{to{opacity:0}}
</style>
</head>

<body>

<!-- PAGE 1 -->
<div class="page show" id="p1">
  <h1>Utkarsha 💖</h1>
  <p>Will you be my Valentine?</p>
  <div id="btnRow">
    <button onclick="go('p2')">Yes</button>
    <button id="noBtn">No</button>
  </div>
</div>

<!-- PAGE 2 -->
<div class="page" id="p2">
  <h1>WUHU 🥰</h1>
  <p>I knew you'd say yes</p>
  <button onclick="go('p3')">Shall we move forward?</button>
</div>

<!-- PAGE 3 -->
<div class="page" id="p3">
  <h2>Gifts for my pasandeeta aurat 💝</h2>
  <button onclick="go('p4')">Tap to open</button>
</div>

<!-- PAGE 4 -->
<div class="page" id="p4">
  <h2>⚠️ Warning</h2>
  <p>Extreme happiness incoming</p>
  <button onclick="go('p5')">Tap to continue</button>
</div>

<!-- PAGE 5 -->
<div class="page" id="p5">
  <h2>Looks like you have 4 gifts my love 🎁</h2>
  <div class="gifts">
    <div class="gift" onclick="openGift(0)">🎁</div>
    <div class="gift" onclick="openGift(1)">🎁</div>
    <div class="gift" onclick="openGift(2)">🎁</div>
    <div class="gift" onclick="openGift(3)">🎁</div>
  </div>
</div>

<!-- IMAGE PAGE -->
<div class="page" id="imgPage">
  <img id="giftImg">
  <div class="photoNav">
    <button class="secondary" onclick="prevGift()">⬅ Prev</button>
    <button onclick="nextGift()">Next ➡</button>
  </div>
</div>

<!-- SONG PAGE -->
<div class="page" id="songPage">
  <h2>For you 💗</h2>

  <div id="bigHeart">💖</div>

  <iframe
    id="songPlayer"
    src=""
    allow="autoplay">
  </iframe>

  <button id="songNextBtn" style="display:none" onclick="go('final')">
    Continue ❤️
  </button>
</div>

<!-- FINAL -->
<div class="page" id="final">
  <h1>I really love you 💗</h1>
  <p>Stay with me forever</p>
  <button onclick="forever()">Forever?</button>
</div>

<script>
function go(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('show'));
  document.getElementById(id).classList.add('show');
}

/* NO BUTTON ESCAPE */
const noBtn=document.getElementById('noBtn');
function moveNo(){
  noBtn.style.position='absolute';
  noBtn.style.left=Math.random()*60+20+'vw';
  noBtn.style.top=Math.random()*50+30+'vh';
}
noBtn.onmouseover=moveNo;
noBtn.ontouchstart=moveNo;

/* GIFTS */
const gifts=[
 "https://lh3.googleusercontent.com/d/1UB-n42axYw27vApv5e1VPcS931c5X6At",
 "https://lh3.googleusercontent.com/d/1pWizK05Ildwxmm16clbvpdX_vZcXJsie",
 "https://lh3.googleusercontent.com/d/11vEHG0WjQIb87Xt61TVC2xnclFlCknkD",
 "https://lh3.googleusercontent.com/d/1qckg38aUepPPL8spNDZSN731nhGlUw27"
];

let cur=0;
const img=document.getElementById('giftImg');

function openGift(i){
  cur=i;
  img.src=gifts[cur];
  go('imgPage');
}

function nextGift(){
  if(cur===gifts.length-1){
    go('songPage');
    startSong();
  }else{
    cur++;
    img.src=gifts[cur];
  }
}

function prevGift(){
  if(cur>0){
    cur--;
    img.src=gifts[cur];
  }
}

/* SONG AUTO START */
function startSong(){
  const iframe=document.getElementById('songPlayer');
  const nextBtn=document.getElementById('songNextBtn');

  iframe.src =
    "https://drive.google.com/file/d/1X8LdbqlkSC02i33pI5NVIackHwq8NwFe/preview?autoplay=1";

  nextBtn.style.display="none";

  // ⏱️ Adjust this to EXACT song length (ms)
  setTimeout(()=>{
    nextBtn.style.display="inline-block";
  }, 180000); // 3 minutes
}

/* FINAL */
function forever(){
  document.body.classList.add('fadeOut');
  setTimeout(()=>{
    document.body.innerHTML =
      "<h1 style='margin-top:40vh;color:#b30059'>Us. Always. 💗</h1>";
  },3000);
}

/* FALLING HEARTS */
setInterval(()=>{
  const h=document.createElement('div');
  h.className='heart';
  h.innerText='💗';
  h.style.left=Math.random()*100+'vw';
  h.style.animationDuration=(Math.random()*3+2)+'s';
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),5000);
},250);
</script>

</body>
</html>
