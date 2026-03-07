<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Spidey Quant Banner</title>
<link href="https://fonts.googleapis.com/css2?family=Bangers&family=Share+Tech+Mono&display=swap" rel="stylesheet"/>
<style>
* { margin:0; padding:0; box-sizing:border-box; }

body {
  background:#000;
  display:flex;
  align-items:center;
  justify-content:center;
  min-height:100vh;
  overflow:hidden;
}

.banner {
  position:relative;
  width:900px;
  height:300px;
  overflow:hidden;
  background:#05060f;
}

/* ── Layers ── */
canvas#bgCanvas  { position:absolute; inset:0; width:100%; height:100%; z-index:1; }
canvas#webCanvas { position:absolute; inset:0; width:100%; height:100%; z-index:2; }
canvas#cityCanvas{ position:absolute; bottom:0; left:0; width:100%; height:100%; z-index:3; }

/* Red vignette edge glow */
.vignette {
  position:absolute; inset:0; z-index:4; pointer-events:none;
  box-shadow: inset 0 0 120px rgba(226,0,26,0.45),
              inset 0 0 40px  rgba(0,10,100,0.3);
}

/* Scan lines */
.scanlines {
  position:absolute; inset:0; z-index:5; pointer-events:none;
  background: repeating-linear-gradient(
    0deg, transparent, transparent 3px,
    rgba(0,0,0,0.06) 3px, rgba(0,0,0,0.06) 4px
  );
}

/* ── Spider silhouette + web rope ── */
.rope {
  position:absolute;
  top:0; left:50%;
  width:2px;
  background:linear-gradient(to bottom, rgba(255,255,255,0.95), rgba(255,255,255,0.1));
  transform-origin:top center;
  z-index:9;
  border-radius:2px;
  box-shadow:0 0 4px rgba(255,255,255,0.6);
  height:0;
  animation: ropeDown 1s cubic-bezier(.4,0,.2,1) 0.4s forwards;
}
@keyframes ropeDown { to { height: 108px; } }

.spidey {
  position:absolute;
  top:100px; left:calc(50% - 28px);
  width:56px; height:72px;
  z-index:10;
  opacity:0;
  transform:scale(0.4) rotate(-8deg);
  animation: spideyDrop 0.6s cubic-bezier(.34,1.56,.64,1) 1.3s forwards;
  filter: drop-shadow(0 0 12px rgba(226,0,26,0.9)) drop-shadow(0 4px 20px rgba(0,0,0,0.8));
}
@keyframes spideyDrop {
  to { opacity:1; transform:scale(1) rotate(0deg); }
}

/* Swinging idle */
.spidey-wrap {
  position:absolute;
  top:100px; left:calc(50% - 28px);
  z-index:10;
  transform-origin: top center;
  animation: ropeDown 1s cubic-bezier(.4,0,.2,1) 0.4s both,
             swing 4s ease-in-out 2.1s infinite;
}
@keyframes swing {
  0%,100% { transform: rotate(0deg); }
  25%      { transform: rotate(6deg); }
  75%      { transform: rotate(-6deg); }
}

/* Web shots from hands */
.webshot {
  position:absolute;
  width:1.5px;
  background:linear-gradient(to bottom, rgba(255,255,255,0.9), transparent);
  transform-origin:top center;
  z-index:8;
  border-radius:1px;
  opacity:0;
  height:0;
}
.webshot.L {
  top:126px; left:calc(50% - 26px);
  transform:rotate(-45deg);
  animation: shootWeb 0.5s ease 2s forwards, webFade 1.5s ease 2.5s infinite;
}
.webshot.R {
  top:126px; left:calc(50% + 26px);
  transform:rotate(45deg);
  animation: shootWeb 0.5s ease 2.1s forwards, webFade 1.5s ease 2.6s infinite;
}
@keyframes shootWeb {
  from { height:0; opacity:0; }
  to   { height:100px; opacity:0.8; }
}
@keyframes webFade {
  0%,100% { opacity:0.8; }
  50%     { opacity:0.3; }
}

/* ── Banner text ── */
.content {
  position:absolute;
  inset:0; z-index:15;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  gap:8px;
  padding-bottom:36px;
}

.eyebrow {
  font-family:'Share Tech Mono', monospace;
  font-size:10px;
  letter-spacing:7px;
  color:rgba(245,197,24,0.9);
  text-transform:uppercase;
  opacity:0;
  text-shadow:0 0 14px rgba(245,197,24,0.7);
  animation: fadeUp 0.6s ease 1.6s forwards;
}

.title {
  font-family:'Bangers', cursive;
  font-size:82px;
  letter-spacing:6px;
  line-height:1;
  color:#fff;
  opacity:0;
  animation: fadeUp 0.7s ease 1.8s forwards, titlePulse 3s ease-in-out 2.8s infinite;
  text-shadow:
    4px 4px 0 #b80015,
    8px 8px 0 rgba(180,0,20,0.35),
    0 0 60px rgba(255,40,40,0.55);
}
.title .r { color:#e2001a; text-shadow: 3px 3px 0 #7a0010, 0 0 30px rgba(255,0,30,0.9); }

.sub {
  font-family:'Share Tech Mono', monospace;
  font-size:12px;
  letter-spacing:3.5px;
  color:rgba(255,255,255,0.5);
  text-transform:uppercase;
  opacity:0;
  animation: fadeUp 0.6s ease 2s forwards;
}
.sub em { color:#f5c518; font-style:normal; text-shadow:0 0 8px rgba(245,197,24,0.6); }

/* ── Ticker ── */
.ticker {
  position:absolute;
  bottom:0; left:0; right:0;
  height:30px;
  background:rgba(226,0,26,0.12);
  border-top:1.5px solid rgba(226,0,26,0.5);
  z-index:20;
  display:flex;
  align-items:center;
  overflow:hidden;
}
.ticker-tag {
  background:#e2001a;
  color:#fff;
  font-family:'Bangers', cursive;
  font-size:12px;
  letter-spacing:2px;
  padding:0 14px;
  height:100%;
  display:flex; align-items:center;
  flex-shrink:0;
  white-space:nowrap;
}
.ticker-scroll {
  overflow:hidden;
  flex:1;
}
.ticker-inner {
  display:flex;
  animation: scroll 28s linear infinite;
  white-space:nowrap;
}
.ticker-inner span {
  font-family:'Share Tech Mono', monospace;
  font-size:10px;
  color:#ffaa55;
  letter-spacing:2px;
  padding:0 26px;
}
.ticker-inner span::before { content:"▸ "; color:#e2001a; }
@keyframes scroll {
  from { transform:translateX(0); }
  to   { transform:translateX(-50%); }
}

/* ── Utility anims ── */
@keyframes fadeUp {
  from { opacity:0; transform:translateY(14px); }
  to   { opacity:1; transform:translateY(0); }
}
@keyframes titlePulse {
  0%,100% { text-shadow: 4px 4px 0 #b80015, 8px 8px 0 rgba(180,0,20,0.35), 0 0 60px rgba(255,40,40,0.55); }
  50%     { text-shadow: 4px 4px 0 #b80015, 8px 8px 0 rgba(180,0,20,0.35), 0 0 100px rgba(255,60,60,0.85); }
}

/* Floating particles */
.pt {
  position:absolute;
  border-radius:50%;
  pointer-events:none;
  z-index:6;
  animation:floatUp linear infinite;
}
@keyframes floatUp {
  0%   { opacity:0.8; transform:translateY(0) scale(1); }
  100% { opacity:0;   transform:translateY(-310px) scale(0.2); }
}

/* Corner brackets */
.corner {
  position:absolute;
  width:18px; height:18px;
  z-index:16;
  opacity:0;
  animation:fadeIn 0.5s ease 2.2s forwards;
}
.corner.tl { top:10px;  left:10px;  border-top:2px solid #e2001a; border-left:2px solid #e2001a; }
.corner.tr { top:10px;  right:10px; border-top:2px solid #e2001a; border-right:2px solid #e2001a; }
.corner.bl { bottom:38px; left:10px;  border-bottom:2px solid #e2001a; border-left:2px solid #e2001a; }
.corner.br { bottom:38px; right:10px; border-bottom:2px solid #e2001a; border-right:2px solid #e2001a; }
@keyframes fadeIn { to { opacity:1; } }
</style>
</head>
<body>
<div class="banner" id="banner">

  <canvas id="bgCanvas"></canvas>
  <canvas id="webCanvas"></canvas>
  <canvas id="cityCanvas"></canvas>
  <div class="vignette"></div>
  <div class="scanlines"></div>

  <!-- Rope + Spidey -->
  <div class="rope"></div>
  <div class="spidey-wrap">
    <svg class="spidey" viewBox="0 0 56 72" fill="none" xmlns="http://www.w3.org/2000/svg">
      <!-- Body -->
      <ellipse cx="28" cy="38" rx="11" ry="14" fill="#e2001a"/>
      <!-- Head -->
      <circle cx="28" cy="18" r="11" fill="#e2001a"/>
      <!-- Eye whites -->
      <ellipse cx="23" cy="17" rx="5" ry="4.5" fill="white" opacity="0.95"/>
      <ellipse cx="33" cy="17" rx="5" ry="4.5" fill="white" opacity="0.95"/>
      <!-- Eye inner shadow -->
      <ellipse cx="23" cy="17.5" rx="3.5" ry="3" fill="rgba(0,10,100,0.15)"/>
      <ellipse cx="33" cy="17.5" rx="3.5" ry="3" fill="rgba(0,10,100,0.15)"/>
      <!-- Web lines on head -->
      <line x1="28" y1="7"  x2="28" y2="29" stroke="#0a1172" stroke-width="0.8" opacity="0.6"/>
      <line x1="17" y1="9"  x2="39" y2="27" stroke="#0a1172" stroke-width="0.8" opacity="0.6"/>
      <line x1="39" y1="9"  x2="17" y2="27" stroke="#0a1172" stroke-width="0.8" opacity="0.6"/>
      <path d="M17 13 Q28 19 39 13" stroke="#0a1172" stroke-width="0.8" fill="none" opacity="0.6"/>
      <path d="M17 21 Q28 27 39 21" stroke="#0a1172" stroke-width="0.8" fill="none" opacity="0.6"/>
      <!-- Web lines on body -->
      <line x1="28" y1="24" x2="28" y2="52" stroke="#0a1172" stroke-width="0.8" opacity="0.5"/>
      <path d="M17 30 Q28 36 39 30" stroke="#0a1172" stroke-width="0.8" fill="none" opacity="0.5"/>
      <path d="M17 39 Q28 45 39 39" stroke="#0a1172" stroke-width="0.8" fill="none" opacity="0.5"/>
      <path d="M18 48 Q28 54 38 48" stroke="#0a1172" stroke-width="0.8" fill="none" opacity="0.5"/>
      <!-- Arms -->
      <line x1="17" y1="30" x2="2"  y2="20" stroke="#0a1172" stroke-width="3.5" stroke-linecap="round"/>
      <line x1="39" y1="30" x2="54" y2="20" stroke="#0a1172" stroke-width="3.5" stroke-linecap="round"/>
      <!-- Legs -->
      <line x1="19" y1="50" x2="6"  y2="66" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
      <line x1="24" y1="52" x2="14" y2="70" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
      <line x1="37" y1="50" x2="50" y2="66" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
      <line x1="32" y1="52" x2="42" y2="70" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
    </svg>
  </div>

  <!-- Web shots from hands -->
  <div class="webshot L"></div>
  <div class="webshot R"></div>

  <!-- Corner decorations -->
  <div class="corner tl"></div>
  <div class="corner tr"></div>
  <div class="corner bl"></div>
  <div class="corner br"></div>

  <!-- Text content -->
  <div class="content">
    <div class="eyebrow">⚡ Quantitative Finance · AI · Mathematics ⚡</div>
    <div class="title">QUANT<span class="r">NET</span></div>
    <div class="sub"><em>Probability</em> · <em>Stochastic Calculus</em> · <em>Alpha Generation</em></div>
  </div>

  <!-- Ticker -->
  <div class="ticker">
    <div class="ticker-tag">LIVE</div>
    <div class="ticker-scroll">
      <div class="ticker-inner">
        <span>Black-Scholes</span><span>Itô's Lemma</span><span>Monte Carlo</span>
        <span>Brownian Motion</span><span>Risk-Neutral Pricing</span><span>Volatility Surface</span>
        <span>Martingale Theory</span><span>Delta Hedging</span><span>Sharpe Ratio</span>
        <span>Statistical Arbitrage</span><span>Factor Models</span><span>ML Alpha</span>
        <!-- duplicate for seamless loop -->
        <span>Black-Scholes</span><span>Itô's Lemma</span><span>Monte Carlo</span>
        <span>Brownian Motion</span><span>Risk-Neutral Pricing</span><span>Volatility Surface</span>
        <span>Martingale Theory</span><span>Delta Hedging</span><span>Sharpe Ratio</span>
        <span>Statistical Arbitrage</span><span>Factor Models</span><span>ML Alpha</span>
      </div>
    </div>
  </div>
</div>

<script>
// ── 1. BACKGROUND: animated deep red/blue gradient pulse ──────────
const bgC  = document.getElementById('bgCanvas');
const bgX  = bgC.getContext('2d');
bgC.width  = 900; bgC.height = 300;
let bgT = 0;
function drawBg() {
  bgT += 0.008;
  const r  = bgC.width, h = bgC.height;
  const cx = r/2 + Math.sin(bgT)*120;
  const cy = h/2 + Math.cos(bgT*0.7)*60;
  const grd = bgX.createRadialGradient(cx, cy, 10, cx, cy, r*0.9);
  grd.addColorStop(0,   'rgba(120,0,20,0.55)');
  grd.addColorStop(0.4, 'rgba(30,0,80,0.4)');
  grd.addColorStop(1,   'rgba(5,6,15,0)');
  bgX.clearRect(0,0,r,h);
  bgX.fillStyle = grd;
  bgX.fillRect(0,0,r,h);
  requestAnimationFrame(drawBg);
}
drawBg();

// ── 2. SPIDER-WEB: animated radial + concentric webs ─────────────
const wC  = document.getElementById('webCanvas');
const wX  = wC.getContext('2d');
wC.width  = 900; wC.height = 300;
let webT  = 0;

const hubs = [
  { x:0,   y:0,   spokes:10, maxR:300 },
  { x:900, y:0,   spokes:10, maxR:300 },
  { x:450, y:300, spokes:8,  maxR:260 },
  { x:0,   y:300, spokes:7,  maxR:220 },
  { x:900, y:300, spokes:7,  maxR:220 },
];

function drawWeb() {
  webT += 0.012;
  wX.clearRect(0,0,900,300);

  hubs.forEach(({x,y,spokes,maxR}) => {
    // Radial lines
    for (let i=0; i<spokes; i++) {
      const angle = (i/spokes)*Math.PI*2;
      wX.beginPath();
      wX.moveTo(x,y);
      wX.lineTo(x + Math.cos(angle)*maxR, y + Math.sin(angle)*maxR);
      wX.strokeStyle = 'rgba(255,255,255,0.12)';
      wX.lineWidth = 0.7;
      wX.stroke();
    }
    // Concentric arcs that breathe
    const rings = 7;
    for (let r=0; r<rings; r++) {
      const base = (r+1) * (maxR/rings);
      const pulse = base + Math.sin(webT + r*0.6)*6;
      wX.beginPath();
      wX.arc(x,y, pulse, 0, Math.PI*2);
      const alpha = 0.06 + 0.04*Math.sin(webT*1.5 + r);
      wX.strokeStyle = `rgba(255,255,255,${alpha})`;
      wX.lineWidth = 0.6;
      wX.stroke();
    }
  });

  // Glowing red center thread
  wX.beginPath();
  wX.moveTo(0,0);
  wX.lineTo(450, 300);
  wX.lineTo(900, 0);
  wX.strokeStyle = `rgba(226,0,26,${0.1+0.06*Math.sin(webT*2)})`;
  wX.lineWidth = 1;
  wX.stroke();

  requestAnimationFrame(drawWeb);
}
drawWeb();

// ── 3. CITY SILHOUETTE ────────────────────────────────────────────
const cC  = document.getElementById('cityCanvas');
const cX  = cC.getContext('2d');
cC.width  = 900; cC.height = 300;

function drawCity() {
  cX.clearRect(0,0,900,300);
  cX.fillStyle = 'rgba(8,10,25,0.88)';

  const buildings = [
    [0,240,28,60],[5,220,18,20],[32,230,42,70],[44,205,6,25],[54,215,5,15],
    [78,240,28,60],[108,215,52,85],[118,190,7,25],[128,195,6,18],
    [163,230,38,70],[204,205,58,95],[214,175,8,30],[235,185,6,22],
    [265,235,32,65],[300,195,65,105],[308,165,7,30],[328,170,6,26],
    [368,225,42,75],[414,205,52,95],[420,180,8,25],[450,190,6,20],
    [469,235,36,65],[509,215,58,85],[515,185,7,28],[540,195,6,18],
    [570,205,42,95],[615,185,60,115],[622,155,6,30],[640,162,7,24],
    [678,225,38,75],[720,200,52,100],[726,170,7,30],[745,178,8,24],
    [775,230,42,70],[820,195,58,105],[828,165,6,30],[848,170,7,24],
    [881,225,36,75],[920,205,48,95],[926,178,6,24],
  ];

  buildings.forEach(([x,y,w,h]) => {
    cX.fillRect(x, y, w, 300-y);
    // window lights
    for (let wy=y+8; wy<300-8; wy+=14) {
      for (let wx=x+5; wx<x+w-5; wx+=10) {
        if (Math.random()>0.45) {
          cX.fillStyle = `rgba(255,220,120,${0.3+Math.random()*0.4})`;
          cX.fillRect(wx, wy, 4, 6);
          cX.fillStyle = 'rgba(8,10,25,0.88)';
        }
      }
    }
  });
}
drawCity();
// Twinkle windows
setInterval(() => {
  drawCity();
}, 1200);

// ── 4. FLOATING PARTICLES ─────────────────────────────────────────
const banner = document.getElementById('banner');
function spawnParticle() {
  const p = document.createElement('div');
  p.className = 'pt';
  const sz = 2 + Math.random()*4;
  const red = Math.random()>0.45;
  p.style.cssText = `
    width:${sz}px;height:${sz}px;
    left:${Math.random()*96}%;
    bottom:${30+Math.random()*50}px;
    background:${red?'#e2001a':'#3355ff'};
    box-shadow:0 0 ${sz*3}px ${red?'rgba(226,0,26,0.8)':'rgba(50,80,255,0.7)'};
    animation-duration:${3+Math.random()*5}s;
    animation-delay:0s;
  `;
  banner.appendChild(p);
  setTimeout(()=>p.remove(), 8000);
}
setInterval(spawnParticle, 280);
</script>
</body>
</html>
