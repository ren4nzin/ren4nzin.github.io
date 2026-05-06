<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lista de Presentes — Vitoria & Renan</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Lato:wght@300;400;700&display=swap" rel="stylesheet">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: 'Lato', sans-serif; background: #fdf9f5; min-height: 100vh; }

    .hero {
      background: #f9f0e8;
      padding: 2.5rem 2rem 1.8rem;
      text-align: center;
      border-bottom: 1px solid #e8d5c4;
      position: relative;
      overflow: hidden;
    }
    .hero::before { content: '✿'; position: absolute; top: 12px; left: 40px; font-size: 28px; opacity: 0.2; color: #c8876a; }
    .hero::after  { content: '✿'; position: absolute; top: 12px; right: 40px; font-size: 28px; opacity: 0.2; color: #c8876a; }
    .hero-title { font-family: 'Playfair Display', serif; font-size: 2.4rem; color: #5c3d2e; }
    .hero-subtitle { font-family: 'Playfair Display', serif; font-style: italic; color: #9e6e56; font-size: 1.1rem; margin-top: 6px; }
    .hero-divider { display: flex; align-items: center; justify-content: center; gap: 12px; margin: 14px auto 0; }
    .hero-divider span { color: #c8876a; font-size: 18px; }
    .hero-line { width: 80px; height: 1px; background: #d4a882; }

    .main { max-width: 960px; margin: 0 auto; padding: 2rem 1.5rem; }

    /* BANNER CONFIRMAÇÃO */
    .confirmation-banner {
      display: none;
      background: #edf9f2;
      border: 1.5px solid #7ac9a0;
      border-radius: 14px;
      padding: 1.4rem 1.6rem;
      margin-bottom: 1.8rem;
      align-items: flex-start;
      gap: 14px;
    }
    .confirmation-banner.show { display: flex; }
    .cb-icon { font-size: 30px; flex-shrink: 0; }
    .cb-title { font-family: 'Playfair Display', serif; font-size: 1.15rem; color: #1e6e45; margin-bottom: 4px; }
    .cb-desc { font-size: 13.5px; color: #3a9163; }
    .cb-gift { display: inline-block; background: #d4f0e2; color: #1e6e45; border-radius: 8px; padding: 3px 10px; font-weight: 700; margin-top: 6px; font-size: 13px; }

    /* FORM */
    .form-section {
      background: #fff;
      border-radius: 16px;
      border: 1px solid #edd9c8;
      padding: 2rem;
      margin-bottom: 2rem;
      box-shadow: 0 2px 10px rgba(160,90,60,0.05);
    }
    .form-title { font-family: 'Playfair Display', serif; font-size: 1.25rem; color: #5c3d2e; margin-bottom: 1.2rem; }
    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-bottom: 1rem; }
    @media (max-width: 560px) { .form-row { grid-template-columns: 1fr; } }
    .form-group { display: flex; flex-direction: column; gap: 5px; }
    .form-group label { font-size: 12px; font-weight: 700; color: #9e6e56; text-transform: uppercase; letter-spacing: 0.08em; }
    .form-group input,
    .form-group textarea {
      padding: 10px 14px;
      border: 1.5px solid #e0c9b8;
      border-radius: 10px;
      font-family: 'Lato', sans-serif;
      font-size: 15px;
      color: #3d2b1f;
      background: #fdf9f5;
      outline: none;
      transition: border-color 0.2s, background 0.2s;
    }
    .form-group input:focus,
    .form-group textarea:focus { border-color: #c8876a; background: #fff; }
    .form-group textarea { resize: vertical; min-height: 80px; }

    /* GRID DE PRESENTES */
    .section-title {
      font-family: 'Playfair Display', serif;
      font-size: 1.25rem;
      color: #5c3d2e;
      margin-bottom: 1.2rem;
      display: flex;
      align-items: center;
      gap: 10px;
      flex-wrap: wrap;
    }
    .counter-badge {
      background: #fdf0e8;
      color: #c8876a;
      border-radius: 20px;
      padding: 3px 12px;
      font-size: 13px;
      font-weight: 700;
      font-family: 'Lato', sans-serif;
      display: none;
    }

    .gift-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
      gap: 1rem;
      margin-bottom: 1.5rem;
    }

    .gift-card {
      background: #fff;
      border: 2px solid #edd9c8;
      border-radius: 14px;
      cursor: pointer;
      transition: border-color 0.18s, transform 0.18s, box-shadow 0.18s;
      overflow: hidden;
      position: relative;
    }
    .gift-card:hover:not(.reserved):not(.mine) {
      border-color: #c8876a;
      transform: translateY(-2px);
      box-shadow: 0 6px 18px rgba(160,90,60,0.12);
    }
    .gift-card.selected {
      border-color: #c8876a;
      background: #fffaf6;
      box-shadow: 0 0 0 3px rgba(200,135,106,0.2);
    }
    .gift-card.reserved {
      cursor: not-allowed;
      background: #f5f5f5;
      border-color: #ddd;
    }
    .gift-card.mine {
      cursor: default;
      background: #f0faf4;
      border-color: #7ac9a0;
      box-shadow: 0 0 0 3px rgba(100,190,140,0.15);
    }

    .gift-emoji {
      width: 100%;
      height: 130px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 54px;
      position: relative;
    }
    .gift-card.reserved .gift-emoji { filter: grayscale(0.7) opacity(0.6); }

    .reserved-overlay {
      position: absolute;
      inset: 0;
      background: rgba(245,245,245,0.6);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 5px;
    }
    .reserved-lock { font-size: 22px; }
    .reserved-label {
      font-size: 10.5px;
      font-weight: 700;
      color: #999;
      text-transform: uppercase;
      letter-spacing: 0.07em;
      background: rgba(255,255,255,0.92);
      padding: 3px 9px;
      border-radius: 20px;
      border: 1px solid #ddd;
    }

    .mine-overlay {
      position: absolute;
      inset: 0;
      background: rgba(230,248,238,0.55);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 5px;
    }
    .mine-check { font-size: 24px; }
    .mine-label {
      font-size: 10.5px;
      font-weight: 700;
      color: #27864d;
      text-transform: uppercase;
      letter-spacing: 0.07em;
      background: rgba(255,255,255,0.95);
      padding: 3px 9px;
      border-radius: 20px;
      border: 1px solid #7ac9a0;
    }

    .selected-badge {
      position: absolute;
      top: 8px;
      left: 8px;
      background: #c8876a;
      width: 24px;
      height: 24px;
      border-radius: 50%;
      display: none;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 13px;
    }
    .gift-card.selected .selected-badge { display: flex; }

    .gift-info { padding: 10px 12px 12px; }
    .gift-name { font-size: 13.5px; font-weight: 700; color: #3d2b1f; margin-bottom: 3px; line-height: 1.3; }
    .gift-card.reserved .gift-name,
    .gift-card.reserved .gift-category { color: #aaa; }
    .gift-category { font-size: 11px; color: #b08060; text-transform: uppercase; letter-spacing: 0.06em; }
    .reserved-by { font-size: 11px; color: #bbb; margin-top: 5px; font-style: italic; }
    .mine-by { font-size: 11px; color: #5aab77; margin-top: 5px; font-weight: 700; }

    /* PRESENTE PERSONALIZADO */
    .custom-option {
      background: #fff;
      border: 2px dashed #d4a882;
      border-radius: 14px;
      padding: 1.4rem;
      margin-bottom: 1.5rem;
      cursor: pointer;
      transition: border-color 0.18s, background 0.18s;
    }
    .custom-option:hover { border-color: #c8876a; background: #fffaf7; }
    .custom-option.active { border-style: solid; border-color: #c8876a; background: #fffaf7; }
    .custom-header { display: flex; align-items: center; gap: 10px; }
    .custom-header input[type="checkbox"] { width: 17px; height: 17px; accent-color: #c8876a; cursor: pointer; flex-shrink: 0; }
    .custom-header span { font-weight: 700; color: #5c3d2e; font-size: 14.5px; }
    .custom-body { display: none; margin-top: 1rem; }
    .custom-option.active .custom-body { display: block; }

    /* BOTÃO CONFIRMAR */
    .submit-btn {
      width: 100%;
      padding: 16px;
      background: #c8876a;
      color: white;
      border: none;
      border-radius: 12px;
      font-family: 'Lato', sans-serif;
      font-size: 16px;
      font-weight: 700;
      cursor: pointer;
      letter-spacing: 0.04em;
      transition: background 0.2s, transform 0.1s;
      margin-bottom: 0.5rem;
    }
    .submit-btn:hover { background: #b5705a; }
    .submit-btn:active { transform: scale(0.99); }

    /* TABELA DE REGISTROS */
    .records-section {
      background: #fff;
      border-radius: 16px;
      border: 1px solid #edd9c8;
      padding: 2rem;
      margin-top: 2rem;
      box-shadow: 0 2px 10px rgba(160,90,60,0.05);
    }
    .records-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 1.2rem;
      flex-wrap: wrap;
      gap: 10px;
    }
    .records-title { font-family: 'Playfair Display', serif; font-size: 1.2rem; color: #5c3d2e; }
    .export-btn {
      background: #5c3d2e;
      color: white;
      border: none;
      border-radius: 8px;
      padding: 9px 18px;
      font-size: 13px;
      font-weight: 700;
      cursor: pointer;
      letter-spacing: 0.04em;
      transition: background 0.18s;
    }
    .export-btn:hover { background: #3d2b1f; }

    .records-table { width: 100%; border-collapse: collapse; font-size: 13.5px; table-layout: fixed; }
    .records-table th {
      padding: 10px 12px;
      background: #fdf0e8;
      color: #9e6e56;
      font-weight: 700;
      text-align: left;
      text-transform: uppercase;
      font-size: 11px;
      letter-spacing: 0.07em;
      border-bottom: 1px solid #edd9c8;
    }
    .records-table td {
      padding: 10px 12px;
      border-bottom: 1px solid #f5ebe0;
      color: #3d2b1f;
      vertical-align: middle;
      word-wrap: break-word;
      overflow-wrap: break-word;
    }
    .records-table tr:last-child td { border-bottom: none; }
    .records-table tr:hover td { background: #fffaf7; }
    .badge-gift {
      background: #fdf0e8;
      color: #c8876a;
      border-radius: 6px;
      padding: 3px 8px;
      font-size: 11.5px;
      font-weight: 700;
      display: inline-block;
      max-width: 100%;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    .empty-state {
      text-align: center;
      padding: 2.5rem;
      color: #b08060;
      font-style: italic;
      font-size: 14px;
    }

    /* TOAST */
    .toast {
      position: fixed;
      bottom: 28px;
      left: 50%;
      transform: translateX(-50%) translateY(120px);
      background: #3d2b1f;
      color: white;
      padding: 13px 28px;
      border-radius: 40px;
      font-size: 14.5px;
      font-weight: 700;
      box-shadow: 0 6px 24px rgba(0,0,0,0.2);
      transition: transform 0.4s cubic-bezier(0.34,1.56,0.64,1);
      z-index: 9999;
      white-space: nowrap;
      pointer-events: none;
    }
    .toast.show { transform: translateX(-50%) translateY(0); }

    /* RESPONSIVE */
    @media (max-width: 480px) {
      .hero-title { font-size: 1.8rem; }
      .gift-grid { grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); }
      .records-table { font-size: 12px; }
    }
  </style>
</head>
<body>

  <div class="hero">
    <div class="hero-title">Lista de Presentes</div>
    <div class="hero-subtitle">Thais &amp; Bruno — 14 de Setembro de 2025</div>
    <div class="hero-divider">
      <div class="hero-line"></div>
      <span>♡</span>
      <div class="hero-line"></div>
    </div>
  </div>

  <div class="main">

    <!-- BANNER DE CONFIRMAÇÃO -->
    <div class="confirmation-banner" id="confirmation-banner">
      <div class="cb-icon">🎁</div>
      <div>
        <div class="cb-title" id="cb-title">Obrigado(a)!</div>
        <div class="cb-desc">Seu presente foi confirmado com sucesso. Os noivos ficarão muito felizes!</div>
        <div class="cb-gift" id="cb-gift"></div>
      </div>
    </div>

    <!-- FORMULÁRIO -->
    <div class="form-section">
      <div class="form-title">💌 Seus dados</div>
      <div class="form-row">
        <div class="form-group">
          <label>Seu nome *</label>
          <input type="text" id="guest-name" placeholder="Como você quer ser chamado(a)">
        </div>
        <div class="form-group">
          <label>Seu sobrenome *</label>
          <input type="text" id="guest-lastname" placeholder="Sobrenome">
        </div>
      </div>
      <div class="form-group">
        <label>Mensagem para os noivos (opcional)</label>
        <textarea id="guest-message" placeholder="Deixe um recado especial para Thais e Bruno..."></textarea>
      </div>
    </div>

    <!-- GRADE DE PRESENTES -->
    <div class="section-title">
      🎁 Escolha seu presente
      <span class="counter-badge" id="sel-counter">1 selecionado</span>
    </div>

    <div class="gift-grid" id="gift-grid"></div>

    <!-- PRESENTE PERSONALIZADO -->
    <div class="custom-option" id="custom-option" onclick="toggleCustom()">
      <div class="custom-header">
        <input type="checkbox" id="custom-check" onclick="event.stopPropagation(); toggleCustom()">
        <span>✏️  Quero dar um presente personalizado</span>
      </div>
      <div class="custom-body">
        <div class="form-group">
          <label>Descreva seu presente</label>
          <textarea id="custom-text" placeholder="Ex: Uma viagem especial, um jantar romântico, uma arte personalizada..." style="min-height:70px"></textarea>
        </div>
      </div>
    </div>

    <!-- CONFIRMAR -->
    <button class="submit-btn" onclick="submitGift()">Confirmar meu presente ♡</button>

    <!-- REGISTROS -->
    <div class="records-section">
      <div class="records-header">
        <div class="records-title">📋 Presentes confirmados</div>
        <button class="export-btn" onclick="exportExcel()">⬇ Exportar Excel</button>
      </div>
      <div id="records-container">
        <div class="empty-state">Nenhum presente confirmado ainda.</div>
      </div>
    </div>

  </div>

  <div class="toast" id="toast"></div>

  <script>
    const GIFTS = [
      { id:1,  name:'Jogo de Panelas Tramontina', category:'Cozinha',     emoji:'🍳', color:'#fde8d8' },
      { id:2,  name:'Jogo de Cama Queen',          category:'Quarto',      emoji:'🛏️', color:'#e8f0fd' },
      { id:3,  name:'Air Fryer 5L',                category:'Cozinha',     emoji:'🍟', color:'#fde8d8' },
      { id:4,  name:'Aspirador Robô',              category:'Casa',        emoji:'🤖', color:'#e8fde8' },
      { id:5,  name:'Jogo de Toalhas Premium',     category:'Banheiro',    emoji:'🛁', color:'#f0e8fd' },
      { id:6,  name:'Mixer Profissional',          category:'Cozinha',     emoji:'🥤', color:'#fde8d8' },
      { id:7,  name:'Smart TV 50"',                category:'Eletrônicos', emoji:'📺', color:'#e8f5fd' },
      { id:8,  name:'Mesa de Jantar 6 Lugares',    category:'Sala',        emoji:'🪑', color:'#fdf5e8' },
      { id:9,  name:'Jogo de Taças Bohemia',       category:'Mesa',        emoji:'🥂', color:'#fde8e8' },
      { id:10, name:'Máquina de Café Nespresso',   category:'Cozinha',     emoji:'☕', color:'#fde8d8' },
      { id:11, name:'Kit Churrasco Weber',         category:'Lazer',       emoji:'🍖', color:'#fdf0e8' },
      { id:12, name:'Batedeira KitchenAid',        category:'Cozinha',     emoji:'🎂', color:'#fde8d8' },
      { id:13, name:'Ventilador de Teto',          category:'Casa',        emoji:'💨', color:'#e8fdfd' },
      { id:14, name:'Espelho Decorativo Grande',   category:'Decoração',   emoji:'🪞', color:'#f5e8fd' },
      { id:15, name:'Secadora de Roupas',          category:'Casa',        emoji:'👕', color:'#e8fde8' },
      { id:16, name:'Conjunto Faqueiro 24 Pcs',    category:'Cozinha',     emoji:'🍽️', color:'#fde8d8' },
    ];

    const STORAGE_KEY     = 'wedding_gifts_v2';
    const SESSION_KEY     = 'my_wedding_session';

    let records       = [];
    let selectedGiftId = null;
    let customActive  = false;
    let myGiftId      = null;
    let myName        = null;

    /* ── PERSISTÊNCIA LOCAL (localStorage) ── */
    function loadData() {
      try {
        const r = localStorage.getItem(STORAGE_KEY);
        if (r) records = JSON.parse(r);
      } catch(e) { records = []; }
      try {
        const s = localStorage.getItem(SESSION_KEY);
        if (s) { const sess = JSON.parse(s); myGiftId = sess.giftId; myName = sess.name; }
      } catch(e) {}
    }

    function saveData() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(records));
    }

    function saveSession(giftId, name) {
      localStorage.setItem(SESSION_KEY, JSON.stringify({ giftId, name }));
    }

    /* ── HELPERS ── */
    function getReservedMap() {
      const map = {};
      records.forEach(r => { if (r.giftId) map[r.giftId] = r.name; });
      return map;
    }

    /* ── RENDER GRID ── */
    function renderGrid() {
      const reserved = getReservedMap();
      document.getElementById('gift-grid').innerHTML = GIFTS.map(g => {
        const reservedBy = reserved[g.id];
        const isReserved  = !!reservedBy && g.id !== myGiftId;
        const isMine      = g.id === myGiftId;
        const isSelected  = selectedGiftId === g.id;

        let cls = 'gift-card';
        if (isMine)      cls += ' mine';
        else if (isReserved) cls += ' reserved';
        else if (isSelected) cls += ' selected';

        const clickable = !isReserved && !isMine;

        return `
          <div class="${cls}" ${clickable ? `onclick="selectGift(${g.id})"` : ''}>
            <div class="selected-badge">✓</div>
            <div class="gift-emoji" style="background:${g.color}">
              ${g.emoji}
              ${isReserved ? `
                <div class="reserved-overlay">
                  <div class="reserved-lock">🔒</div>
                  <div class="reserved-label">Já selecionado</div>
                </div>` : ''}
              ${isMine ? `
                <div class="mine-overlay">
                  <div class="mine-check">✅</div>
                  <div class="mine-label">Meu presente</div>
                </div>` : ''}
            </div>
            <div class="gift-info">
              <div class="gift-name">${g.name}</div>
              <div class="gift-category">${g.category}</div>
              ${isReserved ? `<div class="reserved-by">Selecionado por ${reservedBy.split(' ')[0]}</div>` : ''}
              ${isMine     ? `<div class="mine-by">✓ Você selecionou este presente</div>` : ''}
            </div>
          </div>`;
      }).join('');
    }

    /* ── SELECIONAR PRESENTE ── */
    function selectGift(id) {
      if (myGiftId) return;
      selectedGiftId = (selectedGiftId === id) ? null : id;
      if (selectedGiftId) {
        customActive = false;
        document.getElementById('custom-check').checked = false;
        document.getElementById('custom-option').classList.remove('active');
      }
      updateCounter();
      renderGrid();
    }

    function toggleCustom() {
      if (myGiftId) return;
      customActive = !customActive;
      document.getElementById('custom-check').checked = customActive;
      document.getElementById('custom-option').classList.toggle('active', customActive);
      if (customActive) { selectedGiftId = null; renderGrid(); }
      updateCounter();
    }

    function updateCounter() {
      const c = document.getElementById('sel-counter');
      c.style.display = (selectedGiftId || customActive) ? 'inline-block' : 'none';
    }

    /* ── SUBMETER ── */
    function submitGift() {
      if (myGiftId) { showToast('Você já confirmou seu presente!'); return; }

      const name = document.getElementById('guest-name').value.trim();
      const last = document.getElementById('guest-lastname').value.trim();
      const msg  = document.getElementById('guest-message').value.trim();

      if (!name || !last) { alert('Por favor, preencha seu nome e sobrenome.'); return; }
      if (!selectedGiftId && !customActive) { alert('Por favor, selecione um presente da lista ou descreva um presente personalizado.'); return; }

      let giftName, giftId = null;

      if (customActive) {
        const ct = document.getElementById('custom-text').value.trim();
        if (!ct) { alert('Por favor, descreva seu presente personalizado.'); return; }
        giftName = '🎁 ' + ct;
      } else {
        const g = GIFTS.find(x => x.id === selectedGiftId);
        if (getReservedMap()[g.id]) {
          alert('Este presente já foi selecionado por outra pessoa. Por favor escolha outro.');
          renderGrid(); selectedGiftId = null; updateCounter(); return;
        }
        giftName = g.emoji + ' ' + g.name;
        giftId   = g.id;
      }

      const fullName = name + ' ' + last;
      const record = {
        id:       Date.now(),
        name:     fullName,
        giftName,
        giftId,
        message:  msg,
        date:     new Date().toLocaleDateString('pt-BR'),
        time:     new Date().toLocaleTimeString('pt-BR', { hour:'2-digit', minute:'2-digit' })
      };

      records.push(record);
      saveData();
      myGiftId = giftId;
      myName   = fullName;
      saveSession(giftId, fullName);

      /* reset form */
      document.getElementById('guest-name').value    = '';
      document.getElementById('guest-lastname').value = '';
      document.getElementById('guest-message').value  = '';
      document.getElementById('custom-text').value    = '';
      selectedGiftId = null;
      customActive   = false;
      document.getElementById('custom-check').checked = false;
      document.getElementById('custom-option').classList.remove('active');
      document.getElementById('sel-counter').style.display = 'none';

      renderGrid();
      renderRecords();
      showConfirmationBanner(fullName, giftName);
      showToast('✓ Presente confirmado! Muito obrigado(a) ♡');
    }

    /* ── BANNER CONFIRMAÇÃO ── */
    function showConfirmationBanner(name, giftName) {
      const n  = (name || myName || '').split(' ')[0];
      const gn = giftName || (records.find(r => r.name === myName) || {}).giftName || 'Presente personalizado';
      document.getElementById('cb-title').textContent = 'Obrigado(a), ' + n + '! 🎉';
      document.getElementById('cb-gift').textContent  = gn;
      document.getElementById('confirmation-banner').classList.add('show');
      document.getElementById('confirmation-banner').scrollIntoView({ behavior: 'smooth', block: 'start' });
    }

    /* ── RENDER TABELA ── */
    function renderRecords() {
      const c = document.getElementById('records-container');
      if (!records.length) {
        c.innerHTML = '<div class="empty-state">Nenhum presente confirmado ainda.</div>';
        return;
      }
      c.innerHTML = `
        <table class="records-table">
          <colgroup>
            <col style="width:36px">
            <col style="width:26%">
            <col style="width:32%">
            <col style="width:28%">
            <col style="width:68px">
          </colgroup>
          <thead>
            <tr>
              <th>#</th>
              <th>Convidado(a)</th>
              <th>Presente</th>
              <th>Mensagem</th>
              <th>Data</th>
            </tr>
          </thead>
          <tbody>
            ${records.map((r, i) => `
              <tr>
                <td style="color:#b08060;font-weight:700">${i + 1}</td>
                <td><strong>${r.name}</strong></td>
                <td><span class="badge-gift" title="${r.giftName}">${r.giftName}</span></td>
                <td style="color:#7a5a4a;font-style:italic">${r.message || '—'}</td>
                <td style="color:#b08060;font-size:11.5px">${r.date}</td>
              </tr>`).join('')}
          </tbody>
        </table>`;
    }

    /* ── EXPORTAR EXCEL ── */
    function exportExcel() {
      if (!records.length) { alert('Não há registros para exportar.'); return; }
      const data = records.map((r, i) => ({
        'Nº':           i + 1,
        'Convidado(a)': r.name,
        'Presente':     r.giftName.replace(/\p{Emoji}/gu, '').trim(),
        'Mensagem':     r.message || '',
        'Data':         r.date,
        'Hora':         r.time,
      }));
      const ws = XLSX.utils.json_to_sheet(data);
      ws['!cols'] = [{ wch:4 }, { wch:30 }, { wch:35 }, { wch:40 }, { wch:12 }, { wch:8 }];
      const wb = XLSX.utils.book_new();
      XLSX.utils.book_append_sheet(wb, ws, 'Presentes');
      XLSX.writeFile(wb, 'lista_presentes_casamento.xlsx');
      showToast('📥 Arquivo Excel baixado com sucesso!');
    }

    /* ── TOAST ── */
    function showToast(msg) {
      const t = document.getElementById('toast');
      t.textContent = msg;
      t.classList.add('show');
      setTimeout(() => t.classList.remove('show'), 3200);
    }

    /* ── INIT ── */
    loadData();
    renderGrid();
    renderRecords();
    updateCounter();
    if (myName) showConfirmationBanner();
  </script>

</body>
</html>
