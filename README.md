<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Renan Coutinho — Dev Backend</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg:        #0D1117;
      --bg2:       #161B22;
      --bg3:       #21262D;
      --border:    #30363D;
      --green:     #2ECC71;
      --green-dim: #1a7a45;
      --text:      #E6EDF3;
      --muted:     #8B949E;
      --accent2:   #58A6FF;
      --font-disp: 'Space Grotesk', sans-serif;
      --font-body: 'Inter', sans-serif;
      --font-mono: 'JetBrains Mono', monospace;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-body);
      line-height: 1.6;
      overflow-x: hidden;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      background: rgba(13,17,23,.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
      padding: 0 2rem;
      height: 56px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .nav-logo {
      font-family: var(--font-mono);
      font-size: .85rem;
      color: var(--green);
      letter-spacing: .04em;
    }
    .nav-logo span { color: var(--muted); }
    .nav-links { display: flex; gap: 1.8rem; list-style: none; }
    .nav-links a {
      font-size: .82rem;
      color: var(--muted);
      text-decoration: none;
      font-family: var(--font-body);
      font-weight: 500;
      letter-spacing: .03em;
      transition: color .2s;
    }
    .nav-links a:hover { color: var(--text); }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex;
      align-items: center;
      padding: 6rem 2rem 4rem;
      max-width: 1100px;
      margin: 0 auto;
    }
    .hero-inner { width: 100%; }
    .hero-eyebrow {
      font-family: var(--font-mono);
      font-size: .78rem;
      color: var(--green);
      letter-spacing: .12em;
      text-transform: uppercase;
      margin-bottom: 1.2rem;
      display: flex;
      align-items: center;
      gap: .6rem;
    }
    .hero-eyebrow::before {
      content: '';
      display: inline-block;
      width: 32px; height: 1px;
      background: var(--green);
    }
    h1 {
      font-family: var(--font-disp);
      font-size: clamp(2.8rem, 7vw, 5.5rem);
      font-weight: 700;
      line-height: 1.05;
      letter-spacing: -.02em;
      margin-bottom: 1rem;
    }
    h1 .last { color: var(--green); }
    .hero-sub {
      font-size: clamp(1rem, 2vw, 1.25rem);
      color: var(--muted);
      max-width: 560px;
      margin-bottom: 2.4rem;
      font-weight: 300;
    }

    /* terminal */
    .terminal {
      background: var(--bg2);
      border: 1px solid var(--border);
      border-radius: 10px;
      max-width: 540px;
      overflow: hidden;
      margin-bottom: 2.8rem;
    }
    .terminal-bar {
      background: var(--bg3);
      padding: .55rem 1rem;
      display: flex;
      align-items: center;
      gap: .5rem;
      border-bottom: 1px solid var(--border);
    }
    .dot { width: 11px; height: 11px; border-radius: 50%; }
    .dot-r { background: #FF5F56; }
    .dot-y { background: #FFBD2E; }
    .dot-g { background: #27C93F; }
    .terminal-title {
      font-family: var(--font-mono);
      font-size: .7rem;
      color: var(--muted);
      margin-left: auto;
      margin-right: auto;
    }
    .terminal-body {
      padding: 1rem 1.2rem 1.2rem;
      font-family: var(--font-mono);
      font-size: .82rem;
      line-height: 1.9;
    }
    .terminal-body .prompt { color: var(--green); }
    .terminal-body .cmd    { color: var(--text); }
    .terminal-body .out    { color: var(--muted); }
    .terminal-body .hi     { color: var(--accent2); }
    #cursor {
      display: inline-block;
      width: 8px; height: 14px;
      background: var(--green);
      vertical-align: middle;
      animation: blink 1s step-end infinite;
    }
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

    /* cta buttons */
    .cta-row { display: flex; gap: 1rem; flex-wrap: wrap; }
    .btn {
      display: inline-flex;
      align-items: center;
      gap: .45rem;
      padding: .65rem 1.4rem;
      border-radius: 6px;
      font-family: var(--font-body);
      font-size: .88rem;
      font-weight: 500;
      text-decoration: none;
      transition: all .2s;
      cursor: pointer;
      border: 1px solid transparent;
    }
    .btn-primary {
      background: var(--green);
      color: #0D1117;
      border-color: var(--green);
    }
    .btn-primary:hover { background: #25b562; }
    .btn-outline {
      background: transparent;
      color: var(--text);
      border-color: var(--border);
    }
    .btn-outline:hover { border-color: var(--muted); background: var(--bg2); }

    /* ── SECTIONS ── */
    section {
      max-width: 1100px;
      margin: 0 auto;
      padding: 5rem 2rem;
    }
    .section-label {
      font-family: var(--font-mono);
      font-size: .72rem;
      color: var(--green);
      letter-spacing: .14em;
      text-transform: uppercase;
      margin-bottom: .8rem;
    }
    h2 {
      font-family: var(--font-disp);
      font-size: clamp(1.6rem, 3.5vw, 2.4rem);
      font-weight: 600;
      letter-spacing: -.01em;
      margin-bottom: 2.8rem;
    }
    .divider {
      width: 100%;
      height: 1px;
      background: var(--border);
      max-width: 1100px;
      margin: 0 auto;
    }

    /* ── SKILLS ── */
    .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 1rem;
    }
    .skill-card {
      background: var(--bg2);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1.4rem;
      transition: border-color .2s, transform .2s;
    }
    .skill-card:hover { border-color: var(--green); transform: translateY(-2px); }
    .skill-card h3 {
      font-family: var(--font-disp);
      font-size: .92rem;
      font-weight: 600;
      margin-bottom: .9rem;
      color: var(--text);
      display: flex;
      align-items: center;
      gap: .5rem;
    }
    .skill-card h3 .icon { font-size: 1.1rem; }
    .tag-list { display: flex; flex-wrap: wrap; gap: .4rem; }
    .tag {
      font-family: var(--font-mono);
      font-size: .72rem;
      background: var(--bg3);
      border: 1px solid var(--border);
      border-radius: 4px;
      padding: .2rem .55rem;
      color: var(--muted);
      transition: all .15s;
    }
    .tag:hover { color: var(--green); border-color: var(--green-dim); }

    /* ── EXPERIENCE ── */
    .exp-list { display: flex; flex-direction: column; gap: 1.6rem; }
    .exp-item {
      background: var(--bg2);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1.6rem;
      position: relative;
      transition: border-color .2s;
    }
    .exp-item:hover { border-color: var(--border); }
    .exp-item::before {
      content: '';
      position: absolute;
      left: 0; top: 0; bottom: 0;
      width: 3px;
      border-radius: 3px 0 0 3px;
      background: var(--green);
      opacity: .5;
    }
    .exp-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      flex-wrap: wrap;
      gap: .5rem;
      margin-bottom: .9rem;
    }
    .exp-company {
      font-family: var(--font-disp);
      font-size: 1rem;
      font-weight: 600;
    }
    .exp-period {
      font-family: var(--font-mono);
      font-size: .72rem;
      color: var(--muted);
      background: var(--bg3);
      border: 1px solid var(--border);
      border-radius: 4px;
      padding: .2rem .6rem;
    }
    .exp-role {
      font-size: .82rem;
      color: var(--green);
      font-weight: 500;
      margin-bottom: .6rem;
    }
    .exp-desc {
      font-size: .85rem;
      color: var(--muted);
      line-height: 1.65;
    }

    /* ── PROJECTS ── */
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 1rem;
    }
    .proj-card {
      background: var(--bg2);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1.6rem;
      display: flex;
      flex-direction: column;
      gap: .8rem;
      transition: border-color .2s, transform .2s;
    }
    .proj-card:hover { border-color: var(--accent2); transform: translateY(-2px); }
    .proj-card-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .proj-icon { font-size: 1.5rem; }
    .proj-link {
      color: var(--muted);
      font-size: 1rem;
      text-decoration: none;
      transition: color .2s;
    }
    .proj-link:hover { color: var(--accent2); }
    .proj-card h3 {
      font-family: var(--font-disp);
      font-size: .95rem;
      font-weight: 600;
    }
    .proj-card p {
      font-size: .83rem;
      color: var(--muted);
      line-height: 1.6;
      flex: 1;
    }

    /* ── EDUCATION ── */
    .edu-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 1rem;
    }
    .edu-card {
      background: var(--bg2);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1.4rem;
      transition: border-color .2s;
    }
    .edu-card:hover { border-color: var(--green); }
    .edu-badge {
      display: inline-block;
      font-family: var(--font-mono);
      font-size: .68rem;
      padding: .18rem .55rem;
      border-radius: 3px;
      margin-bottom: .8rem;
      background: rgba(46,204,113,.1);
      border: 1px solid var(--green-dim);
      color: var(--green);
    }
    .edu-card h3 {
      font-family: var(--font-disp);
      font-size: .92rem;
      font-weight: 600;
      margin-bottom: .3rem;
    }
    .edu-card p {
      font-size: .82rem;
      color: var(--muted);
    }

    /* ── CONTACT ── */
    #contact { text-align: center; }
    #contact h2 { margin-bottom: .8rem; }
    #contact .sub {
      font-size: .95rem;
      color: var(--muted);
      margin-bottom: 2.4rem;
      max-width: 440px;
      margin-left: auto;
      margin-right: auto;
    }
    .contact-links {
      display: flex;
      justify-content: center;
      gap: 1rem;
      flex-wrap: wrap;
    }

    /* ── FOOTER ── */
    footer {
      border-top: 1px solid var(--border);
      text-align: center;
      padding: 1.8rem 2rem;
      font-family: var(--font-mono);
      font-size: .72rem;
      color: var(--muted);
    }
    footer a { color: var(--green); text-decoration: none; }

    /* ── FADE-IN ANIMATION ── */
    .fade-in {
      opacity: 0;
      transform: translateY(20px);
      transition: opacity .55s ease, transform .55s ease;
    }
    .fade-in.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 640px) {
      .nav-links { gap: 1.1rem; }
      .nav-links a { font-size: .76rem; }
    }
    @media (prefers-reduced-motion: reduce) {
      .fade-in { transition: none; opacity: 1; transform: none; }
      #cursor { animation: none; }
    }
  </style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo"><span>~/</span>renan-coutinho</div>
  <ul class="nav-links">
    <li><a href="#sobre">sobre</a></li>
    <li><a href="#skills">skills</a></li>
    <li><a href="#experiencia">experiência</a></li>
    <li><a href="#projetos">projetos</a></li>
    <li><a href="#contact">contato</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-inner">
    <div class="hero-eyebrow">disponível para oportunidades</div>
    <h1>Renan<br>Coutinho<br><span class="last">Dev Full Stack</span></h1>
    <p class="hero-sub">
      Desenvolvedor apaixonado por construir soluções completas — do back-end ao mobile — com Java, Node.js, React e muito café.
    </p>

    <div class="terminal">
      <div class="terminal-bar">
        <div class="dot dot-r"></div>
        <div class="dot dot-y"></div>
        <div class="dot dot-g"></div>
        <span class="terminal-title">renan@portfolio ~ zsh</span>
      </div>
      <div class="terminal-body" id="term-output">
        <div><span class="prompt">❯ </span><span class="cmd">whoami</span></div>
        <div class="out">renan-coutinho — dev full stack, es/br</div>
        <div style="margin-top:.4rem"><span class="prompt">❯ </span><span class="cmd">cat stack.json</span></div>
        <div id="stack-out"></div>
        <div id="cursor-line"><span id="cursor"></span></div>
      </div>
    </div>

    <div class="cta-row">
      <a href="https://github.com/ren4nzin" target="_blank" class="btn btn-primary">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
      <a href="https://www.linkedin.com/in/renancoutinho-061289256" target="_blank" class="btn btn-outline">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- SOBRE -->
<section id="sobre" class="fade-in">
  <div class="section-label">// sobre</div>
  <h2>Quem sou eu</h2>
  <p style="max-width:680px; color:var(--muted); font-size:.95rem; line-height:1.8;">
    Tenho 21 anos, sou de Viana — ES, e estou cursando Análise e Desenvolvimento de Sistemas na Universidade Estácio de Sá.
    Trabalho atualmente como Assistente Administrativo na <strong style="color:var(--text)">Elite Construtora e Incorporadora</strong>,
    onde lido com controle de ponto, estoque e processos de compras — experiência que me deu visão de negócio além do código.
    Nos projetos de extensão desenvolvi software real com metodologias ágeis (Scrum), entrevistas com clientes e levantamento de requisitos.
  </p>
</section>

<div class="divider"></div>

<!-- SKILLS -->
<section id="skills" class="fade-in">
  <div class="section-label">// habilidades</div>
  <h2>Stack técnico</h2>
  <div class="skills-grid">
    <div class="skill-card">
      <h3><span class="icon">☕</span> Back-end</h3>
      <div class="tag-list">
        <span class="tag">Java</span>
        <span class="tag">Spring Boot</span>
        <span class="tag">Node.js</span>
        <span class="tag">REST APIs</span>
      </div>
    </div>
    <div class="skill-card">
      <h3><span class="icon">🗄️</span> Banco de Dados</h3>
      <div class="tag-list">
        <span class="tag">MongoDB</span>
        <span class="tag">SQL Server</span>
        <span class="tag">PostgreSQL</span>
        <span class="tag">Redis</span>
      </div>
    </div>
    <div class="skill-card">
      <h3><span class="icon">📱</span> Front-end / Mobile</h3>
      <div class="tag-list">
        <span class="tag">React</span>
        <span class="tag">React Native</span>
        <span class="tag">Expo</span>
        <span class="tag">Vite</span>
      </div>
    </div>
    <div class="skill-card">
      <h3><span class="icon">🔧</span> Ferramentas</h3>
      <div class="tag-list">
        <span class="tag">Git</span>
        <span class="tag">Docker</span>
        <span class="tag">Scrum</span>
        <span class="tag">ERP</span>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- EXPERIENCIA -->
<section id="experiencia" class="fade-in">
  <div class="section-label">// experiência</div>
  <h2>Onde trabalhei</h2>
  <div class="exp-list">
    <div class="exp-item">
      <div class="exp-header">
        <span class="exp-company">Elite Construtora e Incorporadora</span>
        <span class="exp-period">07/2024 → atual</span>
      </div>
      <div class="exp-role">Assistente Administrativo</div>
      <p class="exp-desc">
        Criação e alimentação de planilhas, rotinas administrativas, solicitações e ordens de compra, cadastro de fornecedores, controle de estoque, conferência de notas fiscais, controle de ponto e benefícios de colaboradores, entradas e saídas de materiais.
      </p>
    </div>
    <div class="exp-item">
      <div class="exp-header">
        <span class="exp-company">Imugi Tecnologia e Educação</span>
        <span class="exp-period">07/2022 → 01/2023</span>
      </div>
      <div class="exp-role">Auxiliar Administrativo</div>
      <p class="exp-desc">
        Criação e alimentação de planilhas, rotinas administrativas, cadastros de clientes, auxílio na seleção e recrutamento de estagiários, atendimento ao cliente e operação de sistemas ERP.
      </p>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- PROJETOS -->
<section id="projetos" class="fade-in">
  <div class="section-label">// projetos</div>
  <h2>O que construí</h2>
  <div class="projects-grid">
    <div class="proj-card">
      <div class="proj-card-top">
        <span class="proj-icon">🍔</span>
        <a href="https://github.com/ren4nzin" target="_blank" class="proj-link" title="Ver no GitHub">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        </a>
      </div>
      <h3>Sistema de Pedidos — Lanchonete</h3>
      <p>Sistema full stack com 2 microserviços Spring Boot (PostgreSQL + MongoDB/Redis), API Gateway Node.js, PWA React/Vite, notificações WhatsApp e pagamentos PIX via Mercado Pago.</p>
      <div class="tag-list">
        <span class="tag">Spring Boot</span>
        <span class="tag">MongoDB</span>
        <span class="tag">React</span>
        <span class="tag">Docker</span>
        <span class="tag">PIX</span>
      </div>
    </div>
    <div class="proj-card">
      <div class="proj-card-top">
        <span class="proj-icon">🏥</span>
        <a href="https://github.com/ren4nzin" target="_blank" class="proj-link" title="Ver no GitHub">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        </a>
      </div>
      <h3>App de Consultas Médicas</h3>
      <p>Aplicativo mobile para agendamento, cancelamento e visualização de consultas. API Node.js, React Native + Expo para mobile, Vite para web e MongoDB como banco de dados.</p>
      <div class="tag-list">
        <span class="tag">React Native</span>
        <span class="tag">Expo</span>
        <span class="tag">Node.js</span>
        <span class="tag">MongoDB</span>
      </div>
    </div>
    <div class="proj-card">
      <div class="proj-card-top">
        <span class="proj-icon">⚙️</span>
        <a href="https://github.com/ren4nzin" target="_blank" class="proj-link" title="Ver no GitHub">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        </a>
      </div>
      <h3>Planilha de Controle de Ponto (AFD)</h3>
      <p>Processador do formato AFD/REP-C de relógio de ponto brasileiro, gerando Excel formatado com pares entrada/saída, totais e codificação de cores em português.</p>
      <div class="tag-list">
        <span class="tag">Python</span>
        <span class="tag">Excel</span>
        <span class="tag">AFD/REP-C</span>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- EDUCAÇÃO -->
<section id="educacao" class="fade-in">
  <div class="section-label">// formação</div>
  <h2>Educação</h2>
  <div class="edu-grid">
    <div class="edu-card">
      <span class="edu-badge">cursando</span>
      <h3>Análise e Desenvolvimento de Sistemas</h3>
      <p>Universidade Estácio de Sá</p>
    </div>
    <div class="edu-card">
      <span class="edu-badge" style="background:rgba(88,166,255,.1);border-color:rgba(88,166,255,.3);color:var(--accent2)">concluído</span>
      <h3>Ensino Médio</h3>
      <p>CEEJA Vitória — ES</p>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- CONTACT -->
<section id="contact" class="fade-in">
  <div class="section-label">// contato</div>
  <h2>Vamos conversar?</h2>
  <p class="sub">Aberto a oportunidades de estágio e desenvolvimento. Me manda uma mensagem!</p>
  <div class="contact-links">
    <a href="mailto:renancouti21@gmail.com" class="btn btn-primary">
      <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m2 7 10 7 10-7"/></svg>
      renancouti21@gmail.com
    </a>
    <a href="https://github.com/ren4nzin" target="_blank" class="btn btn-outline">GitHub</a>
    <a href="https://www.linkedin.com/in/renancoutinho-061289256" target="_blank" class="btn btn-outline">LinkedIn</a>
    <a href="tel:+5527998422495" class="btn btn-outline">(27) 99842-2495</a>
  </div>
</section>

<!-- FOOTER -->
<footer>
  Feito com  por <a href="https://github.com/ren4nzin">Renan Coutinho</a> · Viana, ES · 2025
</footer>

<script>
  // ── TERMINAL TYPEWRITER ──
  const stackLines = [
    '  <span class="hi">"backend"</span>: <span class="out">["Java", "Spring Boot", "Node.js"]</span>,',
    '  <span class="hi">"frontend"</span>: <span class="out">["React", "React Native", "Vite"]</span>,',
    '  <span class="hi">"database"</span>: <span class="out">["MongoDB", "PostgreSQL", "Redis"]</span>,',
    '  <span class="hi">"tools"</span>:    <span class="out">["Git", "Docker", "Expo"]</span>',
  ];

  const out = document.getElementById('stack-out');
  const cursorLine = document.getElementById('cursor-line');

  function typeLines(lines, i = 0) {
    if (i === 0) out.innerHTML = '<span class="out">{</span>';
    if (i >= lines.length) {
      out.innerHTML += '<br><span class="out">}</span>';
      cursorLine.innerHTML = '<br><span class="prompt">❯ </span><span id="cursor"></span>';
      return;
    }
    const div = document.createElement('div');
    div.innerHTML = '';
    out.appendChild(div);
    let html = lines[i], charIdx = 0, stripped = [];
    // build stripped (no tags) for typing effect
    const tmp = document.createElement('div');
    tmp.innerHTML = html;
    const plain = tmp.textContent;
    let timer = setInterval(() => {
      charIdx++;
      // progressively reveal the raw html up to current visible char
      let visible = 0, result = '', inTag = false;
      for (let ci = 0; ci < html.length && visible < charIdx; ci++) {
        if (html[ci] === '<') inTag = true;
        result += html[ci];
        if (!inTag) visible++;
        if (html[ci] === '>') inTag = false;
      }
      div.innerHTML = result;
      if (charIdx >= plain.length) {
        clearInterval(timer);
        setTimeout(() => typeLines(lines, i + 1), 80);
      }
    }, 22);
  }

  setTimeout(() => typeLines(stackLines), 600);

  // ── SCROLL FADE-IN ──
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.12 });
  document.querySelectorAll('.fade-in').forEach(el => obs.observe(el));
</script>
</body>
</html>
