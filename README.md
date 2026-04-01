<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>DUMUNDO — Instrumentais</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #080808;
    --bg2: #0f0f0f;
    --bg3: #161616;
    --card: #111111;
    --border: #222222;
    --accent: #e8c84a;
    --accent2: #c4a832;
    --red: #e84a4a;
    --text: #f0f0f0;
    --muted: #666;
    --muted2: #444;
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    overflow-x: hidden;
  }

  /* ── SCROLLBAR ── */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--accent); border-radius: 2px; }

  /* ── NOISE OVERLAY ── */
  body::before {
    content:'';
    position:fixed; inset:0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events:none; z-index:999; opacity:.4;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top:0; left:0; right:0; z-index:100;
    display:flex; align-items:center; justify-content:space-between;
    padding: 18px 48px;
    background: linear-gradient(to bottom, rgba(8,8,8,0.98), transparent);
    backdrop-filter: blur(8px);
    border-bottom: 1px solid rgba(232,200,74,0.08);
  }

  .logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 26px;
    letter-spacing: 4px;
    color: var(--accent);
    text-decoration: none;
  }

  .logo span { color: var(--text); }

  nav ul {
    list-style:none;
    display:flex; gap:36px;
  }

  nav ul a {
    text-decoration:none;
    color: var(--muted);
    font-size: 12px;
    font-weight:600;
    letter-spacing:2px;
    text-transform:uppercase;
    transition: color .2s;
  }

  nav ul a:hover { color: var(--accent); }

  .nav-actions { display:flex; gap:12px; align-items:center; }

  .btn-ghost {
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text);
    padding: 8px 20px;
    font-family: 'Syne', sans-serif;
    font-size:12px; font-weight:700;
    letter-spacing:1.5px; text-transform:uppercase;
    cursor:pointer; transition: all .2s;
    border-radius: 2px;
  }

  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }

  .btn-solid {
    background: var(--accent);
    border: none;
    color: #000;
    padding: 8px 22px;
    font-family: 'Syne', sans-serif;
    font-size:12px; font-weight:800;
    letter-spacing:1.5px; text-transform:uppercase;
    cursor:pointer; transition: all .2s;
    border-radius: 2px;
  }

  .btn-solid:hover { background: var(--accent2); transform: translateY(-1px); }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display:flex; flex-direction:column;
    align-items:center; justify-content:center;
    text-align:center;
    padding: 120px 24px 80px;
    position:relative;
    overflow:hidden;
  }

  .hero-bg {
    position:absolute; inset:0;
    background:
      radial-gradient(ellipse 80% 60% at 50% 0%, rgba(232,200,74,0.07) 0%, transparent 60%),
      radial-gradient(ellipse 40% 40% at 20% 80%, rgba(232,200,74,0.04) 0%, transparent 50%),
      linear-gradient(180deg, #080808 0%, #0a0a0a 100%);
  }

  .hero-tag {
    font-family: 'DM Mono', monospace;
    font-size: 11px; letter-spacing:4px;
    color: var(--accent);
    text-transform:uppercase;
    margin-bottom:24px;
    opacity:0; animation: fadeUp .6s .2s forwards;
  }

  .hero h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(72px, 12vw, 180px);
    line-height: .92;
    letter-spacing: 4px;
    color: var(--text);
    position:relative; z-index:1;
    opacity:0; animation: fadeUp .8s .3s forwards;
  }

  .hero h1 .gold { color: var(--accent); }

  .hero-sub {
    max-width:520px;
    margin: 28px auto 44px;
    color: var(--muted);
    font-size:15px; line-height:1.7;
    opacity:0; animation: fadeUp .6s .5s forwards;
  }

  .hero-ctas {
    display:flex; gap:14px; justify-content:center; flex-wrap:wrap;
    opacity:0; animation: fadeUp .6s .65s forwards;
  }

  .btn-lg {
    padding: 14px 36px;
    font-size:13px; letter-spacing:2px;
  }

  .hero-stats {
    display:flex; gap:60px; margin-top:80px;
    opacity:0; animation: fadeUp .6s .8s forwards;
    position:relative; z-index:1;
  }

  .stat { text-align:center; }

  .stat-num {
    font-family:'Bebas Neue', sans-serif;
    font-size:42px; color: var(--accent);
    line-height:1;
  }

  .stat-label {
    font-size:11px; letter-spacing:2px;
    color: var(--muted); text-transform:uppercase;
    margin-top:4px;
  }

  /* ── SECTION COMMON ── */
  section { padding: 100px 48px; }

  .section-header {
    display:flex; align-items:flex-end; justify-content:space-between;
    margin-bottom: 56px;
    border-bottom: 1px solid var(--border);
    padding-bottom:24px;
  }

  .section-tag {
    font-family:'DM Mono', monospace;
    font-size:11px; letter-spacing:3px;
    color: var(--accent); text-transform:uppercase;
    margin-bottom:8px;
  }

  .section-title {
    font-family:'Bebas Neue', sans-serif;
    font-size: clamp(36px,5vw,64px);
    letter-spacing:2px;
    line-height:1;
  }

  /* ── PLAYER / BEAT LIST ── */
  #beats { background: var(--bg); }

  .beats-filters {
    display:flex; gap:8px; margin-bottom:32px; flex-wrap:wrap;
  }

  .filter-btn {
    background:transparent; border:1px solid var(--border);
    color:var(--muted); padding:7px 18px;
    font-family:'Syne',sans-serif; font-size:11px;
    font-weight:700; letter-spacing:1.5px; text-transform:uppercase;
    cursor:pointer; transition:all .2s; border-radius:2px;
  }

  .filter-btn.active, .filter-btn:hover {
    border-color:var(--accent); color:var(--accent);
    background: rgba(232,200,74,0.05);
  }

  .beat-list { display:flex; flex-direction:column; gap:2px; }

  .beat-row {
    display:grid;
    grid-template-columns: 48px 1fr auto auto auto auto;
    align-items:center; gap:20px;
    padding: 14px 20px;
    background: var(--card);
    border: 1px solid transparent;
    border-radius:4px;
    cursor:pointer;
    transition: all .2s;
    position:relative; overflow:hidden;
  }

  .beat-row::before {
    content:''; position:absolute; left:0; top:0; bottom:0;
    width:3px; background: var(--accent);
    transform: scaleY(0); transition: transform .2s;
  }

  .beat-row:hover, .beat-row.playing {
    background: var(--bg3);
    border-color: var(--border);
  }

  .beat-row:hover::before, .beat-row.playing::before { transform:scaleY(1); }

  .beat-num {
    font-family:'DM Mono',monospace;
    font-size:13px; color:var(--muted);
    text-align:center;
  }

  .beat-row.playing .beat-num { color:var(--accent); }

  .beat-info { min-width:0; }

  .beat-name {
    font-size:14px; font-weight:700;
    white-space:nowrap; overflow:hidden; text-overflow:ellipsis;
  }

  .beat-meta {
    font-size:11px; color:var(--muted);
    font-family:'DM Mono',monospace;
    margin-top:3px;
    display:flex; gap:12px;
  }

  .beat-tag {
    display:inline-block; padding:2px 8px;
    background: rgba(232,200,74,0.1);
    border:1px solid rgba(232,200,74,0.2);
    color:var(--accent); font-size:10px;
    letter-spacing:1px; border-radius:2px;
    text-transform:uppercase; font-weight:700;
  }

  .beat-bpm {
    font-family:'DM Mono',monospace;
    font-size:12px; color:var(--muted);
  }

  .beat-price {
    font-family:'Bebas Neue',sans-serif;
    font-size:22px; color:var(--text);
    min-width:60px; text-align:right;
  }

  .beat-actions { display:flex; gap:8px; }

  .icon-btn {
    width:34px; height:34px;
    border-radius:50%; border:1px solid var(--border);
    background:transparent; color:var(--muted);
    display:flex; align-items:center; justify-content:center;
    cursor:pointer; transition:all .2s; font-size:14px;
  }

  .icon-btn:hover { border-color:var(--accent); color:var(--accent); }

  .play-btn {
    width:40px; height:40px;
    border-radius:50%;
    background: var(--accent);
    border:none; color:#000;
    display:flex; align-items:center; justify-content:center;
    cursor:pointer; transition:all .2s; font-size:16px;
  }

  .play-btn:hover { background:var(--accent2); transform:scale(1.05); }

  /* ── WAVEFORM PLAYER ── */
  .sticky-player {
    position:fixed; bottom:0; left:0; right:0;
    background: rgba(10,10,10,0.97);
    backdrop-filter:blur(20px);
    border-top: 1px solid var(--border);
    padding: 14px 48px;
    display:flex; align-items:center; gap:24px;
    z-index:200;
    transform: translateY(100%);
    transition: transform .3s ease;
  }

  .sticky-player.visible { transform:translateY(0); }

  .player-info { min-width:200px; }

  .player-name { font-size:14px; font-weight:700; }

  .player-artist { font-size:11px; color:var(--muted); margin-top:2px; }

  .player-controls { display:flex; align-items:center; gap:16px; }

  .ctrl-btn {
    background:none; border:none; color:var(--muted);
    font-size:18px; cursor:pointer; transition:color .2s;
  }

  .ctrl-btn:hover { color:var(--text); }

  .play-main {
    width:44px; height:44px; border-radius:50%;
    background:var(--accent); border:none; color:#000;
    font-size:18px; cursor:pointer;
    display:flex; align-items:center; justify-content:center;
    transition:all .2s;
  }

  .play-main:hover { background:var(--accent2); }

  .progress-wrap { flex:1; display:flex; align-items:center; gap:12px; }

  .time { font-family:'DM Mono',monospace; font-size:11px; color:var(--muted); min-width:36px; }

  .progress-bar {
    flex:1; height:3px; background:var(--border);
    border-radius:2px; cursor:pointer; position:relative;
  }

  .progress-fill {
    height:100%; background:var(--accent); border-radius:2px;
    width:35%; transition:width .1s;
  }

  .progress-bar:hover .progress-fill { background:var(--accent2); }

  .volume-wrap { display:flex; align-items:center; gap:8px; }

  .volume-icon { font-size:16px; color:var(--muted); }

  .volume-bar {
    width:80px; height:3px; background:var(--border);
    border-radius:2px; cursor:pointer;
  }

  .volume-fill {
    height:100%; background:var(--muted); border-radius:2px; width:70%;
  }

  /* ── PRICING ── */
  #pricing { background: var(--bg2); }

  .pricing-grid {
    display:grid; grid-template-columns: repeat(auto-fit, minmax(280px,1fr));
    gap:2px;
  }

  .price-card {
    background:var(--card);
    padding:40px 36px;
    border:1px solid var(--border);
    position:relative; overflow:hidden;
    transition: all .25s;
  }

  .price-card:hover { border-color: rgba(232,200,74,0.3); transform:translateY(-3px); }

  .price-card.featured {
    border-color: var(--accent);
    background: linear-gradient(135deg, #111 0%, #131208 100%);
  }

  .price-card.featured::before {
    content:'MAIS POPULAR';
    position:absolute; top:20px; right:-28px;
    background:var(--accent); color:#000;
    font-size:9px; font-weight:800; letter-spacing:2px;
    padding:5px 40px; transform:rotate(45deg);
  }

  .price-tier {
    font-family:'DM Mono',monospace;
    font-size:11px; letter-spacing:3px;
    color:var(--muted); text-transform:uppercase;
    margin-bottom:16px;
  }

  .price-amount {
    font-family:'Bebas Neue',sans-serif;
    font-size:72px; line-height:1; color:var(--text);
    display:flex; align-items:flex-start; gap:4px;
  }

  .price-currency {
    font-size:24px; margin-top:14px;
    color:var(--muted);
  }

  .price-period {
    font-size:13px; color:var(--muted); margin:8px 0 28px;
  }

  .price-features { list-style:none; margin-bottom:36px; }

  .price-features li {
    padding:9px 0;
    border-bottom:1px solid var(--border);
    font-size:13px; color:var(--muted);
    display:flex; align-items:center; gap:10px;
  }

  .price-features li .check { color:var(--accent); font-size:14px; }
  .price-features li .cross { color:var(--muted2); font-size:14px; }

  .btn-price {
    width:100%; padding:14px;
    font-family:'Syne',sans-serif;
    font-size:12px; font-weight:800; letter-spacing:2px;
    text-transform:uppercase; cursor:pointer;
    border-radius:2px; transition:all .2s;
  }

  .btn-price-outline {
    background:transparent; border:1px solid var(--border); color:var(--text);
  }

  .btn-price-outline:hover { border-color:var(--accent); color:var(--accent); }

  .btn-price-fill { background:var(--accent); border:none; color:#000; }

  .btn-price-fill:hover { background:var(--accent2); }

  /* ── ALBUMS / DISCOGRAPHY ── */
  #discografia { background: var(--bg); }

  .albums-grid {
    display:grid; grid-template-columns: repeat(auto-fill, minmax(220px,1fr));
    gap:24px;
  }

  .album-card {
    cursor:pointer; transition:all .25s;
  }

  .album-cover {
    aspect-ratio:1;
    border-radius:4px; overflow:hidden;
    position:relative; margin-bottom:14px;
  }

  .album-cover-img {
    width:100%; height:100%;
    object-fit:cover;
    background: linear-gradient(135deg, #1a1a1a, #0f0f0f);
    display:flex; align-items:center; justify-content:center;
  }

  .album-cover-placeholder {
    width:100%; height:100%;
    display:flex; align-items:center; justify-content:center;
    font-size:48px;
  }

  .album-overlay {
    position:absolute; inset:0;
    background:rgba(0,0,0,0.6);
    display:flex; align-items:center; justify-content:center;
    opacity:0; transition:opacity .2s;
  }

  .album-card:hover .album-overlay { opacity:1; }

  .album-card:hover { transform:translateY(-4px); }

  .album-title { font-size:14px; font-weight:700; margin-bottom:4px; }

  .album-year {
    font-size:11px; color:var(--muted);
    font-family:'DM Mono',monospace;
    display:flex; justify-content:space-between;
  }

  /* ── EVENTS ── */
  #eventos { background: var(--bg2); }

  .events-list { display:flex; flex-direction:column; gap:2px; }

  .event-row {
    display:grid;
    grid-template-columns: 80px 1fr auto;
    align-items:center; gap:32px;
    padding:20px 28px;
    background:var(--card);
    border:1px solid var(--border);
    border-radius:4px;
    transition:all .2s;
  }

  .event-row:hover { border-color:rgba(232,200,74,0.3); background:var(--bg3); }

  .event-date { text-align:center; }

  .event-day {
    font-family:'Bebas Neue',sans-serif;
    font-size:36px; line-height:1; color:var(--accent);
  }

  .event-month {
    font-family:'DM Mono',monospace;
    font-size:10px; letter-spacing:2px; color:var(--muted);
    text-transform:uppercase;
  }

  .event-name { font-size:16px; font-weight:700; margin-bottom:6px; }

  .event-venue {
    font-size:12px; color:var(--muted);
    font-family:'DM Mono',monospace;
  }

  /* ── UPLOAD ── */
  #upload { background: var(--bg); }

  .upload-area {
    border:2px dashed var(--border);
    border-radius:8px;
    padding:80px 40px;
    text-align:center;
    transition:all .2s;
    cursor:pointer;
    background: var(--card);
    position:relative;
  }

  .upload-area:hover, .upload-area.dragover {
    border-color:var(--accent);
    background:rgba(232,200,74,0.03);
  }

  .upload-icon { font-size:48px; margin-bottom:20px; opacity:.5; }

  .upload-title { font-size:20px; font-weight:700; margin-bottom:8px; }

  .upload-sub { font-size:13px; color:var(--muted); margin-bottom:28px; }

  .upload-input { display:none; }

  .file-list { margin-top:24px; display:flex; flex-direction:column; gap:8px; }

  .file-item {
    display:flex; align-items:center; gap:14px;
    padding:12px 18px; background:var(--bg3);
    border:1px solid var(--border); border-radius:4px;
  }

  .file-icon { font-size:20px; }
  .file-name { flex:1; font-size:13px; }
  .file-size { font-size:11px; color:var(--muted); font-family:'DM Mono',monospace; }

  .file-remove {
    background:none; border:none; color:var(--muted);
    cursor:pointer; font-size:16px; transition:color .2s;
  }

  .file-remove:hover { color:var(--red); }

  /* ── CONTACT ── */
  #contato { background: var(--bg2); }

  .contact-grid {
    display:grid; grid-template-columns:1fr 1fr; gap:80px;
  }

  .contact-form { display:flex; flex-direction:column; gap:16px; }

  .form-group { display:flex; flex-direction:column; gap:6px; }

  .form-label {
    font-size:11px; letter-spacing:2px; text-transform:uppercase;
    color:var(--muted); font-weight:700;
  }

  .form-input, .form-textarea {
    background:var(--card); border:1px solid var(--border);
    color:var(--text); padding:12px 16px;
    font-family:'Syne',sans-serif; font-size:14px;
    border-radius:2px; transition:border .2s; outline:none;
  }

  .form-input:focus, .form-textarea:focus { border-color:var(--accent); }

  .form-textarea { height:120px; resize:vertical; }

  .social-links { display:flex; flex-direction:column; gap:16px; margin-top:8px; }

  .social-link {
    display:flex; align-items:center; gap:16px;
    padding:16px 20px; background:var(--card);
    border:1px solid var(--border); border-radius:4px;
    text-decoration:none; color:var(--text);
    transition:all .2s;
  }

  .social-link:hover { border-color:var(--accent); transform:translateX(4px); }

  .social-icon { font-size:20px; width:32px; text-align:center; }
  .social-name { font-size:13px; font-weight:700; }
  .social-handle { font-size:11px; color:var(--muted); margin-top:2px; font-family:'DM Mono',monospace; }

  /* ── MODAL ── */
  .modal-backdrop {
    position:fixed; inset:0; background:rgba(0,0,0,0.85);
    backdrop-filter:blur(8px); z-index:500;
    display:flex; align-items:center; justify-content:center;
    opacity:0; pointer-events:none; transition:opacity .25s;
  }

  .modal-backdrop.open { opacity:1; pointer-events:all; }

  .modal {
    background:var(--bg3); border:1px solid var(--border);
    border-radius:8px; padding:48px;
    width:100%; max-width:480px;
    transform:translateY(20px); transition:transform .25s;
  }

  .modal-backdrop.open .modal { transform:translateY(0); }

  .modal h2 {
    font-family:'Bebas Neue',sans-serif;
    font-size:36px; letter-spacing:2px; margin-bottom:8px;
  }

  .modal-sub { font-size:13px; color:var(--muted); margin-bottom:32px; }

  .modal-tabs {
    display:flex; gap:0; margin-bottom:28px;
    border:1px solid var(--border); border-radius:2px; overflow:hidden;
  }

  .modal-tab {
    flex:1; padding:10px; text-align:center;
    background:transparent; border:none; color:var(--muted);
    font-family:'Syne',sans-serif; font-size:12px; font-weight:700;
    letter-spacing:1.5px; text-transform:uppercase; cursor:pointer;
    transition:all .2s;
  }

  .modal-tab.active { background:var(--accent); color:#000; }

  .modal-form { display:flex; flex-direction:column; gap:14px; }

  .modal-close {
    position:absolute; top:20px; right:20px;
    background:none; border:none; color:var(--muted);
    font-size:22px; cursor:pointer; transition:color .2s;
  }

  .modal-close:hover { color:var(--text); }

  /* ── FOOTER ── */
  footer {
    background:var(--bg); border-top:1px solid var(--border);
    padding:60px 48px 40px;
    display:grid; grid-template-columns: 1fr 1fr 1fr; gap:48px;
  }

  .footer-brand .logo { font-size:22px; display:block; margin-bottom:12px; }

  .footer-brand p { font-size:13px; color:var(--muted); line-height:1.7; max-width:260px; }

  .footer-col h4 {
    font-size:11px; letter-spacing:3px; text-transform:uppercase;
    color:var(--accent); margin-bottom:20px; font-weight:700;
  }

  .footer-col ul { list-style:none; display:flex; flex-direction:column; gap:10px; }

  .footer-col ul a {
    font-size:13px; color:var(--muted); text-decoration:none;
    transition:color .2s;
  }

  .footer-col ul a:hover { color:var(--text); }

  .footer-bottom {
    border-top:1px solid var(--border); padding:24px 48px;
    display:flex; justify-content:space-between; align-items:center;
    font-size:11px; color:var(--muted); font-family:'DM Mono',monospace;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity:0; transform:translateY(24px); }
    to   { opacity:1; transform:translateY(0); }
  }

  /* ── RESPONSIVE ── */
  @media(max-width:768px){
    nav { padding:16px 20px; }
    nav ul { display:none; }
    section { padding:70px 20px; }
    .contact-grid { grid-template-columns:1fr; gap:40px; }
    footer { grid-template-columns:1fr; padding:40px 20px 24px; }
    .footer-bottom { flex-direction:column; gap:8px; padding:20px; }
    .hero-stats { gap:32px; }
    .beat-row { grid-template-columns:40px 1fr auto; }
    .beat-tag, .beat-bpm { display:none; }
    .sticky-player { padding:12px 16px; gap:12px; }
    .player-info { display:none; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a href="#" class="logo">DU<span>MUNDO</span></a>
  <ul>
    <li><a href="#beats">Beats</a></li>
    <li><a href="#pricing">Preços</a></li>
    <li><a href="#discografia">Discografia</a></li>
    <li><a href="#eventos">Eventos</a></li>
    <li><a href="#upload">Upload</a></li>
    <li><a href="#contato">Contato</a></li>
  </ul>
  <div class="nav-actions">
    <button class="btn-ghost" onclick="openModal('login')">Entrar</button>
    <button class="btn-solid" onclick="openModal('register')">Criar Conta</button>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <p class="hero-tag">★ Beats Premium & Instrumentais</p>
  <h1>BEATS QUE<br/><span class="gold">DEFINEM</span><br/>CARREIRAS</h1>
  <p class="hero-sub">Instrumentais exclusivos para produtores e gravadoras. Licenças profissionais, qualidade de estúdio, entrega imediata.</p>
  <div class="hero-ctas">
    <button class="btn-solid btn-lg" onclick="document.getElementById('beats').scrollIntoView({behavior:'smooth'})">▶ Explorar Beats</button>
    <button class="btn-ghost btn-lg" onclick="document.getElementById('pricing').scrollIntoView({behavior:'smooth'})">Ver Preços</button>
  </div>
  <div class="hero-stats">
    <div class="stat"><div class="stat-num">500+</div><div class="stat-label">Beats Disponíveis</div></div>
    <div class="stat"><div class="stat-num">55.7K</div><div class="stat-label">Artistas Ativos</div></div>
    <div class="stat"><div class="stat-num">97,3%</div><div class="stat-label">Satisfação</div></div>
    <div class="stat"><div class="stat-num">10K</div><div class="stat-label">Licenças Vendidas</div></div>
  </div>
</section>

<!-- BEATS PLAYER -->
<section id="beats">
  <div class="section-header">
    <div>
      <div class="section-tag">// 01 — Catálogo</div>
      <h2 class="section-title">BEATS EM DESTAQUE</h2>
    </div>
    <a href="#" style="font-size:12px;color:var(--accent);text-decoration:none;letter-spacing:2px;font-weight:700;">VER TODOS →</a>
  </div>

  <div class="beats-filters">
    <button class="filter-btn active" onclick="setFilter(this,'all')">Todos</button>
    <button class="filter-btn" onclick="setFilter(this,'trap')">Trap</button>
    <button class="filter-btn" onclick="setFilter(this,'drill')">Drill</button>
    <button class="filter-btn" onclick="setFilter(this,'rnb')">R&B</button>
    <button class="filter-btn" onclick="setFilter(this,'Rapcia')">Rapcia</button>
    <button class="filter-btn" onclick="setFilter(this,'afro')">Afrobeat</button>
    <button class="filter-btn" onclick="setFilter(this,'boom')">Boom Bap</button>
    <button class="filter-btn" onclick="setFilter(this,'ambient')">Ambient</button>
    <button class="filter-btn" onclick="setFilter(this, 'KUBENGUE')">KUBENGUE</button>
    
  </div>

  <div class="beat-list" id="beatList"></div>
</section>

<!-- PRICING -->
<section id="pricing">
  <div class="section-header">
    <div>
      <div class="section-tag">// 02 — Licenciamento</div>
      <h2 class="section-title">PLANOS & PREÇOS</h2>
    </div>
  </div>
  <div class="pricing-grid">

    <div class="price-card">
      <div class="price-tier">Licença Básica</div>
      <div class="price-amount"><span class="price-currency">Kz</span>3.900</div>
      <div class="price-period">por beat</div>
      <ul class="price-features">
        <li><span class="check">✓</span> MP3 de Alta Qualidade</li>
        <li><span class="check">✓</span> Uso não-exclusivo</li>
        <li><span class="check">✓</span> Até 10.000 streams</li>
        <li><span class="check">✓</span> 1 vídeo no YouTube</li>
        <li><span class="cross">✗</span> Stems / Tracks</li>
        <li><span class="cross">✗</span> Uso comercial amplo</li>
        <li><span class="cross">✗</span> Distribuição física</li>
      </ul>
      <button class="btn-price btn-price-outline">Comprar Licença</button>
    </div>

    <div class="price-card featured">
      <div class="price-tier">Licença Premium</div>
      <div class="price-amount"><span class="price-currency">Kz</span>8.900</div>
      <div class="price-period">por beat</div>
      <ul class="price-features">
        <li><span class="check">✓</span> WAV sem compressão</li>
        <li><span class="check">✓</span> Uso não-exclusivo</li>
        <li><span class="check">✓</span> Streams ilimitados</li>
        <li><span class="check">✓</span> Vídeos ilimitados</li>
        <li><span class="check">✓</span> Stems / Tracks inclusos</li>
        <li><span class="check">✓</span> Uso comercial</li>
        <li><span class="cross">✗</span> Exclusividade total</li>
      </ul>
      <button class="btn-price btn-price-fill">Comprar Licença</button>
    </div>

    <div class="price-card">
      <div class="price-tier">Licença Exclusiva</div>
      <div class="price-amount"><span class="price-currency">Kz</span>28.999</div>
      <div class="price-period">por beat</div>
      <ul class="price-features">
        <li><span class="check">✓</span> WAV + Stems completos</li>
        <li><span class="check">✓</span> Exclusividade total</li>
        <li><span class="check">✓</span> Streams ilimitados</li>
        <li><span class="check">✓</span> Todos os usos</li>
        <li><span class="check">✓</span> Distribuição física</li>
        <li><span class="check">✓</span> Beat removido do catálogo</li>
        <li><span class="check">✓</span> Suporte prioritário</li>
      </ul>
      <button class="btn-price btn-price-outline">Comprar Licença</button>
    </div>

  </div>
</section>

<!-- DISCOGRAFIA -->
<section id="discografia">
  <div class="section-header">
    <div>
      <div class="section-tag">// 03 — Discografia</div>
      <h2 class="section-title">ÁLBUNS & EPs</h2>
    </div>
    <a href="#" style="font-size:12px;color:var(--accent);text-decoration:none;letter-spacing:2px;font-weight:700;">VER TUDO →</a>
  </div>
  <div class="albums-grid" id="albumGrid"></div>
</section>

<!-- EVENTOS -->
<section id="eventos">
  <div class="section-header">
    <div>
      <div class="section-tag">// 04 — Agenda</div>
      <h2 class="section-title">PRÓXIMOS EVENTOS</h2>
    </div>
  </div>
  <div class="events-list">
    <div class="event-row">
      <div class="event-date"><div class="event-day">15</div><div class="event-month">ABR 2026</div></div>
      <div><div class="event-name">Beat Workshop — ROCHA-PINTO</div><div class="event-venue">📍 BAR DO-DAMBI-av.4 de fev. Luanda.</div></div>
      <button class="btn-solid">Ingressos</button>
    </div>
    <div class="event-row">
      <div class="event-date"><div class="event-day">22</div><div class="event-month">ABRIL 2026</div></div>
      <div><div class="event-name">Freesty on tha Beat</div><div class="event-venue">📍 Calçadão spot do bairro . pedonal da cabine . R.P Luanda</div></div>
      <button class="btn-solid">Ingressos</button>
    </div>
    <div class="event-row">
      <div class="event-date"><div class="event-day">08</div><div class="event-month">MAIO DE 2026</div></div>
      <div><div class="event-name">Secção ao vivo — Streaming</div><div class="event-venue">🎙️ YouTube Live + Twitch · Online . X </div></div>
      <button class="btn-ghost">Lembrete</button>
    </div>
    <div class="event-row">
      <div class="event-date"><div class="event-day">20</div><div class="event-month">MAI0 2026</div></div>
      <div><div class="event-name">DUMUNDO Festival</div><div class="event-venue">📍 UMBA BAR, quintalao do R.P Luanda</div></div>
      <button class="btn-solid">Ingressos</button>
    </div>
  </div>
</section>

<!-- UPLOAD -->
<section id="upload">
  <div class="section-header">
    <div>
      <div class="section-tag">// 05 — Enviar Arquivos</div>
      <h2 class="section-title">UPLOAD DE BEATS</h2>
    </div>
  </div>
  <div class="upload-area" id="uploadArea" onclick="document.getElementById('fileInput').click()">
    <div class="upload-icon">🎵</div>
    <div class="upload-title">Arraste seus arquivos aqui</div>
    <div class="upload-sub">Suporte para MP3, WAV, FLAC, ZIP — Máx 500MB por arquivo</div>
    <button class="btn-solid btn-lg" onclick="event.stopPropagation();document.getElementById('fileInput').click()">Selecionar Arquivos</button>
    <input type="file" id="fileInput" class="upload-input" multiple accept=".mp3,.wav,.flac,.zip" onchange="handleFiles(this.files)"/>
  </div>
  <div class="file-list" id="fileList"></div>
</section>

<!-- CONTATO -->
<section id="contato">
  <div class="section-header">
    <div>
      <div class="section-tag">// 06 — Contato</div>
      <h2 class="section-title">FALE CONOSCO</h2>
    </div>
  </div>
  <div class="contact-grid">
    <div>
      <p style="color:var(--muted);font-size:14px;line-height:1.8;margin-bottom:32px;">Para licenciamentos exclusivos, parcerias com gravadoras ou projetos personalizados, entre em contacto direto.</p>
      <div class="contact-form">
        <div class="form-group"><label class="form-label">Nome</label><input class="form-input" placeholder="Seu nome ou nome artístico"/></div>
        <div class="form-group"><label class="form-label">Email</label><input class="form-input" type="email" placeholder="email@exemplo.com"/></div>
        <div class="form-group"><label class="form-label">Assunto</label>
          <select class="form-input" style="cursor:pointer;">
            <option>Licença Exclusiva</option>
            <option>Parceria / Colaboração</option>
            <option>Beat Personalizado</option>
            <option>Suporte</option>
            <option>Outro</option>
          </select>
        </div>
        <div class="form-group"><label class="form-label">Mensagem</label><textarea class="form-textarea" placeholder="Descreva seu projeto..."></textarea></div>
        <button class="btn-solid btn-lg" style="width:100%;padding:14px;">Enviar Mensagem →</button>
      </div>
    </div>
    <div>
      <div style="font-family:'DM Mono',monospace;font-size:11px;letter-spacing:3px;color:var(--accent);text-transform:uppercase;margin-bottom:20px;">Redes Sociais</div>
      <div class="social-links">
        <a class="social-link" href="#">
          <span class="social-icon">🎵</span>
          <div><div class="social-name">TikTok</div><div class="social-handle">@dumundo.ao</div></div>
          <span style="margin-left:auto;color:var(--muted);">→</span>
        </a>
        <a class="social-link" href="#">
          <span class="social-icon">📷</span>
          <div><div class="social-name">Instagram</div><div class="social-handle">@dumundo.ao</div></div>
          <span style="margin-left:auto;color:var(--muted);">→</span>
        </a>
        <a class="social-link" href="#">
          <span class="social-icon">▶️</span>
          <div><div class="social-name">YouTube</div><div class="social-handle">DUMUNDO Official</div></div>
          <span style="margin-left:auto;color:var(--muted);">→</span>
        </a>
        <a class="social-link" href="#">
          <span class="social-icon">🎧</span>
          <div><div class="social-name">SoundCloud</div><div class="social-handle">dumundo</div></div>
          <span style="margin-left:auto;color:var(--muted);">→</span>
        </a>
        <a class="social-link" href="#">
          <span class="social-icon">💬</span>
          <div><div class="social-name">WhatsApp Business</div><div class="social-handle">+244-947837610</div></div>6
          <span style="margin-left:auto;color:var(--muted);">→</span>
        </a>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-brand">
    <a href="#" class="logo">DU<span>MUNDO</span></a>
    <p>Beats profissionais para artistas, novos talentos e gravadoras — dumundo.ao</p>
  </div>
  <div class="footer-col">
    <h4>Loja</h4>
    <ul>
      <li><a href="#">Todos os Beats</a></li>
      <li><a href="#">Trap</a></li>
      <li><a href="#">Drill</a></li>
      <li><a href="#">KUBENGUE</a></li>
      <li><a href="#">R&B / Soul</a></li>
      <li><a href="#">Afrobeat</a></li>
      <li> <a href="#">Rapcia</a></li>
      <li><a href="#">Boom Bap</a></li>
    </ul>
  </div>
  <div class="footer-col">
    <h4>Suporte</h4>
    <ul>
      <li><a href="#">Tipos de Licença</a></li>
      <li><a href="#">FAQ</a></li>
      <li><a href="#">Política de Reembolso</a></li>
      <li><a href="#">Termos de Uso</a></li>
      <li><a href="#">Privacidade</a></li>
    </ul>
  </div>
</footer>
<div class="footer-bottom">
  <span>© 2026 DUMUNDO — dumundo.ao — Todos os direitos reservados</span><br>
  <span>DUMUNDO</span>
  <span>Pelo amor a música ♪ Em Angola</span>
</div>

<!-- STICKY PLAYER -->
<div class="sticky-player" id="stickyPlayer">
  <div class="player-info">
    <div class="player-name" id="playerName">—</div>
    <div class="player-artist" id="playerArtist">DUMUNDO.AO</div>
  </div>
  <div class="player-controls">
    <button class="ctrl-btn">⏮</button>
    <button class="play-main" id="playMainBtn" onclick="togglePlay()">▶</button>
    <button class="ctrl-btn">⏭</button>
  </div>
  <div class="progress-wrap">
    <span class="time" id="currentTime">0:00</span>
    <div class="progress-bar" onclick="seekTo(event, this)">
      <div class="progress-fill" id="progressFill"></div>
    </div>
    <span class="time" id="duration">3:24</span>
  </div>
  <div class="volume-wrap">
    <span class="volume-icon">🔊</span>
    <div class="volume-bar"><div class="volume-fill"></div></div>
  </div>
  <button class="icon-btn" title="Download" onclick="downloadBeat()">⬇</button>
  <button class="btn-solid" style="white-space:nowrap;font-size:11px;padding:8px 16px;">Comprar</button>
</div>

<!-- AUTH MODAL -->
<div class="modal-backdrop" id="authModal" onclick="closeModalOutside(event)">
  <div class="modal" style="position:relative;">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <h2 id="modalTitle">BEM-VINDO</h2>
    <p class="modal-sub" id="modalSub">Acesse sua conta de produtor.</p>
    <div class="modal-tabs">
      <button class="modal-tab active" id="tabLogin" onclick="switchTab('login')">Entrar</button>
      <button class="modal-tab" id="tabReg" onclick="switchTab('register')">Criar Conta</button>
    </div>
    <div class="modal-form" id="loginForm">
      <div class="form-group"><label class="form-label">Email</label><input class="form-input" type="email" placeholder="email@exemplo.com"/></div>
      <div class="form-group"><label class="form-label">Senha</label><input class="form-input" type="password" placeholder="••••••••"/></div>
      <button class="btn-solid" style="padding:14px;font-size:13px;letter-spacing:2px;">Entrar na Conta</button>
      <p style="text-align:center;font-size:12px;color:var(--muted);">Esqueceu a senha? <a href="#" style="color:var(--accent);">Recuperar</a></p>
    </div>
    <div class="modal-form" id="registerForm" style="display:none;">
      <div class="form-group"><label class="form-label">Nome Artístico</label><input class="form-input" placeholder="Seu nome no mercado"/></div>
      <div class="form-group"><label class="form-label">Email</label><input class="form-input" type="email" placeholder="email@exemplo.com"/></div>
      <div class="form-group"><label class="form-label">Senha</label><input class="form-input" type="password" placeholder="Mínimo 8 caracteres"/></div>
      <div class="form-group"><label class="form-label">Tipo de Conta</label>
        <select class="form-input">
          <option>Produtor Musical</option>
          <option>Gravadora</option>
          <option>Artista</option>
          <option>DJ</option>
        </select>
      </div>
      <button class="btn-solid" style="padding:14px;font-size:13px;letter-spacing:2px;">Criar Minha Conta</button>
    </div>
  </div>
</div>

<script>
// ── DATA ──
const beats = [
  { id:1, name:'Shadow Protocol', genre:'trap', bpm:140, key:'F#m', duration:'2:58', price:'Kz-2.890', tag:'NOVO' },
  { id:2, name:'Crimson Nights', genre:'drill', bpm:148, key:'Dm', duration:'3:12', price:'Kz-2.890', tag:'HOT' },
  { id:3, name:'Velvet Underground', genre:'rnb', bpm:92, key:'Bbm', duration:'3:44', price:'Kz-2.890', tag:'' },
  { id:4, name:'Lagos Dreams', genre:'afro', bpm:106, key:'Em', duration:'3:28', price:'Kz-2.890', tag:'NOVO' },
  { id:5, name:'Street Chronicles', genre:'boom', bpm:88, key:'Am', duration:'2:52', price:'Kz-2.890', tag:'' },
  { id:6, name:'Midnight Cipher', genre:'trap', bpm:135, key:'Gm', duration:'3:05', price:'Kz-2.890', tag:'HOT' },
  { id:7, name:'Eclipse Mode', genre:'drill', bpm:144, key:'Cm', duration:'2:48', price:'Kz-2.890', tag:'EXCL' },
  { id:8, name:'Lunar Frequency', genre:'ambient', bpm:78, key:'Dbm', duration:'4:10', price:'Kz-2.890', tag:'' },
];

const albums = [
  { title:'O Idiota Vol.1', year:'2024', tracks:12, emoji:'🌑' },
  { title:'Filhos do Mundo', year:'2024', tracks:9, emoji:'🏙️' },
  { title:'Afro Renascimento', year:'2023', tracks:14, emoji:'🌍' },
  { title:'Secção noturna', year:'2023', tracks:8, emoji:'🌃' },
  { title:'A frequencia da Alma', year:'2022', tracks:11, emoji:'🎷' },
  { title:'Chuva Forte', year:'2022', tracks:7, emoji:'🔥' },
];

let currentBeat = null;
let isPlaying = false;
let progressInterval = null;
let progress = 0;

// ── RENDER BEATS ──
function renderBeats(filter='all'){
  const list = document.getElementById('beatList');
  const filtered = filter==='all' ? beats : beats.filter(b=>b.genre===filter);
  list.innerHTML = filtered.map((b,i)=>`
    <div class="beat-row ${currentBeat===b.id?'playing':''}" id="beatRow${b.id}">
      <div class="beat-num">${currentBeat===b.id&&isPlaying?'♫':String(i+1).padStart(2,'0')}</div>
      <div class="beat-info">
        <div class="beat-name">${b.name}</div>
        <div class="beat-meta">
          ${b.tag?`<span class="beat-tag">${b.tag}</span>`:''}
          <span>${b.genre.toUpperCase()}</span>
          <span>Key: ${b.key}</span>
        </div>
      </div>
      <span class="beat-bpm">${b.bpm} BPM</span>
      <div class="beat-price">${b.price}</div>
      <div class="beat-actions">
        <button class="icon-btn" title="Download" onclick="event.stopPropagation();downloadBeat('${b.name}')">⬇</button>
        <button class="icon-btn" title="Adicionar" onclick="event.stopPropagation()">♡</button>
        <button class="play-btn" onclick="playBeat(${b.id},'${b.name}','${b.duration}')">
          ${currentBeat===b.id&&isPlaying?'⏸':'▶'}
        </button>
      </div>
    </div>
  `).join('');
}

function setFilter(btn, filter){
  document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  renderBeats(filter);
}

// ── RENDER ALBUMS ──
function renderAlbums(){
  document.getElementById('albumGrid').innerHTML = albums.map(a=>`
    <div class="album-card">
      <div class="album-cover">
        <div class="album-cover-img">
          <div class="album-cover-placeholder">${a.emoji}</div>
        </div>
        <div class="album-overlay">
          <button class="play-btn" style="width:56px;height:56px;font-size:22px;">▶</button>
        </div>
      </div>
      <div class="album-title">${a.title}</div>
      <div class="album-year"><span>${a.year}</span><span>${a.tracks} faixas</span></div>
    </div>
  `).join('');
}

// ── PLAYER ──
function playBeat(id, name, dur){
  const player = document.getElementById('stickyPlayer');
  if(currentBeat===id){
    togglePlay(); return;
  }
  currentBeat = id; isPlaying = true; progress = 0;
  document.getElementById('playerName').textContent = name;
  document.getElementById('duration').textContent = dur;
  player.classList.add('visible');
  document.getElementById('playMainBtn').textContent = '⏸';
  startProgress();
  renderBeats(document.querySelector('.filter-btn.active').dataset.filter||'all');
}

function togglePlay(){
  isPlaying = !isPlaying;
  document.getElementById('playMainBtn').textContent = isPlaying?'⏸':'▶';
  if(isPlaying) startProgress(); else clearInterval(progressInterval);
  renderBeats('all');
}

function startProgress(){
  clearInterval(progressInterval);
  progressInterval = setInterval(()=>{
    progress = (progress+0.5)%100;
    document.getElementById('progressFill').style.width = progress+'%';
    const secs = Math.floor(progress/100*204);
    document.getElementById('currentTime').textContent = Math.floor(secs/60)+':'+(secs%60).toString().padStart(2,'0');
  },500);
}

function seekTo(e,bar){
  const rect = bar.getBoundingClientRect();
  progress = ((e.clientX-rect.left)/rect.width)*100;
  document.getElementById('progressFill').style.width = progress+'%';
}

function downloadBeat(name){
  const a = document.createElement('a');
  a.href = '#';
  alert(`Download iniciado: ${name||'beat'}.mp3\n\n(Conecte ao backend para download real)`);
}

// ── UPLOAD ──
const uploadArea = document.getElementById('uploadArea');
uploadArea.addEventListener('dragover', e=>{ e.preventDefault(); uploadArea.classList.add('dragover'); });
uploadArea.addEventListener('dragleave', ()=>uploadArea.classList.remove('dragover'));
uploadArea.addEventListener('drop', e=>{ e.preventDefault(); uploadArea.classList.remove('dragover'); handleFiles(e.dataTransfer.files); });

function handleFiles(files){
  const list = document.getElementById('fileList');
  Array.from(files).forEach(f=>{
    const item = document.createElement('div');
    item.className='file-item';
    const size = f.size>1024*1024 ? (f.size/1024/1024).toFixed(1)+' MB' : (f.size/1024).toFixed(0)+' KB';
    item.innerHTML=`
      <span class="file-icon">🎵</span>
      <span class="file-name">${f.name}</span>
      <span class="file-size">${size}</span>
      <button class="file-remove" onclick="this.parentElement.remove()">✕</button>
    `;
    list.appendChild(item);
  });
}

// ── MODAL ──
function openModal(tab){
  document.getElementById('authModal').classList.add('open');
  switchTab(tab);
}

function closeModal(){ document.getElementById('authModal').classList.remove('open'); }

function closeModalOutside(e){ if(e.target===document.getElementById('authModal')) closeModal(); }

function switchTab(tab){
  document.getElementById('loginForm').style.display = tab==='login'?'flex':'none';
  document.getElementById('registerForm').style.display = tab==='register'?'flex':'none';
  document.getElementById('tabLogin').classList.toggle('active', tab==='login');
  document.getElementById('tabReg').classList.toggle('active', tab==='register');
}

// ── INIT ──
renderBeats(); renderAlbums();
</script>
</body>
</html>