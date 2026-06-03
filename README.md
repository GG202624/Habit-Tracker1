# Habit-Tracker1
Habit tracker 3/06/26
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="theme-color" content="#0a0a0f">
<title>Habit Tracker</title>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
html, body { background: #0a0a0f; min-height: 100vh; font-family: 'Courier New', monospace; color: #e8e0d0; }
.wrap { max-width: 500px; margin: 0 auto; padding: 24px 16px 90px; }

/* HOME */
.home-title { text-align:center; margin-bottom:32px; }
.home-title .label { font-size:10px; letter-spacing:.2em; color:#555; text-transform:uppercase; margin-bottom:8px; }
.home-title h1 { font-size:22px; font-weight:700; font-family:'Courier New',monospace; }
.home-title .date { font-size:12px; color:#444; margin-top:6px; }
.user-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; }
.user-card { background:#13131a; border:1px solid #2a2a3a; border-radius:14px; padding:20px 12px; cursor:pointer; text-align:center; transition:all .2s; -webkit-appearance:none; width:100%; }
.user-card:active { transform:scale(.97); }
.user-card .uc-emoji { font-size:26px; margin-bottom:8px; }
.user-card .uc-name { font-size:14px; font-weight:700; color:#e8e0d0; font-family:'Courier New',monospace; }
.user-card .uc-nick { font-size:10px; color:#555; margin-top:2px; letter-spacing:.05em; font-family:'Courier New',monospace; }
.user-card .uc-dots { display:flex; justify-content:center; gap:5px; margin-top:12px; }
.uc-dot { width:9px; height:9px; border-radius:50%; background:#2a2a3a; transition:background .3s; }
.user-card .uc-status { font-size:10px; color:#444; margin-top:8px; letter-spacing:.05em; font-family:'Courier New',monospace; }
.home-footer { text-align:center; margin-top:20px; font-size:11px; color:#333; line-height:1.7; }

/* NAV */
.top-bar { display:flex; align-items:center; gap:10px; margin-bottom:20px; }
.back-btn { background:none; border:1px solid #2a2a3a; color:#555; border-radius:8px; padding:7px 12px; cursor:pointer; font-family:'Courier New',monospace; font-size:11px; letter-spacing:.06em; transition:all .2s; white-space:nowrap; }
.back-btn:hover { border-color:#4a4a5a; color:#999; }
.user-label { font-size:10px; letter-spacing:.15em; color:#555; text-transform:uppercase; }

.page-header { margin-bottom:20px; }
.page-header .date-str { font-size:18px; font-weight:700; }

.tab-nav { display:flex; background:#13131a; border:1px solid #2a2a3a; border-radius:10px; padding:4px; margin-bottom:22px; }
.tab-btn { flex:1; padding:9px 4px; border:none; background:none; color:#555; font-family:'Courier New',monospace; font-size:11px; letter-spacing:.08em; text-transform:uppercase; cursor:pointer; border-radius:7px; transition:all .2s; }
.tab-btn.active { background:#1e1e2a; color:#e8e0d0; border:1px solid #3a3a4a; }

/* BADGES */
.badge-row { display:flex; gap:6px; flex-wrap:wrap; margin-bottom:16px; }
.badge { display:inline-flex; align-items:center; padding:3px 9px; border-radius:99px; border:1px solid #2a2a3a; color:#444; font-size:10px; letter-spacing:.08em; text-transform:uppercase; transition:all .3s; font-family:'Courier New',monospace; }
.badge.done { border-color:#4ade80; color:#4ade80; }

/* ALL DONE */
.all-done-banner { border-radius:12px; padding:14px 18px; text-align:center; margin-bottom:16px; animation:fadeIn .5s ease; }
.all-done-banner .ad-emoji { font-size:22px; }
.all-done-banner .ad-text { font-size:13px; margin-top:4px; letter-spacing:.05em; font-family:'Courier New',monospace; }

/* CARDS */
.card { background:#13131a; border:1px solid #2a2a3a; border-radius:12px; padding:18px; margin-bottom:12px; transition:border-color .3s; position:relative; overflow:hidden; }
.card.done { border-color:#4ade80; }
.card.done::after { content:''; position:absolute; inset:0; background:linear-gradient(135deg,rgba(74,222,128,.05) 0%,transparent 60%); pointer-events:none; }
.card.bonus-card { border-style:dashed; border-color:#252530; background:#0f0f18; }
.card-head { display:flex; justify-content:space-between; align-items:flex-start; margin-bottom:10px; }
.card-label { font-size:10px; letter-spacing:.15em; color:#555; text-transform:uppercase; margin-bottom:3px; }
.card-val { font-size:22px; font-weight:700; }
.card-sub { font-size:11px; color:#555; margin-left:4px; font-weight:400; }
.streak { display:inline-flex; align-items:center; gap:4px; background:#1e1e2a; border:1px solid #3a3a4a; border-radius:99px; padding:2px 10px; font-size:11px; color:#aaa; letter-spacing:.04em; font-family:'Courier New',monospace; }
.streak.hot { border-color:#f97316; color:#f97316; }

/* BARS */
.bar-track { background:#1e1e2a; border-radius:99px; height:7px; overflow:hidden; margin-top:10px; }
.bar-fill { height:100%; border-radius:99px; transition:width .5s cubic-bezier(.4,0,.2,1); }

/* BUTTONS */
.btn { background:#1e1e2a; border:1px solid #3a3a4a; color:#e8e0d0; border-radius:8px; padding:9px 18px; cursor:pointer; font-family:'Courier New',monospace; font-size:18px; transition:all .15s; user-select:none; line-height:1; }
.btn:active { transform:scale(.95); }
.btn-log { border-radius:8px; padding:9px 18px; cursor:pointer; font-family:'Courier New',monospace; font-size:12px; letter-spacing:.05em; transition:all .15s; border:1px solid; white-space:nowrap; }
.btn-add { border-radius:8px; padding:9px 14px; cursor:pointer; font-family:'Courier New',monospace; font-size:12px; letter-spacing:.05em; transition:all .15s; border:1px solid #9333ea; background:#1a1a28; color:#a855f7; white-space:nowrap; }
.btn-add:active { transform:scale(.95); }
.row { display:flex; align-items:center; gap:10px; margin-top:12px; }
.ctr { font-size:13px; color:#888; min-width:80px; text-align:center; font-family:'Courier New',monospace; }

/* INPUTS */
input[type=number], input[type=text] { background:#1e1e2a; border:1px solid #3a3a4a; color:#e8e0d0; border-radius:8px; padding:9px 10px; font-family:'Courier New',monospace; font-size:13px; outline:none; transition:border-color .2s; -webkit-appearance:none; }
input[type=number] { width:88px; }
input[type=text] { flex:1; width:100%; }
input[type=number]:focus, input[type=text]:focus { border-color:#9333ea; }
input::placeholder { color:#444; }
input[type=number]::-webkit-inner-spin-button { opacity:.4; }

/* GLASSES */
.glasses-row { display:flex; gap:6px; flex-wrap:wrap; margin-bottom:10px; }
.glass { width:24px; height:30px; border:2px solid #3a3a4a; border-top:none; border-radius:0 0 5px 5px; position:relative; overflow:hidden; background:#1a1a22; }
.glass.filled { border-color:#38bdf8; }
.glass-liq { position:absolute; bottom:0; left:0; right:0; background:#38bdf8; opacity:.7; transition:height .3s ease; height:0; }
.glass.filled .glass-liq { height:75%; }

/* MEALS */
.meals-row { display:flex; gap:8px; margin-bottom:10px; }
.meal-dot { width:28px; height:28px; border-radius:50%; border:2px solid #3a3a4a; display:flex; align-items:center; justify-content:center; font-size:14px; transition:all .25s; }
.meal-dot.filled { border-color:#fbbf24; background:#1a1a0a; }

/* TEETH */
.teeth-row { display:flex; gap:10px; margin-top:4px; }
.teeth-btn { flex:1; padding:12px 6px; border-radius:10px; background:#1a1a22; color:#666; cursor:pointer; font-family:'Courier New',monospace; font-size:11px; letter-spacing:.05em; transition:all .2s; display:flex; flex-direction:column; align-items:center; gap:4px; border:1px solid #2a2a3a; }
.teeth-btn.checked { border-color:#4ade80; background:#0a1f0a; color:#4ade80; }
.teeth-emoji { font-size:20px; }

/* BONUS */
.bonus-entry { display:flex; align-items:flex-start; justify-content:space-between; gap:8px; background:#16161f; border:1px solid #2a2a3a; border-radius:8px; padding:9px 11px; margin-bottom:7px; }
.bonus-text { font-size:12px; color:#c8c0b0; line-height:1.5; }
.bonus-time { font-size:10px; color:#444; margin-top:2px; }
.bonus-del { background:none; border:none; color:#383848; cursor:pointer; font-size:18px; padding:0 2px; flex-shrink:0; transition:color .15s; line-height:1; }
.bonus-del:hover { color:#ef4444; }
.bonus-input-row { display:flex; gap:8px; }

/* STATS */
.range-row { display:flex; gap:8px; margin-bottom:18px; }
.range-btn { padding:5px 13px; border:1px solid #2a2a3a; background:none; color:#555; font-family:'Courier New',monospace; font-size:11px; border-radius:6px; cursor:pointer; transition:all .2s; }
.range-btn.active { }
.stat-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:16px; }
.stat-card { background:#13131a; border:1px solid #2a2a3a; border-radius:10px; padding:14px; }
.stat-num { font-size:26px; font-weight:700; font-family:'Courier New',monospace; }
.stat-lbl { font-size:10px; color:#555; letter-spacing:.1em; text-transform:uppercase; margin-top:3px; font-family:'Courier New',monospace; }
.stat-sub { font-size:10px; color:#444; margin-top:2px; font-family:'Courier New',monospace; }
.chart-card { background:#13131a; border:1px solid #2a2a3a; border-radius:12px; padding:18px; margin-bottom:12px; }
.chart-title { font-size:10px; letter-spacing:.15em; color:#555; text-transform:uppercase; margin-bottom:14px; font-family:'Courier New',monospace; }
.rate-row { margin-bottom:12px; }
.rate-label { display:flex; justify-content:space-between; margin-bottom:4px; font-size:11px; font-family:'Courier New',monospace; }
.rate-name { color:#aaa; }
canvas { display:block; }
.chart-footer { display:flex; justify-content:space-between; font-size:10px; color:#555; margin-top:10px; border-top:1px dashed #1e1e2a; padding-top:10px; font-family:'Courier New',monospace; }
.legend-row { display:flex; gap:12px; justify-content:center; margin-top:10px; }
.legend-item { display:flex; align-items:center; gap:5px; font-size:10px; color:#666; font-family:'Courier New',monospace; }
.legend-dot { width:9px; height:9px; border-radius:2px; display:inline-block; flex-shrink:0; }

/* HEATMAP */
.heatmap-habit { margin-bottom:12px; }
.heatmap-label { font-size:10px; color:#555; letter-spacing:.1em; text-transform:uppercase; margin-bottom:4px; font-family:'Courier New',monospace; }
.heatmap-grid { display:grid; grid-template-columns:repeat(28,1fr); gap:3px; }
.hm-cell { height:13px; border-radius:2px; background:#1e1e2a; opacity:.4; transition:background .3s; }
.hm-cell.filled { opacity:.9; }
.hm-cell.today-cell { box-shadow:0 0 0 1px rgba(255,255,255,.2); }
.heatmap-note { font-size:10px; color:#444; margin-top:6px; text-align:right; font-family:'Courier New',monospace; }

/* JOURNAL */
.journal-day { background:#13131a; border:1px solid #2a2a3a; border-radius:10px; padding:13px 15px; margin-bottom:10px; }
.journal-date { font-size:10px; color:#555; letter-spacing:.1em; text-transform:uppercase; margin-bottom:8px; font-family:'Courier New',monospace; }
.journal-item { font-size:12px; color:#c8c0b0; padding:5px 0; border-bottom:1px solid #1e1e2a; display:flex; justify-content:space-between; font-family:'Courier New',monospace; }
.journal-item:last-child { border-bottom:none; }
.journal-time { font-size:10px; color:#444; }
.journal-empty { text-align:center; padding:40px 20px; color:#333; font-size:13px; font-family:'Courier New',monospace; }
.journal-empty .je-emoji { font-size:28px; margin-bottom:12px; }
.future-card { background:#13131a; border:1px dashed #252530; border-radius:12px; padding:15px 17px; margin-top:24px; }
.future-label { font-size:10px; color:#6b5ea8; letter-spacing:.12em; text-transform:uppercase; margin-bottom:10px; font-family:'Courier New',monospace; }
.future-desc { font-size:12px; color:#444; line-height:1.8; margin-bottom:12px; font-family:'Courier New',monospace; }
.future-item { display:flex; align-items:center; gap:10px; font-size:12px; color:#333; margin-bottom:8px; font-family:'Courier New',monospace; }
.future-box { width:18px; height:18px; border-radius:4px; border:1px dashed #2a2a3a; flex-shrink:0; }

.footer { margin-top:24px; font-size:11px; color:#333; text-align:center; letter-spacing:.05em; font-family:'Courier New',monospace; }
.hidden { display:none !important; }

@keyframes fadeIn { from{opacity:0;transform:translateY(-6px)} to{opacity:1;transform:translateY(0)} }
@keyframes pop { 0%{transform:scale(1)} 40%{transform:scale(1.04)} 100%{transform:scale(1)} }
.pop { animation:pop .5s cubic-bezier(.4,0,.2,1); }
</style>
</head>
<body>

<div class="wrap" id="app"></div>

<script>
const KEY = 'habit-tracker-v4';
const USERS = [
  { id:'giulio', name:'Giulio', nickname:null,    accent:'#818cf8', accentDim:'#2d2b4e', emoji:'👤' },
  { id:'puntu',  name:'Ashma',  nickname:'Puntu', accent:'#f472b6', accentDim:'#3d1f2f', emoji:'🌸' },
];
const HABITS = [
  { key:'sleep', label:'Sleep', color:'#818cf8', check: e => e?.sleep?.logged && e.sleep.hours >= 8 },
  { key:'water', label:'Water', color:'#38bdf8', check: e => (e?.water?.glasses||0) >= 7 },
  { key:'meals', label:'Meals', color:'#fbbf24', check: e => (e?.meals?.count||0)   >= 2 },
  { key:'teeth', label:'Teeth', color:'#4ade80', check: e => !!(e?.teeth?.morning && e?.teeth?.night) },
];
const MEAL_EMOJIS = ['🍳','🥗','🍽️','🌙'];

function todayKey() { return new Date().toISOString().split('T')[0]; }
function defaultDay() { return { sleep:{logged:false,hours:0}, water:{glasses:0}, meals:{count:0}, teeth:{morning:false,night:false}, bonus:[] }; }
function getPastDays(n) {
  const out=[];
  for(let i=n-1;i>=0;i--){ const d=new Date(); d.setDate(d.getDate()-i); out.push(d.toISOString().split('T')[0]); }
  return out;
}
function fmtDate(iso) { return new Date(iso+'T00:00:00').toLocaleDateString('en-AU',{weekday:'long',day:'numeric',month:'long'}); }
function fmtShort(iso) { return new Date(iso+'T00:00:00').toLocaleDateString('en-AU',{day:'numeric',month:'short'}); }

// ── Storage ──────────────────────────────────────────────────────────────────
let allData = {};
try { allData = JSON.parse(localStorage.getItem(KEY)||'{}'); } catch(e) {}
function save() { try { localStorage.setItem(KEY, JSON.stringify(allData)); } catch(e) {} }
function getUserData(uid) { return allData[uid] || {}; }
function getTd(uid) { return getUserData(uid)[todayKey()] || defaultDay(); }
function setTd(uid, td) {
  if (!allData[uid]) allData[uid] = {};
  allData[uid][todayKey()] = td;
  save();
}

// ── State ────────────────────────────────────────────────────────────────────
let activeUser = null;
let activePage = 'today';
let activeRange = 'week';

// ── Render ───────────────────────────────────────────────────────────────────
function render() {
  const app = document.getElementById('app');
  if (!activeUser) { app.innerHTML = renderHome(); bindHome(); }
  else             { app.innerHTML = renderUser(); bindUser(); }
}

// ── HOME ─────────────────────────────────────────────────────────────────────
function renderHome() {
  const today = todayKey();
  const dateStr = new Date().toLocaleDateString('en-AU',{weekday:'long',day:'numeric',month:'long'});
  const cards = USERS.map(u => {
    const td = getTd(u.id);
    const done = HABITS.filter(h=>h.check(td)).length;
    const full = done===4;
    const dots = HABITS.map(h=>`<div class="uc-dot" style="background:${h.check(td)?h.color:'#2a2a3a'}"></div>`).join('');
    return `
      <button class="user-card" data-uid="${u.id}"
        style="border-color:${full?u.accent:'#2a2a3a'};background:${full?u.accentDim:'#13131a'}">
        <div class="uc-emoji">${u.emoji}</div>
        <div class="uc-name" style="color:${full?u.accent:'#e8e0d0'}">${u.nickname||u.name}</div>
        ${u.nickname?`<div class="uc-nick">${u.name}</div>`:''}
        <div class="uc-dots">${dots}</div>
        <div class="uc-status" style="color:${full?u.accent:'#444'}">${full?'All done today ✓':`${done}/4 habits`}</div>
      </button>`;
  }).join('');
  return `
    <div class="home-title">
      <div class="label">Habit Tracker</div>
      <h1>Who's checking in?</h1>
      <div class="date">${dateStr}</div>
    </div>
    <div class="user-grid">${cards}</div>
    <div class="home-footer">Each profile is separate.<br>Data saved on this device.</div>`;
}
function bindHome() {
  document.querySelectorAll('.user-card').forEach(btn => {
    btn.addEventListener('click', () => { activeUser=btn.dataset.uid; activePage='today'; render(); });
  });
}

// ── USER TRACKER ─────────────────────────────────────────────────────────────
function renderUser() {
  const u = USERS.find(u=>u.id===activeUser);
  const dateStr = new Date().toLocaleDateString('en-AU',{weekday:'long',day:'numeric',month:'long'});
  const tabs = ['today','stats','journal'].map(t=>`
    <button class="tab-btn${activePage===t?' active':''}" data-tab="${t}">${t.charAt(0).toUpperCase()+t.slice(1)}</button>`).join('');
  let pageHtml = '';
  if (activePage==='today')   pageHtml = renderToday(u);
  if (activePage==='stats')   pageHtml = renderStats(u);
  if (activePage==='journal') pageHtml = renderJournal(u);
  return `
    <div class="top-bar">
      <button class="back-btn" id="back-btn">← Switch</button>
      <div>
        <div class="user-label">${u.emoji} ${u.id==='puntu'?"Puntu's":"Giulio's"} Habits</div>
      </div>
    </div>
    <div class="page-header"><div class="date-str">${dateStr}</div></div>
    <div class="tab-nav">${tabs}</div>
    ${pageHtml}`;
}

function renderToday(u) {
  const td = getTd(u.id);
  const sleepDone = td.sleep.logged && td.sleep.hours>=8;
  const waterDone = td.water.glasses>=7;
  const mealsDone = td.meals.count>=2;
  const teethDone = !!(td.teeth?.morning && td.teeth?.night);
  const allDone   = sleepDone && waterDone && mealsDone && teethDone;

  const badges = [['sleep',sleepDone],['water',waterDone],['meals',mealsDone],['teeth',teethDone]]
    .map(([l,d])=>`<span class="badge${d?' done':''}">${d?'✓ ':''}${l}</span>`).join('');

  const allDoneBanner = allDone ? `
    <div class="all-done-banner" style="background:linear-gradient(135deg,${u.accentDim},transparent);border:1px solid ${u.accent}">
      <div class="ad-emoji">${u.id==='puntu'?'🌸':'🌿'}</div>
      <div class="ad-text" style="color:${u.accent}">All habits done today. ${u.id==='puntu'?'Well done Puntu!':'Well done Giulio!'}</div>
    </div>` : '';

  // sleep
  const sleepPct = Math.min((td.sleep.hours/8)*100,100);
  const sleepStreak = calcStreak(u.id, e=>e.sleep?.logged && e.sleep.hours>=8);
  const sleepCard = `
    <div class="card${sleepDone?' done':''}" id="card-sleep">
      <div class="card-head">
        <div>
          <div class="card-label">Sleep</div>
          <div class="card-val">${td.sleep.logged?td.sleep.hours+'h':'—'}<span class="card-sub">/ 8h goal</span></div>
        </div>
        ${streakBadge(sleepStreak)}
      </div>
      <div class="bar-track"><div class="bar-fill" id="bar-sleep" style="width:${sleepPct}%;background:${sleepDone?'#4ade80':`linear-gradient(90deg,${u.accent},${u.accent}aa)`}"></div></div>
      <div class="row">
        <input type="number" id="sleep-input" min="0" max="24" step="0.5" placeholder="hours" value="">
        <button class="btn-log" id="sleep-log" style="background:${u.accentDim};border-color:${u.accent};color:${u.accent}">Log</button>
      </div>
    </div>`;

  // water
  const waterPct = Math.min((td.water.glasses/7)*100,100);
  const waterStreak = calcStreak(u.id, e=>(e.water?.glasses||0)>=7);
  const glasses = Array.from({length:7},(_,i)=>`<div class="glass${i<td.water.glasses?' filled':''}"><div class="glass-liq"></div></div>`).join('');
  const waterCard = `
    <div class="card${waterDone?' done':''}" id="card-water">
      <div class="card-head">
        <div>
          <div class="card-label">Water</div>
          <div class="card-val">${(td.water.glasses*0.2).toFixed(1)}L<span class="card-sub">/ 1.4L goal</span></div>
        </div>
        ${streakBadge(waterStreak)}
      </div>
      <div class="glasses-row">${glasses}</div>
      <div class="bar-track"><div class="bar-fill" style="width:${waterPct}%;background:${waterDone?'#4ade80':'linear-gradient(90deg,#0ea5e9,#38bdf8)'}"></div></div>
      <div class="row">
        <button class="btn" id="water-rem">−</button>
        <span class="ctr">${td.water.glasses} / 7 glasses</span>
        <button class="btn" id="water-add">+</button>
      </div>
    </div>`;

  // meals
  const mealsPct = Math.min((td.meals.count/2)*100,100);
  const mealsStreak = calcStreak(u.id, e=>(e.meals?.count||0)>=2);
  const dots = MEAL_EMOJIS.map((e,i)=>`<div class="meal-dot${i<td.meals.count?' filled':''}">${i<td.meals.count?e:''}</div>`).join('');
  const mealsCard = `
    <div class="card${mealsDone?' done':''}" id="card-meals">
      <div class="card-head">
        <div>
          <div class="card-label">Meals</div>
          <div class="card-val">${td.meals.count}<span class="card-sub">/ 2 goal</span></div>
        </div>
        ${streakBadge(mealsStreak)}
      </div>
      <div class="meals-row">${dots}</div>
      <div class="bar-track"><div class="bar-fill" style="width:${mealsPct}%;background:${mealsDone?'#4ade80':'linear-gradient(90deg,#f59e0b,#fbbf24)'}"></div></div>
      <div class="row">
        <button class="btn" id="meals-rem">−</button>
        <span class="ctr">${td.meals.count} meal${td.meals.count!==1?'s':''}</span>
        <button class="btn" id="meals-add">+</button>
      </div>
    </div>`;

  // teeth
  const teethStreak = calcStreak(u.id, e=>!!(e.teeth?.morning && e.teeth?.night));
  const teethCard = `
    <div class="card${teethDone?' done':''}" id="card-teeth">
      <div class="card-head">
        <div>
          <div class="card-label">Teeth Brushing</div>
          <div class="card-val">${[td.teeth?.morning,td.teeth?.night].filter(Boolean).length}<span class="card-sub">/ 2 times</span></div>
        </div>
        ${streakBadge(teethStreak)}
      </div>
      <div class="teeth-row">
        <button class="teeth-btn${td.teeth?.morning?' checked':''}" data-slot="morning">
          <span class="teeth-emoji">🌅</span><span>${td.teeth?.morning?'✓ ':''}Morning</span>
        </button>
        <button class="teeth-btn${td.teeth?.night?' checked':''}" data-slot="night">
          <span class="teeth-emoji">🌙</span><span>${td.teeth?.night?'✓ ':''}Night</span>
        </button>
      </div>
    </div>`;

  // bonus
  const bonusEntries = (td.bonus||[]).map((e,i)=>`
    <div class="bonus-entry">
      <div><div class="bonus-text">${escHtml(e.text)}</div><div class="bonus-time">${e.time}</div></div>
      <button class="bonus-del" data-idx="${i}">×</button>
    </div>`).join('');
  const bonusCard = `
    <div class="card bonus-card">
      <div class="card-label" style="color:#6b5ea8;margin-bottom:5px">⭐ Bonus habit</div>
      <div style="font-size:11px;color:#3a3a50;margin-bottom:12px;line-height:1.7">Not tracked. No pressure. Note something good you did today.</div>
      <div id="bonus-list">${bonusEntries}</div>
      <div class="bonus-input-row">
        <input type="text" id="bonus-input" placeholder="e.g. went to the gym...">
        <button class="btn-add" id="bonus-add">Add</button>
      </div>
    </div>`;

  return `
    <div class="badge-row">${badges}</div>
    ${allDoneBanner}
    ${sleepCard}${waterCard}${mealsCard}${teethCard}${bonusCard}
    <div class="footer">Data saved on this device · Core habits reset each day</div>`;
}

function renderStats(u) {
  const n = activeRange==='week'?7:30;
  const days = getPastDays(n);
  const uData = getUserData(u.id);
  const today = todayKey();

  const daysAllDone = days.filter(k=>HABITS.every(h=>h.check(uData[k]))).length;
  const sleepLogged = days.filter(k=>uData[k]?.sleep?.logged);
  const avgSleep = sleepLogged.length ? (sleepLogged.reduce((a,k)=>a+(uData[k].sleep.hours||0),0)/sleepLogged.length).toFixed(1) : '—';
  const waterDays = days.filter(k=>uData[k]);
  const avgWater = waterDays.length ? ((waterDays.reduce((a,k)=>a+(uData[k].water?.glasses||0),0)/waterDays.length)*0.2).toFixed(1) : '0.0';
  const streaks = HABITS.map(h=>calcStreak(u.id,e=>h.check(e)));
  const bestStreak = Math.max(0,...streaks);

  const habitRates = HABITS.map(h=>({
    ...h, rate:Math.round((days.filter(k=>h.check(uData[k])).length/days.length)*100)
  }));

  const rangeBtns = ['week','month'].map(r=>`
    <button class="range-btn${activeRange===r?' active':''}" data-range="${r}"
      style="${activeRange===r?`border-color:${u.accent};color:${u.accent};background:${u.accentDim}`:''}">
      ${r==='week'?'7 Days':'30 Days'}
    </button>`).join('');

  const rates = habitRates.map(h=>`
    <div class="rate-row">
      <div class="rate-label"><span class="rate-name">${h.label}</span><span style="color:${h.color};font-weight:700">${h.rate}%</span></div>
      <div class="bar-track" style="margin-top:0"><div class="bar-fill" style="width:${h.rate}%;background:${h.color}"></div></div>
    </div>`).join('');

  const heatmapDays = getPastDays(28);
  const heatmap = HABITS.map(h=>{
    const cells = heatmapDays.map(k=>`
      <div class="hm-cell${h.check(uData[k])?' filled':''}${k===today?' today-cell':''}"
        style="${h.check(uData[k])?`background:${h.color}`:''}" title="${k}"></div>`).join('');
    return `<div class="heatmap-habit"><div class="heatmap-label">${h.label}</div><div class="heatmap-grid">${cells}</div></div>`;
  }).join('');

  return `
    <div class="range-row">${rangeBtns}</div>
    <div class="stat-grid">
      <div class="stat-card"><div class="stat-num" style="color:${u.accent}">${daysAllDone}</div><div class="stat-lbl">Perfect days</div><div class="stat-sub">out of ${days.length}</div></div>
      <div class="stat-card"><div class="stat-num" style="color:#818cf8">${avgSleep}h</div><div class="stat-lbl">Avg sleep</div><div class="stat-sub">goal: 8h</div></div>
      <div class="stat-card"><div class="stat-num" style="color:#38bdf8">${avgWater}L</div><div class="stat-lbl">Avg water</div><div class="stat-sub">goal: 1.4L</div></div>
      <div class="stat-card"><div class="stat-num" style="color:#fbbf24">${bestStreak}d</div><div class="stat-lbl">Best streak</div><div class="stat-sub">any habit</div></div>
    </div>
    <div class="chart-card"><div class="chart-title">Habit completion rate</div>${rates}</div>
    <div class="chart-card">
      <div class="chart-title">Habits completed per day</div>
      <canvas id="bar-chart" height="140"></canvas>
      <div class="legend-row">
        <div class="legend-item"><span class="legend-dot" style="background:#4ade80"></span>All 4</div>
        <div class="legend-item"><span class="legend-dot" style="background:#fbbf24"></span>2–3</div>
        <div class="legend-item"><span class="legend-dot" style="background:#ef4444"></span>0–1</div>
      </div>
    </div>
    <div class="chart-card">
      <div class="chart-title">Sleep hours</div>
      <canvas id="sleep-chart" height="130"></canvas>
      <div class="chart-footer">
        <span>Goal: 8h/night</span>
        <span style="color:${parseFloat(avgSleep)>=8?'#4ade80':'#f97316'}">Avg: ${avgSleep}h</span>
      </div>
    </div>
    <div class="chart-card">
      <div class="chart-title">Water intake (L)</div>
      <canvas id="water-chart" height="130"></canvas>
      <div class="chart-footer">
        <span>Goal: 1.4L/day</span>
        <span style="color:${parseFloat(avgWater)>=1.4?'#4ade80':'#f97316'}">Avg: ${avgWater}L</span>
      </div>
    </div>
    <div class="chart-card">
      <div class="chart-title">28-day habit heatmap</div>
      ${heatmap}
      <div class="heatmap-note">Last 28 days · today outlined</div>
    </div>
    <div class="footer">Data stored on this device only</div>`;
}

function renderJournal(u) {
  const uData = getUserData(u.id);
  const today = todayKey();
  const ac = USERS.find(x=>x.id===u.id).accent;
  const journalDays = Object.keys(uData)
    .filter(k=>uData[k]?.bonus?.length>0)
    .sort((a,b)=>b.localeCompare(a)).slice(0,14);

  let content = '';
  if (journalDays.length===0) {
    content = `<div class="journal-empty"><div class="je-emoji">📓</div>No bonus entries yet.<br>Add one from the Today tab.</div>`;
  } else {
    content = journalDays.map(k=>{
      const entries = uData[k].bonus||[];
      const isToday = k===today;
      const items = entries.map(e=>`
        <div class="journal-item"><span>⭐ ${escHtml(e.text)}</span><span class="journal-time">${e.time}</span></div>`).join('');
      return `
        <div class="journal-day">
          <div class="journal-date" style="color:${isToday?ac:'#555'}">${isToday?'Today — ':''}${fmtDate(k)}</div>
          ${items}
        </div>`;
    }).join('');
  }

  const futureItems = ['Gym / movement','Business work','Reading','Meditation']
    .map(h=>`<div class="future-item"><div class="future-box"></div>${h}</div>`).join('');

  return `
    <div style="font-size:12px;color:#555;line-height:1.7;margin-bottom:18px">Bonus habits log — the extras that aren't tracked, just remembered.</div>
    ${content}
    <div class="future-card">
      <div class="future-label">One month from now</div>
      <div class="future-desc">Once the current 4 feel automatic — no effort, no thinking — add the next one. One at a time.</div>
      ${futureItems}
    </div>
    <div class="footer">Showing last 14 days with entries</div>`;
}

// ── Bind user interactions ───────────────────────────────────────────────────
function bindUser() {
  const u = USERS.find(u=>u.id===activeUser);

  document.getElementById('back-btn').addEventListener('click', ()=>{ activeUser=null; render(); });
  document.querySelectorAll('.tab-btn').forEach(btn=>
    btn.addEventListener('click', ()=>{ activePage=btn.dataset.tab; render(); }));

  if (activePage==='today') {
    // sleep
    const sleepLog = () => {
      const val = parseFloat(document.getElementById('sleep-input').value);
      if (isNaN(val)||val<=0||val>24) return;
      const td = getTd(activeUser);
      td.sleep = { logged:true, hours:val };
      setTd(activeUser, td);
      render();
    };
    document.getElementById('sleep-log').addEventListener('click', sleepLog);
    document.getElementById('sleep-input').addEventListener('keydown', e=>{ if(e.key==='Enter') sleepLog(); });

    // water
    document.getElementById('water-add').addEventListener('click', ()=>{
      const td=getTd(activeUser); if(td.water.glasses>=7) return;
      td.water.glasses++; setTd(activeUser,td); render();
    });
    document.getElementById('water-rem').addEventListener('click', ()=>{
      const td=getTd(activeUser); if(td.water.glasses<=0) return;
      td.water.glasses--; setTd(activeUser,td); render();
    });

    // meals
    document.getElementById('meals-add').addEventListener('click', ()=>{
      const td=getTd(activeUser); if(td.meals.count>=4) return;
      td.meals.count++; setTd(activeUser,td); render();
    });
    document.getElementById('meals-rem').addEventListener('click', ()=>{
      const td=getTd(activeUser); if(td.meals.count<=0) return;
      td.meals.count--; setTd(activeUser,td); render();
    });

    // teeth
    document.querySelectorAll('.teeth-btn').forEach(btn=>
      btn.addEventListener('click', ()=>{
        const slot=btn.dataset.slot;
        const td=getTd(activeUser);
        if(!td.teeth) td.teeth={morning:false,night:false};
        td.teeth[slot]=!td.teeth[slot];
        setTd(activeUser,td); render();
      }));

    // bonus
    const addBonus = () => {
      const inp=document.getElementById('bonus-input');
      const text=inp.value.trim(); if(!text) return;
      const time=new Date().toLocaleTimeString('en-AU',{hour:'2-digit',minute:'2-digit'});
      const td=getTd(activeUser);
      if(!td.bonus) td.bonus=[];
      td.bonus.push({text,time});
      setTd(activeUser,td); render();
    };
    document.getElementById('bonus-add').addEventListener('click', addBonus);
    document.getElementById('bonus-input').addEventListener('keydown', e=>{ if(e.key==='Enter') addBonus(); });
    document.querySelectorAll('.bonus-del').forEach(btn=>
      btn.addEventListener('click', ()=>{
        const i=parseInt(btn.dataset.idx);
        const td=getTd(activeUser);
        td.bonus.splice(i,1);
        setTd(activeUser,td); render();
      }));
  }

  if (activePage==='stats') {
    document.querySelectorAll('.range-btn').forEach(btn=>
      btn.addEventListener('click', ()=>{ activeRange=btn.dataset.range; render(); }));
    drawCharts(u);
  }
}

// ── Charts (vanilla canvas) ──────────────────────────────────────────────────
function drawCharts(u) {
  const n = activeRange==='week'?7:30;
  const days = getPastDays(n);
  const uData = getUserData(u.id);

  // bar chart — habits per day
  const bc = document.getElementById('bar-chart');
  if (bc) {
    const dpr = window.devicePixelRatio||1;
    bc.width  = bc.offsetWidth * dpr;
    bc.height = 140 * dpr;
    const ctx = bc.getContext('2d');
    ctx.scale(dpr,dpr);
    const W=bc.offsetWidth, H=140, pad=28, bpad=20;
    const barW = (W-pad*2)/days.length;
    ctx.clearRect(0,0,W,H);
    days.forEach((k,i)=>{
      const done=HABITS.filter(h=>h.check(uData[k])).length;
      const col = done===4?'#4ade80':done>=2?'#fbbf24':'#ef4444';
      const barH = done===0?2:((done/4)*(H-bpad-10));
      const x=pad+i*barW+barW*.15, w=barW*.7, y=H-bpad-barH;
      ctx.fillStyle=col; ctx.beginPath();
      roundRect(ctx,x,y,w,barH,3); ctx.fill();
      if (days.length<=10||(i%(Math.ceil(days.length/7))===0)) {
        ctx.fillStyle='#555'; ctx.font=`9px 'Courier New'`; ctx.textAlign='center';
        ctx.fillText(fmtShort(k).split(' ')[0],x+w/2,H-6);
      }
    });
  }

  // sleep line
  drawLine('sleep-chart', days, uData,
    k=>uData[k]?.sleep?.logged?uData[k].sleep.hours:null, u.accent, 0, 12, 8);

  // water line
  drawLine('water-chart', days, uData,
    k=>(uData[k]?.water?.glasses||0)*0.2, '#38bdf8', 0, 2, 1.4);
}

function drawLine(id, days, uData, valFn, color, min, max, goalLine) {
  const el = document.getElementById(id);
  if (!el) return;
  const dpr = window.devicePixelRatio||1;
  el.width  = el.offsetWidth * dpr;
  el.height = 130 * dpr;
  const ctx = el.getContext('2d');
  ctx.scale(dpr,dpr);
  const W=el.offsetWidth, H=130, padL=28, padB=18, padT=8;
  const plotW=W-padL, plotH=H-padB-padT;
  ctx.clearRect(0,0,W,H);

  // goal line
  const gy = padT + plotH - ((goalLine-min)/(max-min))*plotH;
  ctx.strokeStyle='#2a2a3a'; ctx.lineWidth=1; ctx.setLineDash([4,4]);
  ctx.beginPath(); ctx.moveTo(padL,gy); ctx.lineTo(W,gy); ctx.stroke();
  ctx.setLineDash([]);

  // y axis labels
  ctx.fillStyle='#555'; ctx.font=`9px 'Courier New'`; ctx.textAlign='right';
  [min, (max-min)/2+min, max].forEach(v=>{
    const y=padT+plotH-((v-min)/(max-min))*plotH;
    ctx.fillText(v%1===0?v:v.toFixed(1),padL-3,y+3);
  });

  // line
  const pts=[];
  days.forEach((k,i)=>{
    const v=valFn(k);
    if(v===null||v===undefined) return;
    const x=padL+(i/(days.length-1||1))*plotW;
    const y=padT+plotH-((v-min)/(max-min))*plotH;
    pts.push([x,y]);
  });

  if(pts.length>1){
    ctx.strokeStyle=color; ctx.lineWidth=2; ctx.lineJoin='round';
    ctx.beginPath(); ctx.moveTo(pts[0][0],pts[0][1]);
    pts.slice(1).forEach(p=>ctx.lineTo(p[0],p[1]));
    ctx.stroke();
  }
  pts.forEach(([x,y])=>{
    ctx.fillStyle=color; ctx.beginPath(); ctx.arc(x,y,3,0,Math.PI*2); ctx.fill();
  });

  // x labels
  ctx.fillStyle='#555'; ctx.font=`9px 'Courier New'`; ctx.textAlign='center';
  days.forEach((k,i)=>{
    if(days.length<=10||(i%(Math.ceil(days.length/7))===0)){
      const x=padL+(i/(days.length-1||1))*plotW;
      ctx.fillText(fmtShort(k).split(' ')[0],x,H-4);
    }
  });
}

function roundRect(ctx,x,y,w,h,r){
  if(h<=0){h=1;} if(r>h/2) r=h/2;
  ctx.moveTo(x+r,y); ctx.lineTo(x+w-r,y);
  ctx.arcTo(x+w,y,x+w,y+r,r); ctx.lineTo(x+w,y+h-r);
  ctx.arcTo(x+w,y+h,x+w-r,y+h,r); ctx.lineTo(x+r,y+h);
  ctx.arcTo(x,y+h,x,y+h-r,r); ctx.lineTo(x,y+r);
  ctx.arcTo(x,y,x+r,y,r); ctx.closePath();
}

// ── Helpers ──────────────────────────────────────────────────────────────────
function calcStreak(uid, check) {
  const uData = getUserData(uid);
  let s=0; const d=new Date();
  while(true){
    const k=d.toISOString().split('T')[0];
    if(!uData[k]||!check(uData[k])) break;
    s++; d.setDate(d.getDate()-1);
  }
  return s;
}
function streakBadge(s) {
  return `<span class="streak${s>=3?' hot':''}">${s>=3?'🔥':'○'} ${s}d</span>`;
}
function escHtml(str) {
  return str.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

// ── Init ─────────────────────────────────────────────────────────────────────
render();
</script>
</body>
</html>
