<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>شيبس ديبو — إدارة المستودع والتوزيع</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f8f8f6;--bg2:#f0efeb;--bg3:#e8e7e2;
  --surface:#ffffff;--surface2:#f5f4f0;
  --text:#1a1a18;--text2:#5a5a56;--text3:#9a9a94;
  --border:rgba(0,0,0,.10);--border2:rgba(0,0,0,.18);
  --blue-bg:#e6f1fb;--blue-text:#0c447c;--blue-border:#85b7eb;
  --green-bg:#eaf3de;--green-text:#27500a;--green-border:#97c459;
  --red-bg:#fcebeb;--red-text:#791f1f;--red-border:#f09595;
  --orange-bg:#faeeda;--orange-text:#633806;--orange-border:#ef9f27;
  --warn-bg:#faeeda;--warn-text:#633806;
  --r:8px;--rl:12px;
}
body{font-family:'Segoe UI',Tahoma,Arial,sans-serif;font-size:14px;background:var(--bg);color:var(--text);direction:rtl}
.app{display:flex;min-height:100vh}
/* SIDEBAR */
.sidebar{width:210px;background:var(--surface);border-left:1px solid var(--border);display:flex;flex-direction:column;flex-shrink:0;position:sticky;top:0;height:100vh;overflow-y:auto}
.logo{padding:16px 14px 12px;border-bottom:1px solid var(--border)}
.logo-title{font-size:16px;font-weight:600;color:var(--text)}
.logo-sub{font-size:11px;color:var(--text2);margin-top:2px}
.nav{padding:8px 6px;flex:1}
.nav-sec{font-size:10px;color:var(--text3);padding:8px 10px 3px;letter-spacing:.5px;text-transform:uppercase}
.ni{display:flex;align-items:center;gap:8px;padding:8px 10px;border-radius:var(--r);cursor:pointer;font-size:13px;color:var(--text2);margin-bottom:1px;transition:background .12s}
.ni:hover{background:var(--bg)}
.ni.active{background:var(--bg2);color:var(--text);font-weight:500}
.sidebar-footer{padding:10px 14px;border-top:1px solid var(--border);font-size:11px;color:var(--text3)}
/* MAIN */
.main{flex:1;display:flex;flex-direction:column;min-width:0;overflow:hidden}
.topbar{padding:12px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;background:var(--surface);position:sticky;top:0;z-index:10}
.topbar-title{font-size:15px;font-weight:500}
.content{flex:1;padding:18px 20px;overflow-y:auto}
/* STATS */
.sg4{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:10px;margin-bottom:16px}
.sg5{display:grid;grid-template-columns:repeat(5,minmax(0,1fr));gap:10px;margin-bottom:16px}
.sc{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:13px 15px}
.sl{font-size:11px;color:var(--text2);margin-bottom:3px}
.sv{font-size:20px;font-weight:600;color:var(--text)}
.ss{font-size:11px;color:var(--text2);margin-top:3px}
/* CARD */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);overflow:hidden;margin-bottom:14px}
.ch{padding:11px 16px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;background:var(--surface2)}
.ct{font-size:13px;font-weight:500}
/* TABLE */
table{width:100%;border-collapse:collapse;font-size:12px}
th{background:var(--surface2);padding:8px 12px;text-align:right;font-weight:500;color:var(--text2);border-bottom:1px solid var(--border);font-size:11px}
td{padding:8px 12px;border-bottom:1px solid var(--border);color:var(--text)}
tr:last-child td{border-bottom:none}
tr:hover td{background:var(--bg)}
.tr-total td{font-weight:600;background:var(--surface2)}
/* BADGES */
.badge{display:inline-block;padding:2px 8px;border-radius:20px;font-size:11px;font-weight:500}
.b-ok{background:var(--green-bg);color:var(--green-text);border:1px solid var(--green-border)}
.b-low{background:var(--warn-bg);color:var(--warn-text);border:1px solid var(--orange-border)}
.b-out{background:var(--red-bg);color:var(--red-text);border:1px solid var(--red-border)}
.b-info{background:var(--blue-bg);color:var(--blue-text);border:1px solid var(--blue-border)}
.b-comm{background:var(--orange-bg);color:var(--orange-text);border:1px solid var(--orange-border);display:inline-block;padding:2px 8px;border-radius:20px;font-size:11px;font-weight:500}
/* BUTTONS */
.btn{padding:7px 14px;border-radius:var(--r);border:1px solid var(--border2);background:var(--surface);color:var(--text);cursor:pointer;font-size:12px;font-family:inherit;transition:background .12s}
.btn:hover{background:var(--bg2)}
.btn:disabled{opacity:.4;cursor:default}
.bp{background:var(--blue-bg);border-color:var(--blue-border);color:var(--blue-text)}
.bp:hover{opacity:.85}
.bs{background:var(--green-bg);border-color:var(--green-border);color:var(--green-text)}
.bs:hover{opacity:.85}
.bd{background:var(--red-bg);border-color:var(--red-border);color:var(--red-text)}
.bd:hover{opacity:.85}
.bsm{padding:3px 9px;font-size:11px}
/* MODAL */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.45);display:flex;align-items:center;justify-content:center;z-index:1000}
.modal-box{background:var(--surface);border-radius:var(--rl);border:1px solid var(--border);padding:22px;width:500px;max-width:96vw;max-height:90vh;overflow-y:auto;direction:rtl}
.mt{font-size:15px;font-weight:500;margin-bottom:15px}
.fg{margin-bottom:11px}
.fg label{font-size:12px;color:var(--text2);display:block;margin-bottom:4px}
.fg input,.fg select,.fg textarea{width:100%;padding:7px 10px;border-radius:var(--r);border:1px solid var(--border2);background:var(--bg);color:var(--text);font-size:13px;font-family:inherit;outline:none;transition:border-color .15s}
.fg input:focus,.fg select:focus{border-color:var(--blue-border)}
.fr{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.ma{display:flex;gap:8px;margin-top:14px}
/* RETURN TABLE INPUTS */
.ni2{width:68px!important;padding:5px 6px!important;text-align:center;border:1px solid var(--border2);border-radius:var(--r);background:var(--bg);color:var(--text);font-family:inherit;font-size:13px;outline:none}
.ni2:focus{border-color:var(--blue-border)}
.sc2{font-weight:600;font-size:13px;color:var(--green-text)}
.sc2.z{color:var(--red-text)}
/* RETURN SUMMARY */
.rsum{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r);padding:12px 15px;margin-top:10px;display:grid;grid-template-columns:repeat(4,1fr);gap:10px;text-align:center}
.rl2{font-size:11px;color:var(--text2);margin-bottom:2px}
.rv2{font-size:17px;font-weight:600}
/* MISC */
.empty{text-align:center;padding:28px;color:var(--text3);font-size:13px}
.tc2{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.tu{color:var(--green-text);font-size:11px;font-weight:500}
.td2{color:var(--red-text);font-size:11px;font-weight:500}
.pb{background:var(--bg2);border-radius:20px;height:5px;margin-top:4px;overflow:hidden}
.pbf{height:100%;border-radius:20px;background:#378ADD}
.wn{display:flex;align-items:center;gap:8px}
.wl{font-size:12px;font-weight:500;min-width:150px;text-align:center;color:var(--text)}
/* BAR CHART */
.bar-chart{display:flex;align-items:flex-end;gap:6px;height:130px;border-bottom:1px solid var(--border);padding:0 4px}
.bc2{display:flex;flex-direction:column;align-items:center;flex:1;min-width:32px}
.bv2{font-size:9px;color:var(--text3);margin-bottom:2px;text-align:center}
.bar{width:100%;border-radius:3px 3px 0 0;min-height:2px}
.br{background:#378ADD}.bp2{background:#1D9E75}
.bd2{font-size:10px;color:var(--text2);margin-top:5px;text-align:center}
.cw{padding:14px}
/* DATE RANGE */
.drange{display:flex;align-items:center;gap:8px;flex-wrap:wrap;background:var(--surface2);border:1px solid var(--border);border-radius:var(--r);padding:10px 14px;margin-bottom:14px}
.drange input[type=date]{padding:6px 10px;border-radius:var(--r);border:1px solid var(--border2);background:var(--bg);color:var(--text);font-size:12px;font-family:inherit;outline:none}
.drange input[type=date]:focus{border-color:var(--blue-border)}
/* INVOICE */
.inv-page{max-width:680px;margin:0 auto}
.inv-wrap{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:28px;margin-bottom:16px}
.inv-hdr{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:18px;padding-bottom:14px;border-bottom:1px solid var(--border)}
.inv-company{font-size:20px;font-weight:600;color:var(--text)}
.inv-sub{font-size:12px;color:var(--text2);margin-top:3px}
.inv-meta{text-align:left;font-size:12px;color:var(--text2);line-height:1.8}
.inv-meta b{color:var(--text)}
.inv-info{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r);padding:12px 15px;margin-bottom:16px;display:grid;grid-template-columns:repeat(4,1fr);gap:10px}
.ifl{font-size:10px;color:var(--text2);margin-bottom:2px}
.ifv{font-size:13px;font-weight:500}
.inv-tbl{width:100%;border-collapse:collapse;font-size:12px;margin-bottom:16px}
.inv-tbl th{padding:9px 12px;text-align:right;font-weight:500;font-size:11px;color:var(--text2);border-bottom:2px solid var(--border2);background:var(--surface2)}
.inv-tbl td{padding:9px 12px;border-bottom:1px solid var(--border)}
.inv-tbl .itr td{font-weight:600;background:var(--surface2);border-top:2px solid var(--border2)}
.inv-comm{background:var(--orange-bg);border:1px solid var(--orange-border);border-radius:var(--r);padding:12px 15px;margin-bottom:16px}
.inv-footer{display:flex;justify-content:space-between;padding-top:14px;border-top:1px solid var(--border)}
.sb{text-align:center;width:140px}
.sl2{height:1px;background:var(--border2);margin-bottom:5px;margin-top:40px}
.sl3{font-size:11px;color:var(--text2)}
.inv-act{display:flex;gap:8px;margin-bottom:14px}
/* PRINT */
@media print{
  .sidebar,.topbar,.inv-act,.no-print{display:none!important}
  .main{display:block}
  .content{padding:0}
  body{background:#fff}
  .inv-wrap{border:none;padding:10px}
  .inv-tbl th{background:#f0f0f0}
  .inv-tbl .itr td{background:#f0f0f0}
  .inv-comm{background:#fff8ee;border:1px solid #ccc}
  .inv-footer{display:flex!important}
}
@media(max-width:700px){
  .sidebar{display:none}
  .sg4,.sg5{grid-template-columns:repeat(2,1fr)}
  .tc2{grid-template-columns:1fr}
  .inv-info{grid-template-columns:1fr 1fr}
  .inv-footer{flex-wrap:wrap;gap:14px}
}
</style>
</head>
<body>
<div class="app">
  <!-- SIDEBAR -->
  <div class="sidebar">
    <div class="logo">
      <div class="logo-title">🧂 شيبس ديبو</div>
      <div class="logo-sub">إدارة المستودع والتوزيع</div>
    </div>
    <nav class="nav">
      <div class="nav-sec">العمليات اليومية</div>
      <div class="ni active" onclick="nav('dash',this)">📊 لوحة اليوم</div>
      <div class="ni" onclick="nav('stock',this)">📦 المخزون</div>
      <div class="ni" onclick="nav('workers',this)">👷 العمال والسائقون</div>
      <div class="ni" onclick="nav('trucks',this)">🚛 الشاحنات</div>
      <div class="ni" onclick="nav('dispatch',this)">🔄 تحميل الشاحنات</div>
      <div class="ni" onclick="nav('returns',this)">↩️ تسجيل العودة</div>
      <div class="nav-sec">التقارير</div>
      <div class="ni" onclick="nav('daily',this)">📋 تقرير يومي</div>
      <div class="ni" onclick="nav('weekly',this)">📅 تقرير أسبوعي</div>
      <div class="ni" onclick="nav('monthly',this)">🗓️ تقرير شهري / مخصص</div>
      <div class="ni" onclick="nav('staffrep',this)">👥 تقرير العمال</div>
    </nav>
    <div class="sidebar-footer">
      <div id="save-indicator" style="color:#4a7c28;font-size:11px;margin-bottom:8px"></div>
      <div id="tlbl" style="margin-bottom:10px"></div>
      <div style="display:flex;flex-direction:column;gap:5px">
        <button onclick="exportData()" style="padding:5px 8px;border-radius:6px;border:1px solid rgba(0,0,0,.15);background:#e6f1fb;color:#0c447c;font-size:11px;cursor:pointer;font-family:inherit;text-align:right">💾 تصدير نسخة احتياطية</button>
        <label style="padding:5px 8px;border-radius:6px;border:1px solid rgba(0,0,0,.15);background:#eaf3de;color:#27500a;font-size:11px;cursor:pointer;display:block">
          📂 استيراد نسخة احتياطية
          <input type="file" accept=".json" onchange="importData(this)" style="display:none">
        </label>
        <button onclick="resetAllData()" style="padding:5px 8px;border-radius:6px;border:1px solid rgba(200,0,0,.2);background:#fcebeb;color:#791f1f;font-size:11px;cursor:pointer;font-family:inherit;text-align:right">🗑️ إعادة تعيين البيانات</button>
      </div>
    </div>
  </div>

  <!-- MAIN -->
  <div class="main">
    <div class="topbar no-print">
      <span id="ptitle" class="topbar-title">لوحة اليوم</span>
      <div id="tbbtns" style="display:flex;gap:7px"></div>
    </div>
    <div class="content" id="content"></div>
  </div>
</div>

<!-- MODAL -->
<div id="modal" style="display:none"></div>

<script>
/* ═══════════════════════════════════════
   CONSTANTS & HELPERS
═══════════════════════════════════════ */
const DAYSAR=['الأحد','الاثنين','الثلاثاء','الأربعاء','الخميس','الجمعة','السبت'];
const MONSAR=['يناير','فبراير','مارس','أبريل','مايو','يونيو','يوليو','أغسطس','سبتمبر','أكتوبر','نوفمبر','ديسمبر'];
const NOW=new Date();
const TODAYISO=NOW.toISOString().split('T')[0];
document.getElementById('tlbl').textContent=NOW.toLocaleDateString('ar-DZ',{weekday:'short',year:'numeric',month:'short',day:'numeric'});

function fmtMoney(n){return Math.round(n).toLocaleString('ar-DZ')+' دج';}
function chgPct(a,b){return b>0?Math.round((a-b)/b*100):0;}
function trendBadge(v){
  if(v===0)return'<span style="font-size:10px;color:#888">= السابق</span>';
  return v>0?`<span class="tu">▲${v}%</span>`:`<span class="td2">▼${Math.abs(v)}%</span>`;
}
function getProd(id){return products.find(p=>p.id===id);}
function getWorker(id){return workers.find(w=>w.id===id);}
function getTruck(id){return trucks.find(t=>t.id===id);}
function getReturn(did){return returns.find(r=>r.dispatchId===did);}

/* ═══════════════════════════════════════
   localStorage — حفظ وتحميل تلقائي
═══════════════════════════════════════ */
const LS_KEY='chips_depot_v1';

const DEFAULT_DATA={
  products:[
    {id:1,name:'شيبس عادي مملح',  buyP:45, sellP:60,  stock:500,minStock:100,commRate:2},
    {id:2,name:'شيبس بالجبن',      buyP:45, sellP:60,  stock:380,minStock:100,commRate:2},
    {id:3,name:'شيبس حار',         buyP:50, sellP:70,  stock:250,minStock:80, commRate:3},
    {id:4,name:'شيبس كبير عادي',  buyP:90, sellP:120, stock:200,minStock:50, commRate:4},
    {id:5,name:'شيبس كبير بالجبن',buyP:90, sellP:120, stock:150,minStock:50, commRate:4},
    {id:6,name:'بطاطس مجففة',      buyP:30, sellP:45,  stock:600,minStock:150,commRate:1},
  ],
  workers:[
    {id:1,name:'أمين بلحسن', role:'worker'},
    {id:2,name:'يوسف مصطفى',role:'worker'},
    {id:3,name:'رضا قاسم',   role:'worker'},
    {id:4,name:'محمد أحمد',  role:'driver'},
    {id:5,name:'علي محمود',  role:'driver'},
    {id:6,name:'كريم بوسعيد',role:'driver'},
  ],
  trucks:[
    {id:1,name:'شاحنة 1',plate:'16-ALG-001'},
    {id:2,name:'شاحنة 2',plate:'16-ALG-002'},
    {id:3,name:'شاحنة 3',plate:'09-BLI-015'},
  ],
  dispatches:[],
  returns:[],
  nextPid:7,nextWid:7,nextTid:4,nextDid:1
};

function loadData(){
  try{
    const raw=localStorage.getItem(LS_KEY);
    if(!raw)return DEFAULT_DATA;
    return JSON.parse(raw);
  }catch(e){return DEFAULT_DATA;}
}

function saveData(){
  try{
    localStorage.setItem(LS_KEY,JSON.stringify({
      products,workers,trucks,dispatches,returns,
      nextPid,nextWid,nextTid,nextDid
    }));
  }catch(e){console.warn('localStorage full',e);}
}

/* تحميل البيانات */
const _d=loadData();
let products=_d.products;
let workers=_d.workers;
let trucks=_d.trucks;
let dispatches=_d.dispatches;
let returns=_d.returns;
let nextPid=_d.nextPid,nextWid=_d.nextWid,nextTid=_d.nextTid,nextDid=_d.nextDid;

let currentView='dash';
let weekOff=0,monthOff=0,customFrom='',customTo='';

/* ═══════════════════════════════════════
   CALC
═══════════════════════════════════════ */
function calcDispatch(d){
  const r=getReturn(d.id);
  let loaded=0,sold=0,ret=0,dmg=0,rev=0,profit=0,comm=0;
  d.items.forEach(it=>{
    const p=getProd(it.productId);if(!p)return;
    const ri=r?r.items.find(x=>x.productId===it.productId):null;
    const rt2=ri?ri.returned:0,dm2=ri?ri.damaged:0;
    const sl=r?Math.max(0,it.loaded-rt2-dm2):0;
    loaded+=it.loaded;sold+=sl;ret+=rt2;dmg+=dm2;
    rev+=sl*p.sellP;profit+=sl*(p.sellP-p.buyP);comm+=sl*p.commRate;
  });
  return{loaded,sold,ret,dmg,rev,profit,comm,done:!!r};
}
function calcPeriod(dispList){
  let loaded=0,sold=0,ret=0,dmg=0,rev=0,profit=0,comm=0;
  dispList.forEach(d=>{const c=calcDispatch(d);loaded+=c.loaded;sold+=c.sold;ret+=c.ret;dmg+=c.dmg;rev+=c.rev;profit+=c.profit;comm+=c.comm;});
  return{loaded,sold,ret,dmg,rev,profit,comm};
}
function dispsByDate(from,to){return dispatches.filter(d=>d.date>=from&&d.date<=to);}
function todayDisps(){return dispatches.filter(d=>d.date===TODAYISO);}

/* ═══════════════════════════════════════
   NAVIGATION
═══════════════════════════════════════ */
function nav(view,el){
  document.querySelectorAll('.ni').forEach(n=>n.classList.remove('active'));
  el.classList.add('active');
  currentView=view;
  const titles={dash:'لوحة اليوم',stock:'المخزون',workers:'العمال والسائقون',trucks:'الشاحنات',
    dispatch:'تحميل الشاحنات',returns:'تسجيل العودة',daily:'التقرير اليومي',
    weekly:'التقرير الأسبوعي',monthly:'تقرير شهري / مخصص',staffrep:'تقرير العمال والسائقين'};
  document.getElementById('ptitle').textContent=titles[view]||view;
  const tb=document.getElementById('tbbtns');tb.innerHTML='';
  if(view==='stock')  tb.innerHTML='<button class="btn bp" onclick="openAddProduct()">+ منتج جديد</button>';
  if(view==='workers')tb.innerHTML='<button class="btn bp" onclick="openAddWorker()">+ عامل / سائق</button>';
  if(view==='trucks') tb.innerHTML='<button class="btn bp" onclick="openAddTruck()">+ شاحنة</button>';
  if(['weekly','monthly','staffrep'].includes(view))tb.innerHTML='<button class="btn bp" onclick="window.print()">🖨️ طباعة</button>';
  render();
}
function render(){
  saveData();
  updateSaveIndicator();
  const c=document.getElementById('content');
  const v=currentView;
  if(v==='dash')    c.innerHTML=rDash();
  else if(v==='stock')   c.innerHTML=rStock();
  else if(v==='workers') c.innerHTML=rWorkers();
  else if(v==='trucks')  c.innerHTML=rTrucks();
  else if(v==='dispatch')c.innerHTML=rDispatch();
  else if(v==='returns') c.innerHTML=rReturns();
  else if(v==='daily')   c.innerHTML=rDaily();
  else if(v==='weekly')  c.innerHTML=rWeekly();
  else if(v==='monthly') c.innerHTML=rMonthly();
  else if(v==='staffrep')c.innerHTML=rStaffRep();
}

function updateSaveIndicator(){
  const el=document.getElementById('save-indicator');
  if(!el)return;
  const now=new Date();
  el.textContent='محفوظ '+now.toLocaleTimeString('ar-DZ');
}

function resetAllData(){
  if(!confirm('هل تريد حذف جميع البيانات والعودة للبيانات الافتراضية؟\nلا يمكن التراجع عن هذا الإجراء.'))return;
  localStorage.removeItem(LS_KEY);
  location.reload();
}

function exportData(){
  const data=JSON.stringify({products,workers,trucks,dispatches,returns,nextPid,nextWid,nextTid,nextDid},null,2);
  const blob=new Blob([data],{type:'application/json'});
  const a=document.createElement('a');
  a.href=URL.createObjectURL(blob);
  a.download='chips_depot_backup_'+TODAYISO+'.json';
  a.click();
}

function importData(input){
  const file=input.files[0];if(!file)return;
  const reader=new FileReader();
  reader.onload=e=>{
    try{
      const d=JSON.parse(e.target.result);
      if(!d.products||!d.trucks){alert('الملف غير صحيح');return;}
      products=d.products;workers=d.workers;trucks=d.trucks;
      dispatches=d.dispatches;returns=d.returns;
      nextPid=d.nextPid;nextWid=d.nextWid;nextTid=d.nextTid;nextDid=d.nextDid;
      saveData();alert('تم استيراد البيانات بنجاح');render();
    }catch(e){alert('خطأ في قراءة الملف');}
  };
  reader.readAsText(file);
}

/* ═══════════════════════════════════════
   DASHBOARD
═══════════════════════════════════════ */
function rDash(){
  const td=todayDisps();
  const{rev,profit}=calcPeriod(td);
  const ts=products.reduce((a,p)=>a+p.stock,0);
  const alerts=products.filter(p=>p.stock<=p.minStock);
  return`
  <div class="sg4">
    <div class="sc"><div class="sl">المخزون الكلي</div><div class="sv">${ts.toLocaleString()}</div><div class="ss">كيس</div></div>
    <div class="sc"><div class="sl">شاحنات خرجت اليوم</div><div class="sv" style="color:var(--blue-text)">${td.length}</div><div class="ss">من ${trucks.length} شاحنة</div></div>
    <div class="sc"><div class="sl">إيرادات اليوم</div><div class="sv" style="color:var(--green-text)">${fmtMoney(rev)}</div></div>
    <div class="sc"><div class="sl">ربح صافي اليوم</div><div class="sv" style="color:var(--green-text)">${fmtMoney(profit)}</div></div>
  </div>
  <div class="tc2">
    <div class="card"><div class="ch"><span class="ct">حالة الشاحنات اليوم</span></div>
    ${td.length===0?'<div class="empty">لم تخرج شاحنات بعد</div>':`
    <table><thead><tr><th>الشاحنة</th><th>العامل</th><th>السائق</th><th>الحالة</th><th>مُباع</th></tr></thead><tbody>
    ${td.map(d=>{const c=calcDispatch(d);const t=getTruck(d.truckId);const w=getWorker(d.workerId);const dr=getWorker(d.driverId);
      return`<tr><td style="font-weight:500">${t?t.name:''}</td><td>${w?w.name:''}</td><td>${dr?dr.name:''}</td>
      <td><span class="badge ${c.done?'b-ok':'b-info'}">${c.done?'عادت':'في الطريق'}</span></td>
      <td style="color:var(--green-text);font-weight:500">${c.sold}</td></tr>`;}).join('')}
    </tbody></table>`}
    </div>
    <div class="card"><div class="ch"><span class="ct">تنبيهات المخزون</span></div>
    ${alerts.length===0?'<div class="empty">✅ المخزون جيد</div>':`
    <table><thead><tr><th>المنتج</th><th>المتبقي</th><th>الحالة</th></tr></thead><tbody>
    ${alerts.map(p=>`<tr><td>${p.name}</td><td><b>${p.stock}</b></td>
    <td><span class="badge ${p.stock===0?'b-out':'b-low'}">${p.stock===0?'نفد المخزون':'منخفض'}</span></td></tr>`).join('')}
    </tbody></table>`}
    </div>
  </div>`;
}

/* ═══════════════════════════════════════
   STOCK
═══════════════════════════════════════ */
function rStock(){
  return`<div class="card"><table>
  <thead><tr><th>المنتج</th><th>الكمية</th><th>سعر الشراء</th><th>سعر البيع</th><th>هامش الربح</th><th>عمولة/كيس</th><th>الحالة</th><th>إجراءات</th></tr></thead>
  <tbody>${products.map(p=>{const st=p.stock===0?'b-out':p.stock<=p.minStock?'b-low':'b-ok';
    return`<tr>
      <td style="font-weight:500">${p.name}</td>
      <td><b style="font-size:15px">${p.stock}</b> كيس</td>
      <td>${p.buyP.toLocaleString()} دج</td>
      <td>${p.sellP.toLocaleString()} دج</td>
      <td style="color:var(--green-text);font-weight:500">+${p.sellP-p.buyP} دج</td>
      <td><span class="b-comm">${p.commRate} دج/كيس</span></td>
      <td><span class="badge ${st}">${p.stock===0?'نفد':p.stock<=p.minStock?'منخفض':'جيد'}</span></td>
      <td><div style="display:flex;gap:4px">
        <button class="btn bsm" onclick="openEditProduct(${p.id})">تعديل</button>
        <button class="btn bsm bs" onclick="openRestock(${p.id})">+ تموين</button>
        <button class="btn bsm bd" onclick="delProduct(${p.id})">حذف</button>
      </div></td>
    </tr>`;}).join('')}</tbody></table></div>`;
}

/* ═══════════════════════════════════════
   WORKERS
═══════════════════════════════════════ */
function rWorkers(){
  const ws=workers.filter(w=>w.role==='worker');
  const ds=workers.filter(w=>w.role==='driver');
  return`<div class="tc2">
    <div class="card"><div class="ch"><span class="ct">العمال (${ws.length})</span></div>
    <table><thead><tr><th>الاسم</th><th>الدور</th><th>إجراءات</th></tr></thead><tbody>
    ${ws.map(w=>`<tr><td style="font-weight:500">${w.name}</td><td><span class="badge b-info">عامل</span></td>
    <td><div style="display:flex;gap:4px"><button class="btn bsm" onclick="openEditWorker(${w.id})">تعديل</button>
    <button class="btn bsm bd" onclick="delWorker(${w.id})">حذف</button></div></td></tr>`).join('')}
    </tbody></table></div>
    <div class="card"><div class="ch"><span class="ct">السائقون (${ds.length})</span></div>
    <table><thead><tr><th>الاسم</th><th>الدور</th><th>إجراءات</th></tr></thead><tbody>
    ${ds.map(w=>`<tr><td style="font-weight:500">${w.name}</td><td><span class="badge b-ok">سائق</span></td>
    <td><div style="display:flex;gap:4px"><button class="btn bsm" onclick="openEditWorker(${w.id})">تعديل</button>
    <button class="btn bsm bd" onclick="delWorker(${w.id})">حذف</button></div></td></tr>`).join('')}
    </tbody></table></div>
  </div>`;
}

/* ═══════════════════════════════════════
   TRUCKS
═══════════════════════════════════════ */
function rTrucks(){
  return`<div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px">
  ${trucks.map(t=>`<div style="background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:14px">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <div><div style="font-weight:500;font-size:14px">🚛 ${t.name}</div>
      <div style="font-size:12px;color:var(--text2);margin-top:3px">${t.plate}</div></div>
      <div style="display:flex;gap:4px">
        <button class="btn bsm" onclick="openEditTruck(${t.id})">تعديل</button>
        <button class="btn bsm bd" onclick="delTruck(${t.id})">حذف</button>
      </div>
    </div>
  </div>`).join('')}</div>`;
}

/* ═══════════════════════════════════════
   DISPATCH
═══════════════════════════════════════ */
function rDispatch(){
  const todayD=dispatches.filter(d=>d.date===TODAYISO);
  const usedT=todayD.map(d=>d.truckId);
  const freeTrucks=trucks.filter(t=>!usedT.includes(t.id));
  const wW=workers.filter(w=>w.role==='worker');
  const wD=workers.filter(w=>w.role==='driver');
  return`
  ${freeTrucks.length>0?`<div class="card" style="margin-bottom:14px">
    <div class="ch"><span class="ct">تحميل شاحنة جديدة</span></div>
    <div style="padding:14px 16px">
      <div class="fr" style="margin-bottom:10px">
        <div class="fg"><label>الشاحنة</label><select id="d-truck">${freeTrucks.map(t=>`<option value="${t.id}">${t.name} — ${t.plate}</option>`).join('')}</select></div>
        <div></div>
      </div>
      <div class="fr" style="margin-bottom:14px">
        <div class="fg"><label>👷 العامل المرافق</label><select id="d-worker">${wW.map(w=>`<option value="${w.id}">${w.name}</option>`).join('')}</select></div>
        <div class="fg"><label>🚛 السائق</label><select id="d-driver">${wD.map(w=>`<option value="${w.id}">${w.name}</option>`).join('')}</select></div>
      </div>
      <table>
        <thead><tr><th>المنتج</th><th>الكمية في المخزون</th><th>كمية التحميل</th><th>عمولة/كيس</th></tr></thead>
        <tbody>${products.map(p=>`<tr>
          <td style="font-weight:500">${p.name}</td>
          <td><b>${p.stock}</b> كيس</td>
          <td><input type="number" min="0" max="${p.stock}" value="0" id="dp-${p.id}" class="ni2" style="width:80px"></td>
          <td><span class="b-comm">${p.commRate} دج</span></td>
        </tr>`).join('')}</tbody>
      </table>
      <div style="margin-top:14px">
        <button class="btn bp" onclick="saveDispatch()">✅ تأكيد التحميل والإرسال</button>
      </div>
    </div>
  </div>`:'<div class="empty" style="background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);margin-bottom:14px">جميع الشاحنات خرجت اليوم</div>'}
  ${todayD.length>0?`<div class="card">
    <div class="ch"><span class="ct">شاحنات اليوم</span></div>
    <table><thead><tr><th>الشاحنة</th><th>العامل</th><th>السائق</th><th>محمل</th><th>الحالة</th><th>فاتورة</th></tr></thead>
    <tbody>${todayD.map(d=>{const t=getTruck(d.truckId);const w=getWorker(d.workerId);const dr=getWorker(d.driverId);const c=calcDispatch(d);
      return`<tr>
        <td style="font-weight:500">${t?t.name:''}</td>
        <td>${w?w.name:''}</td><td>${dr?dr.name:''}</td>
        <td>${c.loaded} كيس</td>
        <td><span class="badge ${c.done?'b-ok':'b-info'}">${c.done?'عادت':'في الطريق'}</span></td>
        <td><button class="btn bsm bp" onclick="showInvoice(${d.id})">🖨️ فاتورة</button></td>
      </tr>`;}).join('')}
    </tbody></table>
  </div>`:''}`;
}

/* ═══════════════════════════════════════
   RETURNS  ← الإصلاح هنا
═══════════════════════════════════════ */
function rReturns(){
  const pending=dispatches.filter(d=>d.date===TODAYISO&&!getReturn(d.id));
  const done   =dispatches.filter(d=>d.date===TODAYISO&& getReturn(d.id));
  return`
  ${pending.length>0?`<div class="card" style="margin-bottom:14px">
    <div class="ch"><span class="ct">تسجيل عودة شاحنة</span></div>
    <div style="padding:14px 16px">
      <div class="fg"><label>اختر الشاحنة العائدة</label>
        <select id="ret-sel" onchange="buildRetTbl()">${pending.map(d=>{
          const t=getTruck(d.truckId);const w=getWorker(d.workerId);
          return`<option value="${d.id}">${t?t.name:''} — ${w?w.name:''}</option>`;}).join('')}
        </select>
      </div>
      <div id="ret-tbl"></div>
      <div id="ret-sum" class="rsum" style="display:none">
        <div><div class="rl2">محمل</div><div class="rv2" id="rs-l">0</div></div>
        <div><div class="rl2">مُباع</div><div class="rv2" style="color:var(--green-text)" id="rs-s">0</div></div>
        <div><div class="rl2">مرتجع للمخزون</div><div class="rv2" style="color:var(--blue-text)" id="rs-r">0</div></div>
        <div><div class="rl2">عمولة الفريق</div><div class="rv2" style="color:var(--orange-text)" id="rs-c">0 دج</div></div>
      </div>
      <div style="margin-top:12px;display:flex;gap:8px;align-items:center">
        <button class="btn bs" onclick="saveReturn()">✅ تأكيد العودة وتحديث المخزون</button>
        <span style="font-size:11px;color:var(--text2)">المرتجع يُضاف للمخزون — التالف لا يُضاف</span>
      </div>
    </div>
  </div>`:'<div class="empty" style="background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);margin-bottom:14px">لا توجد شاحنات في الطريق حالياً</div>'}
  ${done.length>0?`<div class="card">
    <div class="ch"><span class="ct">شاحنات عادت اليوم</span></div>
    <table><thead><tr><th>الشاحنة</th><th>العامل</th><th>السائق</th><th>محمل</th><th>مُباع</th><th>مرتجع</th><th>تالف</th><th>إيراد</th><th>ربح</th><th>عمولة الفريق</th></tr></thead>
    <tbody>${done.map(d=>{
      const t=getTruck(d.truckId);const w=getWorker(d.workerId);const dr=getWorker(d.driverId);const c=calcDispatch(d);
      return`<tr>
        <td style="font-weight:500">${t?t.name:''}</td><td>${w?w.name:''}</td><td>${dr?dr.name:''}</td>
        <td>${c.loaded}</td>
        <td style="color:var(--green-text);font-weight:500">${c.sold}</td>
        <td style="color:var(--blue-text)">${c.ret}</td>
        <td style="color:var(--red-text)">${c.dmg}</td>
        <td style="font-weight:500">${fmtMoney(c.rev)}</td>
        <td style="color:var(--green-text)">${fmtMoney(c.profit)}</td>
        <td><span class="b-comm">${fmtMoney(c.comm)}</span></td>
      </tr>`;}).join('')}
    </tbody></table>
  </div>`:''}`;
}

function buildRetTbl(){
  const sel=document.getElementById('ret-sel');
  if(!sel)return;
  const did=+sel.value;
  const d=dispatches.find(x=>x.id===did);
  if(!d){document.getElementById('ret-tbl').innerHTML='';return;}

  const rows=d.items.filter(i=>i.loaded>0).map(i=>{
    const p=getProd(i.productId);
    return`<tr>
      <td style="font-weight:500">${p?p.name:''}</td>
      <td><b>${i.loaded}</b></td>
      <td><input type="number" class="ni2" min="0" max="${i.loaded}" value="0"
          id="r-${i.productId}" oninput="recalcRet(${did})"></td>
      <td><input type="number" class="ni2" min="0" max="${i.loaded}" value="0"
          id="g-${i.productId}" oninput="recalcRet(${did})"></td>
      <td id="s-${i.productId}" class="sc2">${i.loaded}</td>
      <td id="cm-${i.productId}" style="color:var(--orange-text);font-size:12px">${i.loaded*(p?p.commRate:0)} دج</td>
    </tr>`;}).join('');

  document.getElementById('ret-tbl').innerHTML=`
    <table style="margin:10px 0">
      <thead><tr><th>المنتج</th><th>محمل</th><th>مرتجع</th><th>تالف</th><th>مُباع</th><th>عمولة</th></tr></thead>
      <tbody>${rows}</tbody>
    </table>`;
  document.getElementById('ret-sum').style.display='grid';
  recalcRet(did);
}

function recalcRet(did){
  const d=dispatches.find(x=>x.id===did);if(!d)return;
  let tL=0,tS=0,tR=0,tC=0;
  d.items.filter(i=>i.loaded>0).forEach(i=>{
    const p=getProd(i.productId);
    const re=document.getElementById('r-'+i.productId);
    const ge=document.getElementById('g-'+i.productId);
    const se=document.getElementById('s-'+i.productId);
    const ce=document.getElementById('cm-'+i.productId);
    if(!re||!ge||!se)return;
    /* تصحيح القيم */
    let r=Math.max(0,parseInt(re.value)||0);
    let g=Math.max(0,parseInt(ge.value)||0);
    if(r>i.loaded){r=i.loaded;re.value=r;}
    if(r+g>i.loaded){g=i.loaded-r;ge.value=g;}
    const s=i.loaded-r-g;
    /* تحديث الخلايا */
    se.textContent=s;
    se.className='sc2'+(s<=0?' z':'');
    const c=s*(p?p.commRate:0);
    if(ce)ce.textContent=c+' دج';
    tL+=i.loaded;tS+=s;tR+=r;tC+=c;
  });
  const L=document.getElementById('rs-l');
  const S=document.getElementById('rs-s');
  const R=document.getElementById('rs-r');
  const C=document.getElementById('rs-c');
  if(L)L.textContent=tL;
  if(S)S.textContent=tS;
  if(R)R.textContent=tR;
  if(C)C.textContent=fmtMoney(tC);
}

function saveReturn(){
  const sel=document.getElementById('ret-sel');
  if(!sel){alert('اختر شاحنة أولاً');return;}
  const did=+sel.value;
  const d=dispatches.find(x=>x.id===did);
  if(!d)return;
  const items=[];
  for(const i of d.items.filter(x=>x.loaded>0)){
    const retEl=document.getElementById('r-'+i.productId);
    const dmgEl=document.getElementById('g-'+i.productId);
    const r=Math.max(0,parseInt(retEl?retEl.value:0)||0);
    const g=Math.max(0,parseInt(dmgEl?dmgEl.value:0)||0);
    if(r+g>i.loaded){alert(`خطأ: الكميات تتجاوز المحمل في أحد المنتجات`);return;}
    items.push({productId:i.productId,returned:r,damaged:g});
  }
  /* ✅ تحديث المخزون — المرتجع فقط يعود */
  items.forEach(i=>{
    const p=getProd(i.productId);
    if(p)p.stock+=i.returned;
  });
  returns.push({dispatchId:did,items});
  render();
}

/* ═══════════════════════════════════════
   DAILY REPORT
═══════════════════════════════════════ */
function rDaily(){
  const td=todayDisps();
  const{loaded,sold,ret,dmg,rev,profit,comm}=calcPeriod(td);
  return`
  <div class="sg4">
    <div class="sc"><div class="sl">محمل</div><div class="sv">${loaded}</div><div class="ss">كيس</div></div>
    <div class="sc"><div class="sl">مُباع</div><div class="sv" style="color:var(--green-text)">${sold}</div><div class="ss">كيس</div></div>
    <div class="sc"><div class="sl">الإيرادات</div><div class="sv" style="color:var(--green-text)">${fmtMoney(rev)}</div></div>
    <div class="sc"><div class="sl">ربح صافي</div><div class="sv" style="color:var(--green-text)">${fmtMoney(profit)}</div></div>
  </div>
  <div class="card">
    <div class="ch"><span class="ct">تفصيل الشاحنات</span></div>
    <table><thead><tr><th>الشاحنة</th><th>العامل</th><th>السائق</th><th>محمل</th><th>مُباع</th><th>مرتجع</th><th>تالف</th><th>إيراد</th><th>ربح</th><th>عمولة الفريق</th></tr></thead>
    <tbody>${td.length===0?'<tr><td colspan="10"><div class="empty">لا توجد بيانات اليوم</div></td></tr>':
      td.map(d=>{const t=getTruck(d.truckId);const w=getWorker(d.workerId);const dr=getWorker(d.driverId);const c=calcDispatch(d);
        return`<tr>
          <td style="font-weight:500">${t?t.name:''}</td><td>${w?w.name:''}</td><td>${dr?dr.name:''}</td>
          <td>${c.loaded}</td><td style="color:var(--green-text);font-weight:500">${c.sold}</td>
          <td style="color:var(--blue-text)">${c.ret}</td><td style="color:var(--red-text)">${c.dmg}</td>
          <td>${fmtMoney(c.rev)}</td><td style="color:var(--green-text)">${fmtMoney(c.profit)}</td>
          <td><span class="b-comm">${fmtMoney(c.comm)}</span></td>
        </tr>`;}).join('')}
    </tbody></table>
  </div>`;
}

/* ═══════════════════════════════════════
   PERIOD REPORT (shared by weekly & monthly)
═══════════════════════════════════════ */
function periodReport(disps,cur,prv){
  const byDate={};
  disps.forEach(d=>{if(!byDate[d.date])byDate[d.date]=[];byDate[d.date].push(d);});
  const dates=Object.keys(byDate).sort();
  const maxRev=Math.max(...dates.map(dt=>calcPeriod(byDate[dt]).rev),1);
  const recent=dates.slice(-14);

  const bars=recent.map(dt=>{
    const c=calcPeriod(byDate[dt]);
    const rh=Math.max(2,Math.round(c.rev/maxRev*110));
    const ph=Math.max(2,Math.round(c.profit/maxRev*110));
    const isToday=dt===TODAYISO;
    const d2=new Date(dt);
    return`<div class="bc2">
      <div class="bv2">${Math.round(c.rev/1000)}k</div>
      <div style="display:flex;gap:2px;align-items:flex-end;height:110px">
        <div class="bar br" style="height:${rh}px;flex:1;opacity:${isToday?1:.75}"></div>
        <div class="bar bp2" style="height:${ph}px;flex:1;opacity:${isToday?1:.75}"></div>
      </div>
      <div class="bd2">${d2.getDate()}/${d2.getMonth()+1}${isToday?'<br><b>اليوم</b>':''}</div>
    </div>`;}).join('');

  const dayRows=dates.map(dt=>{
    const c=calcPeriod(byDate[dt]);const d2=new Date(dt);const isToday=dt===TODAYISO;
    return`<tr ${isToday?'style="background:var(--blue-bg)"':''}>
      <td style="font-weight:500">${DAYSAR[d2.getDay()]}${isToday?' ◀':''}</td>
      <td style="font-size:11px;color:var(--text2)">${dt}</td>
      <td>${byDate[dt].length}</td>
      <td>${c.loaded}</td>
      <td style="color:var(--green-text);font-weight:500">${c.sold}</td>
      <td style="color:var(--blue-text)">${c.ret}</td>
      <td style="color:var(--red-text)">${c.dmg}</td>
      <td style="font-weight:500">${fmtMoney(c.rev)}</td>
      <td style="color:var(--green-text)">${fmtMoney(c.profit)}</td>
      <td><span class="b-comm">${fmtMoney(c.comm)}</span></td>
    </tr>`;}).join('');

  return`
  <div class="sg5">
    <div class="sc"><div class="sl">الإيرادات</div><div class="sv" style="color:var(--green-text)">${fmtMoney(cur.rev)}</div><div class="ss">${trendBadge(chgPct(cur.rev,prv.rev))}</div></div>
    <div class="sc"><div class="sl">الربح الصافي</div><div class="sv" style="color:var(--green-text)">${fmtMoney(cur.profit)}</div><div class="ss">${trendBadge(chgPct(cur.profit,prv.profit))}</div></div>
    <div class="sc"><div class="sl">إجمالي المُباع</div><div class="sv">${cur.sold.toLocaleString()}</div><div class="ss">${trendBadge(chgPct(cur.sold,prv.sold))}</div></div>
    <div class="sc"><div class="sl">إجمالي المُحمَّل</div><div class="sv">${cur.loaded.toLocaleString()}</div><div class="ss">كيس</div></div>
    <div class="sc"><div class="sl">عمولة الفريق</div><div class="sv" style="color:var(--orange-text)">${fmtMoney(cur.comm)}</div><div class="ss">كامل الفترة</div></div>
  </div>
  ${recent.length>0?`<div class="card" style="margin-bottom:14px">
    <div class="ch"><span class="ct">الرسم البياني اليومي</span>
    <span style="font-size:11px;color:var(--text2)">أزرق = إيراد | أخضر = ربح</span></div>
    <div class="cw"><div class="bar-chart">${bars}</div></div>
  </div>`:''}
  <div class="card">
    <div class="ch"><span class="ct">تفصيل يومي</span></div>
    <table><thead><tr><th>اليوم</th><th>التاريخ</th><th>شاحنات</th><th>محمل</th><th>مُباع</th><th>مرتجع</th><th>تالف</th><th>إيراد</th><th>ربح</th><th>عمولة</th></tr></thead>
    <tbody>
      ${dayRows||'<tr><td colspan="10"><div class="empty">لا توجد بيانات في هذه الفترة</div></td></tr>'}
      ${dates.length>0?`<tr class="tr-total">
        <td colspan="2">الإجمالي</td><td>${disps.length}</td>
        <td>${cur.loaded}</td><td style="color:var(--green-text)">${cur.sold}</td>
        <td style="color:var(--blue-text)">${cur.ret}</td><td style="color:var(--red-text)">${cur.dmg}</td>
        <td>${fmtMoney(cur.rev)}</td><td style="color:var(--green-text)">${fmtMoney(cur.profit)}</td>
        <td><span class="b-comm">${fmtMoney(cur.comm)}</span></td>
      </tr>`:''}
    </tbody></table>
  </div>`;
}

/* ═══════════════════════════════════════
   WEEKLY REPORT
═══════════════════════════════════════ */
function getWeekRange(off){
  const d=new Date(NOW);const day=d.getDay();const diff=day===0?-6:1-day;
  d.setDate(d.getDate()+diff+off*7);
  const from=d.toISOString().split('T')[0];
  const to=new Date(d);to.setDate(d.getDate()+6);
  return{from,to:to.toISOString().split('T')[0]};
}
function fmtD(s){const d=new Date(s);return`${d.getDate()} ${MONSAR[d.getMonth()]}`;}

function rWeekly(){
  const{from,to}=getWeekRange(weekOff);
  const prev=getWeekRange(weekOff-1);
  const cur=calcPeriod(dispsByDate(from,to));
  const prv=calcPeriod(dispsByDate(prev.from,prev.to));
  return`
  <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;flex-wrap:wrap;gap:8px">
    <div style="font-size:13px;color:var(--text2)">${fmtD(from)} — ${fmtD(to)} ${new Date(to).getFullYear()}</div>
    <div class="wn">
      <button class="btn" onclick="weekOff--;render()">&#8250; الأسبوع السابق</button>
      <span class="wl">${weekOff===0?'الأسبوع الحالي':'أسبوع سابق'}</span>
      <button class="btn" ${weekOff>=0?'disabled':''} onclick="if(weekOff<0){weekOff++;render()}">الأسبوع التالي &#8249;</button>
    </div>
  </div>
  ${periodReport(dispsByDate(from,to),cur,prv)}`;
}

/* ═══════════════════════════════════════
   MONTHLY / CUSTOM REPORT
═══════════════════════════════════════ */
function getMonthRange(off){
  const d=new Date(NOW.getFullYear(),NOW.getMonth()+off,1);
  const from=d.toISOString().split('T')[0];
  const last=new Date(d.getFullYear(),d.getMonth()+1,0);
  return{from,to:last.toISOString().split('T')[0],label:`${MONSAR[d.getMonth()]} ${d.getFullYear()}`};
}

function rMonthly(){
  const useCustom=customFrom&&customTo&&customFrom<=customTo;
  let from,to,label;
  if(useCustom){from=customFrom;to=customTo;label=`${from} ← ${to}`;}
  else{const r=getMonthRange(monthOff);from=r.from;to=r.to;label=r.label;}
  const prev=getMonthRange(monthOff-1);
  const cur=calcPeriod(dispsByDate(from,to));
  const prv=useCustom?{rev:0,profit:0,sold:0}:calcPeriod(dispsByDate(prev.from,prev.to));

  return`
  <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;flex-wrap:wrap;gap:8px">
    <div style="font-size:14px;font-weight:500">${label}</div>
    ${!useCustom?`<div class="wn">
      <button class="btn" onclick="monthOff--;render()">&#8250; الشهر السابق</button>
      <span class="wl">${monthOff===0?'الشهر الحالي':'شهر سابق'}</span>
      <button class="btn" ${monthOff>=0?'disabled':''} onclick="if(monthOff<0){monthOff++;render()}">الشهر التالي &#8249;</button>
    </div>`:''}
  </div>
  <div class="drange">
    <span style="font-size:12px;font-weight:500">📅 نطاق مخصص:</span>
    <input type="date" id="cf" value="${customFrom||from}" max="${TODAYISO}">
    <span style="font-size:12px">إلى</span>
    <input type="date" id="ct" value="${customTo||to}" max="${TODAYISO}">
    <button class="btn bp" onclick="customFrom=document.getElementById('cf').value;customTo=document.getElementById('ct').value;render()">تطبيق الفترة</button>
    ${useCustom?`<button class="btn" onclick="customFrom='';customTo='';render()">❌ إلغاء</button>`:''}
  </div>
  ${periodReport(dispsByDate(from,to),cur,prv)}`;
}

/* ═══════════════════════════════════════
   STAFF REPORT
═══════════════════════════════════════ */
function rStaffRep(){
  const useCustom=customFrom&&customTo&&customFrom<=customTo;
  const{from,to}=useCustom?{from:customFrom,to:customTo}:getMonthRange(monthOff);
  const disps=dispsByDate(from,to);
  const stats={};
  workers.forEach(w=>{stats[w.id]={id:w.id,name:w.name,role:w.role,loaded:0,sold:0,ret:0,dmg:0,rev:0,comm:0,trips:0};});
  disps.forEach(d=>{
    const c=calcDispatch(d);
    [d.workerId,d.driverId].forEach(wid=>{
      if(!stats[wid])return;
      stats[wid].trips++;
      stats[wid].loaded+=c.loaded;stats[wid].sold+=c.sold;
      stats[wid].ret+=c.ret;stats[wid].dmg+=c.dmg;
      stats[wid].rev+=c.rev;stats[wid].comm+=c.comm/2;
    });
  });
  const all=Object.values(stats).sort((a,b)=>b.sold-a.sold);
  const wList=all.filter(s=>s.role==='worker');
  const dList=all.filter(s=>s.role==='driver');

  function tbl(list,title){
    const maxS=Math.max(...list.map(s=>s.sold),1);
    return`<div class="card" style="margin-bottom:14px"><div class="ch"><span class="ct">${title}</span></div>
    ${list.length===0?'<div class="empty">لا توجد بيانات</div>':`
    <table><thead><tr><th>#</th><th>الاسم</th><th>رحلات</th><th>كيس محمل</th><th>كيس مُباع</th><th>كيس مرتجع</th><th>نسبة البيع</th><th>إيراد الفريق</th><th>عمولته</th></tr></thead>
    <tbody>${list.map((s,i)=>{
      const pct=s.loaded>0?Math.round(s.sold/s.loaded*100):0;
      const bar=Math.round(s.sold/maxS*100);
      return`<tr>
        <td style="color:var(--text3)">${i+1}</td>
        <td style="font-weight:500">${s.name}</td>
        <td>${s.trips}</td>
        <td>${s.loaded.toLocaleString()}</td>
        <td>
          <div style="font-weight:600;color:var(--green-text)">${s.sold.toLocaleString()}</div>
          <div class="pb"><div class="pbf" style="width:${bar}%"></div></div>
        </td>
        <td style="color:var(--blue-text)">${s.ret}</td>
        <td>${pct}%</td>
        <td>${fmtMoney(s.rev)}</td>
        <td><span class="b-comm">${fmtMoney(Math.round(s.comm))}</span></td>
      </tr>`;}).join('')}
    </tbody></table>`}
    </div>`;
  }

  return`
  <div class="drange">
    <span style="font-size:12px;font-weight:500">📅 اختر الفترة:</span>
    <input type="date" id="sf" value="${from}" max="${TODAYISO}">
    <span style="font-size:12px">إلى</span>
    <input type="date" id="st" value="${to}" max="${TODAYISO}">
    <button class="btn bp" onclick="customFrom=document.getElementById('sf').value;customTo=document.getElementById('st').value;render()">تطبيق</button>
    ${useCustom?`<button class="btn" onclick="customFrom='';customTo='';render()">إلغاء</button>`:''}
  </div>
  ${tbl(wList,'🏆 أداء العمال')}
  ${tbl(dList,'🏆 أداء السائقين')}`;
}

/* ═══════════════════════════════════════
   INVOICE
═══════════════════════════════════════ */
function showInvoice(did){
  const d=dispatches.find(x=>x.id===did);if(!d)return;
  const t=getTruck(d.truckId);
  const w=getWorker(d.workerId);
  const dr=getWorker(d.driverId);
  const loaded=d.items.filter(i=>i.loaded>0);
  const tQty=loaded.reduce((a,i)=>a+i.loaded,0);
  const tVal=loaded.reduce((a,i)=>{const p=getProd(i.productId);return a+(p?p.sellP*i.loaded:0);},0);
  const tComm=loaded.reduce((a,i)=>{const p=getProd(i.productId);return a+(p?p.commRate*i.loaded:0);},0);
  const wComm=Math.round(tComm/2);const dComm=Math.round(tComm/2);

  /* نخفي الـ main ونظهر الفاتورة في نفس المكان */
  document.getElementById('content').innerHTML=`
  <div class="inv-page">
    <div class="inv-act no-print">
      <button class="btn bp" onclick="window.print()">🖨️ طباعة الفاتورة</button>
      <button class="btn" onclick="render()">← العودة</button>
    </div>
    <div class="inv-wrap">
      <div class="inv-hdr">
        <div>
          <div class="inv-company">🧂 مستودع شيبس ديبو</div>
          <div class="inv-sub">وثيقة تحميل وتوزيع</div>
        </div>
        <div class="inv-meta">
          <div>رقم الوثيقة: <b>INV-${String(did).padStart(4,'0')}</b></div>
          <div>التاريخ: <b>${d.date}</b></div>
          <div>الوقت: <b>${d.time||''}</b></div>
        </div>
      </div>
      <div class="inv-info">
        <div><div class="ifl">الشاحنة</div><div class="ifv">${t?t.name:''}</div></div>
        <div><div class="ifl">رقم اللوحة</div><div class="ifv">${t?t.plate:''}</div></div>
        <div><div class="ifl">👷 العامل</div><div class="ifv">${w?w.name:''}</div></div>
        <div><div class="ifl">🚛 السائق</div><div class="ifv">${dr?dr.name:''}</div></div>
      </div>
      <table class="inv-tbl">
        <thead><tr><th>#</th><th>المنتج</th><th>الكمية المحملة</th><th>سعر البيع</th><th>الإجمالي</th><th>عمولة/كيس</th><th>عمولة الفريق</th></tr></thead>
        <tbody>
          ${loaded.map((i,idx)=>{
            const p=getProd(i.productId);
            const tot=p?p.sellP*i.loaded:0;
            const comm=p?p.commRate*i.loaded:0;
            return`<tr>
              <td style="color:var(--text3)">${idx+1}</td>
              <td style="font-weight:500">${p?p.name:''}</td>
              <td style="text-align:center;font-weight:500">${i.loaded} كيس</td>
              <td>${p?p.sellP.toLocaleString():0} دج</td>
              <td style="font-weight:600">${tot.toLocaleString()} دج</td>
              <td><span class="b-comm">${p?p.commRate:0} دج</span></td>
              <td style="color:var(--orange-text);font-weight:500">${comm} دج</td>
            </tr>`;}).join('')}
          <tr class="itr">
            <td colspan="2" style="font-weight:600">الإجمالي</td>
            <td style="text-align:center;font-weight:600">${tQty} كيس</td>
            <td></td>
            <td style="color:var(--green-text);font-weight:600">${tVal.toLocaleString()} دج</td>
            <td></td>
            <td style="color:var(--orange-text);font-weight:600">${tComm} دج</td>
          </tr>
        </tbody>
      </table>
      <div class="inv-comm">
        <div style="font-size:13px;font-weight:600;color:var(--orange-text);margin-bottom:10px">💰 توزيع العمولة</div>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:14px">
          <div>
            <div style="font-size:12px;color:var(--orange-text)">عمولة العامل</div>
            <div style="font-size:13px;font-weight:500;color:var(--orange-text);margin-bottom:2px">${w?w.name:''}</div>
            <div style="font-size:22px;font-weight:700;color:var(--orange-text)">${fmtMoney(wComm)}</div>
          </div>
          <div>
            <div style="font-size:12px;color:var(--orange-text)">عمولة السائق</div>
            <div style="font-size:13px;font-weight:500;color:var(--orange-text);margin-bottom:2px">${dr?dr.name:''}</div>
            <div style="font-size:22px;font-weight:700;color:var(--orange-text)">${fmtMoney(dComm)}</div>
          </div>
        </div>
      </div>
      <div class="inv-footer">
        <div class="sb"><div class="sl2"></div><div class="sl3">توقيع المسؤول</div></div>
        <div class="sb"><div class="sl2"></div><div class="sl3">توقيع العامل<br>${w?w.name:''}</div></div>
        <div class="sb"><div class="sl2"></div><div class="sl3">توقيع السائق<br>${dr?dr.name:''}</div></div>
      </div>
    </div>
  </div>`;
}

/* ═══════════════════════════════════════
   MODALS
═══════════════════════════════════════ */
function showM(html){
  document.getElementById('modal').style.display='block';
  document.getElementById('modal').innerHTML=`<div class="modal-overlay">${html}</div>`;
}
function closeM(){
  document.getElementById('modal').style.display='none';
  document.getElementById('modal').innerHTML='';
}

/* DISPATCH */
function saveDispatch(){
  const tid=+document.getElementById('d-truck').value;
  const wid=+document.getElementById('d-worker').value;
  const did2=+document.getElementById('d-driver').value;
  const items=products.map(p=>({productId:p.id,loaded:Math.max(0,parseInt(document.getElementById('dp-'+p.id).value)||0)})).filter(i=>i.loaded>0);
  if(items.length===0){alert('أدخل كميات للتحميل');return;}
  for(const i of items){const p=getProd(i.productId);if(p&&i.loaded>p.stock){alert(`كمية "${p.name}" تتجاوز المخزون المتاح (${p.stock})`);return;}}
  items.forEach(i=>{const p=getProd(i.productId);if(p)p.stock-=i.loaded;});
  const did=nextDid++;
  dispatches.push({id:did,date:TODAYISO,truckId:tid,workerId:wid,driverId:did2,items,time:new Date().toLocaleTimeString('ar-DZ')});
  render();
  setTimeout(()=>showInvoice(did),50);
}

/* PRODUCT */
function openAddProduct(){showM(`<div class="modal-box">
  <div class="mt">إضافة منتج جديد</div>
  <div class="fg"><label>اسم المنتج</label><input id="m-n" placeholder="مثال: شيبس بالفلفل"></div>
  <div class="fr">
    <div class="fg"><label>سعر الشراء (دج)</label><input id="m-b" type="number" min="0"></div>
    <div class="fg"><label>سعر البيع (دج)</label><input id="m-s" type="number" min="0"></div>
  </div>
  <div class="fr">
    <div class="fg"><label>الكمية الحالية (كيس)</label><input id="m-q" type="number" min="0"></div>
    <div class="fg"><label>حد التنبيه (كيس)</label><input id="m-mn" type="number" min="0" value="50"></div>
  </div>
  <div class="fg"><label>عمولة العامل+السائق (دج/كيس مُباع) — تُقسَّم بالتساوي</label><input id="m-c" type="number" min="0" value="2"></div>
  <div class="ma">
    <button class="btn bp" onclick="saveNewProd()">حفظ</button>
    <button class="btn" onclick="closeM()">إلغاء</button>
  </div>
</div>`);}
function saveNewProd(){
  const n=document.getElementById('m-n').value.trim();if(!n){alert('أدخل اسم المنتج');return;}
  products.push({id:nextPid++,name:n,buyP:+document.getElementById('m-b').value,sellP:+document.getElementById('m-s').value,stock:+document.getElementById('m-q').value,minStock:+document.getElementById('m-mn').value,commRate:+document.getElementById('m-c').value});
  closeM();render();
}
function openEditProduct(id){
  const p=getProd(id);
  showM(`<div class="modal-box">
  <div class="mt">تعديل: ${p.name}</div>
  <div class="fg"><label>اسم المنتج</label><input id="m-n" value="${p.name}"></div>
  <div class="fr">
    <div class="fg"><label>سعر الشراء (دج)</label><input id="m-b" type="number" value="${p.buyP}"></div>
    <div class="fg"><label>سعر البيع (دج)</label><input id="m-s" type="number" value="${p.sellP}"></div>
  </div>
  <div class="fr">
    <div class="fg"><label>الكمية (كيس)</label><input id="m-q" type="number" value="${p.stock}"></div>
    <div class="fg"><label>حد التنبيه</label><input id="m-mn" type="number" value="${p.minStock}"></div>
  </div>
  <div class="fg"><label>عمولة العامل+السائق (دج/كيس)</label><input id="m-c" type="number" value="${p.commRate}"></div>
  <div class="ma">
    <button class="btn bp" onclick="saveEditProd(${id})">حفظ</button>
    <button class="btn" onclick="closeM()">إلغاء</button>
  </div>
</div>`);}
function saveEditProd(id){
  const p=getProd(id);
  p.name=document.getElementById('m-n').value.trim();
  p.buyP=+document.getElementById('m-b').value;p.sellP=+document.getElementById('m-s').value;
  p.stock=+document.getElementById('m-q').value;p.minStock=+document.getElementById('m-mn').value;
  p.commRate=+document.getElementById('m-c').value;
  closeM();render();
}
function openRestock(id){
  const p=getProd(id);
  showM(`<div class="modal-box">
  <div class="mt">تموين: ${p.name}</div>
  <div style="font-size:13px;color:var(--text2);margin-bottom:12px">المخزون الحالي: <b>${p.stock}</b> كيس</div>
  <div class="fg"><label>الكمية المضافة (كيس)</label><input id="m-q" type="number" value="100" min="1"></div>
  <div class="ma">
    <button class="btn bs" onclick="doRestock(${id})">إضافة للمخزون</button>
    <button class="btn" onclick="closeM()">إلغاء</button>
  </div>
</div>`);}
function doRestock(id){const q=+document.getElementById('m-q').value;if(q<1)return;getProd(id).stock+=q;closeM();render();}
function delProduct(id){if(confirm('حذف هذا المنتج نهائياً؟')){products=products.filter(x=>x.id!==id);render();}}

/* WORKER */
function openAddWorker(){showM(`<div class="modal-box">
  <div class="mt">إضافة عامل / سائق</div>
  <div class="fg"><label>الاسم الكامل</label><input id="m-n"></div>
  <div class="fg"><label>الدور</label><select id="m-r"><option value="worker">👷 عامل</option><option value="driver">🚛 سائق</option></select></div>
  <div class="ma">
    <button class="btn bp" onclick="saveNewWorker()">حفظ</button>
    <button class="btn" onclick="closeM()">إلغاء</button>
  </div>
</div>`);}
function saveNewWorker(){const n=document.getElementById('m-n').value.trim();if(!n)return;workers.push({id:nextWid++,name:n,role:document.getElementById('m-r').value});closeM();render();}
function openEditWorker(id){
  const w=getWorker(id);
  showM(`<div class="modal-box">
  <div class="mt">تعديل: ${w.name}</div>
  <div class="fg"><label>الاسم</label><input id="m-n" value="${w.name}"></div>
  <div class="fg"><label>الدور</label><select id="m-r">
    <option value="worker" ${w.role==='worker'?'selected':''}>👷 عامل</option>
    <option value="driver" ${w.role==='driver'?'selected':''}>🚛 سائق</option>
  </select></div>
  <div class="ma">
    <button class="btn bp" onclick="saveEditWorker(${id})">حفظ</button>
    <button class="btn" onclick="closeM()">إلغاء</button>
  </div>
</div>`);}
function saveEditWorker(id){const w=getWorker(id);w.name=document.getElementById('m-n').value.trim();w.role=document.getElementById('m-r').value;closeM();render();}
function delWorker(id){if(confirm('حذف هذا الشخص نهائياً؟')){workers=workers.filter(x=>x.id!==id);render();}}

/* TRUCK */
function openAddTruck(){showM(`<div class="modal-box">
  <div class="mt">إضافة شاحنة جديدة</div>
  <div class="fg"><label>اسم الشاحنة</label><input id="m-n" placeholder="مثال: شاحنة 4"></div>
  <div class="fg"><label>رقم اللوحة</label><input id="m-p" placeholder="مثال: 16-ALG-004"></div>
  <div class="ma">
    <button class="btn bp" onclick="saveNewTruck()">حفظ</button>
    <button class="btn" onclick="closeM()">إلغاء</button>
  </div>
</div>`);}
function saveNewTruck(){const n=document.getElementById('m-n').value.trim();if(!n)return;trucks.push({id:nextTid++,name:n,plate:document.getElementById('m-p').value.trim()});closeM();render();}
function openEditTruck(id){
  const t=getTruck(id);
  showM(`<div class="modal-box">
  <div class="mt">تعديل: ${t.name}</div>
  <div class="fg"><label>اسم الشاحنة</label><input id="m-n" value="${t.name}"></div>
  <div class="fg"><label>رقم اللوحة</label><input id="m-p" value="${t.plate}"></div>
  <div class="ma">
    <button class="btn bp" onclick="saveEditTruck(${id})">حفظ</button>
    <button class="btn" onclick="closeM()">إلغاء</button>
  </div>
</div>`);}
function saveEditTruck(id){const t=getTruck(id);t.name=document.getElementById('m-n').value.trim();t.plate=document.getElementById('m-p').value.trim();closeM();render();}
function delTruck(id){if(confirm('حذف هذه الشاحنة؟')){trucks=trucks.filter(x=>x.id!==id);render();}}

/* ═══════════════════════════════════════
   INIT
═══════════════════════════════════════ */
render();
// عرض مؤشر الحفظ عند البدء
updateSaveIndicator();
</script>
</body>
</html>
