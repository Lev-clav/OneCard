<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OneCard — одна карта вместо пяти</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --bg: #0a0a0a;
  --surface: #111111;
  --border: #1f1f1f;
  --border-light: #2a2a2a;
  --text: #f0ede8;
  --muted: #6b6860;
  --accent: #c8f060;
  --accent-dim: #8aab30;
  --card-w: min(340px, 90vw);
}

html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'DM Mono', monospace;
  font-size: 15px;
  line-height: 1.6;
  overflow-x: hidden;
  cursor: crosshair;
}

/* ── NAV ── */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  padding: 1.25rem 2.5rem;
  display: flex; align-items: center; justify-content: space-between;
  border-bottom: 1px solid var(--border);
  background: rgba(10,10,10,0.92);
  backdrop-filter: blur(12px);
}
.nav-logo { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.2rem; letter-spacing: -0.02em; }
.nav-logo span { color: var(--accent); }
.nav-links { display: flex; gap: 2rem; }
.nav-links a { color: var(--muted); text-decoration: none; font-size: 13px; letter-spacing: 0.04em; transition: color .2s; }
.nav-links a:hover { color: var(--text); }
.nav-cta {
  background: var(--accent); color: #0a0a0a;
  padding: 0.5rem 1.25rem; font-family: 'Syne', sans-serif;
  font-weight: 700; font-size: 13px; border: none; cursor: pointer;
  letter-spacing: 0.04em; transition: background .2s, transform .1s;
}
.nav-cta:hover { background: #d8ff70; transform: translateY(-1px); }

/* ── HERO ── */
#hero {
  min-height: 100vh;
  display: grid; grid-template-columns: 1fr 1fr;
  align-items: center;
  padding: 8rem 2.5rem 4rem;
  position: relative;
  overflow: hidden;
}
.hero-grid-bg {
  position: absolute; inset: 0;
  background-image:
    linear-gradient(var(--border) 1px, transparent 1px),
    linear-gradient(90deg, var(--border) 1px, transparent 1px);
  background-size: 60px 60px;
  opacity: 0.4;
}
.hero-text { position: relative; z-index: 2; }
.hero-tag {
  display: inline-flex; align-items: center; gap: 0.5rem;
  font-size: 11px; letter-spacing: 0.12em; color: var(--accent);
  border: 1px solid var(--accent); padding: 0.3rem 0.75rem;
  margin-bottom: 2rem;
  animation: fadeUp .6s ease both;
}
.hero-tag::before { content: '●'; font-size: 8px; }
h1 {
  font-family: 'Syne', sans-serif;
  font-size: clamp(3rem, 6vw, 5.5rem);
  font-weight: 800;
  line-height: 0.95;
  letter-spacing: -0.03em;
  margin-bottom: 1.5rem;
  animation: fadeUp .6s .1s ease both;
}
h1 em { font-style: normal; color: var(--accent); }
.hero-sub {
  color: var(--muted); font-size: 15px; max-width: 420px;
  margin-bottom: 2.5rem; line-height: 1.8;
  animation: fadeUp .6s .2s ease both;
}
.hero-actions {
  display: flex; gap: 1rem; align-items: center;
  animation: fadeUp .6s .3s ease both;
}
.btn-primary {
  background: var(--accent); color: #0a0a0a;
  padding: 0.85rem 2rem; font-family: 'Syne', sans-serif;
  font-weight: 700; font-size: 14px; border: none;
  cursor: pointer; letter-spacing: 0.04em;
  transition: background .2s, transform .15s;
}
.btn-primary:hover { background: #d8ff70; transform: translateY(-2px); }
.btn-ghost {
  color: var(--muted); font-size: 13px; letter-spacing: 0.04em;
  background: none; border: 1px solid var(--border-light);
  padding: 0.85rem 1.5rem; cursor: pointer;
  transition: color .2s, border-color .2s;
}
.btn-ghost:hover { color: var(--text); border-color: var(--muted); }

/* ── CARD VISUAL ── */
.hero-card-wrap {
  position: relative; z-index: 2;
  display: flex; justify-content: center; align-items: center;
  animation: fadeUp .6s .2s ease both;
}
.card-3d {
  width: var(--card-w);
  aspect-ratio: 85.6/54;
  background: linear-gradient(135deg, #1a1a1a 0%, #141414 50%, #1e1e1e 100%);
  border: 1px solid #2d2d2d;
  border-radius: 12px;
  position: relative;
  box-shadow:
    0 0 0 1px #0f0f0f,
    0 30px 80px rgba(0,0,0,0.8),
    0 0 60px rgba(200,240,96,0.06);
  transform: perspective(1000px) rotateY(-8deg) rotateX(4deg);
  transition: transform .4s ease;
}
.card-3d:hover {
  transform: perspective(1000px) rotateY(-2deg) rotateX(1deg);
  box-shadow:
    0 0 0 1px #0f0f0f,
    0 40px 100px rgba(0,0,0,0.8),
    0 0 80px rgba(200,240,96,0.12);
}
.card-logo {
  position: absolute; top: 18px; left: 20px;
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 14px; letter-spacing: -0.02em;
  color: rgba(240,237,232,0.9);
}
.card-logo span { color: var(--accent); }
.card-eink {
  position: absolute; bottom: 18px; left: 20px;
  background: #e8e5df; border-radius: 4px;
  padding: 4px 10px; font-size: 11px;
  font-family: 'DM Mono', monospace; color: #1a1a1a;
  letter-spacing: 0.06em; font-weight: 400;
}
.card-slider {
  position: absolute; right: -6px; top: 50%;
  transform: translateY(-50%);
  width: 12px; height: 40px;
  background: #2a2a2a; border-radius: 6px;
  border: 1px solid #3a3a3a;
  display: flex; flex-direction: column;
  align-items: center; justify-content: center; gap: 3px;
}
.slider-dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: var(--border-light);
  transition: background .3s;
}
.slider-dot.active { background: var(--accent); }
.card-chips {
  position: absolute; top: 50%; right: 24px;
  transform: translateY(-50%);
  display: flex; flex-direction: column; gap: 5px;
}
.chip {
  width: 28px; height: 20px; border-radius: 3px;
  border: 1px solid #3a3a3a; background: #1e1e1e;
  display: flex; align-items: center; justify-content: center;
  font-size: 7px; color: var(--muted); letter-spacing: 0.05em;
}
.chip.active-chip { border-color: var(--accent-dim); background: rgba(200,240,96,0.05); color: var(--accent); }
.card-glow {
  position: absolute; inset: -2px; border-radius: 14px;
  background: linear-gradient(135deg, transparent 40%, rgba(200,240,96,0.04));
  pointer-events: none;
}

/* ── STATS ── */
.stats-bar {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  display: grid; grid-template-columns: repeat(3, 1fr);
  background: var(--surface);
}
.stat {
  padding: 2rem 2.5rem;
  border-right: 1px solid var(--border);
}
.stat:last-child { border-right: none; }
.stat-num {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 2.5rem; line-height: 1; color: var(--accent);
  letter-spacing: -0.04em; margin-bottom: 0.4rem;
}
.stat-label { font-size: 12px; color: var(--muted); letter-spacing: 0.06em; }

/* ── SECTION BASE ── */
section { padding: 6rem 2.5rem; }
.section-tag {
  font-size: 11px; letter-spacing: 0.14em; color: var(--muted);
  margin-bottom: 1rem; display: flex; align-items: center; gap: 0.75rem;
}
.section-tag::before { content: ''; width: 24px; height: 1px; background: var(--muted); }
h2 {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: clamp(2rem, 4vw, 3.2rem); line-height: 1.05;
  letter-spacing: -0.03em; margin-bottom: 1rem;
}
h2 em { font-style: normal; color: var(--accent); }

/* ── HOW IT WORKS ── */
#how { background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
.how-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1px; background: var(--border); margin-top: 3rem;
}
.how-item {
  background: var(--surface); padding: 2.5rem 2rem;
  position: relative; overflow: hidden;
  transition: background .2s;
}
.how-item:hover { background: #161616; }
.how-num {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 4rem; color: var(--border-light); line-height: 1;
  margin-bottom: 1.5rem; letter-spacing: -0.04em;
}
.how-title {
  font-family: 'Syne', sans-serif; font-weight: 600;
  font-size: 1.1rem; margin-bottom: 0.75rem;
}
.how-desc { font-size: 13px; color: var(--muted); line-height: 1.7; }
.how-item::after {
  content: ''; position: absolute;
  bottom: 0; left: 0; right: 0; height: 2px;
  background: var(--accent); transform: scaleX(0);
  transform-origin: left; transition: transform .3s;
}
.how-item:hover::after { transform: scaleX(1); }

/* ── SPECS ── */
#specs { }
.specs-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; margin-top: 3rem; align-items: start; }
.spec-group { margin-bottom: 2rem; }
.spec-group-title {
  font-size: 11px; letter-spacing: 0.12em; color: var(--accent);
  margin-bottom: 1rem; padding-bottom: 0.5rem;
  border-bottom: 1px solid var(--border);
}
.spec-row {
  display: flex; justify-content: space-between; align-items: baseline;
  padding: 0.6rem 0; border-bottom: 1px solid var(--border);
  font-size: 13px;
}
.spec-key { color: var(--muted); }
.spec-val { color: var(--text); text-align: right; }
.spec-val.good { color: var(--accent); }

/* ── PRICING ── */
#pricing { background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
.pricing-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1px; background: var(--border); margin-top: 3rem;
}
.price-card {
  background: var(--surface); padding: 2rem 1.75rem;
  position: relative; transition: background .2s;
}
.price-card:hover { background: #141414; }
.price-card.featured {
  background: #141414;
  outline: 1px solid var(--accent);
  outline-offset: -1px;
}
.price-badge {
  font-size: 10px; letter-spacing: 0.12em; color: var(--accent);
  margin-bottom: 1rem; display: block;
}
.price-name {
  font-family: 'Syne', sans-serif; font-weight: 700;
  font-size: 1.2rem; margin-bottom: 0.5rem;
}
.price-amount {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 2.2rem; color: var(--text); letter-spacing: -0.04em;
  margin-bottom: 0.25rem;
}
.price-amount sup { font-size: 1rem; font-weight: 400; }
.price-sub { font-size: 12px; color: var(--muted); margin-bottom: 1.5rem; }
.price-features { list-style: none; }
.price-features li {
  font-size: 12px; color: var(--muted);
  padding: 0.4rem 0; border-bottom: 1px solid var(--border);
  display: flex; gap: 0.5rem; align-items: baseline;
}
.price-features li::before { content: '→'; color: var(--accent); flex-shrink: 0; }
.price-features li.dim { opacity: 0.4; }
.price-features li.dim::before { color: var(--muted); content: '—'; }
.price-btn {
  width: 100%; margin-top: 1.5rem; padding: 0.75rem;
  font-family: 'Syne', sans-serif; font-weight: 700; font-size: 13px;
  letter-spacing: 0.04em; cursor: pointer; border: 1px solid var(--border-light);
  background: transparent; color: var(--muted); transition: all .2s;
}
.price-btn:hover { border-color: var(--text); color: var(--text); }
.price-card.featured .price-btn {
  background: var(--accent); border-color: var(--accent); color: #0a0a0a;
}
.price-card.featured .price-btn:hover { background: #d8ff70; }

/* ── FAQ ── */
#faq { }
.faq-layout { display: grid; grid-template-columns: 1fr 2fr; gap: 4rem; margin-top: 3rem; }
.faq-list { display: flex; flex-direction: column; gap: 1px; background: var(--border); }
.faq-item { background: var(--bg); }
.faq-q {
  padding: 1.25rem 1.5rem;
  font-size: 13px; cursor: pointer;
  display: flex; justify-content: space-between; align-items: center;
  transition: background .2s; user-select: none;
}
.faq-q:hover { background: var(--surface); }
.faq-q.open { color: var(--accent); background: var(--surface); }
.faq-arrow { transition: transform .25s; font-size: 16px; color: var(--muted); }
.faq-q.open .faq-arrow { transform: rotate(45deg); color: var(--accent); }
.faq-a {
  max-height: 0; overflow: hidden;
  font-size: 13px; color: var(--muted); line-height: 1.8;
  transition: max-height .3s ease, padding .3s;
  padding: 0 1.5rem;
  background: var(--surface);
}
.faq-a.open { max-height: 200px; padding: 1rem 1.5rem; }

/* ── PREORDER ── */
#preorder {
  background: var(--surface);
  border-top: 1px solid var(--border);
  text-align: center;
  position: relative; overflow: hidden;
}
.preorder-accent {
  position: absolute; top: -100px; left: 50%;
  transform: translateX(-50%);
  width: 400px; height: 400px; border-radius: 50%;
  background: radial-gradient(circle, rgba(200,240,96,0.06) 0%, transparent 70%);
  pointer-events: none;
}
#preorder h2 { margin-bottom: 0.75rem; }
#preorder p { color: var(--muted); max-width: 420px; margin: 0 auto 2.5rem; font-size: 14px; }
.preorder-form {
  display: flex; gap: 0; max-width: 440px; margin: 0 auto;
}
.preorder-form input {
  flex: 1; padding: 0.9rem 1.25rem;
  background: #111; border: 1px solid var(--border-light);
  border-right: none; color: var(--text);
  font-family: 'DM Mono', monospace; font-size: 14px;
  outline: none;
  transition: border-color .2s;
}
.preorder-form input::placeholder { color: var(--muted); }
.preorder-form input:focus { border-color: var(--accent); }
.preorder-form button {
  padding: 0.9rem 1.75rem; background: var(--accent);
  border: none; color: #0a0a0a;
  font-family: 'Syne', sans-serif; font-weight: 700;
  font-size: 13px; letter-spacing: 0.06em; cursor: pointer;
  transition: background .2s;
  white-space: nowrap;
}
.preorder-form button:hover { background: #d8ff70; }
.preorder-note { font-size: 11px; color: var(--muted); margin-top: 1rem; letter-spacing: 0.04em; }

/* ── FOOTER ── */
footer {
  padding: 2rem 2.5rem;
  border-top: 1px solid var(--border);
  display: flex; justify-content: space-between; align-items: center;
  font-size: 12px; color: var(--muted);
}
footer a { color: var(--muted); text-decoration: none; }
footer a:hover { color: var(--text); }

/* ── ANIMATIONS ── */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
.reveal {
  opacity: 0; transform: translateY(24px);
  transition: opacity .6s ease, transform .6s ease;
}
.reveal.visible { opacity: 1; transform: translateY(0); }

/* ── SLIDER ANIMATION ── */
@keyframes sliderCycle {
  0%, 25% { --active: 0; }
  26%, 50% { --active: 1; }
  51%, 75% { --active: 2; }
  76%, 100% { --active: 3; }
}

/* ── RESPONSIVE ── */
@media (max-width: 768px) {
  #hero { grid-template-columns: 1fr; gap: 3rem; padding-top: 6rem; }
  .hero-card-wrap { order: -1; }
  .card-3d { transform: none; }
  .card-3d:hover { transform: none; }
  .stats-bar { grid-template-columns: 1fr; }
  .stat { border-right: none; border-bottom: 1px solid var(--border); }
  .specs-layout { grid-template-columns: 1fr; gap: 2rem; }
  .faq-layout { grid-template-columns: 1fr; }
  nav { padding: 1rem 1.5rem; }
  .nav-links { display: none; }
  section { padding: 4rem 1.5rem; }
  footer { flex-direction: column; gap: 1rem; text-align: center; }
  .preorder-form { flex-direction: column; }
  .preorder-form input { border-right: 1px solid var(--border-light); border-bottom: none; }
}
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">One<span>Card</span></div>
  <div class="nav-links">
    <a href="#how">Как работает</a>
    <a href="#specs">Технологии</a>
    <a href="#pricing">Цены</a>
    <a href="#faq">FAQ</a>
  </div>
  <button class="nav-cta" onclick="document.getElementById('preorder').scrollIntoView({behavior:'smooth'})">Предзаказ</button>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-grid-bg"></div>
  <div class="hero-text">
    <div class="hero-tag">Новый продукт · 2026</div>
    <h1>Одна карта<br>вместо <em>пяти</em></h1>
    <p class="hero-sub">OneCard объединяет все ваши RFID-пропуска в одном устройстве. Без батарейки. Без приложения для прохода. Одно движение ползунком.</p>
    <div class="hero-actions">
      <button class="btn-primary" onclick="document.getElementById('preorder').scrollIntoView({behavior:'smooth'})">Оставить предзаказ</button>
      <button class="btn-ghost" onclick="document.getElementById('how').scrollIntoView({behavior:'smooth'})">Как это работает</button>
    </div>
  </div>
  <div class="hero-card-wrap">
    <div class="card-3d" id="mainCard">
      <div class="card-logo">One<span>Card</span></div>
      <div class="card-chips">
        <div class="chip active-chip" id="chip1">125</div>
        <div class="chip" id="chip2">MF</div>
        <div class="chip" id="chip3">125</div>
        <div class="chip" id="chip4">MF</div>
      </div>
      <div class="card-slider">
        <div class="slider-dot active" id="dot1"></div>
        <div class="slider-dot" id="dot2"></div>
        <div class="slider-dot" id="dot3"></div>
        <div class="slider-dot" id="dot4"></div>
      </div>
      <div class="card-eink" id="cardLabel">🏢 Работа</div>
      <div class="card-glow"></div>
    </div>
  </div>
</section>

<!-- STATS -->
<div class="stats-bar">
  <div class="stat reveal">
    <div class="stat-num">5</div>
    <div class="stat-label">профилей в одной карте</div>
  </div>
  <div class="stat reveal">
    <div class="stat-num">0</div>
    <div class="stat-label">батареек — суперконденсатор</div>
  </div>
  <div class="stat reveal">
    <div class="stat-num">10+</div>
    <div class="stat-label">лет ресурса без замены</div>
  </div>
</div>

<!-- HOW IT WORKS -->
<section id="how">
  <div class="section-tag">КАК ЭТО РАБОТАЕТ</div>
  <h2>Просто, как обычная карта.<br><em>Умнее</em> в пять раз.</h2>
  <div class="how-grid">
    <div class="how-item reveal">
      <div class="how-num">01</div>
      <div class="how-title">Запишите свои карты</div>
      <div class="how-desc">Поднесите оригинальную карту к телефону — приложение считает данные и запишет в нужный слот OneCard за 30 секунд.</div>
    </div>
    <div class="how-item reveal">
      <div class="how-num">02</div>
      <div class="how-title">Назовите слоты</div>
      <div class="how-desc">«Работа», «Парковка», «Домофон» — введите любые названия. E-ink дисплей покажет их на карте без подзарядки.</div>
    </div>
    <div class="how-item reveal">
      <div class="how-num">03</div>
      <div class="how-title">Переключайте ползунком</div>
      <div class="how-desc">Механический свитчер на торце карты. Одно движение — активен нужный профиль. Никаких приложений, никакого Bluetooth.</div>
    </div>
    <div class="how-item reveal">
      <div class="how-num">04</div>
      <div class="how-title">Прикладывайте как обычно</div>
      <div class="how-desc">Считыватель видит OneCard как обычную карту. Турникеты, домофоны, парковки — всё работает без изменений на их стороне.</div>
    </div>
  </div>
</section>

<!-- SPECS -->
<section id="specs">
  <div class="section-tag">ТЕХНИЧЕСКИЕ ХАРАКТЕРИСТИКИ</div>
  <h2>Никаких компромиссов<br>по <em>технологии</em></h2>
  <div class="specs-layout">
    <div>
      <div class="spec-group">
        <div class="spec-group-title">ФИЗИЧЕСКИЕ ПАРАМЕТРЫ</div>
        <div class="spec-row"><span class="spec-key">Размер</span><span class="spec-val">85.6 × 54 мм (ISO 7810)</span></div>
        <div class="spec-row"><span class="spec-key">Толщина</span><span class="spec-val">≤ 1.2 мм</span></div>
        <div class="spec-row"><span class="spec-key">Материал</span><span class="spec-val">Поликарбонат</span></div>
        <div class="spec-row"><span class="spec-key">Влагозащита</span><span class="spec-val good">IP67 (Pro/Elite)</span></div>
        <div class="spec-row"><span class="spec-key">Ресурс свитчера</span><span class="spec-val good">> 50 000 переключений</span></div>
      </div>
      <div class="spec-group">
        <div class="spec-group-title">ПИТАНИЕ</div>
        <div class="spec-row"><span class="spec-key">Тип</span><span class="spec-val good">Без батарейки</span></div>
        <div class="spec-row"><span class="spec-key">Накопитель</span><span class="spec-val">Суперконденсатор 0.1F</span></div>
        <div class="spec-row"><span class="spec-key">Подзарядка</span><span class="spec-val">От любого считывателя / NFC</span></div>
        <div class="spec-row"><span class="spec-key">Ресурс конденсатора</span><span class="spec-val good">> 10 лет</span></div>
      </div>
    </div>
    <div>
      <div class="spec-group">
        <div class="spec-group-title">RFID / NFC</div>
        <div class="spec-row"><span class="spec-key">Слоты 125 kHz</span><span class="spec-val">2 × T5577 (EM-125)</span></div>
        <div class="spec-row"><span class="spec-key">Слоты 13.56 MHz</span><span class="spec-val">2 × Mifare Magic Gen2</span></div>
        <div class="spec-row"><span class="spec-key">Сервисный NFC</span><span class="spec-val">NTAG215 (для приложения)</span></div>
        <div class="spec-row"><span class="spec-key">Совместимость</span><span class="spec-val good">~85% российских систем</span></div>
        <div class="spec-row"><span class="spec-key">Изоляция слотов</span><span class="spec-val good">Механическая (100%)</span></div>
      </div>
      <div class="spec-group">
        <div class="spec-group-title">ДИСПЛЕЙ И ПРИЛОЖЕНИЕ</div>
        <div class="spec-row"><span class="spec-key">Дисплей</span><span class="spec-val">E-ink (0 Вт в статике)</span></div>
        <div class="spec-row"><span class="spec-key">Обновление экрана</span><span class="spec-val">При переключении слота</span></div>
        <div class="spec-row"><span class="spec-key">Приложение</span><span class="spec-val">iOS 15+ / Android 10+</span></div>
        <div class="spec-row"><span class="spec-key">Запись профилей</span><span class="spec-val">Через NFC телефона</span></div>
        <div class="spec-row"><span class="spec-key">Работа без интернета</span><span class="spec-val good">Полностью</span></div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->
<section id="pricing">
  <div class="section-tag">ВЕРСИИ И ЦЕНЫ</div>
  <h2>Выберите свою <em>OneCard</em></h2>
  <div class="pricing-grid">
    <div class="price-card reveal">
      <span class="price-badge">LITE</span>
      <div class="price-name">Базовая</div>
      <div class="price-amount"><sup>от </sup>590 ₽</div>
      <div class="price-sub">Для начала</div>
      <ul class="price-features">
        <li>2–3 слота (один стандарт)</li>
        <li>Механический ползунок</li>
        <li>Цветная метка-индикатор</li>
        <li>PVC-корпус</li>
        <li class="dim">E-ink дисплей</li>
        <li class="dim">Приложение</li>
      </ul>
      <button class="price-btn">Предзаказ</button>
    </div>
    <div class="price-card featured reveal">
      <span class="price-badge">★ РЕКОМЕНДУЕМ</span>
      <div class="price-name">Standard</div>
      <div class="price-amount"><sup>от </sup>1 490 ₽</div>
      <div class="price-sub">Оптимальный выбор</div>
      <ul class="price-features">
        <li>4 слота (125 kHz + Mifare)</li>
        <li>E-ink дисплей с названиями</li>
        <li>Приложение iOS + Android</li>
        <li>Суперконденсатор</li>
        <li>Поликарбонат + влагозащита</li>
        <li>BLE-ридер в комплекте</li>
      </ul>
      <button class="price-btn">Предзаказ</button>
    </div>
    <div class="price-card reveal">
      <span class="price-badge">PRO</span>
      <div class="price-name">Профи</div>
      <div class="price-amount"><sup>от </sup>2 990 ₽</div>
      <div class="price-sub">Максимум функций</div>
      <ul class="price-features">
        <li>5 слотов мультистандарт</li>
        <li>E-ink 3 цвета (ч/б/красный)</li>
        <li>IP67 + силиконовый бампер</li>
        <li>MagSafe-магнит</li>
        <li>Самозапись карт в приложении</li>
        <li>Функция «Карта украдена»</li>
      </ul>
      <button class="price-btn">Предзаказ</button>
    </div>
    <div class="price-card reveal">
      <span class="price-badge">ELITE</span>
      <div class="price-name">Металл</div>
      <div class="price-amount"><sup>от </sup>6 500 ₽</div>
      <div class="price-sub">Статусный аксессуар</div>
      <ul class="price-features">
        <li>Корпус анодированный Al / сталь</li>
        <li>Полноцветный e-ink (7 цветов)</li>
        <li>Лазерная гравировка имени</li>
        <li>Премиум-упаковка</li>
        <li>Всё из версии Pro</li>
        <li>Корп. логотип (B2B)</li>
      </ul>
      <button class="price-btn">Предзаказ</button>
    </div>
  </div>
</section>

<!-- FAQ -->
<section id="faq">
  <div class="section-tag">ЧАСТЫЕ ВОПРОСЫ</div>
  <h2>Всё, что вы хотели<br>спросить об <em>OneCard</em></h2>
  <div class="faq-layout">
    <div>
      <p style="color:var(--muted); font-size:13px; line-height:1.8;">Если не нашли ответ — напишите нам. Отвечаем в течение рабочего дня.</p>
      <br>
      <a href="mailto:hello@onecard.ru" style="color:var(--accent); font-size:13px; text-decoration:none;">hello@onecard.ru →</a>
    </div>
    <div class="faq-list">
      <div class="faq-item">
        <div class="faq-q" onclick="toggleFaq(this)">
          Моя карта подойдёт?
          <span class="faq-arrow">+</span>
        </div>
        <div class="faq-a">OneCard поддерживает ~85% российских систем: большинство домофонов (EM-125), корпоративные пропуска (Mifare Classic), парковки, шлагбаумы. Не поддерживаем Тройку, Стрелку и современные DESFire-пропуска с шифрованием.</div>
      </div>
      <div class="faq-item">
        <div class="faq-q" onclick="toggleFaq(this)">
          Нужно ли заряжать карту?
          <span class="faq-arrow">+</span>
        </div>
        <div class="faq-a">Нет. Суперконденсатор подзаряжается автоматически от поля считывателя при каждом использовании. Если приложить карту к телефону через NFC — зарядится за секунды. Батарейки нет и никогда не потребуется.</div>
      </div>
      <div class="faq-item">
        <div class="faq-q" onclick="toggleFaq(this)">
          Как записать свои карты?
          <span class="faq-arrow">+</span>
        </div>
        <div class="faq-a">Скачайте наше приложение (iOS/Android), поднесите оригинальную карту к телефону — приложение считает данные. Для 125 kHz карт (домофоны) в комплекте идёт небольшой BLE-ридер. Весь процесс занимает 30–60 секунд на карту.</div>
      </div>
      <div class="faq-item">
        <div class="faq-q" onclick="toggleFaq(this)">
          Это законно?
          <span class="faq-arrow">+</span>
        </div>
        <div class="faq-a">Да, при условии что вы копируете только свои карты — те, которые вы имеете право использовать. Копирование чужих карт или карт доступа к чужим объектам запрещено. Транспортные карты (Тройка и аналоги) мы не поддерживаем.</div>
      </div>
      <div class="faq-item">
        <div class="faq-q" onclick="toggleFaq(this)">
          Что если карту украдут?
          <span class="faq-arrow">+</span>
        </div>
        <div class="faq-a">В версиях Pro и Elite есть функция «Карта украдена» в приложении. При следующем поднесении к любому считывателю сервисный чип блокируется. Физические профили доступа блокируются так же, как обычные карты — через службы безопасности.</div>
      </div>
      <div class="faq-item">
        <div class="faq-q" onclick="toggleFaq(this)">
          Есть ли оптовые цены для компаний?
          <span class="faq-arrow">+</span>
        </div>
        <div class="faq-a">Да. При заказе от 20 карт — скидка 15–35% в зависимости от объёма. Для корпоративных клиентов доступна кастомизация: логотип компании, конкретные профили, фирменная упаковка. Напишите нам на hello@onecard.ru.</div>
      </div>
    </div>
  </div>
</section>

<!-- PREORDER -->
<section id="preorder">
  <div class="preorder-accent"></div>
  <div class="section-tag" style="justify-content:center">ПРЕДЗАКАЗ</div>
  <h2>Будьте первыми</h2>
  <p>Оставьте email — пришлём уведомление о старте продаж и скидку 10% для первых 500 предзаказчиков.</p>
  <div class="preorder-form">
    <input type="email" id="emailInput" placeholder="ваш@email.ru">
    <button onclick="submitEmail()">Записаться →</button>
  </div>
  <div class="preorder-note" id="formNote">Без спама. Только важное о запуске.</div>
</section>

<!-- FOOTER -->
<footer>
  <div class="nav-logo" style="font-family:'Syne',sans-serif;font-weight:800;font-size:1rem;">One<span style="color:var(--accent)">Card</span></div>
  <div style="display:flex;gap:2rem;">
    <a href="mailto:hello@onecard.ru">Контакты</a>
    <a href="#">Политика конфиденциальности</a>
    <a href="#">B2B заказы</a>
  </div>
  <div>© 2026 OneCard</div>
</footer>

<script>
// Card slot animation
const labels = ['🏢 Работа', '🚗 Парковка', '🏠 Домофон', '🏋️ Спортзал'];
const chips = [document.getElementById('chip1'), document.getElementById('chip2'),
               document.getElementById('chip3'), document.getElementById('chip4')];
const dots = [document.getElementById('dot1'), document.getElementById('dot2'),
              document.getElementById('dot3'), document.getElementById('dot4')];
const cardLabel = document.getElementById('cardLabel');
let active = 0;

function cycleCard() {
  chips[active].classList.remove('active-chip');
  dots[active].classList.remove('active');
  active = (active + 1) % 4;
  chips[active].classList.add('active-chip');
  dots[active].classList.add('active');
  cardLabel.textContent = labels[active];
}
setInterval(cycleCard, 2000);

// FAQ toggle
function toggleFaq(el) {
  const ans = el.nextElementSibling;
  const isOpen = ans.classList.contains('open');
  document.querySelectorAll('.faq-a.open').forEach(a => {
    a.classList.remove('open');
    a.previousElementSibling.classList.remove('open');
  });
  if (!isOpen) {
    ans.classList.add('open');
    el.classList.add('open');
  }
}

// Email submit
function submitEmail() {
  const val = document.getElementById('emailInput').value;
  if (!val || !val.includes('@')) {
    document.getElementById('formNote').textContent = 'Пожалуйста, введите корректный email.';
    return;
  }
  document.getElementById('formNote').textContent = '✓ Вы в списке. Спасибо! Скидка 10% будет в письме.';
  document.getElementById('emailInput').value = '';
  document.getElementById('emailInput').disabled = true;
  document.querySelector('.preorder-form button').disabled = true;
  document.querySelector('.preorder-form button').style.opacity = '0.5';
}

// Scroll reveal
const observer = new IntersectionObserver(entries => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 80);
    }
  });
}, { threshold: 0.15 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// Pricing buttons
document.querySelectorAll('.price-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.getElementById('preorder').scrollIntoView({behavior:'smooth'});
  });
});
</script>

</body>
</html>
