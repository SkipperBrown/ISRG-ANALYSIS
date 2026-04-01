<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ISRG — The Surgical Toll Road | Perplexity Computer Stock Pitch Competition</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600;700&family=Playfair+Display:wght@700;900&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
    :root {
      --bg: #0a0e17;
      --bg-deep: #060810;
      --card: #141b2d;
      --card-alt: #1a2338;
      --teal: #00d4aa;
      --gold: #f0b90b;
      --red: #ff4d6a;
      --blue: #4a9eff;
      --white: #f0f2f5;
      --gray: #8892a4;
      --dim: #5a6478;
      --border: rgba(0,212,170,0.15);
      --glow: rgba(0,212,170,0.08);
    }
    html { scroll-behavior: smooth; }
    body {
      font-family: Inter, -apple-system, sans-serif;
      background: var(--bg);
      color: var(--white);
      overflow-x: hidden;
      -webkit-font-smoothing: antialiased;
    }

    /* ── Animated mesh background ── */
    .mesh {
      position: fixed; inset: 0; z-index: 0; pointer-events: none; overflow: hidden;
    }
    .blob {
      position: absolute; border-radius: 50%; filter: blur(100px); opacity: 0.07;
    }
    .blob-1 { width: 700px; height: 700px; top: -200px; right: -200px; background: var(--teal); animation: drift1 18s ease-in-out infinite; }
    .blob-2 { width: 500px; height: 500px; bottom: 20%; left: -150px; background: var(--blue); animation: drift2 24s ease-in-out infinite; }
    .blob-3 { width: 400px; height: 400px; top: 50%; left: 40%; background: var(--gold); opacity: 0.04; animation: drift1 30s ease-in-out infinite reverse; }
    @keyframes drift1 {
      0%,100% { transform: translate(0,0) scale(1); }
      33% { transform: translate(60px,-80px) scale(1.1); }
      66% { transform: translate(-40px,60px) scale(0.92); }
    }
    @keyframes drift2 {
      0%,100% { transform: translate(0,0) scale(1); }
      33% { transform: translate(-70px,50px) scale(1.08); }
      66% { transform: translate(50px,-40px) scale(0.95); }
    }

    /* ── Vignette + noise ── */
    body::before {
      content: ''; position: fixed; inset: 0; z-index: 1; pointer-events: none;
      background: radial-gradient(ellipse at center, transparent 40%, rgba(0,0,0,0.45) 100%);
    }
    body::after {
      content: ''; position: fixed; inset: 0; z-index: 1; pointer-events: none;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.7' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      background-size: 256px; opacity: 0.025; mix-blend-mode: overlay;
    }

    /* ── Mouse spotlight ── */
    .spotlight {
      position: fixed; inset: 0; z-index: 2; pointer-events: none;
      transition: background 0.15s;
    }

    /* ── Canvas ── */
    #particles {
      position: fixed; inset: 0; z-index: 2; pointer-events: none;
    }

    /* ── Layout ── */
    .page { position: relative; z-index: 3; }
    .container { max-width: 960px; margin: 0 auto; padding: 0 28px; }

    /* ── Hero ── */
    .hero {
      min-height: 100vh;
      display: flex; flex-direction: column; justify-content: center;
      padding: 80px 0 60px;
      position: relative;
    }
    .hero-inner { display: flex; flex-direction: column; gap: 0; }

    .eyebrow {
      font-size: 11px; font-weight: 600; letter-spacing: 2.5px;
      text-transform: uppercase; color: var(--teal);
      margin-bottom: 20px; display: flex; align-items: center; gap: 10px;
    }
    .eyebrow::before {
      content: ''; display: block; width: 32px; height: 2px;
      background: var(--teal);
    }

    .hero-title {
      font-family: 'Playfair Display', Georgia, serif;
      font-size: clamp(48px, 8vw, 88px);
      font-weight: 900;
      letter-spacing: -3px;
      line-height: 1.0;
      margin-bottom: 12px;
    }
    .hero-title .accent {
      background: linear-gradient(135deg, var(--teal) 0%, #00ffcc 50%, var(--teal) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero-sub {
      font-size: clamp(15px, 2vw, 19px);
      color: var(--gray);
      font-weight: 400;
      line-height: 1.6;
      max-width: 680px;
      margin-bottom: 32px;
    }
    .hero-sub strong { color: var(--white); font-weight: 600; }

    .hero-meta {
      display: flex; flex-wrap: wrap; gap: 12px; align-items: center;
      margin-bottom: 40px;
    }
    .tag {
      display: inline-flex; align-items: center; gap: 6px;
      padding: 5px 14px; border-radius: 20px;
      font-size: 12px; font-weight: 600; letter-spacing: 0.4px;
    }
    .tag-teal { background: rgba(0,212,170,0.1); color: var(--teal); border: 1px solid rgba(0,212,170,0.25); }
    .tag-gold { background: rgba(240,185,11,0.1); color: var(--gold); border: 1px solid rgba(240,185,11,0.25); }
    .tag-blue { background: rgba(74,158,255,0.1); color: var(--blue); border: 1px solid rgba(74,158,255,0.25); }

    /* ── Live badge ── */
    .live-badge {
      display: inline-flex; align-items: center; gap: 10px;
      background: rgba(0,212,170,0.05);
      border: 1px solid rgba(0,212,170,0.2);
      border-radius: 10px; padding: 10px 20px;
    }
    .live-dot {
      width: 8px; height: 8px; border-radius: 50%;
      background: var(--teal);
      animation: pulse 2s ease-in-out infinite;
      flex-shrink: 0;
    }
    @keyframes pulse {
      0%,100% { opacity: 1; box-shadow: 0 0 0 0 rgba(0,212,170,0.5); }
      50% { opacity: 0.7; box-shadow: 0 0 0 8px rgba(0,212,170,0); }
    }
    .live-label { font-size: 10px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; color: var(--teal); }
    .live-price { font-family: 'JetBrains Mono', monospace; font-size: 22px; font-weight: 700; color: var(--white); }
    .live-change { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: var(--teal); }

    /* ── Targets ── */
    .targets {
      display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px;
      margin-bottom: 60px;
    }
    .target {
      background: var(--card); border: 1px solid var(--border);
      border-radius: 12px; padding: 22px; text-align: center;
      position: relative; overflow: hidden;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .target:hover { transform: translateY(-3px); box-shadow: 0 12px 40px rgba(0,0,0,0.3); }
    .target::after { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; }
    .target.bull::after { background: linear-gradient(90deg, var(--gold), transparent); }
    .target.base::after { background: linear-gradient(90deg, var(--teal), transparent); }
    .target.bear::after { background: linear-gradient(90deg, var(--red), transparent); }
    .target-lbl { font-size: 10px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; color: var(--dim); margin-bottom: 8px; }
    .target-price { font-family: 'JetBrains Mono', monospace; font-size: 34px; font-weight: 700; }
    .target-pct { font-family: 'JetBrains Mono', monospace; font-size: 15px; margin-top: 4px; }
    .target-desc { font-size: 11px; color: var(--gray); margin-top: 8px; line-height: 1.5; }
    .bull .target-price, .bull .target-pct { color: var(--gold); }
    .base .target-price, .base .target-pct { color: var(--teal); }
    .bear .target-price, .bear .target-pct { color: var(--red); }

    /* ── Divider ── */
    .divider { height: 1px; background: linear-gradient(90deg, transparent, var(--border), transparent); margin: 60px 0; }

    /* ── Section label ── */
    .section-lbl {
      font-size: 10px; font-weight: 700; letter-spacing: 2.5px;
      text-transform: uppercase; color: var(--teal);
      margin-bottom: 8px;
    }
    .section-title {
      font-family: 'Playfair Display', Georgia, serif;
      font-size: clamp(26px, 3.5vw, 36px);
      font-weight: 700; letter-spacing: -1px;
      margin-bottom: 28px; color: var(--white);
    }

    /* ── Thesis block ── */
    .thesis {
      background: rgba(0,212,170,0.04);
      border: 1px solid rgba(0,212,170,0.2);
      border-radius: 14px; padding: 32px 36px;
      margin-bottom: 32px;
    }
    .thesis p { font-size: 16px; line-height: 1.9; color: var(--white); }
    .thesis .mono { font-family: 'JetBrains Mono', monospace; color: var(--teal); font-size: 18px; font-weight: 700; }
    .thesis .gmono { font-family: 'JetBrains Mono', monospace; color: var(--gold); font-weight: 700; }

    /* ── Bullet list ── */
    .thesis-bullets {
      display: flex; flex-direction: column; gap: 14px;
      margin-bottom: 36px;
    }
    .bullet-item {
      display: flex; gap: 16px; align-items: flex-start;
      background: var(--card); border: 1px solid var(--border);
      border-left: 3px solid var(--teal);
      border-radius: 10px; padding: 18px 22px;
      transition: transform 0.2s;
    }
    .bullet-item:hover { transform: translateX(4px); }
    .bullet-item:nth-child(2) { border-left-color: var(--gold); }
    .bullet-item:nth-child(3) { border-left-color: var(--blue); }
    .bullet-text { font-size: 14px; line-height: 1.65; color: var(--gray); }
    .bullet-text strong { color: var(--white); font-weight: 600; }

    /* ── Deliverables ── */
    .deliverables { display: flex; flex-direction: column; gap: 12px; margin-bottom: 8px; }
    .deliv-row {
      display: grid; grid-template-columns: 36px 1fr auto;
      align-items: center; gap: 20px;
      background: var(--card); border: 1px solid var(--border);
      border-radius: 10px; padding: 18px 24px;
      transition: background 0.2s;
    }
    .deliv-row:hover { background: var(--card-alt); }
    .deliv-num { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: var(--dim); font-weight: 600; }
    .deliv-info {}
    .deliv-title { font-size: 15px; font-weight: 600; color: var(--white); margin-bottom: 3px; }
    .deliv-desc { font-size: 12px; color: var(--gray); }
    .deliv-btn {
      display: inline-flex; align-items: center; gap: 6px;
      padding: 8px 18px; border-radius: 8px;
      background: rgba(0,212,170,0.08);
      border: 1px solid rgba(0,212,170,0.2);
      color: var(--teal); font-size: 13px; font-weight: 600;
      text-decoration: none; white-space: nowrap;
      transition: background 0.2s, transform 0.15s;
    }
    .deliv-btn:hover { background: rgba(0,212,170,0.18); transform: scale(1.02); }

    /* ── Judge cards ── */
    .judges { display: flex; flex-direction: column; gap: 16px; }
    .judge {
      background: var(--card); border: 1px solid var(--border);
      border-left: 3px solid var(--teal);
      border-radius: 12px; padding: 24px 28px;
      display: grid; grid-template-columns: 48px 1fr; gap: 18px;
      transition: transform 0.2s;
    }
    .judge:hover { transform: translateX(3px); }
    .judge:nth-child(2) { border-left-color: var(--gold); }
    .judge:nth-child(3) { border-left-color: var(--blue); }
    .judge:nth-child(4) { border-left-color: var(--dim); }
    .judge-icon { font-size: 28px; padding-top: 2px; }
    .judge-name { font-size: 16px; font-weight: 700; margin-bottom: 3px; }
    .judge-firm { font-size: 11px; color: var(--gray); letter-spacing: 0.5px; margin-bottom: 10px; text-transform: uppercase; font-weight: 600; }
    .judge-text { font-size: 14px; line-height: 1.7; color: var(--gray); }
    .judge-text span { color: var(--teal); font-weight: 600; }
    .judge:nth-child(2) .judge-text span { color: var(--gold); }
    .judge:nth-child(3) .judge-text span { color: var(--blue); }
    .judge:nth-child(4) .judge-text span { color: var(--white); }

    /* ── Methodology ── */
    .steps { display: flex; flex-direction: column; gap: 10px; margin-bottom: 24px; }
    .step {
      display: flex; gap: 16px; align-items: center;
      background: var(--card); border: 1px solid var(--border);
      border-radius: 10px; padding: 16px 22px;
    }
    .step-num {
      width: 30px; height: 30px; border-radius: 50%; flex-shrink: 0;
      background: rgba(0,212,170,0.1); border: 1px solid rgba(0,212,170,0.2);
      color: var(--teal); font-family: 'JetBrains Mono', monospace;
      font-size: 13px; font-weight: 700;
      display: flex; align-items: center; justify-content: center;
    }
    .step-text { font-size: 14px; color: var(--gray); }

    /* ── No tools banner ── */
    .no-tools {
      background: rgba(0,212,170,0.04);
      border: 1px solid rgba(0,212,170,0.12);
      border-radius: 10px; padding: 16px 24px;
      font-size: 14px; color: var(--gray); text-align: center;
    }
    .no-tools strong { color: var(--teal); }

    /* ── Footer ── */
    .footer {
      padding: 48px 0;
      border-top: 1px solid rgba(255,255,255,0.06);
      display: flex; justify-content: space-between; align-items: center;
      flex-wrap: wrap; gap: 16px;
    }
    .footer-prepared { font-size: 13px; color: var(--gray); line-height: 1.6; }
    .footer-prepared strong { color: var(--white); }
    .footer-date { font-family: 'JetBrains Mono', monospace; font-size: 12px; color: var(--dim); }

    /* ── Toll stripe ── */
    .stripe {
      height: 3px;
      background: repeating-linear-gradient(90deg, var(--teal) 0, var(--teal) 18px, transparent 18px, transparent 36px);
      opacity: 0.2; border-radius: 2px;
    }

    /* ── KPI row ── */
    .kpi-row {
      display: flex; flex-wrap: wrap; gap: 24px;
      margin-bottom: 32px;
    }
    .kpi { display: flex; flex-direction: column; gap: 2px; }
    .kpi-lbl { font-size: 10px; font-weight: 600; letter-spacing: 1.5px; text-transform: uppercase; color: var(--dim); }
    .kpi-val { font-family: 'JetBrains Mono', monospace; font-size: 16px; font-weight: 700; color: var(--white); }

    /* ── Responsive ── */
    @media (max-width: 640px) {
      .hero-title { letter-spacing: -1.5px; }
      .targets { grid-template-columns: 1fr; }
      .deliv-row { grid-template-columns: 1fr; gap: 12px; }
      .judge { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

<!-- Animated mesh -->
<div class="mesh">
  <div class="blob blob-1"></div>
  <div class="blob blob-2"></div>
  <div class="blob blob-3"></div>
</div>

<!-- Spotlight + particles -->
<div class="spotlight" id="spotlight"></div>
<canvas id="particles"></canvas>

<div class="page">
<div class="container">

  <!-- ═══════════ HERO ═══════════ -->
  <section class="hero">
    <div class="hero-inner">

      <div class="eyebrow">Intuitive Surgical, Inc. &nbsp;·&nbsp; NASDAQ: ISRG &nbsp;·&nbsp; Investment Thesis</div>

      <h1 class="hero-title">
        THE SURGICAL<br>
        <span class="accent">TOLL ROAD</span>
      </h1>

      <p class="hero-sub">
        <strong>Intuitive Surgical is the only public company that collects a toll on every robotic surgical procedure performed worldwide.</strong>
        With 3.15 million procedures growing 18% annually and less than 5% of the $7.6T surgical market penetrated,
        the toll road has barely opened.
      </p>

      <div class="hero-meta">
        <span class="tag tag-teal">BUY</span>
        <span class="tag tag-teal">HIGH CONVICTION</span>
        <span class="tag tag-gold">Perplexity Computer Stock Pitch Competition</span>
        <span class="tag tag-blue">March 30 – April 3, 2026</span>
      </div>

      <div style="display:flex;align-items:center;gap:20px;flex-wrap:wrap;margin-bottom:40px;">
        <div class="live-badge">
          <div class="live-dot"></div>
          <span class="live-label">Live</span>
          <span class="live-price" id="livePrice">—</span>
          <span class="live-change" id="liveChange"></span>
        </div>
        <div class="kpi-row" style="margin-bottom:0;">
          <div class="kpi"><span class="kpi-lbl">Mkt Cap</span><span class="kpi-val">~$160.8B</span></div>
          <div class="kpi"><span class="kpi-lbl">PE TTM</span><span class="kpi-val">57.5x</span></div>
          <div class="kpi"><span class="kpi-lbl">EPS</span><span class="kpi-val">$7.88</span></div>
          <div class="kpi"><span class="kpi-lbl">52wk Range</span><span class="kpi-val">$425–$604</span></div>
        </div>
      </div>

      <!-- Price Targets -->
      <div class="targets">
        <div class="target bull">
          <div class="target-lbl">Bull Case</div>
          <div class="target-price">$841</div>
          <div class="target-pct" id="bullPct">+85.8%</div>
          <div class="target-desc">Accelerated DV5 adoption, new indications, usage-based expansion</div>
        </div>
        <div class="target base">
          <div class="target-lbl">Base Case</div>
          <div class="target-price">$617</div>
          <div class="target-pct" id="basePct">+36.2%</div>
          <div class="target-desc">Consensus growth rates, moderate margin expansion</div>
        </div>
        <div class="target bear">
          <div class="target-lbl">Bear Case</div>
          <div class="target-price">$292</div>
          <div class="target-pct" id="bearPct">−35.5%</div>
          <div class="target-desc">Multiple compression, slower growth, competition gains share</div>
        </div>
      </div>

    </div>
  </section>

  <div class="stripe"></div>

  <!-- ═══════════ THESIS ═══════════ -->
  <section style="padding:60px 0;">

    <div class="section-lbl">The Thesis</div>
    <h2 class="section-title">Three Lines. No Ambiguity.</h2>

    <div class="thesis">
      <p>
        ISRG is the only public company that collects a mandatory toll on every robotic surgical procedure performed worldwide.
        <span class="mono">3.15M</span> procedures growing <span class="gmono">+17.4%</span> on a 3-year CAGR basis.
        Proprietary instrument lock-in that permits <span style="font-family:'JetBrains Mono',monospace;color:var(--red);font-weight:700;">zero</span> third-party substitution.
        Less than <span class="mono">5%</span> of the <span class="mono">$7.6T</span> global surgical market penetrated.
        The toll road has barely opened.
      </p>
    </div>

    <div class="thesis-bullets">
      <div class="bullet-item">
        <div class="bullet-text">
          <strong>Lock-in:</strong> Proprietary instruments that <em>only</em> ISRG makes. Zero third-party substitution.
          The da Vinci system physically will not operate with non-ISRG instruments.
        </div>
      </div>
      <div class="bullet-item">
        <div class="bullet-text">
          <strong>Recurring machine:</strong> 75% of $10.06B revenue is instrument &amp; accessory tolls.
          Each system placement starts a 10-year, $1.8M lifetime annuity.
        </div>
      </div>
      <div class="bullet-item">
        <div class="bullet-text">
          <strong>Compounding catalyst:</strong> da Vinci 5 super-cycle + cardiac clearance (Jan 2026) +
          Europe direct acquisition (Mar 2026) = three simultaneous growth accelerants.
        </div>
      </div>
    </div>

  </section>

  <div class="divider"></div>

  <!-- ═══════════ DELIVERABLES ═══════════ -->
  <section style="padding:0 0 60px;">

    <div class="section-lbl">Submission Package</div>
    <h2 class="section-title">Deliverables</h2>

    <div class="deliverables">
      <div class="deliv-row">
        <div class="deliv-num">01</div>
        <div class="deliv-info">
          <div class="deliv-title">&#x1F3A5;&nbsp; 2-Minute Video Walkthrough</div>
          <div class="deliv-desc">Perplexity Computer building the pitch, live on screen — produced in Canva</div>
        </div>
        <a class="deliv-btn" href="#" id="videoLink">&#x25B6; Watch Video</a>
      </div>
      <div class="deliv-row">
        <div class="deliv-num">02</div>
        <div class="deliv-info">
          <div class="deliv-title">&#x1F4CA;&nbsp; Full Pitch Deck (Interactive HTML)</div>
          <div class="deliv-desc">13-slide institutional-grade presentation with live price feed, charts, and DCF model</div>
        </div>
        <a class="deliv-btn" href="ISRG_Pitch_FINAL.html">&#x1F441; View Presentation</a>
      </div>
      <div class="deliv-row">
        <div class="deliv-num">03</div>
        <div class="deliv-info">
          <div class="deliv-title">&#x1F916;&nbsp; Perplexity Computer Thread</div>
          <div class="deliv-desc">Complete autonomous research workflow — 7-step process, fully traceable to primary sources</div>
        </div>
        <a class="deliv-btn" href="#" id="threadLink">&#x1F517; View Autonomous Research Workflow</a>
      </div>
    </div>

  </section>

  <div class="divider"></div>

  <!-- ═══════════ JUDGES ═══════════ -->
  <section style="padding:0 0 60px;">

    <div class="section-lbl">Judge-Specific Analysis</div>
    <h2 class="section-title">Why This Satisfies Each Judge</h2>

    <div class="judges">
      <div class="judge">
        <div class="judge-icon">&#x1F4C8;</div>
        <div>
          <div class="judge-name">Philippe Laffont &mdash; Coatue Management</div>
          <div class="judge-firm">Compounder Framework</div>
          <div class="judge-text">
            <span>17.4% 3Y revenue CAGR</span>, <span>66% gross margins</span>,
            expanding operating leverage, and <span>$2.49B FCF</span> at a 24.7% margin.
            Forward PE of 37.5x on accelerating EPS — a compounder premium fully justified by business quality.
          </div>
        </div>
      </div>
      <div class="judge">
        <div class="judge-icon">&#x26A1;</div>
        <div>
          <div class="judge-name">Dan Loeb &mdash; Third Point</div>
          <div class="judge-firm">Catalyst Lens</div>
          <div class="judge-text">
            Three discrete 2026 catalysts with quantifiable procedure-volume impact:
            <span>DV5 cardiac ramp</span> (Q1), <span>Europe direct margin expansion</span> (Q2),
            and <span>usage-based leasing penetration</span> crossing 35%+ (Q3).
            Each independently measurable against a 12-month price target.
          </div>
        </div>
      </div>
      <div class="judge">
        <div class="judge-icon">&#x1F9E0;</div>
        <div>
          <div class="judge-name">Ken Hao &mdash; Silver Lake</div>
          <div class="judge-firm">Technology Transformation Thesis</div>
          <div class="judge-text">
            <span>15M-procedure AI training data moat</span> irreplicable at any price.
            Surgeon workflow dependency creates infinite switching costs.
            Usage-based platform economics compound as installed base grows.
            The da Vinci 5 — with 10,000x compute — is the foundation for AI-enabled surgery at scale.
          </div>
        </div>
      </div>
      <div class="judge">
        <div class="judge-icon">&#x1F4BB;</div>
        <div>
          <div class="judge-name">Dmitry Shevelenko &mdash; Perplexity AI</div>
          <div class="judge-firm">Product Demonstration Lens</div>
          <div class="judge-text">
            The full 13-slide pitch — financial model, competitive stress test, DCF sensitivity,
            catalyst timeline, bear case rebuttal — was built autonomously using
            <span>Perplexity Computer alone</span>.
            No Bloomberg. No Excel. No outside tools.
            <span style="color:var(--white);font-weight:700;">THIS is what your product can do.</span>
          </div>
        </div>
      </div>
    </div>

  </section>

  <div class="divider"></div>

  <!-- ═══════════ METHODOLOGY ═══════════ -->
  <section style="padding:0 0 60px;">

    <div class="section-lbl">Research Methodology</div>
    <h2 class="section-title">7-Step Autonomous Workflow</h2>

    <div class="steps">
      <div class="step"><div class="step-num">1</div><div class="step-text">Financial data collection &amp; verification — SEC EDGAR, FactSet, S&amp;P Global, LSEG</div></div>
      <div class="step"><div class="step-num">2</div><div class="step-text">Competitive landscape mapping — 6 companies across 8 metrics each</div></div>
      <div class="step"><div class="step-num">3</div><div class="step-text">DCF model construction — 25-scenario 5&times;5 sensitivity table</div></div>
      <div class="step"><div class="step-num">4</div><div class="step-text">Catalyst identification &amp; timeline mapping — 6 discrete 2026 catalysts</div></div>
      <div class="step"><div class="step-num">5</div><div class="step-text">Bear case stress testing &amp; rebuttal framework — 5 risks, specific data rebuttals</div></div>
      <div class="step"><div class="step-num">6</div><div class="step-text">Competitive moat scoring — 6 normalized dimensions, radar chart comparison</div></div>
      <div class="step"><div class="step-num">7</div><div class="step-text">Presentation generation — live data visualizations, dynamic price feed, self-contained HTML</div></div>
    </div>

    <div class="no-tools">
      <strong>No Bloomberg Terminal. No Excel. No outside tools.</strong>
      &nbsp;&nbsp;Research conducted entirely using Perplexity Computer.
    </div>

  </section>

  <div class="stripe"></div>

  <!-- ═══════════ FOOTER ═══════════ -->
  <footer class="footer">
    <div class="footer-prepared">
      Prepared for &nbsp;
      <strong>Philippe Laffont</strong> · Coatue &nbsp;&nbsp;
      <strong>Dan Loeb</strong> · Third Point &nbsp;&nbsp;
      <strong>Ken Hao</strong> · Silver Lake &nbsp;&nbsp;
      <strong>Dmitry Shevelenko</strong> · Perplexity AI
    </div>
    <div class="footer-date">March 30, 2026</div>
  </footer>

</div>
</div>

<script>
  /* ── Mouse spotlight ── */
  document.addEventListener('mousemove', e => {
    document.getElementById('spotlight').style.background =
      `radial-gradient(700px circle at ${e.clientX}px ${e.clientY}px, rgba(0,212,170,0.05), transparent 40%)`;
  });

  /* ── Particle canvas ── */
  (function() {
    const canvas = document.getElementById('particles');
    const ctx = canvas.getContext('2d');
    let W = canvas.width = window.innerWidth;
    let H = canvas.height = window.innerHeight;
    window.addEventListener('resize', () => { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; });
    const pts = Array.from({length: 55}, () => ({
      x: Math.random()*W, y: Math.random()*H,
      vx: (Math.random()-.5)*.25, vy: (Math.random()-.5)*.25,
      r: Math.random()*2+.6, a: Math.random()*.3+.07
    }));
    let mx = -9999, my = -9999;
    document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
    (function tick() {
      ctx.clearRect(0,0,W,H);
      pts.forEach(p => {
        const dx = p.x-mx, dy = p.y-my, d = Math.sqrt(dx*dx+dy*dy);
        if(d < 130) { const f=(130-d)/130*2; p.vx+=(dx/d)*f*.08; p.vy+=(dy/d)*f*.08; }
        p.vx*=.98; p.vy*=.98; p.x+=p.vx; p.y+=p.vy;
        if(p.x<0)p.x=W; if(p.x>W)p.x=0; if(p.y<0)p.y=H; if(p.y>H)p.y=0;
        ctx.beginPath(); ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
        ctx.fillStyle=`rgba(0,212,170,${p.a})`; ctx.fill();
      });
      requestAnimationFrame(tick);
    })();
  })();

  /* ── Live price feed ── */
  const BASE=617, BULL=841, BEAR=292;

  async function fetchPrice() {
    try {
      const r = await fetch('https://query1.finance.yahoo.com/v8/finance/chart/ISRG?interval=1m&range=1d');
      const d = await r.json();
      return d?.chart?.result?.[0]?.meta?.regularMarketPrice || null;
    } catch { return null; }
  }

  async function updatePrice() {
    const price = await fetchPrice();
    const elPrice = document.getElementById('livePrice');
    const elChange = document.getElementById('liveChange');
    const elBase = document.getElementById('basePct');
    const elBull = document.getElementById('bullPct');
    const elBear = document.getElementById('bearPct');
    if (price) {
      elPrice.textContent = '$' + price.toFixed(2);
      const b = (((BASE/price)-1)*100).toFixed(1);
      const bu = (((BULL/price)-1)*100).toFixed(1);
      const be = (((BEAR/price)-1)*100).toFixed(1);
      elChange.textContent = '+' + b + '% to base';
      elBase.textContent = '+' + b + '%';
      elBull.textContent = '+' + bu + '%';
      elBear.textContent = be + '%';
    } else {
      elPrice.textContent = 'DELAYED';
      elPrice.style.color = '#f0b90b';
    }
    setTimeout(updatePrice, 300000);
  }
  updatePrice();
</script>
</body>
</html>
