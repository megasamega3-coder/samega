# Raasi
samega
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Raasi Unlock Magic ✨</title>
<style>
  body {
    font-family: "Poppins", sans-serif;
    background: #0f0f4a;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 20px;
    min-height: 100vh;
  }

  .card {
    background: rgba(255,255,255,0.1);
    backdrop-filter: blur(8px);
    padding: 22px;
    width: 350px;
    border-radius: 18px;
    box-shadow: 0 8px 30px rgba(0,0,0,0.5);
    text-align: center;
    margin-bottom: 20px;
    transition: transform 0.3s ease;
  }
  .card:hover { transform: translateY(-7px); }

  select, button {
    padding: 12px 18px;
    border-radius: 10px;
    border: none;
    margin: 10px 0;
    cursor: pointer;
    font-size: 15px;
    font-weight: bold;
    transition: 0.3s ease;
  }

  button:hover:not(:disabled) {
    transform: scale(1.07);
    box-shadow: 0 0 15px rgba(255,255,255,0.7);
  }

  button:disabled {
    background: #555;
    cursor: not-allowed;
  }

  #goInstagramBtn {
    background: #e1306c;
    color: #fff;
  }

  #unlockPredictionBtn {
    background: #ffdb4d;
    color: #000;
  }

  #progressBar {
    width: 0%;
    height: 6px;
    background: #00ff9d;
    border-radius: 6px;
    margin-top: 6px;
    transition: width 0.1s ease;
  }

  #fullPrediction {
    display: none;
    margin-top: 15px;
  }

  .spark {
    position: absolute;
    border-radius: 50%;
    pointer-events: none;
    animation: sparkAnim 1s ease-out infinite;
  }
  @keyframes sparkAnim {
    0% { transform: scale(1); opacity: 1;}
    50% { transform: scale(1.7); opacity: 0.5;}
    100% { opacity: 0; transform: scale(0);}
  }

  /* Modal style */
  #socialModal {
    display:none; 
    background: rgba(0,0,0,0.85); 
    color:#fff; 
    padding:20px; 
    border-radius:12px; 
    text-align:center; 
    position:fixed; 
    top:50%; 
    left:50%; 
    transform:translate(-50%,-50%); 
    z-index:10;
    width: 280px;
    font-weight: bold;
  }

  #socialModal button {
    margin-top: 12px;
    background:#00ff9d; 
    color:#000;
    padding:10px 15px;
    border:none; 
    border-radius:8px;
    cursor:pointer;
    font-weight:bold;
  }

</style>
</head>
<body>

<div class="card">
  <h2>🔮 Choose Your Raasi</h2>
  <select id="raasiSelect">
    <option value="">-- Select Raasi --</option>
  </select>
  <p id="teaser">Pick your Raasi to see a fun hint!</p>

  <button id="readMoreBtn">Read More</button>

  <div id="unlockSection" style="display:none;">
    <button id="goInstagramBtn">Go to Instagram</button>
    <div id="progressBar"></div>
    <button id="unlockPredictionBtn" disabled>Unlock Full Prediction</button>
  </div>
</div>

<div id="fullPrediction" class="card">
  <h2>✨ Your Raasi Insight</h2>
  <pre id="predictionContent"></pre>
</div>

<!-- Social modal -->
<div id="socialModal">
  <p>👍 Like / 💬 Comment / 🔁 Share on Instagram</p>
  <button id="modalDoneBtn">Done</button>
</div>

<canvas id="confetti"></canvas>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
<script>
const raasiData = {
"Mesham": { short:"First in zodiac – “I go first!” 🏃‍♂️", full:`Mesham (Aries / மேஷம்)
Fire sign – hot-headed 🔥
Symbol: Ram – charges at life 🐏
Energy = infinite, coffee optional ☕⚡
Impulsive – “Oops… did I just do that?” 😅
Motto: “Life is short, run fast & roar loud!” 🏆`, element:'fire' },
"Rishabham": { short:"Chill but stubborn 😤", full:`Rishabham (Taurus / ரிஷபம்)
Earth sign – grounded 🌍
Loyal & comfy 🍲😴
Money & security = top priority 💰
Motto: “Slow and steady… but don’t rush me!” 🐌`, element:'earth' },
"Mithunam": { short:"Twins – two minds 😵", full:`Mithunam (Gemini / மிதுனம்)
Air sign – social butterfly 🦋
Curious & chatty 💬
Flexible – “I can do anything, maybe”
Motto: “Life = try everything once!” 🎉`, element:'air' },
"Karkatakam": { short:"Crab vibes – shell on 🦀", full:`Karkatakam (Cancer / கடகம்)
Water sign – emotions 🌊
Protective 🛡️
Home & family = ❤️
Motto: “Home is where my heart & snacks are”`, element:'water' },
"Simham": { short:"Lion – roar first 🦁", full:`Simham (Leo / சிம்மம்)
Fire sign – fiery 🔥
Confident 😎
Creative & bold 💖
Motto: “If life is a stage, I own it!” 🎤`, element:'fire' },
"Kanni": { short:"Maiden – neat freak 🧹", full:`Kanni (Virgo / கன்னி)
Earth sign – practical 🌍
Perfectionist 🌈
Works hard, complains harder
Motto: “Chaos? Not in my house!” 🏠`, element:'earth' },
"Thulam": { short:"Scales – balancing ⚖️", full:`Thulam (Libra / துலாம்)
Air sign – social 🌬️
Polite & diplomatic 😏
Friendship = life goal 🤝
Motto: “Life is too short for bad vibes!” 🌈`, element:'air' },
"Vrischikam": { short:"Scorpion – intense 🦂", full:`Vrischikam (Scorpio / விருச்சிகம்)
Water sign 🌊
Passionate ❤️‍🔥
Motto: “Trust, but verify everything!” 🔍`, element:'water' },
"Dhanusu": { short:"Archer – aims high 🏹", full:`Dhanusu (Sagittarius / தனுசு)
Fire sign – adventurous 🔥
Energetic 🏃
Motto: “Life is adventure, let’s go!” 🚀`, element:'fire' },
"Makaram": { short:"Goat – climbs everything 🐐", full:`Makaram (Capricorn / மகரம்)
Earth sign 🌍
Goal-driven & disciplined ⏳
Motto: “Slow & steady wins everything” 🐢`, element:'earth' },
"Kumbham": { short:"Water-bearer – ideas 🌊", full:`Kumbham (Aquarius / கும்பம்)
Air sign 💨
Innovative & independent 🤯
Motto: “Be original or go home!” 🏠`, element:'air' },
"Meenam": { short:"Fish – swims in dreams 🐟", full:`Meenam (Pisces / மீனம்)
Water sign 🌊
Compassionate 💖
Artistic & dreamy 🎨`, element:'water' },
"Human": { short:"Special Human 😏", full:`Avlothaaa.. emanthute irukiye kumaruuu 😎😂`, element:'fire'}
};

const colors = { fire:'#ff4b1f', earth:'#2b8a3e', air:'#4b7bfc', water:'#9b2aff' };

// Populate dropdown
const select = document.getElementById('raasiSelect');
for(let key in raasiData){
  let opt = document.createElement('option');
  opt.value = key; opt.textContent = key;
  select.appendChild(opt);
}

const teaser = document.getElementById('teaser');
select.onchange = () => {
  const v = select.value;
  if(v){
    teaser.textContent = raasiData[v].short;
    teaser.style.color = colors[raasiData[v].element];
  }
};

document.getElementById('readMoreBtn').onclick = () => {
  if(!select.value) return alert('Choose your Raasi first!');
  document.getElementById('unlockSection').style.display='block';
};

// Instagram modal & progress
const instagramBtn = document.getElementById('goInstagramBtn');
const progressBar = document.getElementById('progressBar');
let timer;

instagramBtn.onclick = () => {
  window.open('https://www.instagram.com/auronest_designs/', '_blank');
  instagramBtn.disabled = true;

  const modal = document.getElementById('socialModal');
  modal.style.display = 'block';

  document.getElementById('modalDoneBtn').onclick = () => {
    modal.style.display = 'none';

    // Start 5-second progress
    let p = 0;
    timer = setInterval(()=>{
      p += 10;
      progressBar.style.width = p+'%';
      if(p>=100){
        clearInterval(timer);
        document.getElementById('unlockPredictionBtn').disabled = false;
        instagramBtn.textContent = "Done! 🎉";
      }
    }, 500);
  };
};

// Unlock Raasi content
document.getElementById('unlockPredictionBtn').onclick = () => {
  const sel = select.value;
  document.getElementById('fullPrediction').style.display='block';
  document.getElementById('predictionContent').textContent = raasiData[sel].full;
  document.getElementById('predictionContent').style.color = colors[raasiData[sel].element];

  confetti({ particleCount:150, spread:90, origin:{y:0.6} });

  for(let i=0;i<30;i++){
    let spark = document.createElement('div');
    spark.classList.add('spark');
    spark.style.background = colors[raasiData[sel].element];
    spark.style.left = Math.random()*window.innerWidth+'px';
    spark.style.top = Math.random()*window.innerHeight+'px';
    document.body.appendChild(spark);
    setTimeout(()=>spark.remove(),1500);
  }

  document.getElementById('unlockPredictionBtn').disabled = true;
};
</script>
</body>
</html>
