<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gabryel Velli – Dev Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --border: #1e1e2e;
    --accent: #00f5c4;
    --accent2: #ff4d6d;
    --accent3: #ffd166;
    --text: #e8e8f0;
    --muted: #6e6e8a;
    --mono: 'Space Mono', monospace;
    --sans: 'Syne', sans-serif;
  }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
    overflow-x: hidden;
  }

  /* noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
  }

  .card {
    position: relative;
    width: 100%;
    max-width: 720px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    z-index: 1;
    animation: fadeIn 0.8s ease forwards;
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* top neon line */
  .card::before {
    content: '';
    display: block;
    height: 3px;
    background: linear-gradient(90deg, var(--accent2), var(--accent), var(--accent3), var(--accent2));
    background-size: 200% 100%;
    animation: slide 3s linear infinite;
  }

  @keyframes slide {
    0%   { background-position: 0% 0%; }
    100% { background-position: 200% 0%; }
  }

  /* ── HEADER ── */
  .header {
    padding: 2.4rem 2.4rem 1.6rem;
    display: flex;
    align-items: flex-start;
    gap: 1.6rem;
    border-bottom: 1px solid var(--border);
    position: relative;
  }

  .avatar {
    width: 72px;
    height: 72px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    flex-shrink: 0;
    box-shadow: 0 0 0 2px var(--bg), 0 0 0 4px var(--accent);
    animation: pulse 3s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 0 2px var(--bg), 0 0 0 4px var(--accent), 0 0 20px rgba(0,245,196,0.15); }
    50%       { box-shadow: 0 0 0 2px var(--bg), 0 0 0 4px var(--accent), 0 0 32px rgba(0,245,196,0.35); }
  }

  .header-text h1 {
    font-size: 1.75rem;
    font-weight: 800;
    letter-spacing: -0.03em;
    line-height: 1;
    margin-bottom: 0.4rem;
  }

  .header-text h1 span { color: var(--accent); }

  .header-text .role {
    font-family: var(--mono);
    font-size: 0.72rem;
    color: var(--muted);
    letter-spacing: 0.12em;
    text-transform: uppercase;
  }

  .status-dot {
    display: inline-block;
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--accent);
    margin-right: 6px;
    animation: blink 2s ease-in-out infinite;
    vertical-align: middle;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0.3; }
  }

  /* ── TYPING LINE ── */
  .typing-wrap {
    padding: 1.2rem 2.4rem;
    border-bottom: 1px solid var(--border);
    font-family: var(--mono);
    font-size: 0.82rem;
    color: var(--accent);
    min-height: 2.4rem;
  }

  .cursor {
    display: inline-block;
    width: 8px; height: 1em;
    background: var(--accent);
    vertical-align: text-bottom;
    animation: blink 0.8s step-end infinite;
    margin-left: 2px;
  }

  /* ── INFO GRID ── */
  .info-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0;
    border-bottom: 1px solid var(--border);
  }

  .info-item {
    padding: 1.2rem 2.4rem;
    border-right: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    transition: background 0.2s;
  }

  .info-item:nth-child(even) { border-right: none; }
  .info-item:nth-last-child(-n+2) { border-bottom: none; }

  .info-item:hover { background: rgba(0,245,196,0.03); }

  .info-item .label {
    font-family: var(--mono);
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 0.3rem;
  }

  .info-item .value {
    font-size: 0.88rem;
    font-weight: 700;
    color: var(--text);
  }

  .info-item .value a {
    color: var(--accent);
    text-decoration: none;
  }

  .info-item .value a:hover { text-decoration: underline; }

  /* ── SKILLS ── */
  .section {
    padding: 1.6rem 2.4rem;
    border-bottom: 1px solid var(--border);
  }

  .section-title {
    font-family: var(--mono);
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.12em;
    text-transform: uppercase;
    margin-bottom: 1rem;
  }

  .skills-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .skill-tag {
    font-family: var(--mono);
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    padding: 0.35rem 0.85rem;
    border-radius: 2px;
    text-transform: uppercase;
    position: relative;
    overflow: hidden;
    cursor: default;
    transition: transform 0.15s, box-shadow 0.15s;
  }

  .skill-tag::after {
    content: '';
    position: absolute;
    inset: 0;
    background: rgba(255,255,255,0.06);
    opacity: 0;
    transition: opacity 0.2s;
  }

  .skill-tag:hover { transform: translateY(-2px); }
  .skill-tag:hover::after { opacity: 1; }

  .t-html  { background: #e34f26; color: #fff; box-shadow: 0 2px 12px rgba(227,79,38,0.35); }
  .t-css   { background: #264de4; color: #fff; box-shadow: 0 2px 12px rgba(38,77,228,0.35); }
  .t-js    { background: #f0db4f; color: #111; box-shadow: 0 2px 12px rgba(240,219,79,0.3); }
  .t-cs    { background: #9b4993; color: #fff; box-shadow: 0 2px 12px rgba(155,73,147,0.35); }
  .t-java  { background: #f89820; color: #111; box-shadow: 0 2px 12px rgba(248,152,32,0.3); }
  .t-sql   { background: var(--accent2); color: #fff; box-shadow: 0 2px 12px rgba(255,77,109,0.35); }
  .t-pw    { background: #2ead33; color: #fff; box-shadow: 0 2px 12px rgba(46,173,51,0.3); }
  .t-ef    { background: #512bd4; color: #fff; box-shadow: 0 2px 12px rgba(81,43,212,0.35); }

  /* ── STATS BAR ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    border-top: 1px solid var(--border);
  }

  .stat {
    padding: 1.2rem 2.4rem;
    text-align: center;
    border-right: 1px solid var(--border);
    transition: background 0.2s;
  }

  .stat:last-child { border-right: none; }
  .stat:hover { background: rgba(0,245,196,0.04); }

  .stat-num {
    font-family: var(--mono);
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--accent);
    display: block;
    line-height: 1;
    margin-bottom: 0.3rem;
  }

  .stat-label {
    font-size: 0.7rem;
    color: var(--muted);
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  /* ── FOOTER ── */
  .footer {
    padding: 1rem 2.4rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .footer-left {
    font-family: var(--mono);
    font-size: 0.65rem;
    color: var(--muted);
  }

  .linkedin-btn {
    font-family: var(--mono);
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    text-decoration: none;
    color: var(--bg);
    background: var(--accent);
    padding: 0.5rem 1.2rem;
    border-radius: 2px;
    transition: box-shadow 0.2s, transform 0.15s;
  }

  .linkedin-btn:hover {
    box-shadow: 0 0 20px rgba(0,245,196,0.5);
    transform: translateY(-1px);
  }

  /* ── SCANLINE ── */
  .card::after {
    content: '';
    position: absolute;
    top: -100%;
    left: 0;
    right: 0;
    height: 60px;
    background: linear-gradient(transparent, rgba(0,245,196,0.025), transparent);
    pointer-events: none;
    animation: scan 6s linear infinite;
  }

  @keyframes scan {
    0%   { top: -10%; }
    100% { top: 110%; }
  }

  @media (max-width: 520px) {
    .info-grid { grid-template-columns: 1fr; }
    .info-item { border-right: none; }
    .info-item:nth-last-child(-n+2) { border-bottom: 1px solid var(--border); }
    .info-item:last-child { border-bottom: none; }
    .stats-row { grid-template-columns: 1fr; }
    .stat { border-right: none; border-bottom: 1px solid var(--border); }
    .stat:last-child { border-bottom: none; }
    .header { flex-direction: column; gap: 1rem; }
  }
</style>
</head>
<body>

<div class="card">

  <div class="header">
    <div class="avatar">👨‍💻</div>
    <div class="header-text">
      <h1>Gabryel <span>Velli</span></h1>
      <p class="role"><span class="status-dot"></span>Junior Analyst · Dev · TOTVS JuriTIs</p>
    </div>
  </div>

  <div class="typing-wrap">
    <span id="typed"></span><span class="cursor"></span>
  </div>

  <div class="info-grid">
    <div class="info-item">
      <div class="label">📚 Estudando</div>
      <div class="value">Análise e Desenv. de Sistemas</div>
    </div>
    <div class="info-item">
      <div class="label">🏢 Empresa</div>
      <div class="value">TOTVS JuriTIs</div>
    </div>
    <div class="info-item">
      <div class="label">📞 Telefone</div>
      <div class="value">(11) 99114-5586</div>
    </div>
    <div class="info-item">
      <div class="label">📧 E-mail</div>
      <div class="value"><a href="mailto:gabryel.velli@gmail.com">gabryel.velli@gmail.com</a></div>
    </div>
  </div>

  <div class="section">
    <div class="section-title">// stack de conhecimentos</div>
    <div class="skills-row">
      <span class="skill-tag t-html">HTML5</span>
      <span class="skill-tag t-css">CSS3</span>
      <span class="skill-tag t-js">JavaScript</span>
      <span class="skill-tag t-cs">C#</span>
      <span class="skill-tag t-java">Java</span>
      <span class="skill-tag t-sql">SQL Server</span>
      <span class="skill-tag t-pw">Playwright</span>
      <span class="skill-tag t-ef">Entity Framework</span>
    </div>
  </div>

  <div class="stats-row">
    <div class="stat">
      <span class="stat-num">8+</span>
      <span class="stat-label">Tecnologias</span>
    </div>
    <div class="stat">
      <span class="stat-num">Jnr 3</span>
      <span class="stat-label">Nível Atual</span>
    </div>
    <div class="stat">
      <span class="stat-num">∞</span>
      <span class="stat-label">Aprendendo</span>
    </div>
  </div>

  <div class="footer">
    <span class="footer-left">// gabryelvelli · github.com</span>
    <a class="linkedin-btn" href="https://linkedin.com" target="_blank">LinkedIn →</a>
  </div>

</div>

<script>
  const lines = [
    '> Olá! Me chamo Gabryel Velli 👋',
    '> Analista Jr. em Desenv. Gerencial',
    '> Apaixonado por código limpo & testes',
    '> Sempre buscando evoluir 🚀',
  ];

  let lineIdx = 0, charIdx = 0, deleting = false;
  const el = document.getElementById('typed');

  function type() {
    const current = lines[lineIdx];
    if (!deleting) {
      charIdx++;
      el.textContent = current.slice(0, charIdx);
      if (charIdx === current.length) {
        deleting = true;
        setTimeout(type, 1800);
        return;
      }
    } else {
      charIdx--;
      el.textContent = current.slice(0, charIdx);
      if (charIdx === 0) {
        deleting = false;
        lineIdx = (lineIdx + 1) % lines.length;
        setTimeout(type, 400);
        return;
      }
    }
    setTimeout(type, deleting ? 28 : 48);
  }

  setTimeout(type, 800);
</script>
</body>
</html>
