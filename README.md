<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Quant README – Spider-Man Theme</title>
<link href="https://fonts.googleapis.com/css2?family=Bangers&family=Share+Tech+Mono&family=Rajdhani:wght@400;600;700&display=swap" rel="stylesheet"/>
<style>
:root {
  --red:    #e2001a;
  --blue:   #0a1172;
  --gold:   #f5c518;
  --white:  #f0f0f0;
  --dark:   #060810;
  --web:    rgba(255,255,255,0.07);
}

* { margin:0; padding:0; box-sizing:border-box; }

body {
  background: var(--dark);
  color: var(--white);
  font-family: 'Rajdhani', sans-serif;
  min-height: 100vh;
  overflow-x: hidden;
}

/* ── BANNER ─────────────────────────────────────────────── */
.banner {
  position: relative;
  width: 100%;
  height: 320px;
  background: linear-gradient(135deg, #0a0010 0%, #0a1172 40%, #1a0005 70%, #e2001a 100%);
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Spider-web SVG canvas */
#webCanvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  opacity: 0.18;
}

/* City silhouette at bottom */
.city {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 110px;
  opacity: 0.22;
}

/* Swinging web line */
.swing-line {
  position: absolute;
  top: 0;
  left: 50%;
  width: 3px;
  height: 0;
  background: linear-gradient(to bottom, rgba(255,255,255,0.9), rgba(255,255,255,0.1));
  transform-origin: top center;
  animation: dropLine 1.2s ease 0.2s forwards;
  border-radius: 2px;
  filter: blur(0.5px);
}
@keyframes dropLine {
  to { height: 120px; }
}

/* Spider silhouette */
.spider-guy {
  position: absolute;
  top: 105px;
  left: calc(50% - 22px);
  width: 44px;
  height: 64px;
  opacity: 0;
  animation: spiderAppear 0.5s ease 1.3s forwards;
}
@keyframes spiderAppear {
  from { opacity:0; transform: scale(0.5); }
  to   { opacity:1; transform: scale(1); }
}

/* Web particles shooting out */
.web-shot {
  position: absolute;
  width: 2px;
  height: 60px;
  background: linear-gradient(to bottom, rgba(255,255,255,0.8), transparent);
  border-radius: 1px;
  transform-origin: top center;
  opacity: 0;
}
.web-shot.left  { top:120px; left:calc(50% - 22px); transform: rotate(-38deg); animation: webShot 0.4s ease 1.8s forwards; }
.web-shot.right { top:120px; left:calc(50% + 22px); transform: rotate(38deg);  animation: webShot 0.4s ease 1.9s forwards; }
@keyframes webShot {
  from { opacity:0; height:0; }
  to   { opacity:0.8; height:90px; }
}

/* Floating particles */
.particle {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  animation: floatPart linear infinite;
}
@keyframes floatPart {
  0%   { transform: translateY(0) scale(1);   opacity: 0.7; }
  50%  { opacity: 0.3; }
  100% { transform: translateY(-320px) scale(0); opacity: 0; }
}

/* Banner text */
.banner-content {
  position: relative;
  z-index: 20;
  text-align: center;
  padding-top: 40px;
}

.banner-eyebrow {
  font-family: 'Share Tech Mono', monospace;
  font-size: 11px;
  letter-spacing: 8px;
  color: var(--gold);
  text-transform: uppercase;
  opacity: 0;
  animation: fadeUp 0.6s ease 0.8s forwards;
  text-shadow: 0 0 12px rgba(245,197,24,0.8);
}

.banner-name {
  font-family: 'Bangers', cursive;
  font-size: 88px;
  letter-spacing: 6px;
  line-height: 1;
  color: #fff;
  opacity: 0;
  animation: fadeUp 0.7s ease 1s forwards;
  text-shadow:
    4px 4px 0 var(--red),
    8px 8px 0 rgba(226,0,26,0.4),
    0 0 60px rgba(255,80,80,0.5);
  position: relative;
}

.banner-name .highlight {
  color: var(--red);
  text-shadow:
    3px 3px 0 #7a0010,
    0 0 40px rgba(255,0,30,0.8);
}

.banner-subtitle {
  font-family: 'Rajdhani', sans-serif;
  font-size: 15px;
  font-weight: 600;
  letter-spacing: 4px;
  color: rgba(255,255,255,0.65);
  text-transform: uppercase;
  opacity: 0;
  animation: fadeUp 0.7s ease 1.3s forwards;
  margin-top: 4px;
}

.banner-subtitle span {
  color: var(--gold);
}

/* Web badge strip at bottom of banner */
.web-strip {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 36px;
  background: rgba(10,17,114,0.6);
  border-top: 2px solid var(--red);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 32px;
  z-index: 25;
  overflow: hidden;
}
.web-strip::before {
  content: '';
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    90deg,
    transparent,
    transparent 80px,
    rgba(226,0,26,0.08) 80px,
    rgba(226,0,26,0.08) 82px
  );
}
.badge {
  font-family: 'Share Tech Mono', monospace;
  font-size: 9px;
  letter-spacing: 2px;
  color: rgba(255,255,255,0.5);
  text-transform: uppercase;
  position: relative;
}
.badge.hot { color: var(--gold); text-shadow: 0 0 8px var(--gold); }

@keyframes fadeUp {
  from { opacity:0; transform: translateY(16px); }
  to   { opacity:1; transform: translateY(0); }
}

/* ── CONTENT ─────────────────────────────────────────────── */
.readme {
  max-width: 860px;
  margin: 0 auto;
  padding: 48px 24px 80px;
}

/* Section header */
.sec-head {
  display: flex;
  align-items: center;
  gap: 12px;
  margin: 48px 0 20px;
}
.sec-head::after {
  content: '';
  flex: 1;
  height: 1px;
  background: linear-gradient(to right, var(--red), transparent);
}
.sec-head h2 {
  font-family: 'Bangers', cursive;
  font-size: 28px;
  letter-spacing: 3px;
  color: var(--white);
  white-space: nowrap;
}
.sec-head .icon { font-size: 20px; }

/* Code block */
.code-block {
  background: #0d0f1a;
  border: 1px solid rgba(226,0,26,0.25);
  border-left: 3px solid var(--red);
  border-radius: 4px;
  padding: 24px 28px;
  font-family: 'Share Tech Mono', monospace;
  font-size: 13px;
  line-height: 1.9;
  color: #c8d0f0;
  position: relative;
  overflow: hidden;
}
.code-block::before {
  content: '';
  position: absolute;
  top: 0; right: 0;
  width: 120px; height: 120px;
  background: radial-gradient(circle at top right, rgba(226,0,26,0.07), transparent 70%);
}
.kw  { color: #ff6b6b; }
.str { color: #a8e6cf; }
.cm  { color: #4a5275; font-style: italic; }
.fn  { color: var(--gold); }
.num { color: #82aaff; }

/* Expertise grid */
.grid-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-top: 4px;
}
.card {
  background: linear-gradient(135deg, #0d0f1a, #10142a);
  border: 1px solid rgba(255,255,255,0.07);
  border-top: 2px solid var(--red);
  border-radius: 6px;
  padding: 20px 18px;
  transition: transform 0.2s, border-color 0.2s;
  position: relative;
  overflow: hidden;
}
.card::after {
  content: '';
  position: absolute;
  bottom: -20px; right: -20px;
  width: 80px; height: 80px;
  background: radial-gradient(circle, rgba(226,0,26,0.08), transparent 70%);
}
.card:hover { transform: translateY(-4px); border-top-color: var(--gold); }
.card-icon { font-size: 22px; margin-bottom: 10px; }
.card h3 {
  font-family: 'Bangers', cursive;
  font-size: 18px;
  letter-spacing: 2px;
  color: var(--red);
  margin-bottom: 10px;
}
.card ul { list-style: none; padding: 0; }
.card ul li {
  font-size: 13px;
  color: rgba(255,255,255,0.6);
  padding: 3px 0;
  border-bottom: 1px solid rgba(255,255,255,0.04);
  font-family: 'Share Tech Mono', monospace;
}
.card ul li::before { content: "▸ "; color: var(--red); }

/* Quote block */
.quote {
  border-left: 4px solid var(--red);
  background: linear-gradient(90deg, rgba(226,0,26,0.07), transparent);
  padding: 18px 24px;
  border-radius: 0 6px 6px 0;
  margin: 24px 0;
  font-size: 17px;
  font-style: italic;
  color: rgba(255,255,255,0.75);
  line-height: 1.6;
  font-family: 'Rajdhani', sans-serif;
  font-weight: 600;
}
.quote span { color: var(--gold); font-style: normal; }

/* Stack badges */
.badges {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 8px;
}
.badge-pill {
  background: rgba(10,17,114,0.5);
  border: 1px solid rgba(226,0,26,0.35);
  border-radius: 20px;
  padding: 6px 16px;
  font-family: 'Share Tech Mono', monospace;
  font-size: 12px;
  color: rgba(255,255,255,0.75);
  transition: all 0.2s;
  cursor: default;
}
.badge-pill:hover {
  background: rgba(226,0,26,0.2);
  border-color: var(--red);
  color: #fff;
  transform: scale(1.05);
}

/* Philosophy section */
.philosophy {
  background: #0d0f1a;
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 6px;
  padding: 28px;
  font-family: 'Share Tech Mono', monospace;
  font-size: 12px;
  line-height: 2;
  color: #8892b0;
}
.philosophy .arrow { color: var(--red); }
.philosophy .bright { color: var(--gold); }
.philosophy .result { color: #a8e6cf; }

/* Currently section */
.currently {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}
.curr-item {
  background: #0d0f1a;
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 6px;
  padding: 14px 18px;
  display: flex;
  align-items: flex-start;
  gap: 12px;
  font-size: 13px;
  color: rgba(255,255,255,0.65);
  font-family: 'Rajdhani', sans-serif;
  font-weight: 600;
  letter-spacing: 0.5px;
  transition: border-color 0.2s;
}
.curr-item:hover { border-color: rgba(226,0,26,0.4); color: #fff; }
.curr-item .emoji { font-size: 18px; flex-shrink: 0; }

/* Stats row */
.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  margin-top: 4px;
}
.stat-box {
  background: linear-gradient(135deg, #0d0f1a, #10142a);
  border: 1px solid rgba(226,0,26,0.2);
  border-radius: 6px;
  padding: 20px;
  text-align: center;
}
.stat-num {
  font-family: 'Bangers', cursive;
  font-size: 38px;
  color: var(--red);
  line-height: 1;
  text-shadow: 0 0 20px rgba(226,0,26,0.5);
}
.stat-label {
  font-size: 10px;
  letter-spacing: 2px;
  color: rgba(255,255,255,0.4);
  text-transform: uppercase;
  font-family: 'Share Tech Mono', monospace;
  margin-top: 4px;
}

/* Footer */
.footer {
  text-align: center;
  margin-top: 60px;
  padding-top: 32px;
  border-top: 1px solid rgba(226,0,26,0.2);
  font-family: 'Share Tech Mono', monospace;
  font-size: 11px;
  color: rgba(255,255,255,0.25);
  letter-spacing: 2px;
}
.footer .red { color: var(--red); }

/* Web hex pattern overlay on sections */
.hex-overlay {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 0;
  opacity: 0.015;
  background-image: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' stroke='white' stroke-width='0.5'%3E%3Cpolygon points='30,5 52,17.5 52,42.5 30,55 8,42.5 8,17.5'/%3E%3C/g%3E%3C/svg%3E");
  background-size: 60px 60px;
}

.readme { position: relative; z-index: 1; }
</style>
</head>
<body>

<div class="hex-overlay"></div>

<!-- ══ BANNER ══════════════════════════════════════════════ -->
<div class="banner">
  <canvas id="webCanvas"></canvas>

  <!-- City silhouette -->
  <svg class="city" viewBox="0 0 1200 110" preserveAspectRatio="xMidYMax slice" fill="rgba(10,17,114,0.8)">
    <rect x="0"   y="60"  width="30"  height="50"/>
    <rect x="5"   y="45"  width="20"  height="15"/>
    <rect x="35"  y="40"  width="45"  height="70"/>
    <rect x="45"  y="25"  width="5"   height="15"/>
    <rect x="55"  y="30"  width="5"   height="10"/>
    <rect x="85"  y="55"  width="30"  height="55"/>
    <rect x="120" y="35"  width="55"  height="75"/>
    <rect x="130" y="15"  width="6"   height="20"/>
    <rect x="180" y="50"  width="40"  height="60"/>
    <rect x="225" y="30"  width="60"  height="80"/>
    <rect x="235" y="10"  width="8"   height="20"/>
    <rect x="290" y="55"  width="35"  height="55"/>
    <rect x="330" y="20"  width="70"  height="90"/>
    <rect x="340" y="5"   width="6"   height="15"/>
    <rect x="355" y="5"   width="6"   height="15"/>
    <rect x="405" y="45"  width="45"  height="65"/>
    <rect x="455" y="35"  width="55"  height="75"/>
    <rect x="460" y="15"  width="8"   height="20"/>
    <rect x="515" y="55"  width="40"  height="55"/>
    <rect x="560" y="25"  width="65"  height="85"/>
    <rect x="570" y="10"  width="5"   height="15"/>
    <rect x="630" y="50"  width="35"  height="60"/>
    <rect x="670" y="30"  width="55"  height="80"/>
    <rect x="730" y="40"  width="45"  height="70"/>
    <rect x="780" y="20"  width="65"  height="90"/>
    <rect x="785" y="5"   width="7"   height="15"/>
    <rect x="850" y="50"  width="35"  height="60"/>
    <rect x="890" y="35"  width="50"  height="75"/>
    <rect x="945" y="55"  width="40"  height="55"/>
    <rect x="990" y="25"  width="60"  height="85"/>
    <rect x="995" y="10"  width="6"   height="15"/>
    <rect x="1055" y="45" width="40"  height="65"/>
    <rect x="1100" y="30" width="55"  height="80"/>
    <rect x="1160" y="50" width="40"  height="60"/>
  </svg>

  <!-- Hanging web line + figure -->
  <div class="swing-line"></div>
  <svg class="spider-guy" viewBox="0 0 44 64" fill="none">
    <!-- body -->
    <ellipse cx="22" cy="28" rx="10" ry="13" fill="#e2001a"/>
    <!-- head -->
    <circle cx="22" cy="13" r="9" fill="#e2001a"/>
    <!-- eyes -->
    <ellipse cx="18" cy="12" rx="4" ry="3.5" fill="white" opacity="0.9"/>
    <ellipse cx="26" cy="12" rx="4" ry="3.5" fill="white" opacity="0.9"/>
    <!-- legs -->
    <line x1="12" y1="35" x2="2"  y2="50" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
    <line x1="17" y1="38" x2="10" y2="55" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
    <line x1="32" y1="35" x2="42" y2="50" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
    <line x1="27" y1="38" x2="34" y2="55" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
    <!-- arms -->
    <line x1="12" y1="25" x2="0"  y2="18" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
    <line x1="32" y1="25" x2="44" y2="18" stroke="#0a1172" stroke-width="3" stroke-linecap="round"/>
    <!-- web lines on suit -->
    <line x1="22" y1="4" x2="22" y2="22" stroke="#0a1172" stroke-width="0.8" opacity="0.5"/>
    <path d="M13 8 Q22 14 31 8" stroke="#0a1172" stroke-width="0.8" fill="none" opacity="0.5"/>
    <path d="M14 20 Q22 26 30 20" stroke="#0a1172" stroke-width="0.8" fill="none" opacity="0.5"/>
  </svg>
  <div class="web-shot left"></div>
  <div class="web-shot right"></div>

  <!-- Banner Text -->
  <div class="banner-content">
    <div class="banner-eyebrow">⚡ Quantitative Researcher · Financial Analyst · AI Explorer ⚡</div>
    <div class="banner-name">QUANT<span class="highlight">NET</span></div>
    <div class="banner-subtitle">
      <span>Probability</span> · <span>Stochastic Calculus</span> · <span>Alpha Generation</span>
    </div>
  </div>

  <!-- Bottom strip -->
  <div class="web-strip">
    <span class="badge">Mathematics</span>
    <span class="badge hot">🔥 Quant Finance</span>
    <span class="badge">AI & ML</span>
    <span class="badge hot">⚡ Open to Opportunities</span>
    <span class="badge">Risk Modeling</span>
  </div>
</div>

<!-- ══ README CONTENT ═══════════════════════════════════════ -->
<div class="readme">

  <!-- WHO AM I -->
  <div class="sec-head">
    <span class="icon">🕷️</span>
    <h2>WHOAMI</h2>
  </div>

  <div class="code-block">
<span class="kw">class</span> <span class="fn">Quant</span>:
  <span class="kw">def</span> <span class="fn">__init__</span>(self):
    self.name        = <span class="str">"Your Name"</span>
    self.title       = [<span class="str">"Quantitative Researcher"</span>, <span class="str">"Financial Analyst"</span>, <span class="str">"AI Builder"</span>]
    self.education   = <span class="str">"B.Sc. Mathematics"</span>
    self.belief      = <span class="str">"Markets are probability theory at scale."</span>
    self.superpower  = <span class="str">"Turning abstract math into financial edge"</span>
    self.stack       = [<span class="str">"Stochastic Calculus"</span>, <span class="str">"Options Pricing"</span>, <span class="str">"ML Strategies"</span>]

  <span class="kw">def</span> <span class="fn">drive</span>(self) -> <span class="str">str</span>:
    <span class="cm"># Not the smartest in the room. Just the last one standing.</span>
    <span class="kw">return</span> <span class="str">"Relentless. Obsessed. Here to build something that matters."</span>

me = <span class="fn">Quant</span>()
<span class="fn">print</span>(me.<span class="fn">drive</span>())
<span class="cm"># → "Relentless. Obsessed. Here to build something that matters."</span>
  </div>

  <div class="quote">
    <span>"</span>With great math comes great responsibility.<span>"</span>
    — Every quant who ever stared at a volatility surface at 2am
  </div>

  <!-- STATS -->
  <div class="sec-head">
    <span class="icon">📊</span>
    <h2>BY THE NUMBERS</h2>
  </div>
  <div class="stats">
    <div class="stat-box">
      <div class="stat-num">∞</div>
      <div class="stat-label">Models to Build</div>
    </div>
    <div class="stat-box">
      <div class="stat-num">24/7</div>
      <div class="stat-label">Market Obsession</div>
    </div>
    <div class="stat-box">
      <div class="stat-num">0</div>
      <div class="stat-label">Days Off From Learning</div>
    </div>
    <div class="stat-box">
      <div class="stat-num">1</div>
      <div class="stat-label">Goal: Be Great</div>
    </div>
  </div>

  <!-- EXPERTISE -->
  <div class="sec-head">
    <span class="icon">🧠</span>
    <h2>EXPERTISE</h2>
  </div>
  <div class="grid-3">
    <div class="card">
      <div class="card-icon">📐</div>
      <h3>Mathematics</h3>
      <ul>
        <li>Probability Theory</li>
        <li>Stochastic Processes</li>
        <li>Measure Theory</li>
        <li>Linear Algebra</li>
        <li>Real Analysis</li>
      </ul>
    </div>
    <div class="card">
      <div class="card-icon">📈</div>
      <h3>Quant Finance</h3>
      <ul>
        <li>Black-Scholes Pricing</li>
        <li>Monte Carlo Sim</li>
        <li>Risk Management</li>
        <li>Portfolio Optimization</li>
        <li>Derivatives & Greeks</li>
      </ul>
    </div>
    <div class="card">
      <div class="card-icon">🤖</div>
      <h3>AI & ML</h3>
      <ul>
        <li>Statistical Learning</li>
        <li>Neural Networks</li>
        <li>Time Series Models</li>
        <li>Bayesian Inference</li>
        <li>RL for Trading</li>
      </ul>
    </div>
  </div>

  <!-- KNOWLEDGE STACK -->
  <div class="sec-head">
    <span class="icon">🛠️</span>
    <h2>STACK</h2>
  </div>
  <div class="badges">
    <div class="badge-pill">Python</div>
    <div class="badge-pill">NumPy</div>
    <div class="badge-pill">Pandas</div>
    <div class="badge-pill">SciPy</div>
    <div class="badge-pill">scikit-learn</div>
    <div class="badge-pill">PyTorch</div>
    <div class="badge-pill">TensorFlow</div>
    <div class="badge-pill">Jupyter</div>
    <div class="badge-pill">LaTeX</div>
    <div class="badge-pill">Git</div>
    <div class="badge-pill">Matplotlib</div>
    <div class="badge-pill">Statsmodels</div>
    <div class="badge-pill">QuantLib</div>
    <div class="badge-pill">Plotly</div>
  </div>

  <!-- PHILOSOPHY -->
  <div class="sec-head">
    <span class="icon">⚡</span>
    <h2>THE QUANT PHILOSOPHY</h2>
  </div>
  <div class="philosophy">
    <span class="bright">Market Efficiency</span>  <span class="arrow">──────►</span>  <span class="result">Opportunity in Inefficiency</span>
    <span class="bright">Random Walk Theory</span>  <span class="arrow">──────►</span>  <span class="result">Patterns Inside the Noise</span>
    <span class="bright">Risk = Uncertainty</span>   <span class="arrow">──────►</span>  <span class="result">Uncertainty = Edge</span>
    <span class="bright">Itô's Lemma</span>          <span class="arrow">──────►</span>  <span class="result">Derivatives from First Principles</span>
    <span class="bright">Pure Math Degree</span>      <span class="arrow">──────►</span>  <span class="result">Thinking in Abstractions Others Can't</span>
                                                   <span class="arrow">         │</span>
                                                   <span class="arrow">         ▼</span>
                                     <span class="result">         Alpha Generation</span>
  </div>

  <!-- CURRENTLY -->
  <div class="sec-head">
    <span class="icon">🌱</span>
    <h2>CURRENTLY SHARPENING</h2>
  </div>
  <div class="currently">
    <div class="curr-item"><span class="emoji">📖</span> Advanced stochastic calculus & jump-diffusion models</div>
    <div class="curr-item"><span class="emoji">🧮</span> Volatility surface construction & calibration</div>
    <div class="curr-item"><span class="emoji">🤖</span> Transformer architectures on financial time series</div>
    <div class="curr-item"><span class="emoji">📊</span> Systematic data-driven factor model research</div>
    <div class="curr-item"><span class="emoji">🕸️</span> Statistical arbitrage strategy development</div>
    <div class="curr-item"><span class="emoji">🔬</span> Bayesian methods for regime detection</div>
  </div>

  <!-- FOOTER -->
  <div class="footer">
    <p>Built with <span class="red">♥</span> &amp; an obsession with markets &nbsp;|&nbsp; <span class="red">"Not the smartest — just the most relentless."</span></p>
    <p style="margin-top:10px; font-size:10px; opacity:0.5">⚡ With Great Math Comes Great Responsibility ⚡</p>
  </div>

</div>

<!-- ══ SPIDER-WEB CANVAS SCRIPT ══════════════════════════════ -->
<script>
const canvas = document.getElementById('webCanvas');
const ctx    = canvas.getContext('2d');

function resize() {
  canvas.width  = canvas.offsetWidth;
  canvas.height = canvas.offsetHeight;
}
resize();
window.addEventListener('resize', () => { resize(); drawWeb(); });

function drawWeb() {
  const W = canvas.width, H = canvas.height;
  ctx.clearRect(0, 0, W, H);

  const webs = [
    { cx: W * 0.12, cy: 0 },
    { cx: W * 0.88, cy: 0 },
    { cx: W * 0.5,  cy: 0 },
    { cx: 0,        cy: H * 0.4 },
    { cx: W,        cy: H * 0.4 },
  ];

  webs.forEach(({cx, cy}) => {
    const lines = 10;
    const maxLen = Math.max(W, H) * 0.8;
    for (let i = 0; i < lines; i++) {
      const angle = (i / lines) * Math.PI * 2;
      const ex = cx + Math.cos(angle) * maxLen;
      const ey = cy + Math.sin(angle) * maxLen;
      ctx.beginPath();
      ctx.moveTo(cx, cy);
      ctx.lineTo(ex, ey);
      ctx.strokeStyle = 'rgba(255,255,255,0.5)';
      ctx.lineWidth = 0.6;
      ctx.stroke();
    }
    // concentric arcs
    for (let r = 40; r < maxLen; r += 55) {
      ctx.beginPath();
      ctx.arc(cx, cy, r, 0, Math.PI * 2);
      ctx.strokeStyle = 'rgba(255,255,255,0.3)';
      ctx.lineWidth = 0.5;
      ctx.stroke();
    }
  });
}

drawWeb();

// Spawn red/blue floating particles
const banner = document.querySelector('.banner');
function spawnParticle() {
  const p = document.createElement('div');
  p.className = 'particle';
  const size = 2 + Math.random() * 4;
  const isRed = Math.random() > 0.5;
  p.style.cssText = `
    width:${size}px; height:${size}px;
    left:${Math.random()*100}%;
    bottom:${28 + Math.random()*40}px;
    background:${isRed ? '#e2001a' : '#4466ff'};
    box-shadow: 0 0 ${size*3}px ${isRed ? '#e2001a' : '#4466ff'};
    animation-duration:${3 + Math.random()*5}s;
    animation-delay:${Math.random()*2}s;
  `;
  banner.appendChild(p);
  setTimeout(() => p.remove(), 8000);
}
setInterval(spawnParticle, 300);
</script>
</body>
</html>
