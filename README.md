<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lista de Presentes — Thais & Bruno</title>

  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600&family=Lato:wght@300;400;700&display=swap" rel="stylesheet">

  <style>
    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
    }

    body{
      font-family:'Lato',sans-serif;
      background:#fdf9f5;
      color:#3d2b1f;
    }

    .hero{
      background:#f9f0e8;
      padding:50px 20px;
      text-align:center;
      border-bottom:1px solid #e7d4c3;
    }

    .hero h1{
      font-family:'Playfair Display',serif;
      font-size:42px;
      color:#5c3d2e;
    }

    .hero p{
      margin-top:10px;
      color:#9e6e56;
      font-size:18px;
    }

    .container{
      max-width:1100px;
      margin:auto;
      padding:30px 20px;
    }

    .form-box{
      background:#fff;
      border-radius:18px;
      padding:25px;
      margin-bottom:30px;
      border:1px solid #ead8c8;
      box-shadow:0 3px 10px rgba(0,0,0,.04);
    }

    .form-title{
      font-size:24px;
      margin-bottom:20px;
      font-family:'Playfair Display',serif;
      color:#5c3d2e;
    }

    .row{
      display:grid;
      grid-template-columns:1fr 1fr;
      gap:15px;
      margin-bottom:15px;
    }

    @media(max-width:700px){
      .row{
        grid-template-columns:1fr;
      }
    }

    input,textarea{
      width:100%;
      padding:14px;
      border-radius:12px;
      border:1px solid #d8c1b0;
      background:#fffaf7;
      font-size:15px;
      outline:none;
    }

    textarea{
      resize:vertical;
      min-height:90px;
    }

    .gift-grid{
      display:grid;
      grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
      gap:18px;
      margin-top:25px;
    }

    .gift-card{
      background:#fff;
      border-radius:18px;
      overflow:hidden;
      border:2px solid #ead8c8;
      cursor:pointer;
      transition:.2s;
      position:relative;
    }

    .gift-card:hover{
      transform:translateY(-3px);
      border-color:#c8876a;
    }

    .gift-card.selected{
      border-color:#c8876a;
      box-shadow:0 0 0 4px rgba(200,135,106,.2);
    }

    .gift-card.reserved{
      opacity:.6;
      cursor:not-allowed;
      background:#f4f4f4;
    }

    .gift-card.mine{
      border-color:#62b57d;
      background:#eefbf2;
    }

    .gift-image{
      height:140px;
      display:flex;
      align-items:center;
      justify-content:center;
      font-size:60px;
    }

    .gift-info{
      padding:14px;
    }

    .gift-name{
      font-weight:700;
      margin-bottom:5px;
    }

    .gift-category{
      font-size:12px;
      color:#9e6e56;
      text-transform:uppercase;
    }

    .reserved-label{
      margin-top:8px;
      font-size:12px;
      color:#999;
      font-style:italic;
    }

    .mine-label{
      margin-top:8px;
      font-size:12px;
      color:#3a9b5e;
      font-weight:bold;
    }

    .custom-box{
      margin-top:25px;
      background:#fff;
      border:2px dashed #c8876a;
      border-radius:18px;
      padding:20px;
    }

    .custom-box textarea{
      margin-top:15px;
    }

    .submit-btn{
      width:100%;
      margin-top:25px;
      border:none;
      background:#c8876a;
      color:white;
      padding:18px;
      border-radius:14px;
      font-size:16px;
      font-weight:bold;
      cursor:pointer;
      transition:.2s;
    }

    .submit-btn:hover{
      background:#b47257;
    }

    .submit-btn:disabled{
      opacity:.7;
      cursor:not-allowed;
    }

    .records{
      margin-top:40px;
      background:#fff;
      border-radius:18px;
      padding:25px;
      border:1px solid #ead8c8;
    }

    table{
      width:100%;
      border-collapse:collapse;
      margin-top:20px;
    }

    th,td{
      padding:12px;
      border-bottom:1px solid #eee;
      text-align:left;
    }

    th{
      background:#fdf0e8;
      color:#9e6e56;
      font-size:13px;
      text-transform:uppercase;
    }

    .toast{
      position:fixed;
      bottom:25px;
      left:50%;
      transform:translateX(-50%);
      background:#3d2b1f;
      color:white;
      padding:15px 25px;
      border-radius:40px;
      opacity:0;
      transition:.3s;
      pointer-events:none;
    }

    .toast.show{
      opacity:1;
    }
  </style>
</head>
<body>

<div class="hero">
  <h1>Lista de Presentes</h1>
  <p>Thais & Bruno — 14 de Setembro de 2025</p>
</div>

<div class="container">

  <div class="form-box">

    <div class="form-title">💌 Seus dados</div>

    <div class="row">
      <input type="text" id="name" placeholder="Seu nome">
      <input type="text" id="lastname" placeholder="Seu sobrenome">
    </div>

    <textarea id="message" placeholder="Mensagem para os noivos (opcional)"></textarea>

  </div>

  <h2>🎁 Escolha um presente</h2>

  <div class="gift-grid" id="gift-grid"></div>

  <div class="custom-box">
    <label>
      <input type="checkbox" id="custom-check">
      Quero dar um presente personalizado
    </label>

    <textarea
      id="custom-text"
      placeholder="Descreva o presente..."
    ></textarea>
  </div>

  <button class="submit-btn" id="submit-btn">
    Confirmar Presente ♡
  </button>

  <div class="records">

    <h2>📋 Presentes Confirmados</h2>

    <table>
      <thead>
        <tr>
          <th>Convidado</th>
          <th>Presente</th>
          <th>Mensagem</th>
        </tr>
      </thead>

      <tbody id="records-body"></tbody>
    </table>

  </div>

</div>

<div class="toast" id="toast"></div>

<script>

  /* =====================================================
      COLE A URL DO GOOGLE APPS SCRIPT AQUI
  ===================================================== */

  const APPS_SCRIPT_URL = 'COLE_AQUI_SUA_URL';

  /* ===================================================== */

  const GIFTS = [
    { id:1,  name:'Jogo de Panelas', emoji:'🍳', category:'Cozinha' },
    { id:2,  name:'Air Fryer', emoji:'🍟', category:'Cozinha' },
    { id:3,  name:'Smart TV', emoji:'📺', category:'Eletrônicos' },
    { id:4,  name:'Mesa de Jantar', emoji:'🪑', category:'Sala' },
    { id:5,  name:'Máquina de Café', emoji:'☕', category:'Cozinha' },
    { id:6,  name:'Jogo de Toalhas', emoji:'🛁', category:'Banheiro' },
    { id:7,  name:'Batedeira', emoji:'🎂', category:'Cozinha' },
    { id:8,  name:'Faqueiro', emoji:'🍽️', category:'Mesa' },
  ];

  let selectedGift = null;
  let records = JSON.parse(localStorage.getItem('records') || '[]');

  function renderGifts(){

    const grid = document.getElementById('gift-grid');

    grid.innerHTML = '';

    GIFTS.forEach(gift => {

      const reserved = records.find(r => r.giftId === gift.id);

      const div = document.createElement('div');

      div.className = 'gift-card';

      if(reserved){
        div.classList.add('reserved');
      }

      if(selectedGift === gift.id){
        div.classList.add('selected');
      }

      div.innerHTML = `
        <div class="gift-image">${gift.emoji}</div>

        <div class="gift-info">
          <div class="gift-name">${gift.name}</div>
          <div class="gift-category">${gift.category}</div>

          ${
            reserved
            ? `<div class="reserved-label">🔒 Selecionado por ${reserved.name.split(' ')[0]}</div>`
            : ''
          }
        </div>
      `;

      if(!reserved){

        div.onclick = () => {

          selectedGift = gift.id;

          renderGifts();
        };
      }

      grid.appendChild(div);

    });

  }

  async function sendToSheets(data){

    try{

      const response = await fetch(APPS_SCRIPT_URL, {
        method:'POST',
        headers:{
          'Content-Type':'application/json'
        },
        body:JSON.stringify(data)
      });

      return await response.json();

    }catch(err){

      console.error(err);

      return {
        success:false,
        message:'Erro ao conectar.'
      };
    }
  }

  async function submitGift(){

    const name = document.getElementById('name').value.trim();
    const lastname = document.getElementById('lastname').value.trim();
    const message = document.getElementById('message').value.trim();

    if(!name || !lastname){

      alert('Preencha nome e sobrenome.');

      return;
    }

    const customCheck = document.getElementById('custom-check').checked;

    let giftName = '';
    let giftId = null;

    if(customCheck){

      giftName = document.getElementById('custom-text').value.trim();

      if(!giftName){

        alert('Descreva o presente.');

        return;
      }

    }else{

      if(!selectedGift){

        alert('Selecione um presente.');

        return;
      }

      const gift = GIFTS.find(g => g.id === selectedGift);

      giftName = gift.name;
      giftId = gift.id;
    }

    const btn = document.getElementById('submit-btn');

    btn.disabled = true;
    btn.innerText = 'Enviando...';

    const payload = {
      name: name + ' ' + lastname,
      giftName,
      giftId,
      message,
      date: new Date().toLocaleDateString('pt-BR'),
      time: new Date().toLocaleTimeString('pt-BR')
    };

    const result = await sendToSheets(payload);

    if(!result.success){

      alert(result.message || 'Erro.');

      btn.disabled = false;
      btn.innerText = 'Confirmar Presente ♡';

      return;
    }

    records.push(payload);

    localStorage.setItem('records', JSON.stringify(records));

    renderRecords();

    renderGifts();

    document.getElementById('name').value = '';
    document.getElementById('lastname').value = '';
    document.getElementById('message').value = '';
    document.getElementById('custom-text').value = '';
    document.getElementById('custom-check').checked = false;

    selectedGift = null;

    showToast('✓ Presente confirmado com sucesso!');

    btn.disabled = false;
    btn.innerText = 'Confirmar Presente ♡';
  }

  function renderRecords(){

    const tbody = document.getElementById('records-body');

    tbody.innerHTML = '';

    records.forEach(r => {

      tbody.innerHTML += `
        <tr>
          <td>${r.name}</td>
          <td>${r.giftName}</td>
          <td>${r.message || '-'}</td>
        </tr>
      `;
    });
  }

  function showToast(text){

    const toast = document.getElementById('toast');

    toast.innerText = text;

    toast.classList.add('show');

    setTimeout(() => {
      toast.classList.remove('show');
    }, 3000);
  }

  document
    .getElementById('submit-btn')
    .addEventListener('click', submitGift);

  renderGifts();

  renderRecords();

</script>

</body>
</html>
