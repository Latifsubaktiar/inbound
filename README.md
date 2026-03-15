# inbound
Kawan Lama
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Inbound Dashboard — NDC Sidoarjo</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
:root{
  --bg:#070b12;--bg2:#0c1220;--bg3:#111828;--bg4:#161f30;
  --border:rgba(56,217,245,0.07);--border2:rgba(56,217,245,0.18);
  --text:#dde8f8;--muted:#4a5f80;--muted2:#7a90b8;
  --cyan:#38d9f5;--cyan-dim:rgba(56,217,245,0.10);
  --gold:#f5c430;--gold-dim:rgba(245,196,48,0.10);
  --green:#1ed98a;--green-dim:rgba(30,217,138,0.10);
  --red:#ff4060;--red-dim:rgba(255,64,96,0.10);
  --blue:#4f8fff;--blue-dim:rgba(79,143,255,0.10);
  --orange:#ff8c42;--r:13px;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{font-family:'Outfit',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden}
body::before{
  content:'';position:fixed;inset:0;pointer-events:none;z-index:0;
  background:
    radial-gradient(ellipse 70% 50% at 10% 5%,rgba(56,217,245,0.035) 0%,transparent 65%),
    radial-gradient(ellipse 60% 40% at 90% 90%,rgba(79,143,255,0.035) 0%,transparent 65%),
    repeating-linear-gradient(0deg,transparent,transparent 47px,rgba(56,217,245,0.012) 48px),
    repeating-linear-gradient(90deg,transparent,transparent 47px,rgba(56,217,245,0.012) 48px);
}
.app{position:relative;z-index:1}

/* LOADER */
#loader{position:fixed;inset:0;background:var(--bg);display:flex;flex-direction:column;align-items:center;justify-content:center;z-index:999;transition:opacity .5s}
.ld-logo{font-family:'Bebas Neue',sans-serif;font-size:52px;color:var(--cyan);letter-spacing:.12em;text-shadow:0 0 40px rgba(56,217,245,.5);animation:lglow 1.5s ease-in-out infinite}
@keyframes lglow{0%,100%{text-shadow:0 0 40px rgba(56,217,245,.4)}50%{text-shadow:0 0 80px rgba(56,217,245,.9)}}
.ld-sub{font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--muted);margin-top:10px;letter-spacing:.08em}
.ld-bar{width:200px;height:2px;background:rgba(56,217,245,.08);border-radius:1px;margin-top:18px;overflow:hidden}
.ld-fill{height:100%;background:linear-gradient(90deg,var(--green),var(--cyan));border-radius:1px;animation:ldfill 1.3s ease forwards}
@keyframes ldfill{from{width:0}to{width:100%}}

/* HEADER */
header{display:flex;align-items:center;justify-content:space-between;padding:16px 32px;border-bottom:1px solid var(--border2);background:rgba(7,11,18,0.92);backdrop-filter:blur(20px);position:sticky;top:0;z-index:100}
.hl{display:flex;align-items:center;gap:16px}
.logo{width:42px;height:42px;border-radius:11px;background:linear-gradient(135deg,#1ed98a,#38d9f5);display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:19px;color:#07090f;box-shadow:0 0 24px rgba(56,217,245,0.2)}
.ht h1{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:.1em}
.ht p{font-family:'JetBrains Mono',monospace;font-size:9px;color:var(--muted);margin-top:2px;letter-spacing:.08em}
.hr{display:flex;align-items:center;gap:8px}
.pill{display:flex;align-items:center;gap:6px;padding:5px 13px;border-radius:20px;font-family:'JetBrains Mono',monospace;font-size:10px}
.pl{background:var(--green-dim);border:1px solid rgba(30,217,138,0.2);color:var(--green)}
.pd{background:var(--gold-dim);border:1px solid rgba(245,196,48,0.2);color:var(--gold)}
.pc{background:var(--bg2);border:1px solid var(--border2);color:var(--muted2)}
.ldot{width:6px;height:6px;border-radius:50%;background:var(--green);animation:blink 2s ease-in-out infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.3}}

/* LAYOUT */
main{padding:24px 32px;max-width:1460px;margin:0 auto}
.mb{margin-bottom:24px}

/* SECTION HEAD */
.sh{display:flex;align-items:center;gap:10px;margin-bottom:14px}
.sl{width:3px;border-radius:2px;height:22px;background:var(--sc,linear-gradient(180deg,var(--cyan),var(--blue)))}
.st{font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:.06em}
.stag{margin-left:auto;font-family:'JetBrains Mono',monospace;font-size:9px;color:var(--muted);padding:3px 9px;background:var(--bg3);border:1px solid var(--border);border-radius:4px}

/* CARD */
.card{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r);padding:20px 22px;position:relative;overflow:hidden;transition:border-color .2s}
.card:hover{border-color:var(--border2)}
.card::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,rgba(56,217,245,0.12),transparent)}

/* ANIM */
.fu{animation:fu .5s ease both}
@keyframes fu{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
.a1{animation-delay:.04s}.a2{animation-delay:.08s}.a3{animation-delay:.12s}
.a4{animation-delay:.16s}.a5{animation-delay:.20s}.a6{animation-delay:.24s}
.a7{animation-delay:.28s}.a8{animation-delay:.32s}.a9{animation-delay:.36s}

/* KPI */
.kpi-strip{display:grid;grid-template-columns:repeat(5,1fr);gap:12px;margin-bottom:24px}
.kpi{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r);padding:16px 18px;position:relative;overflow:hidden;transition:border-color .2s}
.kpi:hover{border-color:var(--border2)}
.kpi::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:var(--kc)}
.kl{font-family:'JetBrains Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;margin-bottom:7px}
.kv{font-family:'Bebas Neue',sans-serif;font-size:38px;line-height:1;color:var(--kc)}
.ks{font-size:11px;color:var(--muted2);margin-top:4px}
.kbar{margin-top:10px;height:2px;background:rgba(255,255,255,0.05);border-radius:1px}
.kbf{height:100%;border-radius:1px;background:var(--kc);transition:width 1s ease}

/* GRIDS */
.g2a{display:grid;grid-template-columns:1fr 1.5fr;gap:14px}
.g2b{display:grid;grid-template-columns:1.6fr 1fr;gap:14px}
.g2c{display:grid;grid-template-columns:1fr 1.4fr;gap:14px}

/* TABLE */
.tw{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:12px}
thead tr{border-bottom:1px solid var(--border2)}
th{padding:9px 11px;font-family:'JetBrains Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:.06em;text-align:left;white-space:nowrap}
td{padding:9px 11px;border-bottom:1px solid var(--border);color:var(--muted2)}
tbody tr:hover{background:rgba(56,217,245,0.025)}
tbody tr:last-child td{border-bottom:none}
.tm{color:var(--text)!important;font-weight:500}
.tmono{font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--text)!important}
.tnum{font-family:'JetBrains Mono',monospace;text-align:right}
.tz{color:var(--muted)!important}

/* CELL */
.cell{display:inline-flex;align-items:center;justify-content:center;min-width:28px;height:21px;border-radius:4px;font-family:'JetBrains Mono',monospace;font-size:11px;font-weight:500;padding:0 5px}
.c0{color:var(--muted)}
.chit{background:var(--green-dim);color:var(--green)}
.cmiss{background:var(--red-dim);color:var(--red)}

/* BADGE */
.bdg{display:inline-flex;align-items:center;padding:2px 8px;border-radius:4px;font-family:'JetBrains Mono',monospace;font-size:10px;font-weight:500}
.bh{background:var(--green-dim);color:var(--green);border:1px solid rgba(30,217,138,0.2)}
.bm{background:var(--red-dim);color:var(--red);border:1px solid rgba(255,64,96,0.2)}
.bst{background:var(--cyan-dim);color:var(--cyan);border:1px solid rgba(56,217,245,0.2)}
.bi{background:var(--blue-dim);color:var(--blue);border:1px solid rgba(79,143,255,0.2)}
.bl{background:var(--gold-dim);color:var(--gold);border:1px solid rgba(245,196,48,0.2)}

/* EKS LIST */
.ew{display:flex;flex-direction:column;gap:5px;max-height:290px;overflow-y:auto}
.er{display:flex;align-items:center;gap:10px;padding:7px 12px;background:var(--bg3);border-radius:8px;border:1px solid var(--border);transition:border-color .15s}
.er:hover{border-color:var(--border2)}
.en{font-size:12px;font-weight:500;color:var(--text);min-width:120px}
.ebb{flex:1;height:3px;background:rgba(255,255,255,0.05);border-radius:2px}
.ebf{height:100%;border-radius:2px;background:linear-gradient(90deg,var(--gold),var(--orange))}
.enum{font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--gold);min-width:18px;text-align:right}

/* FILTER */
.fb-wrap{display:flex;align-items:center;gap:8px;margin-bottom:20px;flex-wrap:wrap}
.fl{font-family:'JetBrains Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em}
.fb{padding:4px 13px;border-radius:20px;border:1px solid var(--border2);background:var(--bg3);color:var(--muted2);font-size:12px;font-family:'Outfit',sans-serif;cursor:pointer;transition:all .15s}
.fb:hover{border-color:var(--cyan);color:var(--text)}
.fb.on{background:var(--cyan);border-color:var(--cyan);color:#07090f;font-weight:600}
.fsep{width:1px;height:16px;background:var(--border2)}

footer{padding:16px 32px;border-top:1px solid var(--border);display:flex;align-items:center;justify-content:space-between}
footer p{font-family:'JetBrains Mono',monospace;font-size:9px;color:var(--muted)}

/* DATE FILTER */
.date-filter-bar{
  display:flex;align-items:center;gap:12px;
  padding:14px 20px;
  background:var(--bg2);border:1px solid var(--border2);
  border-radius:var(--r);margin-bottom:20px;flex-wrap:wrap;
}
.date-filter-bar .fl{font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--cyan);text-transform:uppercase;letter-spacing:.07em;white-space:nowrap}
.date-input-wrap{display:flex;align-items:center;gap:8px}
.date-input-wrap label{font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--muted);white-space:nowrap}
input[type="date"]{
  background:var(--bg3);border:1px solid var(--border2);border-radius:8px;
  color:var(--text);font-family:'JetBrains Mono',monospace;font-size:11px;
  padding:6px 12px;outline:none;cursor:pointer;
  color-scheme:dark;
}
input[type="date"]:focus{border-color:var(--cyan);box-shadow:0 0 0 2px rgba(56,217,245,0.1)}
.date-sep{font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--muted);padding:0 2px}
.date-reset{
  padding:6px 14px;border-radius:8px;border:1px solid var(--border2);
  background:transparent;color:var(--muted2);font-size:11px;
  font-family:'Outfit',sans-serif;cursor:pointer;transition:all .15s;white-space:nowrap;
}
.date-reset:hover{border-color:var(--red);color:var(--red)}
.date-info{
  margin-left:auto;font-family:'JetBrains Mono',monospace;font-size:10px;
  color:var(--muted2);padding:5px 12px;background:var(--bg3);
  border:1px solid var(--border);border-radius:6px;white-space:nowrap;
}
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-track{background:var(--bg2)}
::-webkit-scrollbar-thumb{background:rgba(56,217,245,0.15);border-radius:2px}

@media(max-width:1024px){.kpi-strip{grid-template-columns:repeat(3,1fr)}.g2a,.g2b,.g2c{grid-template-columns:1fr}}
@media(max-width:600px){main,header,footer{padding-left:14px;padding-right:14px}.kpi-strip{grid-template-columns:repeat(2,1fr)}}
</style>
</head>
<body>

<div id="loader">
  <div class="ld-logo">INBOUND</div>
  <div class="ld-sub">LOADING DASHBOARD...</div>
  <div class="ld-bar"><div class="ld-fill"></div></div>
</div>

<div class="app">
<header>
  <div class="hl">
    <div class="logo">IB</div>
    <div class="ht">
      <h1>INBOUND DASHBOARD</h1>
      <p>NDC SIDOARJO · MONITORING UNLOADING KONTAINER</p>
    </div>
  </div>
  <div class="hr">
    <div class="pill pl"><span class="ldot"></span>LIVE</div>
    <div class="pill pd" id="pillDate">—</div>
    <div class="pill pc" id="pillClock">—</div>
  </div>
</header>

<main>

<!-- KPI -->
<div class="kpi-strip" id="kpiStrip"></div>

<!-- DATE FILTER -->
<div class="date-filter-bar fu a1">
  <span class="fl">📅 Filter Tanggal</span>
  <div class="date-input-wrap">
    <label>Start</label>
    <input type="date" id="dateStart" onchange="setDateFilter()">
  </div>
  <span class="date-sep">→</span>
  <div class="date-input-wrap">
    <label>End</label>
    <input type="date" id="dateEnd" onchange="setDateFilter()">
  </div>
  <button class="date-reset" onclick="quickDate(0)">Hari Ini</button>
  <button class="date-reset" onclick="quickDate(7)">7 Hari</button>
  <button class="date-reset" onclick="quickDate(30)">30 Hari</button>
  <button class="date-reset" onclick="resetDate()" style="color:var(--red)">✕ Reset</button>
  <div class="date-info" id="dateInfo">Semua tanggal</div>
</div>

<!-- FILTER TIPE & STATUS -->
<div class="fb-wrap fu a2">
  <span class="fl">Tipe</span>
  <button class="fb on" onclick="setF('type','all',this)">Semua</button>
  <button class="fb" onclick="setF('type','STOCK TRANSFER',this)">Stock Transfer</button>
  <button class="fb" onclick="setF('type','IMPORT',this)">Import</button>
  <button class="fb" onclick="setF('type','LOKAL',this)">Lokal</button>
  <div class="fsep"></div>
  <span class="fl">Status</span>
  <button class="fb on" onclick="setF('hm','all',this)">Semua</button>
  <button class="fb" onclick="setF('hm','HIT',this)">HIT</button>
  <button class="fb" onclick="setF('hm','MISS',this)">MISS</button>
</div>

<!-- PLAN UNLOADING -->
<div class="mb">
  <div class="sh fu a2">
    <div class="sl"></div>
    <span class="st">Plan Unloading</span>
    <span class="stag">Per Jenis Armada × Tipe</span>
  </div>
  <div class="g2a">
    <div class="card fu a3">
      <div class="tw">
        <table>
          <thead><tr>
            <th>Armada</th>
            <th style="text-align:right">Stock Transfer</th>
            <th style="text-align:right">Import</th>
            <th style="text-align:right">Lokal</th>
            <th style="text-align:right">Total</th>
          </tr></thead>
          <tbody id="planTbody"></tbody>
        </table>
      </div>
    </div>
    <div class="card fu a4">
      <div style="height:240px;position:relative"><canvas id="planChart"></canvas></div>
    </div>
  </div>
</div>

<!-- HIT / MISS -->
<div class="mb">
  <div class="sh fu a3">
    <div class="sl" style="--sc:linear-gradient(180deg,var(--green),var(--red))"></div>
    <span class="st">Hit / Miss</span>
    <span class="stag">Per Tipe × Tanggal</span>
  </div>
  <div class="g2b">
    <div class="card fu a4">
      <div class="tw" id="hmWrap"></div>
    </div>
    <div class="card fu a5">
      <div style="height:260px;position:relative"><canvas id="hmChart"></canvas></div>
    </div>
  </div>
</div>

<!-- TIPE PENGIRIMAN -->
<div class="mb">
  <div class="sh fu a5">
    <div class="sl" style="--sc:linear-gradient(180deg,var(--gold),var(--orange))"></div>
    <span class="st">Tipe Pengiriman</span>
    <span class="stag">Per Ekspedisi</span>
  </div>
  <div class="g2c">
    <div class="card fu a6">
      <div class="ew" id="eksList"></div>
    </div>
    <div class="card fu a7">
      <div style="height:300px;position:relative"><canvas id="tipeChart"></canvas></div>
    </div>
  </div>
</div>

<!-- DETAIL -->
<div class="mb">
  <div class="sh fu a7">
    <div class="sl" style="--sc:linear-gradient(180deg,var(--blue),var(--cyan))"></div>
    <span class="st">Detail Unloading</span>
    <span class="stag" id="detBadge">— baris</span>
  </div>
  <div class="card fu a8">
    <div class="tw">
      <table style="min-width:1040px">
        <thead><tr>
          <th>#</th><th>No Polisi</th><th>Ekspedisi</th><th>Armada</th>
          <th>Site From</th><th>BU</th><th>Perjalanan</th><th>Antrian</th>
          <th>ETA</th><th>Hit/Miss</th><th>% Dept</th><th>Type</th>
          <th style="text-align:right">CBM</th><th style="text-align:right">Gross Weight</th>
          <th>Tanggal</th>
        </tr></thead>
        <tbody id="detTbody"></tbody>
      </table>
    </div>
  </div>
</div>

</main>
<footer>
  <p>Inbound Dashboard · NDC Sidoarjo · 2026</p>
  <p>Update data: ganti SHEET_ID lalu set Google Sheets ke "Anyone with link can view"</p>
</footer>
</div>

<script>
// ── DATA ────────────────────────────────────────────────────
const planData = [
  {arm:'CONT-40',st:0,imp:0,lok:0},{arm:'WINGBOX',st:3,imp:0,lok:0},
  {arm:'CONT-20',st:0,imp:0,lok:0},{arm:'FUSO',st:0,imp:0,lok:0},
  {arm:'CONT40',st:0,imp:3,lok:0},{arm:'CDE',st:0,imp:0,lok:0},
  {arm:'WB',st:0,imp:0,lok:0},{arm:'CDD',st:0,imp:0,lok:0},
];
const hmDates = ['3/1','3/2','3/3','3/4','3/5','3/6','3/7','3/8'];
const hmData = [
  {tipe:'STOCK TRANSFER',vals:[0,2,2,3,2,2,0,2]},
  {tipe:'IMPORT',        vals:[0,0,0,0,0,0,1,0]},
  {tipe:'LOKAL',         vals:[0,0,2,0,0,0,0,0]},
];
const ekspedisi = ['CGS','DMM','JPT','BS','PT.DANEX','DINOYO','JME','CGL','DUNEX','INTERNAL AHI','EUREKA','SPP','AHI','PT AMANAH','DUMMY-LK-EKSP','BBR'];
const detail = [
  {no:'SEGU6686556',eks:'CGS',arm:'CONT-40',site:'A001',bu:'AHI',upd:'NDC SIDOARJO',ant:3,eta:'WT1 08-11',hm:'HIT',dept:'R100AS',type:'STOCK TRANSFER',cbm:41.6,gw:8574,plan:'3/2/2026'},
  {no:'MEDU8906416',eks:'CGS',arm:'CONT-40',site:'A001',bu:'AHI',upd:'NDC SIDOARJO',ant:5,eta:'WT1 08-11',hm:'HIT',dept:'R100AF',type:'STOCK TRANSFER',cbm:23.0,gw:4077,plan:'3/2/2026'},
  {no:'MSDU7522809',eks:'CGS',arm:'CONT-40',site:'A001',bu:'AHI',upd:'NDC SIDOARJO',ant:0,eta:'WT1 08-11',hm:'HIT',dept:'R100AD',type:'STOCK TRANSFER',cbm:52.0,gw:7542,plan:'3/3/2026'},
  {no:'TRLU8186711',eks:'CGS',arm:'CONT-40',site:'A001',bu:'AHI',upd:'NDC SIDOARJO',ant:0,eta:'WT1 08-11',hm:'MISS',dept:'R100AR',type:'STOCK TRANSFER',cbm:35.4,gw:7509,plan:'3/2/2026'},
  {no:'MSMU8315910',eks:'CGS',arm:'CONT-40',site:'A001',bu:'AHI',upd:'NDC SIDOARJO',ant:8,eta:'WT1 08-11',hm:'MISS',dept:'R100AT',type:'STOCK TRANSFER',cbm:33.8,gw:6680,plan:'3/2/2026'},
  {no:'EGSU6553015',eks:'69206',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:5,eta:'WT1 08-11',hm:'HIT',dept:'CLEANING',type:'IMPORT',cbm:68.5,gw:6048,plan:'3/1/2026'},
  {no:'EITU9748785',eks:'—',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:4,eta:'WT1 08-11',hm:'HIT',dept:'CLEANING',type:'IMPORT',cbm:68.5,gw:6048,plan:'3/1/2026'},
  {no:'TCNU2127725',eks:'69205',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:3,eta:'WT1 08-11',hm:'HIT',dept:'CLEANING',type:'IMPORT',cbm:68.5,gw:6054,plan:'3/1/2026'},
  {no:'CMAU6883226',eks:'33535',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:0,eta:'WT1 08-11',hm:'HIT',dept:'OUTDOOR COMFORT',type:'IMPORT',cbm:65.6,gw:10510,plan:'3/3/2026'},
  {no:'WHSU5302859',eks:'5073',arm:'CONT40',site:'FT 28%',bu:'AHI',upd:'NDC SIDOARJO',ant:0,eta:'WT1 08-11',hm:'HIT',dept:'FAN & AIR',type:'IMPORT',cbm:66.5,gw:5617,plan:'3/4/2026'},
  {no:'EGSU1596098',eks:'33546',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:0,eta:'WT1 08-11',hm:'HIT',dept:'HOME STORAGE',type:'IMPORT',cbm:68.6,gw:8098,plan:'3/4/2026'},
  {no:'CSNU5762122',eks:'33544',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:7,eta:'WT2 12-15',hm:'HIT',dept:'OUTDOOR COMFORT',type:'IMPORT',cbm:68.0,gw:12031,plan:'3/5/2026'},
  {no:'EGSU6064272',eks:'90934',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:4,eta:'WT1 08-11',hm:'HIT',dept:'LCR',type:'IMPORT',cbm:40.9,gw:25450,plan:'3/5/2026'},
  {no:'BMOU6621007',eks:'47817',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:5,eta:'WT1 08-11',hm:'HIT',dept:'TOOLS',type:'IMPORT',cbm:65.8,gw:5929,plan:'3/5/2026'},
  {no:'TIIU7249200',eks:'69224',arm:'CONT40',site:'FT 19%',bu:'AHI',upd:'NDC SIDOARJO',ant:2,eta:'WT1 08-11',hm:'HIT',dept:'PLBM',type:'IMPORT',cbm:69.0,gw:4503,plan:'3/6/2026'},
  {no:'OOCU9450144',eks:'90936',arm:'CONT40',site:'FT 47%',bu:'AHI',upd:'NDC SIDOARJO',ant:4,eta:'WT1 08-11',hm:'HIT',dept:'ELECTRICAL',type:'IMPORT',cbm:56.4,gw:8815,plan:'3/6/2026'},
  {no:'OOCU7678217',eks:'69240',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:10,eta:'WT1 08-11',hm:'MISS',dept:'TRAVEL',type:'IMPORT',cbm:71.4,gw:6885,plan:'3/7/2026'},
  {no:'FFAU5826153',eks:'5076',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:10,eta:'WT2 12-15',hm:'HIT',dept:'FAN & AIR',type:'IMPORT',cbm:66.1,gw:6639,plan:'3/9/2026'},
  {no:'CMAU6350295',eks:'33520',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:3,eta:'WT2 12-15',hm:'HIT',dept:'OUTDOOR COMFORT',type:'IMPORT',cbm:65.4,gw:10348,plan:'3/10/2026'},
  {no:'SKHU9108978',eks:'33548',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:8,eta:'WT1 08-11',hm:'MISS',dept:'SAFE/OFFC',type:'IMPORT',cbm:33.7,gw:14421,plan:'3/10/2026'},
  {no:'TGBU5333801',eks:'47830',arm:'CONT40',site:'FT 61%',bu:'AHI',upd:'NDC SIDOARJO',ant:7,eta:'WT2 12-15',hm:'HIT',dept:'TOOLS',type:'IMPORT',cbm:68.0,gw:11902,plan:'3/11/2026'},
  {no:'EISU8322488',eks:'90951',arm:'CONT40',site:'FT 9%',bu:'AHI',upd:'NDC SIDOARJO',ant:4,eta:'WT1 08-11',hm:'HIT',dept:'LCR',type:'IMPORT',cbm:68.4,gw:11780,plan:'3/11/2026'},
  {no:'EGSU9624088',eks:'—',arm:'CONT40',site:'FT 9%',bu:'AHI',upd:'NDC SIDOARJO',ant:8,eta:'WT1 08-11',hm:'MISS',dept:'LCR',type:'IMPORT',cbm:68.4,gw:11780,plan:'3/11/2026'},
  {no:'YMMU6271650',eks:'33553',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:5,eta:'WT1 08-11',hm:'HIT',dept:'OUTDOOR COMFORT',type:'IMPORT',cbm:65.0,gw:9260,plan:'3/14/2026'},
  {no:'TGBU6972875',eks:'47833',arm:'CONT40',site:'IMPORT',bu:'AHI',upd:'NDC SIDOARJO',ant:4,eta:'WT1 08-11',hm:'HIT',dept:'TOOLS',type:'IMPORT',cbm:68.0,gw:11981,plan:'3/14/2026'},
];

// ── FILTER ──────────────────────────────────────────────────
const F={type:'all',hm:'all'};
let dateStart=null, dateEnd=null;
let cPlan,cHm,cTipe;

// Parse tanggal dari format "3/1/2026" atau "3/1" menjadi Date
function parseDate(str){
  if(!str)return null;
  // format "M/D/YYYY"
  const m1=str.match(/^(\d+)\/(\d+)\/(\d{4})$/);
  if(m1)return new Date(+m1[3],+m1[1]-1,+m1[2]);
  // format "M/D"
  const m2=str.match(/^(\d+)\/(\d+)$/);
  if(m2)return new Date(2026,+m2[1]-1,+m2[2]);
  return null;
}

function setDateFilter(){
  const s=document.getElementById('dateStart').value;
  const e=document.getElementById('dateEnd').value;
  dateStart = s ? new Date(s) : null;
  dateEnd   = e ? new Date(e+'T23:59:59') : null;
  // update info label
  const fmt=d=>d.toLocaleDateString('id-ID',{day:'2-digit',month:'short',year:'numeric'});
  let info='Semua tanggal';
  if(dateStart&&dateEnd) info=`${fmt(dateStart)} → ${fmt(dateEnd)}`;
  else if(dateStart) info=`Sejak ${fmt(dateStart)}`;
  else if(dateEnd)   info=`Sampai ${fmt(dateEnd)}`;
  document.getElementById('dateInfo').textContent=info;
  render();
}

function resetDate(){
  dateStart=null; dateEnd=null;
  document.getElementById('dateStart').value='';
  document.getElementById('dateEnd').value='';
  document.getElementById('dateInfo').textContent='Semua tanggal';
  render();
}

function setF(k,v,btn){
  F[k]=v;
  btn.closest('.fb-wrap').querySelectorAll('.fb').forEach(b=>{
    if(b.getAttribute('onclick')&&b.getAttribute('onclick').includes(`'${k}'`)) b.classList.remove('on');
  });
  btn.classList.add('on');
  render();
}

function fd(){
  return detail.filter(d=>{
    if(F.type!=='all'&&d.type!==F.type)return false;
    if(F.hm!=='all'&&d.hm!==F.hm)return false;
    // date filter — d.plan berisi string tanggal e.g. "3/1/2026"
    if(dateStart||dateEnd){
      const dp=parseDate(d.plan);
      if(!dp)return false;
      if(dateStart&&dp<dateStart)return false;
      if(dateEnd&&dp>dateEnd)return false;
    }
    return true;
  });
}

// ── RENDER ──────────────────────────────────────────────────
function render(){
  const d=fd();
  doKPI(d); doPlan(d); doHM(); doTipe(); doDetail(d);
}

function doKPI(d){
  const total=d.length, hit=d.filter(x=>x.hm==='HIT').length, miss=d.filter(x=>x.hm==='MISS').length;
  const pct=total?Math.round(hit/total*100):0;
  const cbm=d.reduce((s,x)=>s+x.cbm,0);
  const depts=[...new Set(d.map(x=>x.dept))].length;
  const K=[
    {l:'Total Kontainer',v:total,    s:'pengiriman',    c:'var(--cyan)', p:100},
    {l:'HIT Tepat Waktu',v:hit,      s:`${pct}% on-time`,c:'var(--green)',p:pct},
    {l:'MISS Terlambat', v:miss,     s:`${100-pct}% late`,c:'var(--red)', p:100-pct},
    {l:'Total CBM',      v:cbm.toFixed(1),s:'m³ volume',c:'var(--blue)', p:Math.min(cbm/20,100)},
    {l:'Departemen',     v:depts,    s:'dept aktif',    c:'var(--gold)', p:Math.min(depts*8,100)},
  ];
  document.getElementById('kpiStrip').innerHTML=K.map((k,i)=>`
    <div class="kpi fu" style="--kc:${k.c};animation-delay:${i*0.06}s">
      <div class="kl">${k.l}</div>
      <div class="kv">${k.v}</div>
      <div class="ks">${k.s}</div>
      <div class="kbar"><div class="kbf" style="width:${k.p}%"></div></div>
    </div>`).join('');
}

function doPlan(d){
  document.getElementById('planTbody').innerHTML=planData.map(p=>{
    const t=p.st+p.imp+p.lok;
    return `<tr>
      <td class="tm">${p.arm}</td>
      <td class="tnum ${p.st===0?'tz':''}">${p.st||'—'}</td>
      <td class="tnum ${p.imp===0?'tz':''}">${p.imp||'—'}</td>
      <td class="tnum ${p.lok===0?'tz':''}">${p.lok||'—'}</td>
      <td class="tnum" style="color:var(--cyan);font-family:'JetBrains Mono',monospace">${t||'—'}</td>
    </tr>`;
  }).join('');
  if(cPlan)cPlan.destroy();
  cPlan=new Chart(document.getElementById('planChart'),{
    type:'bar',
    data:{labels:planData.map(p=>p.arm),datasets:[
      {label:'Stock Transfer',data:planData.map(p=>p.st),backgroundColor:'rgba(56,217,245,0.7)',borderRadius:4,borderSkipped:false},
      {label:'Import',data:planData.map(p=>p.imp),backgroundColor:'rgba(79,143,255,0.7)',borderRadius:4,borderSkipped:false},
      {label:'Lokal',data:planData.map(p=>p.lok),backgroundColor:'rgba(245,196,48,0.7)',borderRadius:4,borderSkipped:false},
    ]},
    options:{responsive:true,maintainAspectRatio:false,
      plugins:{legend:{labels:{color:'#7a90b8',font:{size:11},boxWidth:10}},tooltip:{backgroundColor:'#0c1220',borderColor:'rgba(56,217,245,.2)',borderWidth:1,titleColor:'#dde8f8',bodyColor:'#7a90b8',padding:10}},
      scales:{x:{ticks:{color:'#4a5f80',font:{size:10}},grid:{display:false},border:{display:false}},y:{ticks:{color:'#4a5f80',font:{size:10}},grid:{color:'rgba(56,217,245,0.05)'},border:{display:false},beginAtZero:true}}}
  });
}

function doHM(){
  document.getElementById('hmWrap').innerHTML=`<table>
    <thead><tr><th>Tipe</th>${hmDates.map(d=>`<th style="text-align:center">${d}</th>`).join('')}<th style="text-align:center">Total</th></tr></thead>
    <tbody>${hmData.map(row=>{
      const tot=row.vals.reduce((a,b)=>a+b,0);
      return `<tr><td class="tm">${row.tipe}</td>${row.vals.map(v=>`<td style="text-align:center"><span class="cell ${v===0?'c0':'cmiss'}">${v===0?'—':v}</span></td>`).join('')}<td style="text-align:center;font-family:'JetBrains Mono',monospace;color:var(--cyan)">${tot||'—'}</td></tr>`;
    }).join('')}</tbody></table>`;
  if(cHm)cHm.destroy();
  cHm=new Chart(document.getElementById('hmChart'),{
    type:'line',
    data:{labels:hmDates,datasets:hmData.map((r,i)=>({
      label:r.tipe,data:r.vals,
      borderColor:['var(--cyan)','var(--blue)','var(--gold)'][i],
      backgroundColor:['rgba(56,217,245,0.07)','rgba(79,143,255,0.07)','rgba(245,196,48,0.07)'][i],
      borderWidth:2,pointRadius:4,pointHoverRadius:6,tension:.4,fill:true,
    }))},
    options:{responsive:true,maintainAspectRatio:false,
      plugins:{legend:{labels:{color:'#7a90b8',font:{size:11},boxWidth:10}},tooltip:{backgroundColor:'#0c1220',borderColor:'rgba(56,217,245,.2)',borderWidth:1,titleColor:'#dde8f8',bodyColor:'#7a90b8',padding:10}},
      scales:{x:{ticks:{color:'#4a5f80',font:{size:10,family:'JetBrains Mono'}},grid:{display:false},border:{display:false}},y:{ticks:{color:'#4a5f80',font:{size:10}},grid:{color:'rgba(56,217,245,0.05)'},border:{display:false},beginAtZero:true}}}
  });
}

function doTipe(){
  const cnt={};detail.forEach(d=>{cnt[d.eks]=(cnt[d.eks]||0)+1});
  const mx=Math.max(...ekspedisi.map(e=>cnt[e]||0),1);
  document.getElementById('eksList').innerHTML=ekspedisi.map(e=>{
    const n=cnt[e]||0,p=Math.round(n/mx*100);
    return `<div class="er"><div class="en">${e}</div><div class="ebb"><div class="ebf" style="width:${p}%"></div></div><div class="enum">${n}</div></div>`;
  }).join('');
  const tc={IMPORT:0,'STOCK TRANSFER':0,LOKAL:0};
  detail.forEach(d=>{if(tc[d.type]!==undefined)tc[d.type]++});
  if(cTipe)cTipe.destroy();
  cTipe=new Chart(document.getElementById('tipeChart'),{
    type:'doughnut',
    data:{labels:Object.keys(tc),datasets:[{data:Object.values(tc),backgroundColor:['rgba(79,143,255,0.8)','rgba(56,217,245,0.8)','rgba(245,196,48,0.8)'],borderWidth:0,hoverOffset:6}]},
    options:{responsive:true,maintainAspectRatio:false,cutout:'62%',
      plugins:{legend:{display:true,position:'bottom',labels:{color:'#7a90b8',font:{size:11},boxWidth:10,padding:14,usePointStyle:true,pointStyleWidth:8}},tooltip:{backgroundColor:'#0c1220',borderColor:'rgba(56,217,245,.2)',borderWidth:1,titleColor:'#dde8f8',bodyColor:'#7a90b8',padding:10}}}
  });
}

function quickDate(days){
  const now=new Date();
  const p=d=>d.toISOString().split('T')[0];
  if(days===0){
    document.getElementById('dateStart').value=p(now);
    document.getElementById('dateEnd').value=p(now);
  } else {
    const past=new Date(now); past.setDate(now.getDate()-days);
    document.getElementById('dateStart').value=p(past);
    document.getElementById('dateEnd').value=p(now);
  }
  setDateFilter();
}

function doDetail(d){
  document.getElementById('detBadge').textContent=`${d.length} baris`;
  document.getElementById('detTbody').innerHTML=d.map((r,i)=>`
    <tr>
      <td style="color:var(--muted);font-family:'JetBrains Mono',monospace;font-size:10px">${String(i+1).padStart(2,'0')}</td>
      <td class="tmono">${r.no}</td>
      <td>${r.eks}</td><td>${r.arm}</td>
      <td style="font-family:'JetBrains Mono',monospace;font-size:10px">${r.site}</td>
      <td>${r.bu}</td><td>${r.upd}</td>
      <td style="text-align:center;font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--cyan)">${r.ant||'—'}</td>
      <td style="font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--muted2)">${r.eta}</td>
      <td><span class="bdg ${r.hm==='HIT'?'bh':'bm'}">${r.hm==='HIT'?'↑':'↓'} ${r.hm}</span></td>
      <td class="tm">${r.dept}</td>
      <td><span class="bdg ${r.type==='IMPORT'?'bi':r.type==='LOKAL'?'bl':'bst'}">${r.type==='STOCK TRANSFER'?'ST':r.type}</span></td>
      <td class="tnum" style="color:var(--blue)">${r.cbm.toFixed(1)}</td>
      <td class="tnum" style="color:var(--muted2)">${r.gw.toLocaleString()}</td>
      <td style="font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--gold)">${r.plan}</td>
    </tr>`).join('');
}

// CLOCK
function tick(){
  const now=new Date(),p=n=>String(n).padStart(2,'0');
  const D=['Minggu','Senin','Selasa','Rabu','Kamis','Jumat','Sabtu'];
  const M=['Jan','Feb','Mar','Apr','Mei','Jun','Jul','Ags','Sep','Okt','Nov','Des'];
  document.getElementById('pillDate').textContent=`${D[now.getDay()]} ${p(now.getDate())} ${M[now.getMonth()]} ${now.getFullYear()}`;
  document.getElementById('pillClock').textContent=`${p(now.getHours())}:${p(now.getMinutes())}:${p(now.getSeconds())}`;
}
tick();setInterval(tick,1000);

// LOADER
window.addEventListener('load',()=>{
  setTimeout(()=>{const l=document.getElementById('loader');l.style.opacity='0';setTimeout(()=>l.style.display='none',500);},1300);
});

render();
</script>
</body>
</html>
