# Gym-Log
Gym Log
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="Gym Log">
<meta name="theme-color" content="#f0f2f5">
<title>Gym Log</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --safe-top: env(safe-area-inset-top, 44px);
    --safe-bottom: env(safe-area-inset-bottom, 34px);
    --bg:       #f0f2f5;
    --bg2:      #ffffff;
    --bg3:      #e8eaee;
    --border:   #dde0e6;
    --text:     #1a1d23;
    --muted:    #8a8f9a;
    --faint:    #eef0f4;
    --input-bg: #f7f8fa;
    --accent:   #4a90d9;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
  html, body { height: 100%; background: var(--bg); overflow: hidden; }
  body { font-family: 'DM Mono', monospace; color: var(--text); }
  #app { display: flex; flex-direction: column; height: 100vh; height: -webkit-fill-available; }

/* Header */
#header {
padding: calc(var(–safe-top) + 8px) 18px 0;
background: var(–bg2); border-bottom: 1px solid var(–border);
flex-shrink: 0; box-shadow: 0 1px 8px rgba(0,0,0,0.06);
}
.header-row { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 12px; }
.app-title { font-family: ‘Bebas Neue’, sans-serif; font-size: 30px; letter-spacing: 3px; line-height: 1; }
.app-sub { font-size: 9px; color: var(–muted); letter-spacing: 2px; margin-top: 2px; }
.date-input {
background: var(–faint); border: 1px solid var(–border); border-radius: 8px;
color: var(–text); padding: 6px 10px; font-size: 11px; font-family: inherit;
-webkit-appearance: none; outline: none;
}
.date-label { font-size: 9px; color: var(–muted); letter-spacing: 1px; margin-top: 3px; text-align: right; }
.nav-tabs { display: flex; }
.nav-tab {
padding: 8px 14px; font-size: 10px; letter-spacing: 2px; text-transform: uppercase;
color: var(–muted); border-bottom: 2px solid transparent; cursor: pointer;
transition: color 0.2s; user-select: none;
}
.nav-tab.active { color: var(–accent); border-bottom-color: var(–accent); font-weight: 500; }

/* Scroll */
#scroll { flex: 1; overflow-y: auto; -webkit-overflow-scrolling: touch; padding: 0 16px calc(var(–safe-bottom) + 90px); }

/* Muscle grid */
.muscle-grid { display: grid; grid-template-columns: 1fr 1fr 1fr 1fr; gap: 8px; margin-top: 16px; }
.muscle-btn {
background: var(–bg2); border-radius: 10px; padding: 10px 4px;
display: flex; flex-direction: column; align-items: center; gap: 4px;
font-family: inherit; font-size: 9px; letter-spacing: 1.5px; text-transform: uppercase;
cursor: pointer; transition: all 0.2s; border: 1.5px solid var(–border);
color: var(–muted); -webkit-appearance: none; box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}
.muscle-btn .icon { font-size: 22px; }

/* Week toggle */
.week-row { display: flex; gap: 8px; margin-top: 10px; }
.week-btn {
flex: 1; padding: 10px 8px; border-radius: 8px; font-family: inherit;
font-size: 9px; letter-spacing: 2px; text-transform: uppercase; cursor: pointer;
background: var(–bg2); border: 1.5px solid var(–border); color: var(–muted);
transition: all 0.2s; -webkit-appearance: none; line-height: 1.4;
box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}

/* Progress */
.progress-header { display: flex; justify-content: space-between; font-size: 9px; letter-spacing: 1px; color: var(–muted); margin: 14px 0 5px; }
.progress-bar { height: 4px; background: var(–faint); border-radius: 2px; overflow: hidden; }
.progress-fill { height: 100%; border-radius: 2px; transition: width 0.4s ease; }

/* Exercise cards */
.ex-card {
background: var(–bg2); border: 1.5px solid var(–border); border-radius: 12px;
overflow: hidden; margin-top: 12px; transition: border-color 0.3s, box-shadow 0.3s;
box-shadow: 0 1px 4px rgba(0,0,0,0.05);
}
.ex-header {
padding: 12px 14px; border-bottom: 1px solid var(–border);
display: flex; justify-content: space-between; align-items: center;
}
.ex-name { font-size: 13px; font-weight: 500; transition: color 0.2s; color: var(–text); }
.ex-target { font-size: 9px; color: var(–muted); margin-top: 3px; letter-spacing: 1px; }
.ex-count { font-size: 10px; letter-spacing: 1px; color: var(–muted); }
.col-labels {
display: grid; grid-template-columns: 28px 1fr 1fr 36px;
gap: 6px; padding: 6px 14px; font-size: 8px; color: var(–muted);
letter-spacing: 2px; border-bottom: 1px solid var(–faint); background: var(–faint);
}
.set-row {
display: grid; grid-template-columns: 28px 1fr 1fr 36px;
gap: 6px; padding: 8px 14px; align-items: center;
border-bottom: 1px solid var(–faint); transition: background 0.15s;
}
.set-row:last-child { border-bottom: none; }
.set-num { font-size: 11px; color: var(–muted); }
.set-input {
background: var(–input-bg); border: 1.5px solid var(–border); border-radius: 7px;
padding: 8px 6px; color: var(–text); font-size: 14px; font-family: inherit;
width: 100%; outline: none; -webkit-appearance: none; text-align: center;
transition: border-color 0.15s;
}
.set-input:focus { border-color: var(–accent); }
.check-btn {
width: 34px; height: 34px; border-radius: 8px; border: 1.5px solid var(–border);
background: var(–faint); display: flex; align-items: center; justify-content: center;
font-size: 15px; cursor: pointer; transition: all 0.15s; -webkit-appearance: none;
flex-shrink: 0; color: transparent;
}

/* Save button */
.save-wrap {
position: fixed; bottom: 0; left: 0; right: 0;
padding: 12px 16px calc(var(–safe-bottom) + 10px);
background: linear-gradient(0deg, var(–bg) 70%, transparent);
}
.save-btn {
width: 100%; padding: 15px; border-radius: 12px; font-family: inherit;
font-size: 11px; letter-spacing: 3px; font-weight: 500; cursor: pointer;
transition: all 0.2s; -webkit-appearance: none; border-width: 1.5px; border-style: solid;
box-shadow: 0 2px 10px rgba(0,0,0,0.08);
}
.save-btn.saved { background: #f0fdf4 !important; border-color: #34c472 !important; color: #34c472 !important; }

/* Cardio */
.section-label { font-size: 9px; color: var(–muted); letter-spacing: 2px; margin: 18px 0 8px; text-transform: uppercase; }
.cardio-type-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; }
.cardio-type-btn {
background: var(–bg2); border: 1.5px solid var(–border); border-radius: 10px;
padding: 12px 6px; display: flex; flex-direction: column; align-items: center; gap: 5px;
font-family: inherit; font-size: 9px; letter-spacing: 1.5px; text-transform: uppercase;
cursor: pointer; transition: all 0.2s; color: var(–muted); -webkit-appearance: none;
box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}
.cardio-type-btn .cicon { font-size: 24px; }
.cardio-type-btn.active { border-color: #0ea5e9; background: #f0f9ff; color: #0284c7; box-shadow: 0 0 0 3px rgba(14,165,233,0.15); font-weight: 500; }
.field-card {
background: var(–bg2); border: 1.5px solid var(–border); border-radius: 12px;
overflow: hidden; margin-top: 10px; box-shadow: 0 1px 4px rgba(0,0,0,0.05);
}
.field-row {
display: flex; justify-content: space-between; align-items: center;
padding: 13px 16px; border-bottom: 1px solid var(–faint);
}
.field-row:last-child { border-bottom: none; }
.field-label { font-size: 10px; color: var(–muted); letter-spacing: 1px; }
.input-wrap { display: flex; align-items: center; gap: 7px; }
.cardio-input {
background: var(–input-bg); border: 1.5px solid var(–border); border-radius: 8px;
padding: 8px 10px; color: var(–text); font-size: 14px; font-family: inherit;
width: 100px; outline: none; -webkit-appearance: none; text-align: center;
transition: border-color 0.15s;
}
.cardio-input:focus { border-color: #0ea5e9; }
.unit-label { font-size: 10px; color: var(–muted); letter-spacing: 1px; min-width: 30px; }
.intensity-row { display: flex; gap: 8px; }
.intensity-btn {
flex: 1; padding: 11px 4px; border-radius: 8px; font-family: inherit;
font-size: 9px; letter-spacing: 1px; text-transform: uppercase; cursor: pointer;
background: var(–faint); border: 1.5px solid var(–border); color: var(–muted);
transition: all 0.2s; -webkit-appearance: none; box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}
.int-low  { background: #f0fdf4; border-color: #86efac; color: #16a34a; font-weight: 500; }
.int-mod  { background: #fffbeb; border-color: #fcd34d; color: #d97706; font-weight: 500; }
.int-high { background: #fff1f2; border-color: #fda4af; color: #e11d48; font-weight: 500; }
.cardio-notes {
background: var(–input-bg); border: 1.5px solid var(–border); border-radius: 10px;
padding: 12px; color: var(–text); font-size: 13px; font-family: inherit;
width: 100%; outline: none; -webkit-appearance: none; resize: none; line-height: 1.6;
transition: border-color 0.15s;
}
.cardio-notes:focus { border-color: #0ea5e9; }

/* History */
.history-entry {
background: var(–bg2); border: 1.5px solid var(–border); border-radius: 12px;
padding: 14px 16px; margin-top: 10px; display: flex;
justify-content: space-between; align-items: center; cursor: pointer;
transition: all 0.15s; box-shadow: 0 1px 4px rgba(0,0,0,0.05);
}
.history-entry:active { transform: scale(0.98); opacity: 0.8; }
.history-left { display: flex; align-items: center; gap: 12px; }
.history-icon { font-size: 24px; }
.history-name { font-size: 13px; color: var(–text); font-weight: 500; }
.history-meta { font-size: 9px; color: var(–muted); letter-spacing: 1px; margin-top: 3px; }
.history-arrow { font-size: 11px; letter-spacing: 1px; }
.empty-state { text-align: center; padding: 40px 20px; font-size: 11px; color: var(–muted); letter-spacing: 2px; }

/* Animations */
@keyframes fadeUp { from { opacity:0; transform:translateY(8px); } to { opacity:1; transform:none; } }
.fade-up { animation: fadeUp 0.25s ease forwards; }
@keyframes pop { 0%{transform:scale(1)} 40%{transform:scale(1.18)} 100%{transform:scale(1)} }
.pop { animation: pop 0.18s ease; }

input[type=number] { -moz-appearance: textfield; }
input[type=number]::-webkit-outer-spin-button,
input[type=number]::-webkit-inner-spin-button { -webkit-appearance: none; }
</style>

</head>
<body>
<div id="app">
  <div id="header">
    <div class="header-row">
      <div>
        <div class="app-title" id="appTitle">GYM LOG</div>
        <div class="app-sub">A/B SPLIT TRACKER</div>
      </div>
      <div>
        <input type="date" class="date-input" id="dateInput">
        <div class="date-label">TRAINING DATE</div>
      </div>
    </div>
    <div class="nav-tabs">
      <div class="nav-tab active" data-view="workout">WORKOUT</div>
      <div class="nav-tab" data-view="cardio">CARDIO</div>
      <div class="nav-tab" data-view="history">HISTORY</div>
    </div>
  </div>

  <div id="scroll">
    <div id="workoutView"></div>
    <div id="cardioView" style="display:none"></div>
    <div id="historyView" style="display:none"></div>
  </div>

  <div class="save-wrap" id="saveWrap">
    <button class="save-btn" id="saveBtn">SAVE WORKOUT</button>
  </div>
  <div class="save-wrap" id="cardioSaveWrap" style="display:none">
    <button class="save-btn" id="cardioSaveBtn"
      style="background:#f0f9ff;border-color:#0ea5e9;color:#0284c7">SAVE CARDIO SESSION</button>
  </div>
</div>

<script>
const WORKOUTS = {
  chest: {
    label:"Chest", icon:"💪",
    color:"#c0392b", bg:"#fff5f4", border:"#fca99f",
    weeks:{
      A:{ label:"Power & Volume", exercises:[
        {name:"Barbell Bench Press",         sets:5, reps:"5"},
        {name:"Incline Dumbbell Press",       sets:4, reps:"8–10"},
        {name:"Dumbbell Fly",                 sets:3, reps:"12–15"},
        {name:"Weighted Dips",                sets:3, reps:"8–10"},
        {name:"Low-to-High Cable Fly",        sets:3, reps:"12–15"},
        {name:"OHP Barbell",                  sets:4, reps:"6–8"},
      ]},
      B:{ label:"Angles & Isolation", exercises:[
        {name:"Dumbbell Bench Press",         sets:5, reps:"6–8"},
        {name:"Barbell Incline Press",        sets:4, reps:"8–10"},
        {name:"Low-to-High Dumbbell Fly",     sets:4, reps:"10–12"},
        {name:"Hammer Strength Chest Press",  sets:3, reps:"10–12"},
        {name:"Push-Up Variation (Archer/Ring)", sets:3, reps:"Failure"},
        {name:"Pec Deck Machine",             sets:3, reps:"15"},
      ]},
    }
  },
  back: {
    label:"Back", icon:"🏋️",
    color:"#1565c0", bg:"#f0f7ff", border:"#90caf9",
    weeks:{
      A:{ label:"Trap Bar Focused", exercises:[
        {name:"Trap Bar Deadlift",            sets:5, reps:"3–5"},
        {name:"Weighted Pull-Ups",            sets:4, reps:"6–8"},
        {name:"Barbell Bent-Over Row",        sets:4, reps:"8"},
        {name:"Seated Cable Row (Close Grip)",sets:3, reps:"10–12"},
        {name:"Face Pulls",                   sets:3, reps:"15–20"},
      ]},
      B:{ label:"Volume & Variety", exercises:[
        {name:"Trap Bar Deadlift",            sets:5, reps:"4–6"},
        {name:"Chest-Supported DB Row",       sets:4, reps:"8–10"},
        {name:"Lat Pulldown (Wide Grip)",     sets:4, reps:"10–12"},
        {name:"Machine Low Row",              sets:3, reps:"10–12"},
        {name:"Machine Reverse Fly",          sets:3, reps:"12–15"},
      ]},
    }
  },
  legs: {
    label:"Legs", icon:"🦵",
    color:"#1b7a40", bg:"#f0fdf4", border:"#86efac",
    weeks:{
      A:{ label:"Squat & Hamstring", exercises:[
        {name:"Barbell Back Squat",           sets:5, reps:"5"},
        {name:"Romanian Deadlift",            sets:4, reps:"8–10"},
        {name:"Leg Press",                    sets:4, reps:"10–12"},
        {name:"Walking Lunges (DB)",          sets:3, reps:"12 each leg"},
        {name:"Seated Leg Curl",              sets:3, reps:"12–15"},
        {name:"Standing Calf Raise",          sets:4, reps:"15–20"},
      ]},
      B:{ label:"Unilateral & Quad", exercises:[
        {name:"Front Squat or Hack Squat",    sets:5, reps:"6–8"},
        {name:"Bulgarian Split Squat (DB)",   sets:4, reps:"8–10 each"},
        {name:"Leg Extension",                sets:3, reps:"12–15"},
        {name:"Nordic Curl or Lying Leg Curl",sets:3, reps:"8–10"},
        {name:"Goblet Squat (Pause)",         sets:3, reps:"10–12"},
        {name:"Standing Calf Raise",          sets:4, reps:"15–20"},
      ]},
    }
  },
  arms: {
    label:"Arms", icon:"💥",
    color:"#a05c00", bg:"#fffbeb", border:"#fcd34d",
    weeks:{
      A:{ label:"Strength Base", exercises:[
        {name:"Close-Grip Bench Press",       sets:4, reps:"6–8"},
        {name:"EZ-Bar Curl",                  sets:4, reps:"8–10"},
        {name:"Overhead Tricep Ext (Cable)",  sets:3, reps:"10–12"},
        {name:"Incline Dumbbell Curl",        sets:3, reps:"10–12"},
        {name:"Tricep Rope Pushdown",         sets:3, reps:"12–15"},
        {name:"Hammer Curl",                  sets:3, reps:"12 each"},
      ]},
      B:{ label:"Isolation & Peak", exercises:[
        {name:"Weighted Tricep Dips",         sets:4, reps:"8–10"},
        {name:"Barbell Curl",                 sets:4, reps:"6–8"},
        {name:"Skull Crushers (EZ Bar)",      sets:3, reps:"10–12"},
        {name:"Cable Curl (High Pulley)",     sets:3, reps:"12–15"},
        {name:"Single-Arm Overhead DB Ext",   sets:3, reps:"12 each"},
        {name:"Reverse Curl",                 sets:3, reps:"12–15"},
      ]},
    }
  }
};

const CARDIO_TYPES = [
  {id:"run",      label:"Run",        icon:"🏃"},
  {id:"bike",     label:"Bike",       icon:"🚴"},
  {id:"row",      label:"Row",        icon:"🚣"},
  {id:"swim",     label:"Swim",       icon:"🏊"},
  {id:"elliptic", label:"Elliptical", icon:"⚙️"},
  {id:"other",    label:"Other",      icon:"⚡"},
];

let state = {
  muscle:'chest', week:'A', view:'workout',
  date: new Date().toISOString().slice(0,10),
  logData:{},
  cardio:{type:'run', duration:'', distance:'', hr:'', cals:'', intensity:'', notes:''},
};

const sKey      = () => `gymlog:workout:${state.muscle}:${state.week}:${state.date}`;
const cardioKey = () => `gymlog:cardio:${state.date}`;

function loadLog() {
  try { const r=localStorage.getItem(sKey()); state.logData=r?JSON.parse(r):{}; }
  catch { state.logData={}; }
}
function saveLog() {
  try { localStorage.setItem(sKey(),JSON.stringify(state.logData)); return true; }
  catch { return false; }
}
function loadCardio() {
  try {
    const r=localStorage.getItem(cardioKey());
    state.cardio = r ? {...{type:'run',duration:'',distance:'',hr:'',cals:'',intensity:'',notes:''},...JSON.parse(r)} : {type:'run',duration:'',distance:'',hr:'',cals:'',intensity:'',notes:''};
  } catch { state.cardio={type:'run',duration:'',distance:'',hr:'',cals:'',intensity:'',notes:''}; }
}
function saveCardio() {
  try { localStorage.setItem(cardioKey(),JSON.stringify(state.cardio)); return true; }
  catch { return false; }
}

const W = () => WORKOUTS[state.muscle];

// ── Render Workout ────────────────────────────────────────────────────────────
function renderWorkout() {
  const w = W();
  const exs = w.weeks[state.week].exercises;
  const totalSets = exs.reduce((a,e)=>a+e.sets,0);
  const doneSets  = Object.values(state.logData).reduce((a,s)=>a+(Array.isArray(s)?s.filter(x=>x&&x.done).length:0),0);
  const pct = totalSets ? Math.round(doneSets/totalSets*100) : 0;

  document.getElementById('appTitle').style.color = w.color;
  document.documentElement.style.setProperty('--accent', w.color);

  const muscleBtns = Object.entries(WORKOUTS).map(([k,m])=>`
    <button class="muscle-btn" onclick="selMuscle('${k}')"
      style="${state.muscle===k?`border-color:${m.color};background:${m.bg};color:${m.color};box-shadow:0 0 0 3px ${m.border}55`:''}">
      <span class="icon">${m.icon}</span><span style="color:${state.muscle===k?m.color:''}">${m.label}</span>
    </button>`).join('');

  const weekBtns = ['A','B'].map(wk=>`
    <button class="week-btn" onclick="selWeek('${wk}')"
      style="${state.week===wk?`border-color:${w.color};background:${w.bg};color:${w.color};font-weight:500`:''}">
      WEEK ${wk} — ${w.weeks[wk].label.toUpperCase()}
    </button>`).join('');

  const cards = exs.map((ex,ei)=>{
    const sets=state.logData[ei]||[];
    const done=sets.filter(s=>s&&s.done).length;
    const full=done===ex.sets;
    const rows=Array.from({length:ex.sets},(_,si)=>{
      const s=sets[si]||{};
      return `
        <div class="set-row" id="row-${ei}-${si}" style="${s.done?`background:${w.bg}`:''}">
          <div class="set-num">${si+1}</div>
          <input class="set-input" type="number" inputmode="decimal" placeholder="kg"
            value="${s.weight||''}" onchange="updSet(${ei},${si},'weight',this.value)"
            style="${s.done?`border-color:${w.border}`:''}">
          <input class="set-input" type="number" inputmode="numeric" placeholder="reps"
            value="${s.reps||''}" onchange="updSet(${ei},${si},'reps',this.value)"
            style="${s.done?`border-color:${w.border}`:''}">
          <button class="check-btn" onclick="togDone(${ei},${si})"
            style="${s.done?`background:${w.color};border-color:${w.color};color:#fff`:''}">
            ${s.done?'✓':''}
          </button>
        </div>`;
    }).join('');
    return `
      <div class="ex-card" style="${full?`border-color:${w.color};box-shadow:0 0 0 3px ${w.border}55`:''}">
        <div class="ex-header">
          <div>
            <div class="ex-name" style="${full?`color:${w.color}`:''}">${ex.name}</div>
            <div class="ex-target">TARGET: ${ex.sets} × ${ex.reps} REPS</div>
          </div>
          <div class="ex-count" style="${full?`color:${w.color};font-weight:500`:''}">${done}/${ex.sets}</div>
        </div>
        <div class="col-labels"><span>SET</span><span>WEIGHT</span><span>REPS</span><span>✓</span></div>
        ${rows}
      </div>`;
  }).join('');

  document.getElementById('workoutView').innerHTML = `
    <div class="fade-up">
      <div class="muscle-grid">${muscleBtns}</div>
      <div class="week-row">${weekBtns}</div>
      <div class="progress-header">
        <span>PROGRESS</span>
        <span style="color:${w.color};font-weight:500">${doneSets}/${totalSets} SETS · ${pct}%</span>
      </div>
      <div class="progress-bar">
        <div class="progress-fill" style="width:${pct}%;background:${w.color}"></div>
      </div>
      ${cards}
    </div>`;

  const sb=document.getElementById('saveBtn');
  sb.style.cssText=`background:${w.bg};border-color:${w.color};color:${w.color}`;
}

// ── Render Cardio ─────────────────────────────────────────────────────────────
function renderCardio() {
  const c = state.cardio;
  const typeBtns = CARDIO_TYPES.map(t=>`
    <button class="cardio-type-btn ${c.type===t.id?'active':''}" onclick="selCardioType('${t.id}')">
      <span class="cicon">${t.icon}</span><span>${t.label}</span>
    </button>`).join('');

  const intClass = (id) => {
    if(c.intensity!==id) return '';
    return id==='low'?'int-low':id==='mod'?'int-mod':'int-high';
  };

  document.getElementById('cardioView').innerHTML = `
    <div class="fade-up">
      <div class="section-label">SESSION TYPE</div>
      <div class="cardio-type-grid">${typeBtns}</div>

      <div class="section-label">SESSION DETAILS</div>
      <div class="field-card">
        <div class="field-row">
          <div class="field-label">DURATION</div>
          <div class="input-wrap">
            <input class="cardio-input" type="number" inputmode="numeric" placeholder="0"
              value="${c.duration||''}" onchange="updCardio('duration',this.value)">
            <span class="unit-label">MIN</span>
          </div>
        </div>
        <div class="field-row">
          <div class="field-label">DISTANCE</div>
          <div class="input-wrap">
            <input class="cardio-input" type="number" inputmode="decimal" placeholder="0.0"
              value="${c.distance||''}" onchange="updCardio('distance',this.value)">
            <span class="unit-label">KM</span>
          </div>
        </div>
        <div class="field-row">
          <div class="field-label">AVG HEART RATE</div>
          <div class="input-wrap">
            <input class="cardio-input" type="number" inputmode="numeric" placeholder="0"
              value="${c.hr||''}" onchange="updCardio('hr',this.value)">
            <span class="unit-label">BPM</span>
          </div>
        </div>
        <div class="field-row">
          <div class="field-label">CALORIES</div>
          <div class="input-wrap">
            <input class="cardio-input" type="number" inputmode="numeric" placeholder="0"
              value="${c.cals||''}" onchange="updCardio('cals',this.value)">
            <span class="unit-label">KCAL</span>
          </div>
        </div>
      </div>

      <div class="section-label">INTENSITY</div>
      <div class="intensity-row">
        <button class="intensity-btn ${intClass('low')}" onclick="selIntensity('low')">🟢 Zone 2</button>
        <button class="intensity-btn ${intClass('mod')}" onclick="selIntensity('mod')">🟡 Moderate</button>
        <button class="intensity-btn ${intClass('high')}" onclick="selIntensity('high')">🔴 High</button>
      </div>

      <div class="section-label">NOTES</div>
      <textarea class="cardio-notes" rows="3"
        placeholder="Route, conditions, how it felt..."
        onchange="updCardio('notes',this.value)">${c.notes||''}</textarea>

```
</div>`;
```

}

// ── Render History ────────────────────────────────────────────────────────────
function renderHistory() {
const workouts=[], cardios=[];
for(let i=0;i<localStorage.length;i++){
const key=localStorage.key(i);
if(!key.startsWith(‘gymlog:’)) continue;
const parts=key.replace(‘gymlog:’,’’).split(’:’);
if(parts[0]===‘workout’&&parts.length===4) workouts.push({muscle:parts[1],week:parts[2],date:parts[3]});
if(parts[0]===‘cardio’ &&parts.length===2) cardios.push({date:parts[1]});
}
workouts.sort((a,b)=>b.date.localeCompare(a.date));
cardios.sort((a,b)=>b.date.localeCompare(a.date));

const wHTML = workouts.length ? workouts.map(e=>{
const m=WORKOUTS[e.muscle]; if(!m) return ‘’;
return ` <div class="history-entry" onclick="loadWorkoutEntry('${e.muscle}','${e.week}','${e.date}')" style="border-left:3px solid ${m.color}"> <div class="history-left"> <div class="history-icon">${m.icon}</div> <div> <div class="history-name">${m.label} — Week ${e.week}</div> <div class="history-meta">${e.date}</div> </div> </div> <div class="history-arrow" style="color:${m.color}">VIEW →</div> </div>`;
}).join(’’) : ‘<div class="empty-state">NO WORKOUTS SAVED YET</div>’;

const cHTML = cardios.length ? cardios.map(e=>{
let d={}; try{d=JSON.parse(localStorage.getItem(`gymlog:cardio:${e.date}`)||’{}’);}catch{}
const t=CARDIO_TYPES.find(x=>x.id===d.type)||CARDIO_TYPES[0];
const detail=[d.duration?d.duration+’ min’:null, d.distance?d.distance+’ km’:null].filter(Boolean).join(’ · ‘);
return ` <div class="history-entry" onclick="loadCardioEntry('${e.date}')" style="border-left:3px solid #0ea5e9"> <div class="history-left"> <div class="history-icon">${t.icon}</div> <div> <div class="history-name">${t.label}${detail?' — '+detail:''}</div> <div class="history-meta">${e.date}</div> </div> </div> <div class="history-arrow" style="color:#0ea5e9">VIEW →</div> </div>`;
}).join(’’) : ‘<div class="empty-state">NO CARDIO SAVED YET</div>’;

document.getElementById(‘historyView’).innerHTML = ` <div class="fade-up"> <div class="section-label" style="margin-top:16px">WORKOUTS</div> ${wHTML} <div class="section-label" style="margin-top:24px">CARDIO SESSIONS</div> ${cHTML} </div>`;
}

// ── Actions ───────────────────────────────────────────────────────────────────
function selMuscle(m)       { state.muscle=m; loadLog(); renderWorkout(); }
function selWeek(w)         { state.week=w;   loadLog(); renderWorkout(); }
function selCardioType(t)   { state.cardio.type=t; renderCardio(); }
function selIntensity(i)    { state.cardio.intensity=state.cardio.intensity===i?’’:i; renderCardio(); }
function updCardio(f,v)     { state.cardio[f]=v; }

function updSet(ei,si,field,val) {
if(!state.logData[ei]) state.logData[ei]=[];
if(!state.logData[ei][si]) state.logData[ei][si]={weight:’’,reps:’’,done:false};
state.logData[ei][si][field]=val;
}
function togDone(ei,si) {
if(!state.logData[ei]) state.logData[ei]=[];
if(!state.logData[ei][si]) state.logData[ei][si]={weight:’’,reps:’’,done:false};
state.logData[ei][si].done=!state.logData[ei][si].done;
const btn=document.querySelector(`#row-${ei}-${si} .check-btn`);
if(btn){btn.classList.add(‘pop’);setTimeout(()=>btn.classList.remove(‘pop’),200);}
renderWorkout();
}

function loadWorkoutEntry(muscle,week,date) {
state.muscle=muscle; state.week=week; state.date=date;
document.getElementById(‘dateInput’).value=date;
loadLog(); switchView(‘workout’);
}
function loadCardioEntry(date) {
state.date=date;
document.getElementById(‘dateInput’).value=date;
loadCardio(); switchView(‘cardio’);
}

function switchView(v) {
state.view=v;
document.querySelectorAll(’.nav-tab’).forEach(t=>t.classList.toggle(‘active’,t.dataset.view===v));
document.getElementById(‘workoutView’).style.display   = v===‘workout’?’’:‘none’;
document.getElementById(‘cardioView’).style.display    = v===‘cardio’ ?’’:‘none’;
document.getElementById(‘historyView’).style.display   = v===‘history’?’’:‘none’;
document.getElementById(‘saveWrap’).style.display      = v===‘workout’?’’:‘none’;
document.getElementById(‘cardioSaveWrap’).style.display= v===‘cardio’ ?’’:‘none’;
if(v===‘history’) renderHistory();
if(v===‘cardio’)  { loadCardio(); renderCardio(); }
if(v===‘workout’) renderWorkout();
document.getElementById(‘scroll’).scrollTop=0;
}

// Save buttons
document.getElementById(‘saveBtn’).addEventListener(‘click’, ()=>{
const ok=saveLog(), w=W(), btn=document.getElementById(‘saveBtn’);
btn.textContent=ok?‘✓  WORKOUT SAVED’:‘⚠  SAVE FAILED’;
btn.classList.toggle(‘saved’,ok);
setTimeout(()=>{ btn.textContent=‘SAVE WORKOUT’; btn.classList.remove(‘saved’);
btn.style.cssText=`background:${w.bg};border-color:${w.color};color:${w.color}`; },2000);
});
document.getElementById(‘cardioSaveBtn’).addEventListener(‘click’, ()=>{
const ok=saveCardio(), btn=document.getElementById(‘cardioSaveBtn’);
btn.textContent=ok?‘✓  SESSION SAVED’:‘⚠  SAVE FAILED’;
btn.classList.toggle(‘saved’,ok);
setTimeout(()=>{ btn.textContent=‘SAVE CARDIO SESSION’; btn.classList.remove(‘saved’);
btn.style.cssText=‘background:#f0f9ff;border-color:#0ea5e9;color:#0284c7’; },2000);
});

// Date input
const dateInput=document.getElementById(‘dateInput’);
dateInput.value=state.date;
dateInput.addEventListener(‘change’,()=>{
state.date=dateInput.value;
if(state.view===‘workout’){loadLog();renderWorkout();}
if(state.view===‘cardio’){loadCardio();renderCardio();}
});

// Nav tabs
document.querySelectorAll(’.nav-tab’).forEach(t=>t.addEventListener(‘click’,()=>switchView(t.dataset.view)));

// Init
loadLog();
renderWorkout();
</script>

</body>
</html>
