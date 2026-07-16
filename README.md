<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GRADEDESK — Free AI Setup Grading for Traders</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #0B0F14;
    --bg-raised: #10161D;
    --bg-inset: #080B0F;
    --line: #1D2630;
    --line-soft: #161D25;
    --ink: #E8ECEF;
    --ink-dim: #8B96A3;
    --ink-faint: #5B6672;
    --bull: #00D9A3;
    --bear: #FF5C5C;
    --amber: #FFB020;
    --font-display: 'Space Grotesk', sans-serif;
    --font-body: 'Inter', sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
  }

  *{margin:0; padding:0; box-sizing:border-box;}

  html{scroll-behavior:smooth;}

  body{
    background: var(--bg);
    color: var(--ink);
    font-family: var(--font-body);
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
    overflow-x: hidden;
  }

  @media (prefers-reduced-motion: reduce){
    *{animation-duration: 0.01ms !important; animation-iteration-count: 1 !important; transition-duration: 0.01ms !important;}
  }

  a{color:inherit; text-decoration:none;}
  button{font-family:inherit; cursor:pointer;}

  ::selection{ background: var(--amber); color: #0B0F14; }

  :focus-visible{
    outline: 2px solid var(--amber);
    outline-offset: 3px;
  }

  .wrap{
    max-width: 1180px;
    margin: 0 auto;
    padding: 0 28px;
  }

  /* ---------- Ticker ---------- */
  .ticker-bar{
    background: var(--bg-inset);
    border-bottom: 1px solid var(--line);
    overflow: hidden;
    white-space: nowrap;
    height: 34px;
    display:flex;
    align-items:center;
  }
  .ticker-track{
    display:inline-flex;
    animation: scroll-left 45s linear infinite;
  }
  .ticker-item{
    font-family: var(--font-mono);
    font-size: 11.5px;
    letter-spacing: 0.02em;
    padding: 0 22px;
    color: var(--ink-dim);
    border-right: 1px solid var(--line-soft);
  }
  .ticker-item b{ color: var(--ink); font-weight: 500; margin-right: 6px;}
  .up{ color: var(--bull); }
  .down{ color: var(--bear); }
  @keyframes scroll-left{
    0% { transform: translate3d(0, 0, 0); }
    100% { transform: translate3d(-50%, 0, 0); }
  }

  /* ---------- Nav ---------- */
  nav{
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding: 20px 0;
    border-bottom: 1px solid var(--line);
  }
  .logo{
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 19px;
    letter-spacing: -0.01em;
    display:flex;
    align-items:center;
    gap: 9px;
  }
  .logo-mark{
    width: 22px; height: 22px;
    display:flex; align-items:center; justify-content:center;
  }
  .nav-links{
    display:flex;
    align-items:center;
    gap: 34px;
    font-size: 13.5px;
    color: var(--ink-dim);
  }
  .nav-links a:hover{ color: var(--ink); }
  
  /* Класс кнопки в меню */
  .nav-cta{
    background: var(--bull);
    color: #06120E;
    padding: 9px 18px;
    border-radius: 5px;
    font-weight: 600;
    font-size: 13px;
    transition: filter 0.15s;
    border: none;
  }
  .nav-cta:hover{ filter: brightness(1.08); }
  .nav-mobile-hide{ display:flex; }
  @media (max-width: 760px){
    .nav-mobile-hide{ display:none; }
  }

  /* ---------- Hero ---------- */
  .hero{
    padding: 88px 0 70px;
    display:grid;
    grid-template-columns: 1.05fr 0.95fr;
    gap: 40px;
    align-items:center;
    position:relative;
  }
  @media (max-width: 900px){
    .hero{ grid-template-columns: 1fr; padding: 56px 0 48px; }
  }

  .eyebrow{
    font-family: var(--font-mono);
    font-size: 11.5px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--amber);
    display:flex;
    align-items:center;
    gap: 9px;
    margin-bottom: 22px;
  }
  .eyebrow::before{
    content:'';
    width: 7px; height: 7px;
    background: var(--amber);
    border-radius: 50%;
    box-shadow: 0 0 0 3px rgba(255,176,32,0.15);
  }

  h1{
    font-family: var(--font-display);
    font-size: clamp(36px, 4.6vw, 58px);
    line-height: 1.03;
    font-weight: 700;
    letter-spacing: -0.02em;
    margin-bottom: 22px;
  }
  h1 em{
    font-style: normal;
    color: var(--bull);
  }

  .hero-sub{
    font-size: 16.5px;
    color: var(--ink-dim);
    max-width: 460px;
    margin-bottom: 32px;
  }

  .hero-actions{
    display:flex;
    align-items:center;
    gap: 18px;
    flex-wrap:wrap;
  }

  .btn-primary{
    background: var(--ink);
    color: #0B0F14;
    padding: 13px 24px;
    border-radius: 6px;
    font-weight: 600;
    font-size: 14.5px;
    border: none;
    transition: transform 0.15s, filter 0.15s;
    display:inline-flex;
    align-items:center;
    gap: 8px;
  }
  .btn-primary:hover{ transform: translateY(-1px); filter: brightness(1.05); }

  .btn-ghost{
    font-size: 13.5px;
    color: var(--ink-dim);
    display:flex;
    align-items:center;
    gap: 8px;
    border-bottom: 1px solid var(--line);
    padding-bottom: 2px;
  }
  .btn-ghost:hover{ color: var(--ink); border-color: var(--ink-dim); }

  .hero-meta{
    margin-top: 26px;
    font-family: var(--font-mono);
    font-size: 11.5px;
    color: var(--ink-faint);
  }

  /* ---------- Hero visual: chart + stamp ---------- */
  .hero-visual{
    position:relative;
    background: var(--bg-raised);
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 22px 22px 18px;
    transition: border-color 0.3s ease;
  }
  .visual-head{
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-bottom: 14px;
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--ink-faint);
  }
  .visual-head .sym{ color: var(--ink); font-weight: 700; letter-spacing: 0.03em; }
  .dot-row{ display:flex; gap:6px; }
  .dot-row span{ width:7px; height:7px; border-radius:50%; background: var(--line); display:inline-block; }

  .chart-svg{ width: 100%; height: auto; display:block; }

  .stamp{
    position:absolute;
    top: 34px;
    right: 22px;
    transform: rotate(-9deg);
    border: 3px solid var(--bull);
    color: var(--bull);
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 34px;
    padding: 4px 14px;
    border-radius: 8px;
    letter-spacing: 0.02em;
    background: rgba(0,217,163,0.06);
    box-shadow: 0 0 0 3px rgba(0,217,163,0.05);
  }
  .stamp small{
    display:block;
    font-family: var(--font-mono);
    font-size: 9px;
    letter-spacing: 0.1em;
    text-align:center;
    font-weight: 500;
    margin-top: 1px;
  }

  .visual-stats{
    display:grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
    border-radius: 7px;
    overflow:hidden;
    margin-top: 16px;
  }
  .vstat{
    background: var(--bg-inset);
    padding: 11px 12px;
  }
  .vstat .l{ font-family: var(--font-mono); font-size: 9.5px; color: var(--ink-faint); text-transform:uppercase; letter-spacing: 0.06em; margin-bottom: 5px;}
  .vstat .v{ font-family: var(--font-mono); font-size: 14px; font-weight: 700; }
  .vstat .v.bull{ color: var(--bull); }
  .vstat .v.bear{ color: var(--bear); }

  /* ---------- Section shared ---------- */
  section{ padding: 76px 0; border-top: 1px solid var(--line); }
  .section-head{
    display:flex;
    justify-content:space-between;
    align-items:flex-end;
    gap: 24px;
    margin-bottom: 46px;
    flex-wrap: wrap;
  }
  .section-label{
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--ink-faint);
    margin-bottom: 12px;
  }
  h2{
    font-family: var(--font-display);
    font-size: clamp(26px, 3vw, 36px);
    font-weight: 600;
    letter-spacing: -0.015em;
    max-width: 560px;
  }
  .section-sub{
    color: var(--ink-dim);
    font-size: 14.5px;
    max-width: 340px;
  }

  /* ---------- How it works ---------- */
  .flow{
    display:grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
    border-radius: 10px;
    overflow: hidden;
  }
  @media (max-width: 800px){ .flow{ grid-template-columns: 1fr; } }

  .flow-step{
    background: var(--bg-raised);
    padding: 30px 26px 26px;
    position:relative;
  }
  .flow-tag{
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--amber);
    letter-spacing: 0.08em;
    margin-bottom: 20px;
    display:block;
  }
  .flow-step h3{
    font-family: var(--font-display);
    font-size: 19px;
    font-weight: 600;
    margin-bottom: 10px;
  }
  .flow-step p{
    font-size: 13.5px;
    color: var(--ink-dim);
    line-height: 1.6;
  }

  /* ---------- Sample grade cards ---------- */
  .grades{
    display:grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }
  @media (max-width: 900px){ .grades{ grid-template-columns: 1fr; } }

  .gcard{
    background: var(--bg-raised);
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 22px;
    transition: border-color 0.2s, transform 0.2s;
  }
  .gcard:hover{ border-color: var(--ink-faint); transform: translateY(-2px); }

  .gcard-top{
    display:flex;
    justify-content:space-between;
    align-items:flex-start;
    margin-bottom: 18px;
  }
  .gcard-sym{
    font-family: var(--font-mono);
    font-weight: 700;
    font-size: 14px;
  }
  .gcard-tf{ font-family: var(--font-mono); font-size: 10.5px; color: var(--ink-faint); }

  .badge{
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 22px;
    padding: 3px 11px;
    border-radius: 6px;
    line-height: 1;
  }
  .badge.a{ background: rgba(0,217,163,0.12); color: var(--bull); border: 1px solid rgba(0,217,163,0.35); }
  .badge.b{ background: rgba(255,176,32,0.12); color: var(--amber); border: 1px solid rgba(255,176,32,0.35); }
  .badge.d{ background: rgba(255,92,92,0.12); color: var(--bear); border: 1px solid rgba(255,92,92,0.35); }

  .gcard-row{
    display:flex;
    justify-content:space-between;
    font-family: var(--font-mono);
    font-size: 12px;
    padding: 8px 0;
    border-top: 1px solid var(--line-soft);
  }
  .gcard-row .l{ color: var(--ink-faint); }
  .gcard-row .v{ color: var(--ink); font-weight: 500; }

  .gcard-note{
    margin-top: 14px;
    font-size: 12.5px;
    color: var(--ink-dim);
    line-height: 1.55;
    padding-top: 14px;
    border-top: 1px solid var(--line-soft);
  }

  /* ---------- Stats strip ---------- */
  .stats-strip{
    display:grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
    border-radius: 10px;
    overflow:hidden;
  }
  @media (max-width: 700px){ .stats-strip{ grid-template-columns: repeat(2, 1fr); } }
  .sstat{
    background: var(--bg-raised);
    padding: 26px 22px;
  }
  .sstat .n{
    font-family: var(--font-display);
    font-size: 30px;
    font-weight: 700;
    margin-bottom: 6px;
  }
  .sstat .l{ font-size: 12.5px; color: var(--ink-dim); }

  /* ---------- CTA ---------- */
  .cta-block{
    text-align:center;
    padding: 90px 0 100px;
  }
  .cta-block h2{ margin: 0 auto 16px; }
  .cta-block .section-sub{ margin: 0 auto 34px; max-width: 420px; text-align:center; }

  /* ---------- Footer ---------- */
  footer{
    border-top: 1px solid var(--line);
    padding: 40px 0 60px;
  }
  .foot-top{
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding-bottom: 28px;
    border-bottom: 1px solid var(--line);
    margin-bottom: 24px;
    flex-wrap: wrap;
    gap: 16px;
  }
  .foot-links{
    display:flex;
    gap: 26px;
    font-size: 13px;
    color: var(--ink-dim);
  }
  .foot-links a:hover{ color: var(--ink); }
  .foot-bottom{
    display:flex;
    justify-content:space-between;
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--ink-faint);
    flex-wrap: wrap;
    gap: 10px;
  }
  .foot-legal{ max-width: 560px; line-height: 1.6; }
</style>
</head>
<body>

  <div class="ticker-bar">
    <div class="ticker-track" id="tickerTrack"></div>
  </div>

  <div class="wrap">
    <nav>
      <div class="logo">
        <span class="logo-mark">
          <svg width="22" height="22" viewBox="0 0 100 100"><polygon points="50,8 86,28 86,72 50,92 14,72 14,28" fill="none" stroke="#00D9A3" stroke-width="4"></polygon><rect x="32" y="56" width="7" height="22" fill="#00D9A3"></rect><rect x="46" y="42" width="7" height="36" fill="#FFB020"></rect><rect x="60" y="30" width="7" height="48" fill="#00D9A3"></rect></svg>
        </span>
        GRADEDESK
      </div>
      <div class="nav-links nav-mobile-hide">
        <a href="#how">How it works</a>
        <a href="#samples">Sample grades</a>
        <a href="#faq">FAQ</a>
      </div>
      <!-- Кнопка в меню с ID "navCtaBtn" -->
      <button class="nav-cta" id="navCtaBtn">Analyze chart free</button>
    </nav>

    <section class="hero" style="border-top:none; padding-top:88px;">
      <div>
        <div class="eyebrow">Now grading forex, crypto &amp; futures</div>
        <h1>Know if the setup is <em>real</em><br>before you click buy.</h1>
        <p class="hero-sub">Upload a screenshot of any chart. GradeDesk reads the structure, checks it against your trading profile, and hands back a letter grade with the entry, stop, and targets — in under ten seconds.</p>
        <div class="hero-actions">
          <!-- Кнопка в шапке с ID "analyzeBtn" -->
          <button class="btn-primary" id="analyzeBtn">
            Grade my next chart
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
          </button>
          <a href="#samples" class="btn-ghost">See a real grade →</a>
        </div>
        <div class="hero-meta">NO REGISTRATION · UNLIMITED USE · RESULTS IN ~8S</div>
      </div>

      <div class="hero-visual" id="heroVisual">
        <div class="visual-head">
          <span class="sym">NVDA · 5M</span>
          <div class="dot-row"><span></span><span></span><span></span></div>
        </div>
        <svg class="chart-svg" viewBox="0 0 460 190" id="chartSvg">
          <defs>
            <linearGradient id="fillGrad" x1="0" y1="0" x2="0" y2="1">
              <stop offset="0%" stop-color="#00D9A3" stop-opacity="0.22"/>
              <stop offset="100%" stop-color="#00D9A3" stop-opacity="0"/>
            </linearGradient>
          </defs>
          <g stroke="#161D25" stroke-width="1">
            <line x1="0" y1="30" x2="460" y2="30"/>
            <line x1="0" y1="70" x2="460" y2="70"/>
            <line x1="0" y1="110" x2="460" y2="110"/>
            <line x1="0" y1="150" x2="460" y2="150"/>
          </g>
          <polyline points="0,140 20,148 40,130 60,138 80,120 100,126 120,100 140,108 160,90 180,96 200,72 220,80 240,60 260,68 280,48 300,54 320,36 340,42 360,26 380,32 400,18 420,24 440,14 460,10"
            fill="none" stroke="#00D9A3" stroke-width="2.5" stroke-linejoin="round" stroke-linecap="round"/>
          <polygon points="0,140 20,148 40,130 60,138 80,120 100,126 120,100 140,108 160,90 180,96 200,72 220,80 240,60 260,68 280,48 300,54 320,36 340,42 360,26 380,32 400,18 420,24 440,14 460,10 460,190 0,190"
            fill="url(#fillGrad)"/>
          <line x1="0" y1="96" x2="460" y2="96" stroke="#5B6672" stroke-width="1" stroke-dasharray="4 4"/>
          <line x1="0" y1="158" x2="460" y2="158" stroke="#FF5C5C" stroke-width="1" stroke-dasharray="4 4"/>
        </svg>
        <div class="stamp">A+<small>SETUP</small></div>
        <div class="visual-stats">
          <div class="vstat"><div class="l">Entry</div><div class="v">881.40</div></div>
          <div class="vstat"><div class="l">Stop</div><div class="v bear">874.10</div></div>
          <div class="vstat"><div class="l">Target 2</div><div class="v bull">896.80</div></div>
          <div class="vstat"><div class="l">R:R</div><div class="v">1 : 2.1</div></div>
        </div>
      </div>
    </section>
  </div>

  <section id="how">
    <div class="wrap">
      <div class="section-head">
        <div>
          <div class="section-label">Process</div>
          <h2>Three steps, no chart theory required.</h2>
        </div>
        <p class="section-sub">You bring the screenshot. GradeDesk brings the pattern recognition and the discipline you skip at 9:32am.</p>
      </div>
      <div class="flow">
        <div class="flow-step">
          <span class="flow-tag">STEP 1 — UPLOAD</span>
          <h3>Drop in any chart</h3>
          <p>TradingView, ThinkOrSwim, Webull, MT4 — screenshot it straight from your platform. No account linking, no API keys.</p>
        </div>
        <div class="flow-step">
          <span class="flow-tag">STEP 2 — READ</span>
          <h3>It reads the structure</h3>
          <p>Price action, volume, MACD, EMAs, VWAP — checked against your saved trading profile: your instrument, timeframe, and risk tolerance.</p>
        </div>
        <div class="flow-step">
          <span class="flow-tag">STEP 3 — GRADE</span>
          <h3>Get a graded plan</h3>
          <p>A letter grade, entry, invalidation, and two profit targets. Skip the setups graded C and below — that's the whole point.</p>
        </div>
      </div>
    </div>
  </section>

  <section id="samples">
    <div class="wrap">
      <div class="section-head">
        <div>
          <div class="section-label">Sample output</div>
          <h2>What a grade actually looks like.</h2>
        </div>
        <p class="section-sub">Three real submissions, graded blind, from three different traders.</p>
      </div>
      <div class="grades">
        <div class="gcard">
          <div class="gcard-top">
            <div><div class="gcard-sym">MSTR · 15M</div><div class="gcard-tf">Breakout continuation</div></div>
            <div class="badge a">A</div>
          </div>
          <div class="gcard-row"><span class="l">Entry</span><span class="v">203.40</span></div>
          <div class="gcard-row"><span class="l">Stop</span><span class="v">198.90</span></div>
          <div class="gcard-row"><span class="l">Target 1 / 2</span><span class="v">211.0 / 219.5</span></div>
          <div class="gcard-row"><span class="l">Risk : Reward</span><span class="v">1 : 2.4</span></div>
          <div class="gcard-note">Clean break above the 20EMA with rising volume. VWAP reclaim confirms — the kind of structure worth sizing up.</div>
        </div>
        <div class="gcard">
          <div class="gcard-top">
            <div><div class="gcard-sym">EUR/USD · 1H</div><div class="gcard-tf">Range fade</div></div>
            <div class="badge b">C+</div>
          </div>
          <div class="gcard-row"><span class="l">Entry</span><span class="v">1.0862</span></div>
          <div class="gcard-row"><span class="l">Stop</span><span class="v">1.0841</span></div>
          <div class="gcard-row"><span class="l">Target 1 / 2</span><span class="v">1.0890 / 1.0912</span></div>
          <div class="gcard-row"><span class="l">Risk : Reward</span><span class="v">1 : 1.3</span></div>
          <div class="gcard-note">Setup works but reward is thin against the stop distance. Fine as a scalp, weak as a swing.</div>
        </div>
        <div class="gcard">
          <div class="gcard-top">
            <div><div class="gcard-sym">SOL/USDT · 5M</div><div class="gcard-tf">Late-entry chase</div></div>
            <div class="badge d">D</div>
          </div>
          <div class="gcard-row"><span class="l">Entry</span><span class="v">146.20</span></div>
          <div class="gcard-row"><span class="l">Stop</span><span class="v">143.10</span></div>
          <div class="gcard-row"><span class="l">Target 1 / 2</span><span class="v">148.0 / —</span></div>
          <div class="gcard-row"><span class="l">Risk : Reward</span><span class="v">1 : 0.6</span></div>
          <div class="gcard-note">Already extended 4% off the base with no pullback. Stop is wide, target is close. Let it come back.</div>
        </div>
      </div>
    </div>
  </section>

  <section>
    <div class="wrap">
      <div class="stats-strip">
        <div class="sstat"><div class="n">210K+</div><div class="l">charts graded to date</div></div>
        <div class="sstat"><div class="n">~8s</div><div class="l">average grade time</div></div>
        <div class="sstat"><div class="n">14</div><div class="l">indicators cross-checked</div></div>
        <div class="sstat"><div class="n">6</div><div class="l">asset classes supported</div></div>
      </div>
    </div>
  </section>

  <section id="faq">
    <div class="wrap">
      <div class="section-head">
        <div>
          <div class="section-label">Before you ask</div>
          <h2>A few things worth knowing.</h2>
        </div>
      </div>
      <div class="flow">
        <div class="flow-step">
          <h3>Is this financial advice?</h3>
          <p>No. GradeDesk grades chart structure against your own rules — it doesn't know your account size or your life. Every grade is a starting point, not an order.</p>
        </div>
        <div class="flow-step">
          <h3>What's a "trading profile"?</h3>
          <p>The risk tolerance, timeframe, and instruments you tell GradeDesk about once. Every grade after that is checked against your rules, not a generic template.</p>
        </div>
        <div class="flow-step">
          <h3>Can I export a grade?</h3>
          <p>Yes — every graded chart can be saved to your journal or exported as an image, so you can review what you actually took versus what you skipped.</p>
        </div>
      </div>
    </div>
  </section>

  <section class="cta-block" style="border-top: 1px solid var(--line);">
    <div class="wrap">
      <h2>Absolutely free. No card, no catch.</h2>
      <p class="section-sub">Grade unlimited charts whenever you need them.</p>
      <!-- Кнопка внизу с ID "analyzeBtn2" -->
      <button class="btn-primary" id="analyzeBtn2">Grade my next chart</button>
    </div>
  </section>

  <footer>
    <div class="wrap">
      <div class="foot-top">
        <div class="logo" style="font-size:16px;">
          <span class="logo-mark">
            <svg width="18" height="18" viewBox="0 0 100 100"><polygon points="50,8 86,28 86,72 50,92 14,72 14,28" fill="none" stroke="#00D9A3" stroke-width="4"></polygon><rect x="32" y="56" width="7" height="22" fill="#00D9A3"></rect><rect x="46" y="42" width="7" height="36" fill="#FFB020"></rect><rect x="60" y="30" width="7" height="48" fill="#00D9A3"></rect></svg>
          </span>
          GRADEDESK
        </div>
        <div class="foot-links">
          <a href="#how">How it works</a>
          <a href="#samples">Sample grades</a>
          <a href="#faq">FAQ</a>
        </div>
      </div>
      <div class="foot-bottom">
        <div class="foot-legal">GradeDesk is a free chart-analysis tool, not a licensed financial advisor. Grades reflect technical structure only and are not investment advice. Trading involves risk of loss.</div>
        <div>© 2026 GRADEDESK</div>
      </div>
    </div>
  </footer>

<script>
  // Ticker content
  const tickerData = [
    ['NVDA', '881.40', '+2.3%', true],
    ['BTC/USD', '68,214', '-1.1%', false],
    ['EUR/USD', '1.0862', '+0.2%', true],
    ['MSTR', '203.40', '+4.8%', true],
    ['SOL/USDT', '146.20', '-3.4%', false],
    ['AAPL', '224.10', '+0.6%', true],
    ['GBP/JPY', '198.30', '-0.4%', false],
    ['ETH/USD', '3,412', '+1.7%', true],
    ['TSLA', '256.90', '-2.0%', false],
    ['XAU/USD', '2,398', '+0.9%', true],
  ];
  const track = document.getElementById('tickerTrack');
  function buildTicker(){
    let html = '';
    for(let rep=0; rep<4; rep++){
      tickerData.forEach(([sym, price, chg, up])=>{
        html += `<span class="ticker-item"><b>${sym}</b>${price} <span class="${up?'up':'down'}">${chg}</span></span>`;
      });
    }
    track.innerHTML = html;
  }
  buildTicker();

  // Функция для анимации штампа и рамки графика
  function pulseStamp(){
    const stamp = document.querySelector('.stamp');
    const visual = document.getElementById('heroVisual');
    if(!stamp || !visual) return;
    
    visual.style.borderColor = 'var(--bull)';
    stamp.style.transition = 'transform 0.35s ease';
    stamp.style.transform = 'rotate(-9deg) scale(1.25)';
    
    setTimeout(()=>{ 
      stamp.style.transform = 'rotate(-9deg) scale(1)'; 
      visual.style.borderColor = 'var(--line)';
    }, 350);
  }
  
  // Плавный скролл к графику
  const scrollAndPulse = (e) => {
    if (e) e.preventDefault(); // Предотвращаем перезагрузку страницы или скачок
    const target = document.getElementById('heroVisual');
    if (target) {
      target.scrollIntoView({ behavior: 'smooth', block: 'center' });
      setTimeout(pulseStamp, 400);
    }
  };

  // Навешиваем слушатели событий на кнопки
  document.addEventListener('DOMContentLoaded', () => {
    const btn1 = document.getElementById('analyzeBtn');
    const btn2 = document.getElementById('analyzeBtn2');
    const navBtn = document.getElementById('navCtaBtn');

    if (btn1) btn1.addEventListener('click', scrollAndPulse);
    if (btn2) btn2.addEventListener('click', scrollAndPulse);
    if (navBtn) navBtn.addEventListener('click', scrollAndPulse);
  });
</script>

</body>
</html>
