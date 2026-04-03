[index.html.html](https://github.com/user-attachments/files/26454378/index.html.html)
<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PRINT∞LAB — 3D打印工作室</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Noto+Sans+TC:wght@300;400;500&family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050810;
    --bg2: #080d1a;
    --cyan: #00f5ff;
    --cyan2: #00bcd4;
    --orange: #ff6b35;
    --white: #e8f4f8;
    --gray: #4a6070;
    --grid: rgba(0,245,255,0.04);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--white);
    font-family: 'Noto Sans TC', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    border: 1px solid var(--cyan);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, border-color 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-dot {
    width: 4px; height: 4px;
    background: var(--cyan);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
  }

  /* Grid background */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image:
      linear-gradient(var(--grid) 1px, transparent 1px),
      linear-gradient(90deg, var(--grid) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none; z-index: 0;
  }

  /* Scanline */
  body::after {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.03) 2px,
      rgba(0,0,0,0.03) 4px
    );
    pointer-events: none; z-index: 1;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 20px 60px;
    background: linear-gradient(to bottom, rgba(5,8,16,0.95), transparent);
    backdrop-filter: blur(4px);
  }
  .nav-logo {
    font-family: 'Orbitron', monospace;
    font-size: 1.2rem;
    font-weight: 900;
    color: var(--cyan);
    letter-spacing: 0.15em;
    text-decoration: none;
    text-shadow: 0 0 20px rgba(0,245,255,0.5);
  }
  .nav-logo span { color: var(--orange); }
  .nav-links { display: flex; gap: 40px; list-style: none; }
  .nav-links a {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.75rem;
    color: var(--gray);
    text-decoration: none;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    transition: color 0.3s;
  }
  .nav-links a:hover { color: var(--cyan); }

  /* HERO */
  #hero {
    position: relative; z-index: 2;
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center; align-items: flex-start;
    padding: 0 60px;
    overflow: hidden;
  }

  .hero-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--cyan);
    letter-spacing: 0.3em;
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.8s 0.3s forwards;
  }
  .hero-tag::before { content: '// '; color: var(--orange); }

  h1 {
    font-family: 'Orbitron', monospace;
    font-size: clamp(3rem, 8vw, 7rem);
    font-weight: 900;
    line-height: 1;
    letter-spacing: -0.02em;
    margin-bottom: 8px;
    opacity: 0;
    animation: fadeUp 0.8s 0.5s forwards;
  }
  h1 .line1 { display: block; color: var(--white); }
  h1 .line2 {
    display: block;
    -webkit-text-stroke: 1px var(--cyan);
    color: transparent;
    text-shadow: 0 0 40px rgba(0,245,255,0.3);
  }

  .hero-sub {
    font-size: 1rem;
    color: var(--gray);
    max-width: 440px;
    line-height: 1.8;
    margin: 32px 0 48px;
    opacity: 0;
    animation: fadeUp 0.8s 0.7s forwards;
  }

  .hero-cta {
    display: flex; gap: 16px;
    opacity: 0;
    animation: fadeUp 0.8s 0.9s forwards;
  }
  .btn-primary {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.8rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--bg);
    background: var(--cyan);
    border: none;
    padding: 14px 32px;
    cursor: none;
    text-decoration: none;
    display: inline-block;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
    transition: background 0.2s, box-shadow 0.2s;
  }
  .btn-primary:hover {
    background: #fff;
    box-shadow: 0 0 30px rgba(0,245,255,0.6);
  }
  .btn-secondary {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.8rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--cyan);
    background: transparent;
    border: 1px solid rgba(0,245,255,0.3);
    padding: 14px 32px;
    cursor: none;
    text-decoration: none;
    display: inline-block;
    transition: border-color 0.2s, background 0.2s;
  }
  .btn-secondary:hover {
    border-color: var(--cyan);
    background: rgba(0,245,255,0.05);
  }

  /* Rotating 3D shape */
  .hero-visual {
    position: absolute; right: 8%; top: 50%; transform: translateY(-50%);
    width: 380px; height: 380px;
    opacity: 0;
    animation: fadeIn 1.2s 1s forwards;
  }
  .hex-ring {
    position: absolute; inset: 0;
    border: 1px solid rgba(0,245,255,0.15);
    border-radius: 50%;
    animation: spin 20s linear infinite;
  }
  .hex-ring:nth-child(2) {
    inset: 30px;
    border-color: rgba(0,245,255,0.1);
    animation-direction: reverse;
    animation-duration: 15s;
  }
  .hex-ring:nth-child(3) {
    inset: 60px;
    border-color: rgba(255,107,53,0.1);
    animation-duration: 25s;
  }
  .hex-center {
    position: absolute; inset: 90px;
    background: radial-gradient(circle at 40% 40%, rgba(0,245,255,0.1), transparent 60%),
                radial-gradient(circle at 70% 70%, rgba(255,107,53,0.05), transparent 50%);
    border: 1px solid rgba(0,245,255,0.2);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
  }
  .hex-center::before {
    content: '3D';
    font-family: 'Orbitron', monospace;
    font-size: 2.5rem;
    font-weight: 900;
    color: transparent;
    -webkit-text-stroke: 1px rgba(0,245,255,0.5);
  }
  .dot-orbit {
    position: absolute; inset: 0;
    animation: spin 8s linear infinite;
  }
  .dot-orbit::before {
    content: '';
    position: absolute; top: 0; left: 50%;
    width: 8px; height: 8px;
    background: var(--cyan);
    border-radius: 50%;
    transform: translate(-50%, -4px);
    box-shadow: 0 0 12px var(--cyan);
  }
  .dot-orbit2 {
    position: absolute; inset: 30px;
    animation: spin 12s linear infinite reverse;
  }
  .dot-orbit2::before {
    content: '';
    position: absolute; right: 0; top: 50%;
    width: 6px; height: 6px;
    background: var(--orange);
    border-radius: 50%;
    transform: translate(3px, -50%);
    box-shadow: 0 0 10px var(--orange);
  }

  /* SECTION base */
  section { position: relative; z-index: 2; padding: 100px 60px; }
  .section-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    color: var(--cyan);
    letter-spacing: 0.4em;
    text-transform: uppercase;
    margin-bottom: 16px;
  }
  .section-tag::before { content: '['; color: var(--orange); margin-right: 4px; }
  .section-tag::after { content: ']'; color: var(--orange); margin-left: 4px; }
  h2 {
    font-family: 'Orbitron', monospace;
    font-size: clamp(1.8rem, 4vw, 3rem);
    font-weight: 700;
    margin-bottom: 48px;
    letter-spacing: -0.02em;
  }
  h2 .accent { color: var(--cyan); }

  /* GALLERY */
  #gallery { background: var(--bg2); }
  .gallery-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: auto auto;
    gap: 2px;
  }
  .gallery-item {
    position: relative;
    overflow: hidden;
    background: #0d1520;
    aspect-ratio: 1;
    cursor: none;
  }
  .gallery-item:first-child {
    grid-column: span 2;
    aspect-ratio: 2/1;
  }
  .gallery-placeholder {
    width: 100%; height: 100%;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    gap: 12px;
    background: linear-gradient(135deg, #0d1520, #0a1830);
    transition: transform 0.4s;
  }
  .gallery-item:hover .gallery-placeholder { transform: scale(1.04); }
  .gallery-icon {
    font-family: 'Orbitron', monospace;
    font-size: 2rem;
    color: rgba(0,245,255,0.2);
  }
  .gallery-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--gray);
    letter-spacing: 0.2em;
  }
  .gallery-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(5,8,16,0.95) 0%, transparent 60%);
    opacity: 0;
    transition: opacity 0.3s;
    display: flex; align-items: flex-end;
    padding: 20px;
  }
  .gallery-item:hover .gallery-overlay { opacity: 1; }
  .gallery-info h3 {
    font-family: 'Orbitron', monospace;
    font-size: 0.9rem;
    color: var(--white);
    margin-bottom: 4px;
  }
  .gallery-info p {
    font-size: 0.75rem;
    color: var(--cyan);
    font-family: 'Share Tech Mono', monospace;
    letter-spacing: 0.1em;
  }
  .gallery-border {
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .gallery-item:hover .gallery-border { opacity: 1; }

  /* SERVICES */
  #services { background: var(--bg); }
  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: rgba(0,245,255,0.05);
  }
  .service-card {
    background: var(--bg);
    padding: 40px 32px;
    position: relative;
    overflow: hidden;
    transition: background 0.3s;
  }
  .service-card:hover { background: rgba(0,245,255,0.03); }
  .service-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--orange), var(--cyan));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }
  .service-card:hover::before { transform: scaleX(1); }
  .service-num {
    font-family: 'Orbitron', monospace;
    font-size: 3rem;
    font-weight: 900;
    color: rgba(0,245,255,0.06);
    line-height: 1;
    margin-bottom: 20px;
  }
  .service-name {
    font-family: 'Orbitron', monospace;
    font-size: 1rem;
    font-weight: 700;
    margin-bottom: 12px;
    color: var(--white);
  }
  .service-desc {
    font-size: 0.85rem;
    color: var(--gray);
    line-height: 1.8;
    margin-bottom: 24px;
  }
  .service-price {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.75rem;
    color: var(--cyan);
    letter-spacing: 0.15em;
  }
  .service-price span {
    font-size: 1.4rem;
    font-family: 'Orbitron', monospace;
    margin-right: 4px;
  }

  /* ABOUT */
  #about {
    background: var(--bg2);
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
  }
  .about-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
    background: rgba(0,245,255,0.05);
    margin-top: 40px;
  }
  .stat-box {
    background: var(--bg2);
    padding: 28px;
    text-align: center;
  }
  .stat-num {
    font-family: 'Orbitron', monospace;
    font-size: 2.2rem;
    font-weight: 900;
    color: var(--cyan);
    display: block;
    text-shadow: 0 0 20px rgba(0,245,255,0.4);
  }
  .stat-label {
    font-size: 0.75rem;
    color: var(--gray);
    margin-top: 4px;
    letter-spacing: 0.1em;
  }
  .about-visual {
    position: relative;
    height: 400px;
    display: flex; align-items: center; justify-content: center;
  }
  .about-box {
    width: 240px; height: 240px;
    border: 1px solid rgba(0,245,255,0.15);
    position: relative;
    display: flex; align-items: center; justify-content: center;
    animation: pulse-border 3s ease-in-out infinite;
  }
  .about-box::before, .about-box::after {
    content: '';
    position: absolute;
    width: 16px; height: 16px;
    border-color: var(--cyan);
    border-style: solid;
  }
  .about-box::before { top: -1px; left: -1px; border-width: 2px 0 0 2px; }
  .about-box::after { bottom: -1px; right: -1px; border-width: 0 2px 2px 0; }
  .about-inner {
    width: 180px; height: 180px;
    border: 1px solid rgba(255,107,53,0.1);
    display: flex; align-items: center; justify-content: center;
    animation: spin 30s linear infinite;
  }
  .about-core {
    font-family: 'Orbitron', monospace;
    font-size: 0.7rem;
    color: var(--cyan);
    letter-spacing: 0.3em;
    text-align: center;
  }

  /* REVIEWS */
  #reviews { background: var(--bg); }
  .reviews-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: rgba(0,245,255,0.05);
  }
  .review-card {
    background: var(--bg);
    padding: 36px 28px;
    position: relative;
  }
  .review-card::after {
    content: '"';
    position: absolute; top: 20px; right: 24px;
    font-family: 'Orbitron', monospace;
    font-size: 4rem;
    color: rgba(0,245,255,0.05);
    line-height: 1;
  }
  .stars {
    color: var(--orange);
    font-size: 0.8rem;
    letter-spacing: 0.1em;
    margin-bottom: 16px;
  }
  .review-text {
    font-size: 0.85rem;
    color: var(--gray);
    line-height: 1.9;
    margin-bottom: 20px;
  }
  .review-author {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--cyan);
    letter-spacing: 0.2em;
  }
  .review-author::before { content: '— '; color: var(--orange); }

  /* CONTACT / ORDER CTA */
  #order {
    background: var(--bg2);
    text-align: center;
    padding: 120px 60px;
    position: relative;
    overflow: hidden;
  }
  #order::before {
    content: '';
    position: absolute;
    width: 600px; height: 600px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(0,245,255,0.04) 0%, transparent 70%);
    top: 50%; left: 50%; transform: translate(-50%,-50%);
    pointer-events: none;
  }
  .order-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(2rem, 5vw, 4rem);
    font-weight: 900;
    margin-bottom: 20px;
  }
  .order-sub {
    color: var(--gray);
    max-width: 480px;
    margin: 0 auto 48px;
    line-height: 1.8;
  }
  .order-btns {
    display: flex; gap: 16px; justify-content: center; flex-wrap: wrap;
  }
  .btn-whatsapp {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.85rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--bg);
    background: var(--cyan);
    border: none;
    padding: 18px 48px;
    cursor: none;
    text-decoration: none;
    display: inline-flex; align-items: center; gap: 10px;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
    transition: box-shadow 0.2s;
    font-weight: 700;
  }
  .btn-whatsapp:hover { box-shadow: 0 0 40px rgba(0,245,255,0.5); }
  .btn-line {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.85rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--bg);
    background: #06c755;
    border: none;
    padding: 18px 48px;
    cursor: none;
    text-decoration: none;
    display: inline-flex; align-items: center; gap: 10px;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
    transition: box-shadow 0.2s;
    font-weight: 700;
  }
  .btn-line:hover { box-shadow: 0 0 40px rgba(6,199,85,0.5); }

  /* FOOTER */
  footer {
    position: relative; z-index: 2;
    border-top: 1px solid rgba(0,245,255,0.08);
    padding: 32px 60px;
    display: flex; align-items: center; justify-content: space-between;
  }
  .footer-logo {
    font-family: 'Orbitron', monospace;
    font-size: 0.9rem;
    font-weight: 900;
    color: var(--cyan);
    letter-spacing: 0.15em;
  }
  .footer-copy {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    color: var(--gray);
    letter-spacing: 0.2em;
  }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  @keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  @keyframes pulse-border {
    0%, 100% { box-shadow: 0 0 0 0 rgba(0,245,255,0); }
    50% { box-shadow: 0 0 0 8px rgba(0,245,255,0.04); }
  }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s, transform 0.7s;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Mobile */
  @media (max-width: 768px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    #hero { padding: 120px 24px 60px; }
    .hero-visual { display: none; }
    section { padding: 80px 24px; }
    .gallery-grid { grid-template-columns: 1fr 1fr; }
    .gallery-item:first-child { grid-column: span 2; }
    .services-grid, .reviews-grid { grid-template-columns: 1fr; }
    #about { grid-template-columns: 1fr; gap: 40px; padding: 80px 24px; }
    .about-visual { height: 240px; }
    footer { padding: 24px; flex-direction: column; gap: 12px; text-align: center; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-dot" id="cursorDot"></div>

<!-- NAV -->
<nav>
  <a href="#hero" class="nav-logo">PRINT<span>∞</span>LAB</a>
  <ul class="nav-links">
    <li><a href="#gallery">作品</a></li>
    <li><a href="#services">服務</a></li>
    <li><a href="#about">關於</a></li>
    <li><a href="#reviews">評價</a></li>
    <li><a href="#order">下單</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <p class="hero-tag">3D Printing Studio · Est. 2020</p>
  <h1>
    <span class="line1">打印你的</span>
    <span class="line2">無限想像</span>
  </h1>
  <p class="hero-sub">從概念到實物，我們將您的創意轉化為精密的三維現實。定制模型、產品原型、藝術裝置，一切皆可成型。</p>
  <div class="hero-cta">
    <a href="#gallery" class="btn-primary">查看作品</a>
    <a href="#order" class="btn-secondary">立即下單</a>
  </div>

  <div class="hero-visual">
    <div class="hex-ring"></div>
    <div class="hex-ring"></div>
    <div class="hex-ring"></div>
    <div class="hex-center"></div>
    <div class="dot-orbit"></div>
    <div class="dot-orbit2"></div>
  </div>
</section>

<!-- GALLERY -->
<section id="gallery">
  <p class="section-tag reveal">作品展示</p>
  <h2 class="reveal">精選<span class="accent">作品集</span></h2>
  <div class="gallery-grid reveal">
    <div class="gallery-item">
      <div class="gallery-placeholder">
        <div class="gallery-icon">◈</div>
        <div class="gallery-label">UPLOAD YOUR WORK</div>
      </div>
      <div class="gallery-border"></div>
      <div class="gallery-overlay">
        <div class="gallery-info">
          <h3>精密機械模型</h3>
          <p>PLA材質 · 0.1mm精度</p>
        </div>
      </div>
    </div>
    <div class="gallery-item">
      <div class="gallery-placeholder">
        <div class="gallery-icon">⬡</div>
        <div class="gallery-label">UPLOAD YOUR WORK</div>
      </div>
      <div class="gallery-border"></div>
      <div class="gallery-overlay">
        <div class="gallery-info">
          <h3>客製化人偶</h3>
          <p>樹脂材質 · 彩色渲染</p>
        </div>
      </div>
    </div>
    <div class="gallery-item">
      <div class="gallery-placeholder">
        <div class="gallery-icon">◎</div>
        <div class="gallery-label">UPLOAD YOUR WORK</div>
      </div>
      <div class="gallery-border"></div>
      <div class="gallery-overlay">
        <div class="gallery-info">
          <h3>建築縮比模型</h3>
          <p>多材質混合列印</p>
        </div>
      </div>
    </div>
    <div class="gallery-item">
      <div class="gallery-placeholder">
        <div class="gallery-icon">⬟</div>
        <div class="gallery-label">UPLOAD YOUR WORK</div>
      </div>
      <div class="gallery-border"></div>
      <div class="gallery-overlay">
        <div class="gallery-info">
          <h3>產品原型</h3>
          <p>ABS材質 · 快速打樣</p>
        </div>
      </div>
    </div>
    <div class="gallery-item">
      <div class="gallery-placeholder">
        <div class="gallery-icon">◇</div>
        <div class="gallery-label">UPLOAD YOUR WORK</div>
      </div>
      <div class="gallery-border"></div>
      <div class="gallery-overlay">
        <div class="gallery-info">
          <h3>藝術裝置</h3>
          <p>TPU柔性材質</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section id="services">
  <p class="section-tag reveal">服務項目</p>
  <h2 class="reveal">我們的<span class="accent">服務</span></h2>
  <div class="services-grid reveal">
    <div class="service-card">
      <div class="service-num">01</div>
      <div class="service-name">FDM 熔融沉積</div>
      <p class="service-desc">適合功能性零件、外殼及大型模型。支援PLA、ABS、PETG、TPU等多種材質，尺寸最大可達 300×300×400mm。</p>
      <div class="service-price">起價 <span>$50</span> / 件</div>
    </div>
    <div class="service-card">
      <div class="service-num">02</div>
      <div class="service-name">樹脂精密打印</div>
      <p class="service-desc">超高精度光固化樹脂列印，適合珠寶、微型模型、牙科及精密零件，表面光滑度極佳。</p>
      <div class="service-price">起價 <span>$80</span> / 件</div>
    </div>
    <div class="service-card">
      <div class="service-num">03</div>
      <div class="service-name">建模設計服務</div>
      <p class="service-desc">沒有3D檔案？我們提供從草圖或參考圖的3D建模服務，將您的想法轉化為可打印的數位模型。</p>
      <div class="service-price">起價 <span>$200</span> / 小時</div>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-content">
    <p class="section-tag reveal">關於我們</p>
    <h2 class="reveal">品牌<span class="accent">故事</span></h2>
    <p class="reveal" style="color:var(--gray);line-height:1.9;margin-bottom:20px;font-size:0.95rem;">
      我們成立於2020年，由一群熱愛設計與製造的工程師和藝術家組成。我們相信，3D打印技術能夠讓每個人都成為創造者。
    </p>
    <p class="reveal" style="color:var(--gray);line-height:1.9;font-size:0.95rem;">
      從個人收藏品到企業原型，我們以嚴謹的工藝態度和創新的思維，為每位客戶打造獨一無二的作品。
    </p>
    <div class="about-stats reveal">
      <div class="stat-box">
        <span class="stat-num">500+</span>
        <div class="stat-label">完成項目</div>
      </div>
      <div class="stat-box">
        <span class="stat-num">98%</span>
        <div class="stat-label">客戶滿意度</div>
      </div>
      <div class="stat-box">
        <span class="stat-num">48H</span>
        <div class="stat-label">快速交件</div>
      </div>
      <div class="stat-box">
        <span class="stat-num">12+</span>
        <div class="stat-label">可用材質</div>
      </div>
    </div>
  </div>
  <div class="about-visual reveal">
    <div class="about-box">
      <div class="about-inner">
        <div class="about-core">PRINT<br>LAB<br>∞</div>
      </div>
    </div>
  </div>
</section>

<!-- REVIEWS -->
<section id="reviews">
  <p class="section-tag reveal">顧客評價</p>
  <h2 class="reveal">真實<span class="accent">回饋</span></h2>
  <div class="reviews-grid reveal">
    <div class="review-card">
      <div class="stars">★★★★★</div>
      <p class="review-text">精度非常高，我訂制的機械零件完全符合設計規格，細節處理得非常好，下次還會再合作。</p>
      <div class="review-author">陳先生 · 工程師</div>
    </div>
    <div class="review-card">
      <div class="stars">★★★★★</div>
      <p class="review-text">幫我打印了一個客製化的生日禮物，對方收到後非常感動！質量比預期好很多，交件也很準時。</p>
      <div class="review-author">林小姐 · 設計師</div>
    </div>
    <div class="review-card">
      <div class="stars">★★★★★</div>
      <p class="review-text">建模服務很專業，我只提供了草圖，他們就幫我做出了完美的3D模型，整個過程溝通非常順暢。</p>
      <div class="review-author">王先生 · 創業者</div>
    </div>
  </div>
</section>

<!-- ORDER CTA -->
<section id="order">
  <p class="section-tag reveal" style="justify-content:center;display:flex;">立即下單</p>
  <h2 class="order-title reveal">準備好<span class="accent">開始</span>了嗎？</h2>
  <p class="order-sub reveal">告訴我們您的想法，我們將在24小時內給您報價。</p>
  <div class="order-btns reveal">
    <a href="https://wa.me/85298765432" class="btn-whatsapp" target="_blank">
      WhatsApp 聯絡
    </a>
    <a href="https://line.me/ti/p/~yourlineId" class="btn-line" target="_blank">
      LINE 下單
    </a>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">PRINT∞LAB</div>
  <div class="footer-copy">© 2025 PRINTLAB · ALL RIGHTS RESERVED</div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const dot = document.getElementById('cursorDot');
  let mx = 0, my = 0, cx = 0, cy = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; dot.style.left = mx + 'px'; dot.style.top = my + 'px'; });
  function animCursor() {
    cx += (mx - cx) * 0.12;
    cy += (my - cy) * 0.12;
    cursor.style.left = cx + 'px';
    cursor.style.top = cy + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const obs = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 80);
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(el => obs.observe(el));
</script>
</body>
</html>
