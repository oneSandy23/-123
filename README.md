[多采的文化饗宴 (2).html](https://github.com/user-attachments/files/35004640/2.html)
# -123<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>多采的文化饗宴</title>
<style>
:root{--bg:#f8f4ec;--card:#fffaf4;--ink:#3a2418;--mute:#8a7566;--red:#b3201a;--line:#e6d6bf;--c0:#b3201a;--c1:#5f7a35;--c2:#2f6f8f;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){color-scheme:dark;--bg:#241913;--card:#33251c;--ink:#f6e9d8;--mute:#bba58f;--red:#ff7b6b;--line:#5a4435;--c0:#ff7b6b;--c1:#a6c46a;--c2:#6fb7d8}}
:root[data-theme="dark"]{color-scheme:dark;--bg:#241913;--card:#33251c;--ink:#f6e9d8;--mute:#bba58f;--red:#ff7b6b;--line:#5a4435;--c0:#ff7b6b;--c1:#a6c46a;--c2:#6fb7d8}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:"Noto Sans TC","PingFang TC","Microsoft JhengHei",sans-serif;min-height:100vh}
body::before{content:"";position:fixed;inset:0 0 auto;height:env(safe-area-inset-top,0px);background:var(--bg);z-index:10}
#app{max-width:1500px;margin:0 auto;padding:16px}
h1,h2{margin:0}
.bar{display:flex;flex-wrap:wrap;gap:8px;align-items:center;justify-content:space-between;margin-bottom:14px}
.title{font-size:1.6rem;font-weight:800;color:var(--red)}
.btns{display:flex;flex-wrap:wrap;gap:6px}
button{font:inherit;border:2px solid var(--line);background:var(--card);color:var(--ink);border-radius:12px;padding:8px 14px;cursor:pointer;font-weight:700}
button.on{background:var(--red);border-color:var(--red);color:#fff}
button.big{font-size:1.5rem;padding:20px 30px}
button.danger{border-color:var(--red);color:var(--red)}
.land{display:flex;flex-direction:column;align-items:center;gap:18px;margin-top:10vh;text-align:center}
.cols{display:grid;grid-template-columns:repeat(3,1fr);gap:14px}
.col{background:var(--card);border:3px solid var(--line);border-radius:18px;padding:14px;min-height:60vh}
.col.live{border-color:var(--c);box-shadow:0 0 0 3px var(--c)}
.col h2{color:var(--c);font-size:2rem;text-align:center;margin-bottom:10px}
.chips,.zone{display:flex;flex-wrap:wrap;gap:8px;align-content:flex-start}
.chip{background:var(--c,var(--red));color:#fff;border-radius:12px;padding:6px 12px;font-size:1.25rem;font-weight:700;display:inline-flex;gap:6px;align-items:center}
.chip small{font-size:.7rem;opacity:.8;font-weight:500}
.chip b{cursor:pointer;opacity:.85}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px}
.card{background:var(--card);border:3px solid var(--c);border-radius:16px;padding:12px}
.card h3{margin:0 0 8px;color:var(--c);font-size:1.3rem}
.two{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.sub{border:2px dashed var(--line);border-radius:12px;padding:8px;min-height:90px}
.sub h4{margin:0 0 6px;font-size:1.05rem}
.cloud{display:flex;flex-wrap:wrap;gap:10px 22px;justify-content:center;align-items:center;padding:10px;min-height:50vh}
.cloud span{font-weight:800;line-height:1.1;color:var(--c)}
.hint{color:var(--mute)}
.stu .zone{min-height:80px;border:3px dashed var(--line);border-radius:14px;padding:10px;background:var(--card)}
.stu .zone.over{border-color:var(--c);background:color-mix(in srgb,var(--c) 12%,var(--card))}
.stu .chip{touch-action:none;user-select:none;-webkit-user-select:none;cursor:grab;font-size:1.3rem}
.chip.sel{outline:4px solid var(--ink)}
.ghost{position:fixed;pointer-events:none;z-index:99;opacity:.9;transform:translate(-50%,-50%)}
input[type=text]{font:inherit;font-size:1.2rem;padding:10px 12px;border:2px solid var(--line);border-radius:10px;background:var(--card);color:var(--ink);width:100%}
.row{display:flex;gap:8px}
.namebox{display:flex;align-items:center;gap:6px;margin-bottom:6px;font-weight:700;font-size:1.1rem}
.namebox input{width:9em}
@media (max-width:820px){.cols,.grid{grid-template-columns:1fr}.two{grid-template-columns:1fr 1fr}}
</style>
</head>
<body>
<div id="app"></div>
<script>
const TOPICS=['春節','端午節','聖誕節'], GROUPS={A:0,B:0,C:1,D:1,E:2,F:2}, LETTERS=Object.keys(GROUPS);
const esc=s=>String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
let db=null,user=null,canEdit=false,S={phase:1,topic:0},words=[],cats={},group=null,sel=null,dragging=false,ready=false,msg='',myQ=0,goCat=false;
try{group=localStorage.getItem('cf_group')}catch(e){}
const route=()=>location.hash.replace('#','');
const app=document.getElementById('app');

function render(){
  if(dragging)return;
  const r=route();
  if(r==='student'&&document.activeElement&&document.activeElement.tagName==='INPUT'&&S.phase===2)return;
  if(r==='board')return app.innerHTML=board();
  if(r==='student')return app.innerHTML=student();
  app.innerHTML=`<div class="land"><h1 class="title" style="font-size:2.6rem">多采的文化饗宴</h1><p class="hint">春節・端午節・聖誕節</p>
  <button class="big on" onclick="location.hash='board'">👩‍🏫 老師／電子白板</button>
  <button class="big" onclick="location.hash='student'">🧒 學生（平板）</button>
  ${db?'':'<p class="hint">資料庫連線中或未登入… 若一直無法連線，請確認已登入並以可編輯權限分享連結。</p>'}</div>`;
}
window.addEventListener('hashchange',render);

/* ---------- board (whiteboard) ---------- */
function board(){
  const ph=S.phase;
  const ctl=canEdit?`<div class="btns">${[1,2,3].map(p=>`<button class="${ph===p?'on':''}" onclick="setS({phase:${p}})">${['①聯想','②分類','③文字雲'][p-1]}</button>`).join('')}
  ${ph===1?TOPICS.map((t,i)=>`<button class="${S.topic===i?'on':''}" onclick="setS({topic:${i}})">出題：${t}</button>`).join('')+`<button class="on" style="background:var(--c${Math.min(S.topic+1,2)});border-color:var(--c${Math.min(S.topic+1,2)})" onclick="nextQ()">${S.topic<2?'下一題 ▶ '+TOPICS[S.topic+1]:'進入分類 ▶'}</button>`:''}
  <button class="danger" id="clr" onclick="clearAll()">清空資料</button></div>`:`<span class="hint">階段 ${ph}</span>`;
  let body='';
  if(ph===1){
    body=`<div class="cols">${TOPICS.map((t,i)=>`<section class="col ${S.topic===i?'live':''}" style="--c:var(--c${i})"><h2>${t}${S.topic===i?' ✎':''}</h2><div class="chips">${words.filter(w=>w.topic===i).map(w=>`<span class="chip" style="--c:var(--c${i})">${esc(w.text)}<small>${w.group}</small>${canEdit?`<b onclick="delWord('${w.id}')">×</b>`:''}</span>`).join('')}</div></section>`).join('')}</div>`;
  }else if(ph===2){
    body=`<div class="grid">${LETTERS.map(g=>{const t=GROUPS[g],c=cats[g]||{names:['',''],assign:{}},ws=words.filter(w=>w.topic===t);
      const sub=k=>`<div class="sub"><h4>跟「${esc(c.names[k]||'…')}」有關</h4><div class="chips">${ws.filter(w=>c.assign[w.id]===k).map(w=>`<span class="chip" style="--c:var(--c${t});font-size:1rem">${esc(w.text)}</span>`).join('')}</div></div>`;
      return `<div class="card" style="--c:var(--c${t})"><h3>${g}組 · ${TOPICS[t]} <small class="hint">未分類 ${ws.filter(w=>c.assign[w.id]===undefined).length}</small></h3><div class="two">${sub(0)}${sub(1)}</div></div>`}).join('')}</div>`;
  }else{
    body=`<div class="cols">${TOPICS.map((t,i)=>{const m={};LETTERS.filter(g=>GROUPS[g]===i).forEach(g=>((cats[g]||{}).names||[]).forEach(n=>{n=(n||'').trim();if(n)m[n]=(m[n]||0)+1}));
      const es=Object.entries(m),mx=Math.max(1,...es.map(e=>e[1]));
      return `<section class="col" style="--c:var(--c${i})"><h2>${t}</h2><div class="cloud">${es.length?es.map(([n,c],j)=>`<span style="font-size:${(2+ (c/mx)*2.2+ (j%3)*.25).toFixed(2)}rem;opacity:${(.65+.35*c/mx).toFixed(2)}">${esc(n)}</span>`).join(''):'<span class="hint" style="font-size:1.2rem">尚無分類</span>'}</div></section>`}).join('')}</div>`;
  }
  return `<div class="bar"><div class="btns" style="align-items:center"><button onclick="goHome()">← 返回</button><h1 class="title">多采的文化饗宴</h1></div>${ctl}</div>${body}`;
}

/* ---------- student ---------- */
function student(){
  if(!group)return `<div class="land"><h1 class="title">你是哪一組？</h1><div class="btns">${LETTERS.map(g=>`<button class="big" onclick="pick('${g}')">${g}組</button>`).join('')}</div><button onclick="goHome()">← 返回</button></div>`;
  const t=GROUPS[group],head=`<div class="bar"><h1 class="title">${group}組${S.phase===1?'':`　<small style="color:var(--c${t})">${TOPICS[t]}分類</small>`}</h1><div class="btns"><button onclick="stuBack()">← 返回</button><button onclick="pick(null)">換組</button></div></div>`;
  if(S.phase===1&&!goCat){
    if(myQ>2)return `<div class="stu">${head}<p style="font-size:1.5rem">✅ 你們都寫完了！請按下一頁，開始分類。</p><div class="btns"><button class="big" onclick="myQ=2;render()">◀ 回去補充</button><button class="big on" onclick="goCat=true;render()">下一頁：分類 ▶</button></div></div>`;
    const mine=words.filter(w=>w.group===group&&w.topic===myQ);
    return `<div class="stu">${head}<h2 style="color:var(--c${myQ});margin-bottom:10px">第${myQ+1}／3 題：想到「${TOPICS[myQ]}」，你會想到什麼？</h2>
    <div class="row"><input type="text" id="w" maxlength="12" placeholder="輸入聯想詞（按 Enter 送出）" onkeydown="if(event.key==='Enter')addWord()"><button class="on" onclick="addWord()">送出</button></div>
    <p class="hint">${esc(msg)}</p><div class="chips">${mine.map(w=>`<span class="chip" style="--c:var(--c${myQ})">${esc(w.text)}</span>`).join('')}</div>
    <div class="btns" style="margin-top:18px">${myQ>0?'<button class="big" onclick="myQ--;render()">◀ 上一題</button>':''}<button class="big on" onclick="myQ++;render()">${myQ<2?'下一題 ▶':'完成 ✔'}</button></div></div>`;
  }
  if(S.phase===3)return `<div class="stu">${head}<p class="hint" style="font-size:1.4rem">請看電子白板 👀</p></div>`;
  const c=cats[group]||{names:['',''],assign:{}},ws=words.filter(w=>w.topic===t);
  const chip=w=>`<span class="chip ${sel===w.id?'sel':''}" data-id="${w.id}" style="--c:var(--c${t})">${esc(w.text)}</span>`;
  const col=k=>`<div><div class="namebox">跟<input type="text" maxlength="8" value="${esc(c.names[k]||'')}" placeholder="寫分類名" oninput="setName(${k},this.value)">有關</div><div class="zone" data-zone="${k}" style="--c:var(--c${t})">${ws.filter(w=>c.assign[w.id]===k).map(chip).join('')}</div></div>`;
  return `<div class="stu">${head}${goCat?'<button onclick="goCat=false;myQ=2;render()">◀ 回去補充聯想詞</button>':''}<p class="hint">拖曳詞語到下面兩邊（或先點詞語，再點要放的框）。操作手拖，大家一起討論！</p>
  <div class="zone" data-zone="p" style="--c:var(--c${t});margin-bottom:12px">${ws.filter(w=>c.assign[w.id]===undefined).map(chip).join('')||'<span class="hint">都分完了 🎉</span>'}</div>
  <div class="two" style="gap:14px">${col(0)}${col(1)}</div></div>`;
}

/* ---------- actions ---------- */
function nextQ(){S.topic<2?setS({topic:S.topic+1}):setS({phase:2})}
function stuBack(){if(goCat){goCat=false;myQ=3}else if(S.phase===1&&myQ>0){myQ--}else{pick(null);return}render()}
function goHome(){location.hash='';render()}
function pick(g){group=g;try{g?localStorage.setItem('cf_group',g):localStorage.removeItem('cf_group')}catch(e){}render()}
async function setS(p){S={...S,...p};render();try{await db.doc('meta/state').set(S)}catch(e){}}
async function addWord(){
  const el=document.getElementById('w'),v=(el.value||'').trim();if(!v||!db)return;
  el.value='';
  try{await db.collection('words').add({topic:myQ,group,text:v,ts:Date.now()});msg=''}catch(e){msg='送出失敗，請告訴老師'}
}
async function delWord(id){try{await db.doc('words/'+id).delete()}catch(e){}}
async function saveCat(patch){
  const cur=cats[group]||{group,topic:GROUPS[group],names:['',''],assign:{}};
  cats[group]={...cur,...patch};render();
  try{await db.doc('cats/'+group).set(cats[group])}catch(e){}
}
function move(id,z){
  const c=cats[group]||{names:['',''],assign:{}},a={...c.assign};
  if(z==='p')delete a[id];else a[id]=+z;
  sel=null;saveCat({assign:a});
}
let nt;function setName(k,v){const c=cats[group]||{names:['','']},n=[...c.names];n[k]=v;cats[group]={...(cats[group]||{group,topic:GROUPS[group],assign:{}}),names:n};clearTimeout(nt);nt=setTimeout(()=>db.doc('cats/'+group).set(cats[group]).catch(()=>{}),500)}
let armed=false;
async function clearAll(){
  const b=document.getElementById('clr');
  if(!armed){armed=true;b.textContent='再按一次確認清空';setTimeout(()=>{armed=false;render()},3000);return}
  armed=false;
  for(const n of ['words','cats']){const s=await db.collection(n).get();await Promise.all(s.docs.map(d=>db.doc(n+'/'+d.id).delete().catch(()=>{})))}
  setS({phase:1,topic:0});
}

/* ---------- drag & tap (pointer events, works on tablets) ---------- */
let dr=null;
document.addEventListener('pointerdown',e=>{
  const ch=e.target.closest('.stu .chip[data-id]');if(!ch)return;
  dr={id:ch.dataset.id,x:e.clientX,y:e.clientY,el:ch,ghost:null};
});
document.addEventListener('pointermove',e=>{
  if(!dr)return;
  if(!dr.ghost&&Math.hypot(e.clientX-dr.x,e.clientY-dr.y)>8){dragging=true;dr.ghost=dr.el.cloneNode(true);dr.ghost.className='chip ghost';dr.ghost.style.setProperty('--c',getComputedStyle(dr.el).getPropertyValue('--c'));document.body.appendChild(dr.ghost);dr.el.style.opacity=.3}
  if(dr.ghost){dr.ghost.style.left=e.clientX+'px';dr.ghost.style.top=e.clientY+'px';
    document.querySelectorAll('.zone.over').forEach(z=>z.classList.remove('over'));
    const z=document.elementFromPoint(e.clientX,e.clientY)?.closest('.zone');if(z)z.classList.add('over')}
});
document.addEventListener('pointerup',e=>{
  if(!dr)return;const d=dr;dr=null;
  if(d.ghost){const z=document.elementFromPoint(e.clientX,e.clientY)?.closest('.zone');d.ghost.remove();dragging=false;
    if(z)move(d.id,z.dataset.zone);else render();}
  else{sel=sel===d.id?null:d.id;render()}
});
document.addEventListener('click',e=>{
  const z=e.target.closest('.stu .zone');
  if(z&&sel&&!e.target.closest('.chip'))move(sel,z.dataset.zone);
});

/* ---------- live data ---------- */
(async()=>{
  render();
  try{user=await claude.use('user');canEdit=user?user.canEdit():false;db=await claude.use('db')}catch(e){}
  if(!db){render();return}
  db.doc('meta/state').onSnapshot(s=>{if(s.exists)S={phase:1,topic:0,...s.data()};render()});
  db.collection('words').onSnapshot(s=>{words=s.docs.map(d=>({id:d.id,...d.data()})).sort((a,b)=>a.ts-b.ts);render()});
  db.collection('cats').onSnapshot(s=>{if(dragging)return;const o={};s.docs.forEach(d=>o[d.id]=d.data());cats=o;render()});
  render();
})();
</script>
</body>
</html>
