# Nexora

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Nexora AI — Your Business. Fully Automated.</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --bg:        #080808;
      --bg2:       #0d0d0d;
      --bg3:       #121212;
      --green:     #39FF14;
      --green-dim: #1a7a08;
      --green-glow:rgba(57,255,20,0.15);
      --red:       #ff2d2d;
      --white:     #f0f0f0;
      --grey:      #666;
      --grey2:     #333;
      --border:    rgba(57,255,20,0.12);
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--white);
      font-family: 'Outfit', sans-serif;
      overflow-x: hidden;
      cursor: none;
    }

    .cursor {
      width: 8px; height: 8px;
      background: var(--green);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 99999;
      transition: transform 0.1s;
      box-shadow: 0 0 10px var(--green), 0 0 20px var(--green);
    }
    .cursor-ring {
      width: 32px; height: 32px;
      border: 1px solid rgba(57,255,20,0.5);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 99998;
      transition: all 0.12s ease;
    }

    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background: repeating-linear-gradient(
        0deg, transparent, transparent 2px,
        rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px
      );
      pointer-events: none;
      z-index: 9998;
    }

    .grid-bg {
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(57,255,20,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(57,255,20,0.03) 1px, transparent 1px);
      background-size: 60px 60px;
      pointer-events: none;
      z-index: 0;
    }

    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 1000;
      padding: 20px 60px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: rgba(8,8,8,0.85);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
    }

    .nav-logo {
      display: flex;
      align-items: center;
      gap: 12px;
      text-decoration: none;
    }

    .nav-logo-img {
      width: 36px; height: 36px;
      object-fit: contain;
      filter: drop-shadow(0 0 8px rgba(57,255,20,0.4));
    }

    .nav-logo-text {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 22px;
      letter-spacing: 3px;
      color: var(--white);
    }

    .nav-logo-text span { color: var(--green); text-shadow: 0 0 12px var(--green); }

    .nav-links {
      display: flex;
      align-items: center;
      gap: 40px;
      list-style: none;
    }

    .nav-links a {
      text-decoration: none;
      color: var(--grey);
      font-size: 11px;
      font-weight: 500;
      letter-spacing: 2px;
      text-transform: uppercase;
      transition: color 0.2s;
      font-family: 'JetBrains Mono', monospace;
    }

    .nav-links a:hover { color: var(--green); }

    .nav-cta {
      background: transparent !important;
      color: var(--green) !important;
      border: 1px solid var(--green) !important;
      padding: 9px 24px;
      border-radius: 2px;
      box-shadow: 0 0 12px rgba(57,255,20,0.1);
      transition: all 0.2s !important;
    }

    .nav-cta:hover {
      background: var(--green) !important;
      color: var(--bg) !important;
      box-shadow: 0 0 24px rgba(57,255,20,0.4) !important;
    }

    .hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 140px 60px 80px;
      position: relative;
      z-index: 1;
      overflow: hidden;
    }

    .hero-glow {
      position: absolute;
      top: -20%; right: -5%;
      width: 700px; height: 700px;
      background: radial-gradient(circle, rgba(57,255,20,0.05) 0%, transparent 65%);
      pointer-events: none;
    }

    .hero-glow-2 {
      position: absolute;
      bottom: -10%; left: -10%;
      width: 500px; height: 500px;
      background: radial-gradient(circle, rgba(255,45,45,0.04) 0%, transparent 65%);
      pointer-events: none;
    }

    .hero-tag {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 32px;
      opacity: 0;
      animation: fadeUp 0.8s ease forwards 0.2s;
    }

    .hero-tag-dot {
      width: 6px; height: 6px;
      background: var(--green);
      border-radius: 50%;
      box-shadow: 0 0 8px var(--green);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.3; }
    }

    .hero-tag-text {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      letter-spacing: 3px;
      text-transform: uppercase;
      color: var(--green);
    }

    .hero-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(72px, 10vw, 140px);
      line-height: 0.92;
      letter-spacing: 2px;
      margin-bottom: 8px;
      opacity: 0;
      animation: fadeUp 0.8s ease forwards 0.35s;
    }

    .hero-title .line-green {
      color: var(--green);
      text-shadow: 0 0 40px rgba(57,255,20,0.4), 0 0 80px rgba(57,255,20,0.15);
      display: block;
    }

    .hero-title .line-dim {
      color: var(--grey2);
      display: block;
    }

    .hero-sub {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(20px, 3vw, 38px);
      letter-spacing: 4px;
      color: var(--grey);
      margin-bottom: 56px;
      opacity: 0;
      animation: fadeUp 0.8s ease forwards 0.5s;
    }

    .hero-buttons {
      display: flex;
      gap: 16px;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.8s ease forwards 0.65s;
    }

    .btn-primary {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      background: var(--green);
      color: var(--bg);
      padding: 16px 36px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      font-weight: 500;
      letter-spacing: 2px;
      text-transform: uppercase;
      text-decoration: none;
      border-radius: 2px;
      transition: all 0.25s;
      box-shadow: 0 0 24px rgba(57,255,20,0.3);
    }

    .btn-primary:hover {
      box-shadow: 0 0 48px rgba(57,255,20,0.6);
      transform: translateY(-2px);
    }

    .btn-secondary {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      background: transparent;
      color: var(--white);
      padding: 16px 36px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      letter-spacing: 2px;
      text-transform: uppercase;
      text-decoration: none;
      border-radius: 2px;
      border: 1px solid var(--grey2);
      transition: all 0.25s;
    }

    .btn-secondary:hover {
      border-color: var(--green);
      color: var(--green);
      box-shadow: 0 0 20px rgba(57,255,20,0.1);
      transform: translateY(-2px);
    }

    .ticker {
      position: relative;
      z-index: 1;
      padding: 16px 0;
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      overflow: hidden;
      background: rgba(57,255,20,0.02);
    }

    .ticker-inner {
      display: flex;
      gap: 60px;
      animation: ticker 25s linear infinite;
      white-space: nowrap;
    }

    .ticker-item {
      display: inline-flex;
      align-items: center;
      gap: 12px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--grey);
      flex-shrink: 0;
    }

    .ticker-item span { color: var(--green); }

    @keyframes ticker {
      from { transform: translateX(0); }
      to { transform: translateX(-50%); }
    }

    .section {
      position: relative;
      z-index: 1;
      padding: 100px 60px;
    }

    .section-header { margin-bottom: 64px; }

    .section-tag {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      letter-spacing: 3px;
      text-transform: uppercase;
      color: var(--green);
      margin-bottom: 16px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .section-tag::before {
      content: '';
      width: 20px; height: 1px;
      background: var(--green);
    }

    .section-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(42px, 6vw, 80px);
      letter-spacing: 2px;
      line-height: 0.95;
    }

    .section-desc {
      color: var(--grey);
      font-size: 15px;
      max-width: 480px;
      margin-top: 20px;
      line-height: 1.8;
      font-weight: 300;
    }

    .demo-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1px;
      background: var(--border);
    }

    .demo-card {
      background: var(--bg2);
      padding: 48px 40px;
      text-decoration: none;
      color: inherit;
      display: block;
      position: relative;
      overflow: hidden;
      transition: background 0.3s;
    }

    .demo-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 2px;
      background: var(--green);
      transform: scaleX(0);
      transform-origin: left;
      transition: transform 0.4s;
      box-shadow: 0 0 12px var(--green);
    }

    .demo-card:hover { background: var(--bg3); }
    .demo-card:hover::before { transform: scaleX(1); }

    .demo-num {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      color: var(--green);
      letter-spacing: 2px;
      margin-bottom: 28px;
      opacity: 0.6;
    }

    .demo-card-icon {
      font-size: 32px;
      margin-bottom: 20px;
      display: block;
    }

    .demo-card-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 28px;
      letter-spacing: 1px;
      margin-bottom: 12px;
    }

    .demo-card-desc {
      color: var(--grey);
      font-size: 14px;
      line-height: 1.7;
      margin-bottom: 32px;
      font-weight: 300;
    }

    .demo-link {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--green);
      display: flex;
      align-items: center;
      gap: 8px;
      transition: gap 0.2s;
    }

    .demo-card:hover .demo-link { gap: 14px; }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 1px;
      background: var(--border);
    }

    .stat-item {
      background: var(--bg2);
      padding: 48px 40px;
      position: relative;
    }

    .stat-item::after {
      content: '';
      position: absolute;
      bottom: 0; left: 40px;
      width: 40px; height: 1px;
      background: var(--green);
      box-shadow: 0 0 8px var(--green);
    }

    .stat-num {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 72px;
      letter-spacing: -1px;
      line-height: 1;
      color: var(--green);
      text-shadow: 0 0 30px rgba(57,255,20,0.3);
      margin-bottom: 10px;
    }

    .stat-label {
      color: var(--grey);
      font-size: 13px;
      line-height: 1.5;
      font-weight: 300;
    }

    .social-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1px;
      background: var(--border);
    }

    .social-card {
      background: var(--bg2);
      padding: 40px;
      display: flex;
      align-items: center;
      gap: 20px;
      text-decoration: none;
      color: inherit;
      transition: background 0.3s;
    }

    .social-card:hover { background: var(--bg3); }

    .social-icon {
      width: 52px; height: 52px;
      border: 1px solid var(--grey2);
      border-radius: 2px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 18px;
      flex-shrink: 0;
      font-family: 'JetBrains Mono', monospace;
      transition: all 0.2s;
    }

    .social-card:hover .social-icon {
      border-color: var(--green);
      color: var(--green);
      box-shadow: 0 0 12px rgba(57,255,20,0.2);
    }

    .social-handle {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 18px;
      letter-spacing: 1px;
      margin-bottom: 4px;
    }

    .social-desc { color: var(--grey); font-size: 12px; font-weight: 300; }

    .clients-box {
      border: 1px dashed var(--grey2);
      padding: 80px 40px;
      text-align: center;
      position: relative;
    }

    .clients-box::before {
      content: 'COMING SOON';
      position: absolute;
      top: 20px; right: 24px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 10px;
      letter-spacing: 3px;
      color: var(--grey2);
    }

    .clients-box-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 28px;
      letter-spacing: 2px;
      color: var(--green);
      margin-bottom: 12px;
    }

    .clients-box-desc {
      color: var(--grey);
      font-size: 14px;
      font-weight: 300;
      line-height: 1.7;
    }

    .cta-band {
      margin: 0 60px 80px;
      border: 1px solid var(--border);
      padding: 80px 60px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 40px;
      position: relative;
      overflow: hidden;
      background: var(--bg2);
      z-index: 1;
    }

    .cta-band::before {
      content: '';
      position: absolute;
      top: -1px; left: 0;
      width: 200px; height: 2px;
      background: linear-gradient(90deg, var(--green), transparent);
      box-shadow: 0 0 12px var(--green);
    }

    .cta-band::after {
      content: '';
      position: absolute;
      top: -60px; right: -60px;
      width: 300px; height: 300px;
      background: radial-gradient(circle, rgba(57,255,20,0.04) 0%, transparent 70%);
      pointer-events: none;
    }

    .cta-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(32px, 4vw, 56px);
      letter-spacing: 2px;
      line-height: 1;
    }

    .cta-title span { color: var(--green); }

    .cta-buttons {
      display: flex;
      flex-direction: column;
      gap: 12px;
      flex-shrink: 0;
    }

    footer {
      padding: 40px 60px;
      border-top: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: space-between;
      position: relative;
      z-index: 1;
    }

    .footer-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 18px;
      letter-spacing: 3px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .footer-logo-img {
      width: 24px; height: 24px;
      object-fit: contain;
      filter: drop-shadow(0 0 4px rgba(57,255,20,0.3));
    }

    .footer-logo span { color: var(--green); }

    .footer-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }

    .footer-links a {
      color: var(--grey);
      text-decoration: none;
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      transition: color 0.2s;
    }

    .footer-links a:hover { color: var(--green); }

    .footer-copy {
      color: var(--grey2);
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(28px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .reveal {
      opacity: 0;
      transform: translateY(32px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }

    .reveal.visible { opacity: 1; transform: translateY(0); }

    @media (max-width: 960px) {
      nav { padding: 18px 24px; }
      .nav-links { display: none; }
      .hero { padding: 120px 24px 60px; }
      .section { padding: 60px 24px; }
      .demo-grid, .stats-grid, .social-grid { grid-template-columns: 1fr; }
      .cta-band { margin: 0 24px 60px; padding: 48px 32px; flex-direction: column; }
      footer { padding: 32px 24px; flex-direction: column; gap: 20px; text-align: center; }
    }
  </style>
</head>
<body>

  <div class="cursor" id="cursor"></div>
  <div class="cursor-ring" id="cursorRing"></div>
  <div class="grid-bg"></div>

  <!-- NAV -->
  <nav>
    <a href="index.html" class="nav-logo">
      <img class="nav-logo-img" src="89666.jpg" alt="Nexora AI"/>
      <span class="nav-logo-text">NEXORA<span> AI</span></span>
    </a>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="contact.html">Contact</a></li>
      <li><a href="contact.html" class="nav-cta">Book A Call</a></li>
    </ul>
  </nav>

  <!-- HERO -->
  <section class="hero">
    <div class="hero-glow"></div>
    <div class="hero-glow-2"></div>
    <div class="hero-tag">
      <div class="hero-tag-dot"></div>
      <span class="hero-tag-text">AI Automation Agency — Est. 2026</span>
    </div>
    <h1 class="hero-title">
      <span class="line-green">Your Business.</span>
      <span class="line-dim">Fully</span>
      <span class="line-green">Automated.</span>
    </h1>
    <p class="hero-sub">AI Agents That Work While You Sleep.</p>
    <div class="hero-buttons">
      <a href="contact.html" class="btn-primary">Book Free Discovery Call →</a>
      <a href="https://gumroad.com/YOUR_LINK" target="_blank" class="btn-secondary">Strategy Session — $120</a>
    </div>
  </section>

  <!-- TICKER -->
  <div class="ticker">
    <div class="ticker-inner">
      <div class="ticker-item"><span>◆</span> AI Voice Receptionists</div>
      <div class="ticker-item"><span>◆</span> Chatbot Agents</div>
      <div class="ticker-item"><span>◆</span> Workflow Automation</div>
      <div class="ticker-item"><span>◆</span> Custom SaaS</div>
      <div class="ticker-item"><span>◆</span> 48hr Deployment</div>
      <div class="ticker-item"><span>◆</span> 24/7 Operation</div>
      <div class="ticker-item"><span>◆</span> Zero Downtime</div>
      <div class="ticker-item"><span>◆</span> Global Clients</div>
      <div class="ticker-item"><span>◆</span> AI Voice Receptionists</div>
      <div class="ticker-item"><span>◆</span> Chatbot Agents</div>
      <div class="ticker-item"><span>◆</span> Workflow Automation</div>
      <div class="ticker-item"><span>◆</span> Custom SaaS</div>
      <div class="ticker-item"><span>◆</span> 48hr Deployment</div>
      <div class="ticker-item"><span>◆</span> 24/7 Operation</div>
      <div class="ticker-item"><span>◆</span> Zero Downtime</div>
      <div class="ticker-item"><span>◆</span> Global Clients</div>
    </div>
  </div>

  <!-- DEMO -->
  <section class="section">
    <div class="section-header reveal">
      <div class="section-tag">Our Products</div>
      <h2 class="section-title">See It<br>In Action.</h2>
      <p class="section-desc">Every agent is live-tested and battle-ready. Watch before you commit to anything.</p>
    </div>
    <div class="demo-grid">
      <a href="https://twitter.com/NexoraForge" target="_blank" class="demo-card reveal">
        <div class="demo-num">01 / VOICE</div>
        <span class="demo-card-icon">🎙</span>
        <div class="demo-card-title">AI Voice Receptionist</div>
        <p class="demo-card-desc">Answers every inbound call 24/7. Books appointments. Handles FAQs. Sounds completely human. Never misses a client.</p>
        <span class="demo-link">Watch Demo on X →</span>
      </a>
      <a href="https://twitter.com/NexoraForge" target="_blank" class="demo-card reveal">
        <div class="demo-num">02 / CHAT</div>
        <span class="demo-card-icon">💬</span>
        <div class="demo-card-title">AI Chatbot Agent</div>
        <p class="demo-card-desc">Handles customer queries on your website, WhatsApp and Telegram. Captures leads automatically around the clock.</p>
        <span class="demo-link">Watch Demo on X →</span>
      </a>
      <a href="https://twitter.com/NexoraForge" target="_blank" class="demo-card reveal">
        <div class="demo-num">03 / AUTO</div>
        <span class="demo-card-icon">⚙️</span>
        <div class="demo-card-title">Workflow Automation</div>
        <p class="demo-card-desc">Connect your CRM, email, calendar, and payments into one automated system that runs itself day and night.</p>
        <span class="demo-link">Watch Demo on X →</span>
      </a>
    </div>
  </section>

  <!-- STATS -->
  <div class="stats-grid" style="position:relative;z-index:1;">
    <div class="stat-item reveal">
      <div class="stat-num">100%</div>
      <div class="stat-label">Calls answered<br>automatically</div>
    </div>
    <div class="stat-item reveal">
      <div class="stat-num">48H</div>
      <div class="stat-label">Average deployment<br>time per client</div>
    </div>
    <div class="stat-item reveal">
      <div class="stat-num">24/7</div>
      <div class="stat-label">Your business<br>never closes again</div>
    </div>
    <div class="stat-item reveal">
      <div class="stat-num">80%</div>
      <div class="stat-label">Cost saved vs<br>hiring staff manually</div>
    </div>
  </div>

  <!-- SOCIAL -->
  <section class="section">
    <div class="section-header reveal">
      <div class="section-tag">Follow The Build</div>
      <h2 class="section-title">We Share<br>Everything.</h2>
      <p class="section-desc">Wins, builds, client results and AI breakdowns. All public. No gatekeeping.</p>
    </div>
    <div class="social-grid">
      <a href="https://twitter.com/NexoraForge" target="_blank" class="social-card reveal">
        <div class="social-icon">𝕏</div>
        <div>
          <div class="social-handle">@NexoraForge</div>
          <div class="social-desc">Daily AI automation insights + live demos</div>
        </div>
      </a>
      <a href="https://linkedin.com/company/nexoraai" target="_blank" class="social-card reveal">
        <div class="social-icon" style="font-family:'Outfit',sans-serif;font-size:14px;">in</div>
        <div>
          <div class="social-handle">Nexora AI</div>
          <div class="social-desc">Case studies + industry insights</div>
        </div>
      </a>
      <a href="contact.html" class="social-card reveal">
        <div class="social-icon" style="font-size:16px;">✉</div>
        <div>
          <div class="social-handle">hello@nexoraai.tk</div>
          <div class="social-desc">We respond within 2 hours</div>
        </div>
      </a>
    </div>
  </section>

  <!-- CLIENTS -->
  <section class="section" style="padding-top:0;">
    <div class="section-header reveal">
      <div class="section-tag">Client Work</div>
      <h2 class="section-title">Trusted By<br>Forward Thinkers.</h2>
    </div>
    <div class="clients-box reveal">
      <div class="clients-box-title">Founding Clients Section</div>
      <p class="clients-box-desc">
        Client logos, case studies and project results will appear here.<br>
        Currently accepting 5 founding clients with special early pricing.
      </p>
    </div>
  </section>

  <!-- CTA -->
  <div class="cta-band reveal">
    <h2 class="cta-title">Ready To Put Your<br>Business On <span>Autopilot?</span></h2>
    <div class="cta-buttons">
      <a href="contact.html" class="btn-primary">Book Free Discovery Call</a>
      <a href="https://gumroad.com/YOUR_LINK" target="_blank" class="btn-secondary">Strategy Session — $120</a>
    </div>
  </div>

  <!-- FOOTER -->
  <footer>
    <div class="footer-logo">
      <img class="footer-logo-img" src="89666.jpg" alt="Nexora AI"/>
      NEXORA<span> AI</span>
    </div>
    <ul class="footer-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
    <p class="footer-copy">© 2026 Nexora AI. All rights reserved.</p>
  </footer>

  <script>
    const cursor = document.getElementById('cursor');
    const ring = document.getElementById('cursorRing');
    let mx = 0, my = 0, rx = 0, ry = 0;

    document.addEventListener('mousemove', e => {
      mx = e.clientX; my = e.clientY;
      cursor.style.left = mx - 4 + 'px';
      cursor.style.top = my - 4 + 'px';
    });

    (function animateRing() {
      rx += (mx - rx) * 0.12;
      ry += (my - ry) * 0.12;
      ring.style.left = rx - 16 + 'px';
      ring.style.top = ry - 16 + 'px';
      requestAnimationFrame(animateRing);
    })();

    document.querySelectorAll('a, button').forEach(el => {
      el.addEventListener('mouseenter', () => {
        cursor.style.transform = 'scale(2.5)';
        ring.style.transform = 'scale(1.5)';
        ring.style.borderColor = 'rgba(57,255,20,0.8)';
      });
      el.addEventListener('mouseleave', () => {
        cursor.style.transform = 'scale(1)';
        ring.style.transform = 'scale(1)';
        ring.style.borderColor = 'rgba(57,255,20,0.5)';
      });
    });

    const observer = new IntersectionObserver((entries) => {
      entries.forEach((e, i) => {
        if (e.isIntersecting) {
          setTimeout(() => e.target.classList.add('visible'), i * 80);
        }
      });
    }, { threshold: 0.08 });

    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
  </script>
</body>
</html>
