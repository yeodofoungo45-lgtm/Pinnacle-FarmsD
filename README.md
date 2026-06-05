<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <meta name="theme-color" content="#1a2218" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="apple-mobile-web-app-title" content="Pinnacle Farms" />
  <title>Pinnacle Farms</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
    body { font-family: Georgia, serif; background: #0f1410; color: #e8ede4; height: 100dvh; overflow: hidden; display: flex; flex-direction: column; }
    button { font-family: Georgia, serif; }
    input, select, textarea { font-family: Georgia, serif; }
    ::-webkit-scrollbar { width: 4px; } ::-webkit-scrollbar-track { background: #1a2218; } ::-webkit-scrollbar-thumb { background: #3a5a2c; border-radius: 4px; }
    #app { display: flex; flex-direction: column; height: 100dvh; }
    .topbar { background: #1a2218; border-bottom: 1px solid #2d3d2a; padding: 12px 16px; padding-top: max(12px, env(safe-area-inset-top)); display: flex; align-items: center; justify-content: space-between; flex-shrink: 0; }
    .logo { display: flex; align-items: center; gap: 10px; }
    .logo-icon { width: 34px; height: 34px; border-radius: 8px; background: linear-gradient(135deg, #7eb856, #4a8a2c); display: flex; align-items: center; justify-content: center; font-size: 18px; }
    .logo-text { font-weight: 700; font-size: 15px; color: #c8e0b8; letter-spacing: 1px; }
    .status-dot { background: #1e2e1a; border: 1px solid #2d3d2a; border-radius: 8px; padding: 5px 12px; font-size: 12px; color: #9fd878; }
    .page-header { padding: 14px 16px 10px; border-bottom: 1px solid #1e2e1a; flex-shrink: 0; }
    .page-title { font-size: 18px; font-weight: 700; color: #c8e0b8; }
    .page-date { font-size: 11px; color: #5a7a50; margin-top: 2px; }
    .content { flex: 1; overflow-y: auto; padding: 14px 14px 90px; -webkit-overflow-scrolling: touch; }
    .bottomnav { position: fixed; bottom: 0; left: 0; right: 0; background: #1a2218; border-top: 1px solid #2d3d2a; display: flex; padding-bottom: env(safe-area-inset-bottom); z-index: 50; }
    .nav-btn { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 3px; padding: 10px 4px; border: none; background: transparent; cursor: pointer; color: #5a7a50; font-size: 9px; letter-spacing: 0.5px; transition: color 0.2s; position: relative; }
    .nav-btn.active { color: #9fd878; }
    .nav-btn .nav-icon { font-size: 20px; }
    .nav-badge { position: absolute; top: 6px; right: calc(50% - 16px); background: #c0392b; color: #fff; font-size: 9px; padding: 1px 5px; border-radius: 10px; }
    .grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 12px; }
    .kpi { background: #1a2218; border: 1px solid #2d3d2a; border-radius: 14px; padding: 16px; }
    .kpi-icon { font-size: 20px; margin-bottom: 8px; }
    .kpi-label { font-size: 11px; color: #6b8a60; margin-bottom: 4px; }
    .kpi-val { font-size: 24px; font-weight: 700; margin-bottom: 2px; }
    .kpi-sub { font-size: 10px; color: #4a6a40; }
    .card { background: #1a2218; border: 1px solid #2d3d2a; border-radius: 14px; padding: 18px; margin-bottom: 12px; }
    .card-title { font-size: 11px; font-weight: 700; color: #8ab880; margin-bottom: 14px; text-transform: uppercase; letter-spacing: 1px; }
    .row { display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid #1e2e1a; align-items: center; }
    .row:last-child { border-bottom: none; }
    .row-label { font-size: 12px; color: #6b8a60; }
    .row-val { font-size: 13px; color: #c8e0b8; font-weight: 600; }
    .chart { display: flex; align-items: flex-end; gap: 6px; height: 70px; padding-top: 6px; }
    .chart-col { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 3px; }
    .chart-bar { width: 100%; border-radius: 3px 3px 0 0; min-height: 4px; opacity: 0.85; }
    .chart-lbl { font-size: 8px; color: #4a6a40; }
    .prog-wrap { height: 6px; background: #1e2e1a; border-radius: 3px; margin-top: 6px; }
    .prog-bar { height: 100%; border-radius: 3px; }
    .bat-card { background: #1a2218; border: 1px solid #2d3d2a; border-radius: 14px; padding: 18px; margin-bottom: 10px; border-left-width: 4px; border-left-style: solid; }
    .badge { font-size: 10px; padding: 3px 10px; border-radius: 20px; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; }
    .alert-item { background: #1a2218; border-radius: 12px; padding: 16px; display: flex; gap: 12px; margin-bottom: 10px; border: 1px solid; }
    .modal-bg { position: fixed; inset: 0; background: rgba(0,0,0,0.75); display: flex; align-items: flex-end; justify-content: center; z-index: 100; }
    .modal { background: #1a2218; border: 1px solid #3a5a2c; border-radius: 20px 20px 0 0; padding: 24px; width: 100%; padding-bottom: max(24px, env(safe-area-inset-bottom)); max-height: 90dvh; overflow-y: auto; }
    .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
    .modal-title { font-size: 18px; font-weight: 700; color: #c8e0b8; }
    .close-btn { background: none; border: none; color: #6b8a60; font-size: 24px; cursor: pointer; padding: 4px; }
    .btn-row { display: flex; gap: 10px; margin-top: 16px; }
    .btn-outline { flex: 1; padding: 12px; border-radius: 10px; border: 1px solid #3a5a2c; background: transparent; color: #9fd878; cursor: pointer; font-size: 14px; }
    .btn-solid { flex: 1; padding: 12px; border-radius: 10px; border: none; background: linear-gradient(135deg, #7eb856, #4a8a2c); color: #fff; cursor: pointer; font-size: 14px; font-weight: 700; }
    .btn-danger { flex: 1; padding: 12px; border-radius: 10px; border: 1px solid #c0392b; background: transparent; color: #e74c3c; cursor: pointer; font-size: 14px; }
    .field { margin-bottom: 14px; }
    .field label { display: block; font-size: 12px; color: #6b8a60; margin-bottom: 6px; }
    .field input, .field select { width: 100%; background: #0f1410; border: 1px solid #3a5a2c; border-radius: 8px; padding: 10px 12px; color: #e8ede4; font-size: 14px; outline: none; }
    .field input:focus, .field select:focus { border-color: #7eb856; }
    .field select option { background: #1a2218; }
    .stock-card { background: #1a2218; border-radius: 14px; padding: 18px; }
    .stock-val { font-size: 26px; font-weight: 700; margin-bottom: 10px; }
    .pills { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 14px; }
    .pill { padding: 6px 14px; border-radius: 20px; border: 1px solid #2d3d2a; background: transparent; color: #9fd878; cursor: pointer; font-size: 12px; font-family: Georgia, serif; }
    .edit-btn { background: #1e3a15; border: 1px solid #3a5a2c; border-radius: 8px; color: #9fd878; padding: 6px 12px; font-size: 12px; cursor: pointer; font-family: Georgia, serif; }
    .range-wrap { display: flex; align-items: center; gap: 10px; }
    .range-wrap input[type=range] { flex: 1; accent-color: #7eb856; }
    .range-val { font-size: 14px; color: #c8e0b8; font-weight: 700; min-width: 45px; text-align: right; }
    .toast { position: fixed; top: 80px; left: 50%; transform: translateX(-50%); background: #2d4a22; border: 1px solid #7eb856; color: #9fd878; padding: 10px 20px; border-radius: 10px; font-size: 13px; z-index: 200; opacity: 0; transition: opacity 0.3s; pointer-events: none; white-space: nowrap; }
    .toast.show { opacity: 1; }
  </style>
</head>
<body>
<div id="app">
  <div class="topbar">
    <div class="logo">
      <div class="logo-icon">🐔</div>
      <div class="logo-text">PINNACLE FARMS</div>
    </div>
    <div class="status-dot">● Actif</div>
  </div>
  <div class="page-header">
    <div class="page-title" id="pageTitle">Tableau de bord</div>
    <div class="page-date" id="pageDate"></div>
  </div>
  <div class="content" id="content"></div>
  <nav class="bottomnav">
    <button class="nav-btn active" onclick="nav('dashboard')" id="nav-dashboard"><span class="nav-icon">⊞</span>Dashboard</button>
    <button class="nav-btn" onclick="nav('batiments')" id="nav-batiments"><span class="nav-icon">🏚</span>Bâtiments</button>
    <button class="nav-btn" onclick="nav('sante')" id="nav-sante"><span class="nav-icon">♥</span>Santé</button>
    <button class="nav-btn" onclick="nav('stocks')" id="nav-stocks"><span class="nav-icon">▦</span>Stocks</button>
    <button class="nav-btn" onclick="nav('production')" id="nav-production"><span class="nav-icon">📈</span>Production</button>
    <button class="nav-btn" onclick="nav('alertes')" id="nav-alertes"><span class="nav-icon">⚠</span>Alertes<span class="nav-badge" id="badge-alertes"></span></button>
  </nav>
</div>

<div class="modal-bg" id="modal" style="display:none">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="modal-title"></div>
      <button class="close-btn" onclick="closeModal()">✕</button>
    </div>
    <div id="modal-body"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ── DONNÉES SAUVEGARDÉES LOCALEMENT ──
function loadData() {
  try {
    const saved = localStorage.getItem('pinnacle-data');
    if (saved) return JSON.parse(saved);
  } catch(e) {}
  return {
    batiments: [
      { id:1, nom:"Bâtiment A", capacite:5000, occupation:4800, age:32, race:"Ross 308", statut:"actif" },
      { id:2, nom:"Bâtiment B", capacite:6000, occupation:5900, age:18, race:"Cobb 500", statut:"actif" },
      { id:3, nom:"Bâtiment C", capacite:4500, occupation:0, age:0, race:"—", statut:"vide" },
      { id:4, nom:"Bâtiment D", capacite:5500, occupation:5200, age:45, race:"Ross 308", statut:"récolte" },
    ],
    stocks: { aliment:12400, eau:98, medicaments:74, vaccins:88 },
    alertes: [
      { id:1, type:"danger", msg:"Bâtiment D: température élevée (32°C)", heure:"09:14" },
      { id:2, type:"warning", msg:"Stock aliment sous 15 000 kg", heure:"08:30" },
      { id:3, type:"info", msg:"Vaccination prévue Bâtiment B demain", heure:"07:00" },
    ],
    mortalites: [{d:"Lun",v:12},{d:"Mar",v:8},{d:"Mer",v:15},{d:"Jeu",v:6},{d:"Ven",v:10},{d:"Sam",v:9},{d:"Dim",v:7}],
    productions: [{s:"S1",p:1.2},{s:"S2",p:1.8},{s:"S3",p:2.5},{s:"S4",p:3.1},{s:"S5",p:3.8},{s:"S6",p:4.4}],
    nextId: 5
  };
}

function saveData() {
  try { localStorage.setItem('pinnacle-data', JSON.stringify(DATA)); } catch(e) {}
}

let DATA = loadData();
let currentPage = 'dashboard';
const TITLES = { dashboard:'Tableau de bord', batiments:'Bâtiments', sante:'Santé & Mortalité', stocks:'Stocks', production:'Production', alertes:'Alertes' };

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2500);
}

function nav(page) {
  currentPage = page;
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('nav-' + page).classList.add('active');
  document.getElementById('pageTitle').textContent = TITLES[page];
  document.getElementById('content').scrollTop = 0;
  updateBadge();
  render();
}

function updateBadge() {
  const dangers = DATA.alertes.filter(a => a.type === 'danger').length;
  const badge = document.getElementById('badge-alertes');
  badge.textContent = dangers > 0 ? dangers : '';
  badge.style.display = dangers > 0 ? 'block' : 'none';
}

function setDate() {
  document.getElementById('pageDate').textContent = new Date().toLocaleDateString('fr-FR', { weekday:'long', year:'numeric', month:'long', day:'numeric' });
}

function statut_color(s) { return s==='actif'?'#7eb856':s==='récolte'?'#e67e22':'#4a6a40'; }
function statut_bg(s) { return s==='actif'?'#1e3a15':s==='récolte'?'#3a2010':'#1e2e1a'; }

function barChart(data, keyX, keyY, color) {
  const max = Math.max(...data.map(d => d[keyY]));
  return `<div class="chart">${data.map(d => `<div class="chart-col"><div class="chart-bar" style="height:${Math.round(d[keyY]/max*56)}px;background:${color}"></div><div class="chart-lbl">${d[keyX]}</div></div>`).join('')}</div>`;
}

function kpi(icon, label, val, sub, color) {
  return `<div class="kpi"><div class="kpi-icon">${icon}</div><div class="kpi-label">${label}</div><div class="kpi-val" style="color:${color}">${val}</div>${sub?`<div class="kpi-sub">${sub}</div>`:''}</div>`;
}

// ── RENDER PAGES ──
function render() {
  const c = document.getElementById('content');
  if (currentPage==='dashboard') c.innerHTML = renderDashboard();
  else if (currentPage==='batiments') c.innerHTML = renderBatiments();
  else if (currentPage==='sante') c.innerHTML = renderSante();
  else if (currentPage==='stocks') c.innerHTML = renderStocks();
  else if (currentPage==='production') c.innerHTML = renderProduction();
  else if (currentPage==='alertes') c.innerHTML = renderAlertes();
}

function renderDashboard() {
  const total = DATA.batiments.reduce((a,b)=>a+b.occupation,0);
  const cap = DATA.batiments.reduce((a,b)=>a+b.capacite,0);
  const taux = cap>0?Math.round(total/cap*100):0;
  const mort = DATA.mortalites[DATA.mortalites.length-1].v;
  const dangers = DATA.alertes.filter(a=>a.type==='danger').length;
  return `
    <div class="grid2">
      ${kpi('🐔','Total Poulets',total.toLocaleString(),'en élevage','#7eb856')}
      ${kpi('⊞','Occupation',taux+'%',DATA.batiments.length+' bâtiments','#5ba3d9')}
      ${kpi('♥','Mortalité/jour',mort,'poulets',mort>10?'#e74c3c':'#7eb856')}
      ${kpi('⚠','Alertes',dangers,'urgentes',dangers>0?'#e67e22':'#7eb856')}
    </div>
    <div class="card">
      <div class="card-title">État des bâtiments</div>
      ${DATA.batiments.map(b=>`
        <div style="margin-bottom:12px">
          <div style="display:flex;justify-content:space-between;margin-bottom:5px">
            <span style="font-size:12px;color:#b0c8a0">${b.nom}</span>
            <span style="font-size:11px;color:#6b8a60">${b.occupation.toLocaleString()}/${b.capacite.toLocaleString()}</span>
          </div>
          <div class="prog-wrap"><div class="prog-bar" style="width:${Math.round(b.occupation/b.capacite*100)}%;background:${b.statut==='récolte'?'#e67e22':b.statut==='vide'?'#3d5a35':'linear-gradient(90deg,#7eb856,#4a8a2c)'}"></div></div>
        </div>`).join('')}
    </div>
    <div class="card">
      <div class="card-title">Alertes récentes</div>
      ${DATA.alertes.length===0?'<div style="color:#4a6a40;font-size:13px">Aucune alerte</div>':DATA.alertes.slice(0,3).map(a=>`
        <div class="row">
          <div style="display:flex;gap:8px;align-items:flex-start">
            <div style="width:8px;height:8px;border-radius:50%;background:${a.type==='danger'?'#e74c3c':a.type==='warning'?'#e67e22':'#5ba3d9'};margin-top:4px;flex-shrink:0"></div>
            <div style="font-size:12px;color:#b0c8a0">${a.msg}<br><span style="font-size:10px;color:#4a6a40">${a.heure}</span></div>
          </div>
        </div>`).join('')}
    </div>
    <div class="card">
      <div class="card-title">Mortalité — 7 derniers jours</div>
      ${barChart(DATA.mortalites.map(d=>({date:d.d,val:d.v})),'date','val','#e74c3c')}
    </div>`;
}

function renderBatiments() {
  return `
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px">
      <span style="color:#6b8a60;font-size:13px">${DATA.batiments.length} bâtiment(s)</span>
      <button class="btn-solid" style="padding:8px 16px;font-size:13px" onclick="openNouveauBat()">+ Nouveau</button>
    </div>
    ${DATA.batiments.map(b=>`
      <div class="bat-card" style="border-left-color:${statut_color(b.statut)}">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
          <span style="font-size:17px;font-weight:700;color:#c8e0b8">${b.nom}</span>
          <div style="display:flex;gap:6px;align-items:center">
            <span class="badge" style="background:${statut_bg(b.statut)};color:${statut_color(b.statut)}">${b.statut}</span>
            <button class="edit-btn" onclick="openEditBat(${b.id})">✏️ Modifier</button>
          </div>
        </div>
        <div style="font-size:12px;color:#6b8a60;margin-bottom:8px">Race: <span style="color:#b0c8a0">${b.race}</span></div>
        ${b.occupation>0?`
          <div style="display:flex;justify-content:space-between;margin-bottom:5px;font-size:11px;color:#6b8a60">
            <span>${b.occupation.toLocaleString()} poulets</span><span>${Math.round(b.occupation/b.capacite*100)}%</span>
          </div>
          <div class="prog-wrap"><div class="prog-bar" style="width:${Math.round(b.occupation/b.capacite*100)}%;background:${b.statut==='récolte'?'#e67e22':'linear-gradient(90deg,#7eb856,#4a8a2c)'}"></div></div>
          <div style="font-size:11px;color:#5a7a50;margin-top:8px">Âge: ${b.age} jours</div>`
        :`<div style="color:#3d5a35;font-size:12px">Bâtiment vide — prêt pour un nouveau lot</div>`}
      </div>`).join('')}`;
}

function renderSante() {
  const totalMort = DATA.mortalites.reduce((a,b)=>a+b.v,0);
  const total = DATA.batiments.reduce((a,b)=>a+b.occupation,0);
  const taux = total>0?(totalMort/total*100).toFixed(2):'0.00';
  return `
    <div class="grid2">
      ${kpi('♥','Mortalité 7j',totalMort,'total','#e74c3c')}
      ${kpi('%','Taux mortalité',taux+'%','','#7eb856')}
    </div>
    <div class="card">
      <div class="card-title">Mortalité par jour — Modifier</div>
      ${DATA.mortalites.map((d,i)=>`
        <div class="row">
          <span class="row-label">${d.d}</span>
          <div style="display:flex;align-items:center;gap:8px">
            <button onclick="changeMort(${i},-1)" style="background:#1e3a15;border:1px solid #3a5a2c;color:#9fd878;border-radius:6px;width:28px;height:28px;cursor:pointer;font-size:16px">−</button>
            <span style="color:#e74c3c;font-weight:700;min-width:24px;text-align:center">${d.v}</span>
            <button onclick="changeMort(${i},1)" style="background:#1e3a15;border:1px solid #3a5a2c;color:#9fd878;border-radius:6px;width:28px;height:28px;cursor:pointer;font-size:16px">+</button>
          </div>
        </div>`).join('')}
    </div>
    <div class="card">
      <div class="card-title">Graphique mortalité</div>
      ${barChart(DATA.mortalites.map(d=>({date:d.d,val:d.v})),'date','val','#e74c3c')}
    </div>`;
}

function renderStocks() {
  const items = [
    {key:'aliment',label:'Aliment (kg)',max:20000,icon:'🌾',seuil:5000,unite:'kg'},
    {key:'eau',label:'Eau',max:100,icon:'💧',seuil:20,unite:'%'},
    {key:'medicaments',label:'Médicaments',max:100,icon:'💊',seuil:20,unite:'%'},
    {key:'vaccins',label:'Vaccins',max:100,icon:'💉',seuil:20,unite:'%'},
  ];
  return `
    ${items.map(item=>{
      const val = DATA.stocks[item.key];
      const pct = Math.round(val/item.max*100);
      const low = val<=item.seuil;
      return `<div class="card" style="border:1px solid ${low?'#c0392b':'#2d3d2a'}">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
          <div style="display:flex;align-items:center;gap:8px"><span style="font-size:22px">${item.icon}</span><span style="font-size:13px;color:#6b8a60">${item.label}</span></div>
          ${low?'<span style="background:#3a1010;color:#e74c3c;font-size:10px;padding:2px 8px;border-radius:10px">⚠ Stock bas</span>':''}
        </div>
        <div class="stock-val" style="color:${low?'#e74c3c':'#c8e0b8'}">${val.toLocaleString()} ${item.unite}</div>
        <div class="prog-wrap" style="margin-bottom:12px"><div class="prog-bar" style="width:${pct}%;background:${low?'#c0392b':'linear-gradient(90deg,#7eb856,#4a8a2c)'}"></div></div>
        <div class="range-wrap">
          <input type="range" min="0" max="${item.max}" value="${val}" oninput="updateStock('${item.key}',this.value,this)" />
          <span class="range-val">${pct}%</span>
        </div>
      </div>`;
    }).join('')}`;
}

function renderProduction() {
  return `
    <div class="grid2">
      ${kpi('⚖','Poids moyen',DATA.productions[DATA.productions.length-1].p+' kg','sem. '+DATA.productions.length,'#7eb856')}
      ${kpi('📦','Prêts récolte',DATA.batiments.filter(b=>b.statut==='récolte').length,'bâtiment(s)','#e67e22')}
    </div>
    <div class="card">
      <div class="card-title">Poids par semaine — Modifier</div>
      ${DATA.productions.map((d,i)=>`
        <div class="row">
          <span class="row-label">${d.s}</span>
          <div style="display:flex;align-items:center;gap:8px">
            <button onclick="changePoids(${i},-0.1)" style="background:#1e3a15;border:1px solid #3a5a2c;color:#9fd878;border-radius:6px;width:28px;height:28px;cursor:pointer;font-size:14px">−</button>
            <span style="color:#7eb856;font-weight:700;min-width:40px;text-align:center">${d.p.toFixed(1)} kg</span>
            <button onclick="changePoids(${i},0.1)" style="background:#1e3a15;border:1px solid #3a5a2c;color:#9fd878;border-radius:6px;width:28px;height:28px;cursor:pointer;font-size:14px">+</button>
          </div>
        </div>`).join('')}
      <button onclick="ajouterSemaine()" style="width:100%;margin-top:12px;padding:10px;border-radius:8px;border:1px dashed #3a5a2c;background:transparent;color:#6b8a60;cursor:pointer;font-size:13px;font-family:Georgia,serif">+ Ajouter une semaine</button>
    </div>
    <div class="card">
      <div class="card-title">Courbe de croissance</div>
      ${barChart(DATA.productions.map(d=>({semaine:d.s,poids:d.p})),'semaine','poids','#7eb856')}
    </div>`;
}

function renderAlertes() {
  const dangers = DATA.alertes.filter(a=>a.type==='danger').length;
  return `
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px">
      <span style="color:#6b8a60;font-size:13px">${DATA.alertes.length} alerte(s) — ${dangers} urgente(s)</span>
      <button class="btn-solid" style="padding:8px 14px;font-size:12px" onclick="openNouvelleAlerte()">+ Nouvelle</button>
    </div>
    ${DATA.alertes.length===0?'<div class="card" style="text-align:center;color:#4a6a40">✓ Aucune alerte active</div>':DATA.alertes.map((a,i)=>`
      <div class="alert-item" style="border-color:${a.type==='danger'?'#c0392b':a.type==='warning'?'#8a5a1a':'#1a3a5a'}">
        <div style="width:36px;height:36px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;background:${a.type==='danger'?'#3a1010':a.type==='warning'?'#3a2010':'#102030'}">
          ${a.type==='danger'?'🚨':a.type==='warning'?'⚠️':'ℹ️'}
        </div>
        <div style="flex:1">
          <div style="font-size:13px;color:#c8e0b8;margin-bottom:4px">${a.msg}</div>
          <div style="font-size:11px;color:#4a6a40">${a.heure}</div>
        </div>
        <button onclick="resoudreAlerte(${i})" style="padding:6px 10px;border-radius:6px;border:1px solid #2d3d2a;background:transparent;color:#7eb856;cursor:pointer;font-size:11px;flex-shrink:0;font-family:Georgia,serif">✓ Résoudre</button>
      </div>`).join('')}`;
}

// ── ACTIONS ──
function changeMort(i, delta) {
  DATA.mortalites[i].v = Math.max(0, DATA.mortalites[i].v + delta);
  saveData(); render();
}

function changePoids(i, delta) {
  DATA.productions[i].p = Math.max(0, Math.round((DATA.productions[i].p + delta) * 10) / 10);
  saveData(); render();
}

function ajouterSemaine() {
  const n = DATA.productions.length + 1;
  DATA.productions.push({s:'S'+n, p:0.0});
  saveData(); render();
}

function updateStock(key, val, input) {
  DATA.stocks[key] = parseInt(val);
  const max = {aliment:20000,eau:100,medicaments:100,vaccins:100}[key];
  input.nextElementSibling.textContent = Math.round(val/max*100)+'%';
  saveData();
  setTimeout(render, 0);
}

function resoudreAlerte(i) {
  DATA.alertes.splice(i, 1);
  saveData(); updateBadge(); render();
  showToast('✓ Alerte résolue');
}

// ── MODALS ──
function openEditBat(id) {
  const b = DATA.batiments.find(x=>x.id===id);
  document.getElementById('modal-title').textContent = 'Modifier — ' + b.nom;
  document.getElementById('modal-body').innerHTML = `
    <div class="field"><label>Nom du bâtiment</label><input id="e-nom" value="${b.nom}"></div>
    <div class="field"><label>Race</label><input id="e-race" value="${b.race}"></div>
    <div class="field"><label>Capacité (poulets)</label><input id="e-cap" type="number" value="${b.capacite}"></div>
    <div class="field"><label>Occupation actuelle (poulets)</label><input id="e-occ" type="number" value="${b.occupation}"></div>
    <div class="field"><label>Âge du lot (jours)</label><input id="e-age" type="number" value="${b.age}"></div>
    <div class="field"><label>Statut</label>
      <select id="e-statut">
        <option value="actif" ${b.statut==='actif'?'selected':''}>Actif</option>
        <option value="vide" ${b.statut==='vide'?'selected':''}>Vide</option>
        <option value="récolte" ${b.statut==='récolte'?'selected':''}>Récolte</option>
      </select>
    </div>
    <div class="btn-row">
      <button class="btn-danger" onclick="supprimerBat(${id})">🗑 Supprimer</button>
      <button class="btn-solid" onclick="sauvegarderBat(${id})">💾 Sauvegarder</button>
    </div>`;
  document.getElementById('modal').style.display = 'flex';
}

function sauvegarderBat(id) {
  const b = DATA.batiments.find(x=>x.id===id);
  b.nom = document.getElementById('e-nom').value;
  b.race = document.getElementById('e-race').value;
  b.capacite = parseInt(document.getElementById('e-cap').value)||0;
  b.occupation = parseInt(document.getElementById('e-occ').value)||0;
  b.age = parseInt(document.getElementById('e-age').value)||0;
  b.statut = document.getElementById('e-statut').value;
  saveData(); closeModal(); render();
  showToast('✓ Bâtiment mis à jour');
}

function supprimerBat(id) {
  if (!confirm('Supprimer ce bâtiment ?')) return;
  DATA.batiments = DATA.batiments.filter(x=>x.id!==id);
  saveData(); closeModal(); render();
  showToast('🗑 Bâtiment supprimé');
}

function openNouveauBat() {
  document.getElementById('modal-title').textContent = 'Nouveau bâtiment';
  document.getElementById('modal-body').innerHTML = `
    <div class="field"><label>Nom du bâtiment</label><input id="n-nom" placeholder="ex: Bâtiment E"></div>
    <div class="field"><label>Race</label><input id="n-race" placeholder="ex: Ross 308"></div>
    <div class="field"><label>Capacité (poulets)</label><input id="n-cap" type="number" placeholder="5000"></div>
    <div class="field"><label>Occupation actuelle</label><input id="n-occ" type="number" placeholder="0"></div>
    <div class="field"><label>Âge du lot (jours)</label><input id="n-age" type="number" placeholder="0"></div>
    <div class="field"><label>Statut</label>
      <select id="n-statut">
        <option value="vide">Vide</option>
        <option value="actif">Actif</option>
        <option value="récolte">Récolte</option>
      </select>
    </div>
    <div class="btn-row">
      <button class="btn-outline" onclick="closeModal()">Annuler</button>
      <button class="btn-solid" onclick="creerBat()">✓ Créer</button>
    </div>`;
  document.getElementById('modal').style.display = 'flex';
}

function creerBat() {
  const nom = document.getElementById('n-nom').value.trim();
  if (!nom) { alert('Entrez un nom'); return; }
  DATA.batiments.push({
    id: DATA.nextId++,
    nom, race: document.getElementById('n-race').value||'—',
    capacite: parseInt(document.getElementById('n-cap').value)||0,
    occupation: parseInt(document.getElementById('n-occ').value)||0,
    age: parseInt(document.getElementById('n-age').value)||0,
    statut: document.getElementById('n-statut').value
  });
  saveData(); closeModal(); render();
  showToast('✓ Bâtiment créé');
}

function openNouvelleAlerte() {
  document.getElementById('modal-title').textContent = 'Nouvelle alerte';
  document.getElementById('modal-body').innerHTML = `
    <div class="field"><label>Message</label><input id="a-msg" placeholder="Description de l'alerte..."></div>
    <div class="field"><label>Type</label>
      <select id="a-type">
        <option value="danger">🚨 Danger</option>
        <option value="warning">⚠️ Avertissement</option>
        <option value="info">ℹ️ Information</option>
      </select>
    </div>
    <div class="btn-row">
      <button class="btn-outline" onclick="closeModal()">Annuler</button>
      <button class="btn-solid" onclick="creerAlerte()">✓ Ajouter</button>
    </div>`;
  document.getElementById('modal').style.display = 'flex';
}

function creerAlerte() {
  const msg = document.getElementById('a-msg').value.trim();
  if (!msg) { alert('Entrez un message'); return; }
  const now = new Date();
  const heure = now.getHours().toString().padStart(2,'0')+':'+now.getMinutes().toString().padStart(2,'0');
  DATA.alertes.unshift({ id: DATA.nextId++, type: document.getElementById('a-type').value, msg, heure });
  saveData(); closeModal(); updateBadge(); render();
  showToast('✓ Alerte ajoutée');
}

function closeModal() { document.getElementById('modal').style.display = 'none'; }

// Init
setDate();
updateBadge();
render();
</script>
</body>
</html>
