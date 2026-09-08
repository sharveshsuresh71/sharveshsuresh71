<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sharvesh Suresh — Shark Coding</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@400;600;700;800&family=Inter:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #0a0d16;
    --bg-2: #0f1320;
    --panel: rgba(255,255,255,0.045);
    --panel-border: rgba(255,255,255,0.09);
    --violet: #8b6bff;
    --mint: #34e4b8;
    --coral: #ff6b4a;
    --text: #eceefb;
    --muted: #8a8ea8;
    --mono: 'IBM Plex Mono', monospace;
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html,body{
    background: radial-gradient(ellipse 120% 80% at 50% -10%, #171c33 0%, var(--bg) 55%);
    color: var(--text);
    font-family: 'Inter', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }
  /* parallax grid backdrop */
  .grid-layer{
    position: fixed;
    inset: -10%;
    background-image:
      linear-gradient(rgba(139,107,255,0.07) 1px, transparent 1px),
      linear-gradient(90deg, rgba(139,107,255,0.07) 1px, transparent 1px);
    background-size: 46px 46px;
    transform: perspective(600px) rotateX(55deg) translateZ(0);
    transform-origin: top center;
    z-index: 0;
    pointer-events: none;
    mask-image: linear-gradient(to bottom, black, transparent 70%);
  }
  .glow-orb{
    position: fixed;
    width: 480px; height: 480px;
    border-radius: 50%;
    filter: blur(110px);
    opacity: 0.25;
    z-index: 0;
    pointer-events: none;
  }
  .glow-orb.a{ background: var(--violet); top: -120px; left: -100px; }
  .glow-orb.b{ background: var(--mint); bottom: -160px; right: -120px; }

  main{
    position: relative;
    z-index: 1;
    max-width: 980px;
    margin: 0 auto;
    padding: 72px 24px 120px;
  }

  /* ===== HERO 3D CARD ===== */
  .stage{ perspective: 1200px; margin-bottom: 64px; }
  .hero{
    position: relative;
    background: var(--panel);
    border: 1px solid var(--panel-border);
    backdrop-filter: blur(18px);
    border-radius: 26px;
    padding: 48px 44px;
    transform-style: preserve-3d;
    transition: transform 0.12s ease-out;
    box-shadow: 0 40px 80px -30px rgba(0,0,0,0.6);
    will-change: transform;
  }
  .hero::before{
    content:'';
    position:absolute; inset:0;
    border-radius: 26px;
    padding: 1px;
    background: linear-gradient(135deg, rgba(139,107,255,0.6), rgba(52,228,184,0.15) 40%, transparent 70%);
    -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
    -webkit-mask-composite: xor;
    mask-composite: exclude;
    pointer-events: none;
  }
  .hero-inner{ transform: translateZ(40px); transform-style: preserve-3d; }
  .eyebrow{
    display:inline-flex; align-items:center; gap:8px;
    font-family: var(--mono);
    font-size: 12.5px;
    color: var(--mint);
    letter-spacing: 0.02em;
    margin-bottom: 18px;
  }
  .eyebrow .dot{ width:6px; height:6px; border-radius:50%; background: var(--mint); box-shadow: 0 0 10px var(--mint); }
  h1{
    font-family: 'Sora', sans-serif;
    font-weight: 800;
    font-size: clamp(34px, 5vw, 52px);
    line-height: 1.05;
    letter-spacing: -0.02em;
    transform: translateZ(60px);
  }
  h1 span{ color: var(--violet); }
  .role{
    margin-top: 14px;
    font-size: 17px;
    color: var(--muted);
    max-width: 520px;
    line-height: 1.55;
    transform: translateZ(30px);
  }
  .tags{
    margin-top: 26px;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    transform: translateZ(25px);
  }
  .tag{
    font-family: var(--mono);
    font-size: 12.5px;
    padding: 7px 14px;
    border-radius: 999px;
    border: 1px solid var(--panel-border);
    color: var(--muted);
    background: rgba(255,255,255,0.02);
  }
  .cta-row{
    margin-top: 34px;
    display:flex; gap:14px; flex-wrap: wrap;
    transform: translateZ(45px);
  }
  .btn{
    font-family: 'Inter', sans-serif;
    font-weight: 600;
    font-size: 14.5px;
    padding: 13px 24px;
    border-radius: 12px;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    transition: transform 0.15s ease, box-shadow 0.15s ease;
  }
  .btn.primary{
    background: linear-gradient(135deg, var(--violet), #6a4bff);
    color: #fff;
    box-shadow: 0 12px 30px -10px rgba(139,107,255,0.6);
  }
  .btn.ghost{
    background: transparent;
    border: 1px solid var(--panel-border);
    color: var(--text);
  }
  .btn:hover{ transform: translateY(-2px); }

  /* ===== SECTION LABEL ===== */
  .section-head{
    display: flex; align-items: baseline; justify-content: space-between;
    margin: 0 0 22px;
  }
  .section-head h2{
    font-family: 'Sora', sans-serif;
    font-size: 22px;
    font-weight: 700;
  }
  .section-head p{ color: var(--muted); font-size: 14px; }

  /* ===== BENTO PROJECT GRID ===== */
  .bento{
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 18px;
    margin-bottom: 68px;
  }
  .card{
    position: relative;
    background: var(--panel);
    border: 1px solid var(--panel-border);
    border-radius: 20px;
    padding: 26px;
    perspective: 900px;
    overflow: hidden;
    cursor: pointer;
  }
  .card-inner{
    transform-style: preserve-3d;
    transition: transform 0.35s cubic-bezier(.2,.9,.3,1);
    height: 100%;
    display: flex; flex-direction: column; justify-content: space-between;
  }
  .card:hover .card-inner{ transform: translateZ(24px) rotateX(4deg); }
  .card .glow{
    position:absolute; width: 220px; height: 220px; border-radius: 50%;
    filter: blur(60px); opacity: 0; transition: opacity 0.35s ease;
    top: -60px; right: -60px; pointer-events:none;
  }
  .card:hover .glow{ opacity: 0.35; }
  .card.c1{ grid-column: span 4; grid-row: span 2; min-height: 240px; }
  .card.c1 .glow{ background: var(--violet); }
  .card.c2{ grid-column: span 2; grid-row: span 1; }
  .card.c2 .glow{ background: var(--mint); }
  .card.c3{ grid-column: span 2; grid-row: span 1; }
  .card.c3 .glow{ background: var(--coral); }
  .card.c4{ grid-column: span 3; grid-row: span 1; }
  .card.c4 .glow{ background: var(--mint); }
  .card.c5{ grid-column: span 3; grid-row: span 1; }
  .card.c5 .glow{ background: var(--violet); }

  .card-label{ font-family: var(--mono); font-size: 11.5px; color: var(--mint); letter-spacing: 0.03em; margin-bottom: 10px; }
  .card h3{ font-family: 'Sora', sans-serif; font-size: 19px; font-weight: 700; margin-bottom: 10px; }
  .card.c1 h3{ font-size: 25px; }
  .card p{ color: var(--muted); font-size: 13.5px; line-height: 1.55; }
  .card .stack{ margin-top: 16px; display:flex; gap:8px; flex-wrap: wrap; }
  .card .stack span{
    font-family: var(--mono); font-size: 10.5px; color: var(--text);
    background: rgba(255,255,255,0.06); padding: 4px 9px; border-radius: 6px;
  }
  .card .arrow{
    align-self: flex-end;
    font-family: var(--mono);
    font-size: 13px;
    color: var(--muted);
    margin-top: 14px;
  }

  /* ===== FOOTER ===== */
  footer{
    text-align: center;
    color: var(--muted);
    font-family: var(--mono);
    font-size: 12.5px;
    padding-top: 30px;
    border-top: 1px solid var(--panel-border);
  }

  @media (max-width: 720px){
    .bento{ grid-template-columns: repeat(2, 1fr); }
    .card.c1, .card.c2, .card.c3, .card.c4, .card.c5{ grid-column: span 2; }
    .hero{ padding: 34px 26px; }
  }

  @media (prefers-reduced-motion: reduce){
    .hero, .card-inner{ transition: none !important; }
  }
</style>
</head>
<body>

<div class="grid-layer" id="gridLayer"></div>
<div class="glow-orb a"></div>
<div class="glow-orb b"></div>

<main>
  <div class="stage">
    <div class="hero" id="heroCard">
      <div class="hero-inner">
        <div class="eyebrow"><span class="dot"></span> AVAILABLE FOR WORK</div>
        <h1>Sharvesh Suresh<br><span>builds things that hold up.</span></h1>
        <p class="role">B.Tech Information Technology student at Panimalar Engineering College, Chennai — building under the brand <strong style="color:var(--text)">Shark Coding</strong>. AI tooling, security, and clean web builds.</p>
        <div class="tags">
          <span class="tag">React</span>
          <span class="tag">Python</span>
          <span class="tag">Node.js</span>
          <span class="tag">Security</span>
          <span class="tag">AI/ML</span>
        </div>
        <div class="cta-row">
          <a class="btn primary" href="https://portfoliosharveshz.vercel.app" target="_blank">View Portfolio</a>
          <a class="btn ghost" href="https://github.com/sharveshsuresh71" target="_blank">GitHub ↗</a>
        </div>
      </div>
    </div>
  </div>

  <div class="section-head">
    <h2>Featured builds</h2>
    <p>move your cursor over a card</p>
  </div>

  <div class="bento">
    <div class="card c1">
      <div class="glow"></div>
      <div class="card-inner">
        <div>
          <div class="card-label">FEATURED · AI/ML</div>
          <h3>AI Expense Tracker</h3>
          <p>Type "spent 500 on dinner" and it logs, categorizes, and budgets automatically — no forms, no manual entry.</p>
          <div class="stack"><span>HTML</span><span>ML</span><span>NLP</span></div>
        </div>
        <div class="arrow">sharveshsuresh71/AI-Expense-tracker →</div>
      </div>
    </div>

    <div class="card c2">
      <div class="glow"></div>
      <div class="card-inner">
        <div>
          <div class="card-label">SECURITY</div>
          <h3>Vulnerability Scanner</h3>
          <p>Automated recon + web app checks.</p>
        </div>
        <div class="arrow">Python →</div>
      </div>
    </div>

    <div class="card c3">
      <div class="glow"></div>
      <div class="card-inner">
        <div>
          <div class="card-label">SECURITY</div>
          <h3>Password Analyzer</h3>
          <p>Grades strength vs. real cracking methods.</p>
        </div>
        <div class="arrow">HTML/JS →</div>
      </div>
    </div>

    <div class="card c4">
      <div class="glow"></div>
      <div class="card-inner">
        <div>
          <div class="card-label">ML PIPELINE</div>
          <h3>Phishing Email Detection</h3>
          <p>Flags malicious emails via text stats + structural red flags.</p>
        </div>
        <div class="arrow">Python →</div>
      </div>
    </div>

    <div class="card c5">
      <div class="glow"></div>
      <div class="card-inner">
        <div>
          <div class="card-label">SYSTEMS</div>
          <h3>Billing System</h3>
          <p>Product pricing, discounts, tax, final bill — end to end.</p>
        </div>
        <div class="arrow">C →</div>
      </div>
    </div>
  </div>

  <footer>designed &amp; built by Shark Coding — tilt responds to your cursor, not a screenshot</footer>
</main>

<script>
  const hero = document.getElementById('heroCard');
  const grid = document.getElementById('gridLayer');
  const stage = document.querySelector('.stage');

  stage.addEventListener('mousemove', (e) => {
    const r = hero.getBoundingClientRect();
    const x = (e.clientX - r.left) / r.width - 0.5;
    const y = (e.clientY - r.top) / r.height - 0.5;
    hero.style.transform = `rotateY(${x * 10}deg) rotateX(${-y * 10}deg)`;
    grid.style.transform = `perspective(600px) rotateX(55deg) translate(${x * 20}px, ${y * 10}px)`;
  });
  stage.addEventListener('mouseleave', () => {
    hero.style.transform = 'rotateY(0deg) rotateX(0deg)';
    grid.style.transform = 'perspective(600px) rotateX(55deg) translate(0,0)';
  });

  // subtle per-card mouse-driven tilt
  document.querySelectorAll('.card').forEach(card => {
    const inner = card.querySelector('.card-inner');
    card.addEventListener('mousemove', (e) => {
      const r = card.getBoundingClientRect();
      const x = (e.clientX - r.left) / r.width - 0.5;
      const y = (e.clientY - r.top) / r.height - 0.5;
      inner.style.transform = `translateZ(24px) rotateX(${-y * 8}deg) rotateY(${x * 8}deg)`;
      card.querySelector('.glow').style.left = `${e.clientX - r.left - 110}px`;
      card.querySelector('.glow').style.top = `${e.clientY - r.top - 110}px`;
    });
    card.addEventListener('mouseleave', () => {
      inner.style.transform = 'translateZ(0) rotateX(0) rotateY(0)';
    });
  });
</script>
</body>
</html>
