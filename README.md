# solarpm-pro
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1"/>
<title>☀ SolarPM Pro v3</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
:root{
  --bg:#03080f;--s1:#071020;--s2:#0b1830;--s3:#111e35;
  --brd:#162540;--brd2:#1e3560;
  --amb:#f59e0b;--grn:#22c55e;--red:#f87171;--blu:#60a5fa;--cyn:#22d3ee;--pur:#a78bfa;--ora:#fb923c;
  --t1:#f1f5f9;--t2:#94a3b8;--t3:#4a6080;--t4:#1a3050;
}
html,body{background:var(--bg);color:var(--t1);font-family:'Courier New',Courier,monospace;min-height:100vh;overflow-x:hidden;font-size:13px;}
body::before{content:'';position:fixed;inset:0;background:radial-gradient(ellipse 70% 50% at 20% 30%,#f59e0b06,transparent),radial-gradient(ellipse 60% 40% at 80% 70%,#22c55e04,transparent);pointer-events:none;z-index:0;}
*{scrollbar-width:thin;scrollbar-color:var(--brd2) var(--s1);}
::-webkit-scrollbar{width:4px;height:4px;}::-webkit-scrollbar-thumb{background:var(--brd2);border-radius:2px;}
select option{background:var(--s2);}
input[type=number]{-moz-appearance:textfield;}
input[type=number]::-webkit-inner-spin-button{opacity:.3;}

/* ──── LAYOUT ──── */
#root{position:relative;z-index:1;}
.app{display:flex;flex-direction:column;min-height:100vh;}

#hdr{background:linear-gradient(135deg,var(--s2),#0a1a08);border-bottom:1px solid var(--brd);padding:10px 16px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:300;}
.logo{font-size:20px;font-weight:900;color:var(--amb);letter-spacing:-.5px;}
.logo-sub{font-size:8px;color:var(--t3);letter-spacing:.12em;text-transform:uppercase;margin-top:1px;}
.hdr-right{display:flex;align-items:center;gap:10px;}
.chip{padding:4px 10px;border-radius:20px;font-size:10px;font-weight:700;border:1px solid;line-height:1.4;}
.kw-box{text-align:right;}
.kw-lbl{font-size:8px;color:var(--t3);text-transform:uppercase;letter-spacing:.1em;}
.kw-val{font-size:17px;font-weight:700;color:var(--grn);}

#ticker{background:var(--s1);border-bottom:1px solid var(--brd);padding:6px 14px;display:flex;gap:18px;overflow-x:auto;-webkit-overflow-scrolling:touch;scrollbar-width:none;}
#ticker::-webkit-scrollbar{display:none;}
.tick{flex-shrink:0;}.tick-l{font-size:7px;color:var(--t3);letter-spacing:.1em;text-transform:uppercase;}.tick-v{font-size:12px;font-weight:700;line-height:1.3;}

#body{display:flex;flex:1;}
#sidenav{width:52px;background:var(--s1);border-right:1px solid var(--brd);display:flex;flex-direction:column;padding:6px 0;gap:1px;flex-shrink:0;overflow:hidden;transition:width .2s;}
#sidenav:hover{width:190px;}
.snbtn{display:flex;align-items:center;gap:10px;padding:9px 14px;background:none;border:none;border-left:3px solid transparent;cursor:pointer;color:var(--t3);font-family:inherit;font-size:11px;font-weight:700;letter-spacing:.03em;white-space:nowrap;width:100%;text-align:left;transition:all .12s;}
.snbtn:hover{color:var(--t2);background:var(--s2);}
.snbtn.on{color:var(--amb);background:var(--s2);border-left-color:var(--amb);}
.sn-ico{font-size:14px;flex-shrink:0;width:24px;text-align:center;}

#main{flex:1;overflow-y:auto;-webkit-overflow-scrolling:touch;}
.content{padding:18px;max-width:920px;padding-bottom:40px;}

#rpanel{width:185px;flex-shrink:0;background:var(--s1);border-left:1px solid var(--brd);padding:12px;overflow-y:auto;}
.rp-sec{font-size:9px;font-weight:900;color:var(--amb);letter-spacing:.14em;text-transform:uppercase;margin:10px 0 4px;padding-bottom:3px;border-bottom:1px solid var(--brd);}
.rp-sec:first-child{margin-top:0;}
.rp-row{display:flex;justify-content:space-between;align-items:baseline;padding:3px 0;border-bottom:1px solid var(--brd);}
.rp-l{font-size:9px;color:var(--t3);}.rp-v{font-size:10px;font-weight:700;}

#bnav{display:none;background:var(--s1);border-top:1px solid var(--brd);position:sticky;bottom:0;z-index:300;padding-bottom:env(safe-area-inset-bottom,0);}
.bnav-inner{display:flex;flex-wrap:wrap;}
.bnbtn{flex:1;min-width:60px;display:flex;flex-direction:column;align-items:center;gap:1px;padding:6px 2px;background:none;border:none;cursor:pointer;font-family:inherit;font-size:7px;font-weight:700;color:var(--t3);letter-spacing:.03em;text-transform:uppercase;}
.bnbtn.on{color:var(--amb);}
.bn-ico{font-size:16px;line-height:1.2;}

/* ──── FORM ELEMENTS ──── */
.sec-hd{display:flex;align-items:center;gap:8px;margin-bottom:16px;padding-bottom:9px;border-bottom:1px solid var(--brd);}
.sec-ttl{font-size:14px;font-weight:900;color:var(--t1);letter-spacing:.05em;text-transform:uppercase;}
.sec-ico{font-size:14px;}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;}
.g4{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:10px;}
.fld{display:flex;flex-direction:column;gap:3px;}
.fld-l{font-size:9px;font-weight:700;color:var(--amb);letter-spacing:.1em;text-transform:uppercase;}
.fld-h{font-size:9px;color:var(--t3);}
.inp,.sel{width:100%;background:var(--s2);border:1px solid var(--brd2);border-radius:6px;padding:8px 10px;color:var(--t1);font-size:12px;font-family:inherit;outline:none;transition:border-color .12s;-webkit-appearance:none;appearance:none;}
.inp:focus,.sel:focus{border-color:var(--amb);}
.sel{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='10' height='6'%3E%3Cpath d='M0 0l5 6 5-6z' fill='%234a6080'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 10px center;padding-right:28px;}
.chkrow{display:flex;align-items:center;gap:8px;cursor:pointer;padding:4px 0;user-select:none;}
.chkbox{width:17px;height:17px;min-width:17px;border-radius:4px;border:2px solid var(--brd2);display:flex;align-items:center;justify-content:center;transition:all .12s;font-size:11px;font-weight:900;color:transparent;}
.chkbox.on{border-color:var(--amb);background:#f59e0b1a;color:var(--amb);}
.chk-l{font-size:12px;color:var(--t2);}
.ibox{background:var(--s2);border:1px solid var(--brd2);border-radius:6px;padding:8px 12px;font-size:11px;color:var(--t2);line-height:1.6;}
.ibox.warn{border-color:#f59e0b55;background:#f59e0b08;}
.ibox.ok{border-color:#22c55e44;background:#22c55e06;}
.ibox.bad{border-color:#f8717144;background:#f8717108;}
.v{color:var(--amb);font-weight:700;}.g{color:var(--grn);font-weight:700;}.r{color:var(--red);font-weight:700;}.b{color:var(--blu);font-weight:700;}
.mt8{margin-top:8px;}.mt12{margin-top:12px;}.mt16{margin-top:16px;}.mt20{margin-top:20px;}.mt24{margin-top:24px;}
.badge{display:inline-block;padding:2px 8px;border-radius:20px;font-size:9px;font-weight:700;letter-spacing:.06em;text-transform:uppercase;}

/* ──── STATION CARDS ──── */
.st-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(145px,1fr));gap:10px;}
.stcard{background:var(--s2);border:2px solid var(--brd);border-radius:13px;padding:13px 11px;cursor:pointer;transition:all .15s;display:flex;flex-direction:column;align-items:center;text-align:center;gap:5px;position:relative;overflow:hidden;}
.stcard:active{transform:scale(.97);}
.stcard.on{transform:translateY(-2px);}
.st-glow{position:absolute;top:-30px;right:-20px;width:70px;height:70px;border-radius:50%;opacity:.12;filter:blur(18px);}
.st-ico{font-size:26px;}.st-nm{font-size:12px;font-weight:900;letter-spacing:.04em;text-transform:uppercase;line-height:1.2;}
.st-desc{font-size:9px;color:var(--t3);line-height:1.4;}.st-kw{font-size:9px;color:var(--t3);font-weight:700;}
.st-tag{font-size:8px;font-weight:700;padding:1px 6px;border-radius:20px;letter-spacing:.06em;text-transform:uppercase;}

/* ──── METRIC CARDS ──── */
.mgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:9px;}
.mgrid4{display:grid;grid-template-columns:repeat(4,1fr);gap:9px;}
.mcard{background:var(--s2);border:1px solid var(--brd);border-radius:9px;padding:10px 12px;border-left:3px solid var(--amb);}
.mcard.hi{background:linear-gradient(135deg,#0d2a10,#071508);border-color:#22c55e22;}
.mc-l{font-size:8px;color:var(--t3);letter-spacing:.08em;text-transform:uppercase;margin-bottom:3px;}
.mc-v{font-size:14px;font-weight:700;}.mc-s{font-size:8px;color:var(--t3);margin-top:2px;}

/* ──── TABLE ──── */
.tbl{width:100%;border-collapse:collapse;font-size:11px;}
.tbl th{background:var(--s2);padding:7px 10px;font-size:9px;font-weight:700;color:var(--amb);letter-spacing:.06em;text-transform:uppercase;text-align:right;white-space:nowrap;border-bottom:1px solid var(--brd);}
.tbl th:first-child{text-align:left;}
.tbl td{padding:6px 10px;border-bottom:1px solid var(--brd);text-align:right;color:var(--t2);white-space:nowrap;}
.tbl td:first-child{text-align:left;color:var(--t1);}
.tbl tr:last-child td{border-bottom:none;}
.tbl tr.bold td{font-weight:700;color:var(--t1);border-top:1px solid var(--brd2);}
.tbl tr:hover td{background:#ffffff05;}
.neg{color:var(--red)!important;}.pos{color:var(--grn)!important;}
.tbl-wrap{overflow-x:auto;background:var(--s1);border:1px solid var(--brd);border-radius:9px;margin-top:8px;}

/* ──── BOM ──── */
.bom{background:var(--s1);border:1px solid var(--brd);border-radius:9px;overflow:hidden;margin-top:16px;}
.bom-hd{display:grid;grid-template-columns:1fr auto;padding:7px 12px;background:var(--s2);border-bottom:1px solid var(--brd);}
.bom-hd span{font-size:9px;font-weight:700;color:var(--amb);letter-spacing:.08em;text-transform:uppercase;}
.bom-row{display:grid;grid-template-columns:1fr auto;padding:6px 12px;font-size:11px;}
.bom-row+.bom-row{border-top:1px solid var(--brd);}
.bom-row.sub{background:var(--s3);border-top:1px solid var(--brd2)!important;}
.bom-row.tot{background:linear-gradient(135deg,#0d2a10,#060f06);border-top:2px solid var(--grn)!important;}
.bl{color:var(--t2);}.bl.b{color:var(--t1);font-weight:700;}
.bv{text-align:right;}.bv.a{color:var(--amb);font-weight:700;}.bv.g{color:var(--grn);font-weight:700;font-size:13px;}

/* ──── TIER CARDS ──── */
.tiers{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-top:12px;}
.tc{background:var(--s2);border:1px solid var(--brd);border-radius:9px;padding:12px;text-align:center;}
.tc.on{background:linear-gradient(135deg,#0d2a10,#060f06);border-color:#22c55e33;}

/* ──── PROMPT ──── */
.pbtn{width:100%;padding:14px;border:none;border-radius:9px;font-family:inherit;font-size:16px;font-weight:900;letter-spacing:.06em;cursor:pointer;transition:all .2s;text-transform:uppercase;}
.pbtn.idle{background:linear-gradient(135deg,#d97706,#92400e);color:#fff;box-shadow:0 0 28px #f59e0b20;}
.pbtn.done{background:linear-gradient(135deg,#166534,#14532d);color:#fff;box-shadow:0 0 28px #22c55e20;}
.ppreview{background:var(--s1);border:1px solid var(--brd);border-radius:9px;padding:12px;max-height:150px;overflow-y:auto;margin-top:10px;}
.ppreview pre{font-size:9px;color:var(--t3);white-space:pre-wrap;line-height:1.7;}

/* ──── HELP ──── */
.help-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.help-card{background:var(--s2);border:1px solid var(--brd);border-radius:9px;padding:14px;}
.help-term{font-size:13px;font-weight:900;color:var(--amb);margin-bottom:4px;letter-spacing:.03em;}
.help-abbr{font-size:10px;color:var(--t3);font-weight:700;letter-spacing:.08em;text-transform:uppercase;margin-bottom:6px;}
.help-def{font-size:11px;color:var(--t2);line-height:1.6;}
.help-ex{font-size:10px;color:var(--grn);margin-top:4px;font-style:italic;}

/* ──── ENGINEERING ──── */
.eng-box{background:var(--s2);border:1px solid var(--brd);border-radius:9px;padding:14px;margin-top:12px;}
.eng-title{font-size:11px;font-weight:900;color:var(--amb);letter-spacing:.08em;text-transform:uppercase;margin-bottom:10px;}
.checklist{display:flex;flex-direction:column;gap:6px;}
.chk-item{display:flex;align-items:flex-start;gap:8px;font-size:11px;color:var(--t2);padding:6px 10px;border-radius:6px;background:var(--s3);}
.chk-item .ico{font-size:13px;margin-top:1px;flex-shrink:0;}

/* ──── TRANSPORT ──── */
.trans-summary{background:linear-gradient(135deg,#0d1f35,#071020);border:1px solid var(--brd2);border-radius:9px;padding:14px;margin-top:12px;}

/* ──── PROGRESS BAR ──── */
.pbar-wrap{background:var(--s3);border-radius:20px;height:6px;overflow:hidden;margin-top:4px;}
.pbar{height:100%;border-radius:20px;transition:width .3s;}

/* ──── ANIMATION ──── */
@keyframes fi{from{opacity:0;transform:translateY(5px);}to{opacity:1;transform:translateY(0);}}
.fi{animation:fi .15s ease;}

/* ──── RESPONSIVE ──── */
@media(max-width:760px){
  #sidenav,#rpanel{display:none!important;}
  #bnav{display:block;}
  .content{padding:13px;padding-bottom:110px;}
  .g2,.g3,.g4{grid-template-columns:1fr!important;}
  .mgrid,.mgrid4{grid-template-columns:1fr 1fr;}
  .st-grid{grid-template-columns:1fr 1fr;}
  .tiers{grid-template-columns:1fr;}
  .help-grid{grid-template-columns:1fr;}
  .chip{display:none;}
}
@media(max-width:380px){.mgrid,.mgrid4{grid-template-columns:1fr 1fr;}.logo{font-size:16px;}}
@media(min-width:761px) and (max-width:1060px){#rpanel{width:158px;}.g3,.g4{grid-template-columns:1fr 1fr;}}
</style>
</head>
<body>
<div class="app">
<div id="hdr">
  <div><div class="logo">☀ SolarPM Pro</div><div class="logo-sub">Universal Solar Configurator v3</div></div>
  <div class="hdr-right">
    <div id="hdr-chip" class="chip"></div>
    <div class="kw-box"><div class="kw-lbl">System</div><div class="kw-val" id="hdr-kwp">—</div></div>
  </div>
</div>
<div id="ticker"></div>
<div id="body">
  <div id="sidenav"></div>
  <div id="main"><div class="content" id="content"></div></div>
  <div id="rpanel"></div>
</div>
<div id="bnav"><div class="bnav-inner" id="bnav-inner"></div></div>
</div>

<script>
// ══════════════════════════════════════════════════════
// MATH
// ══════════════════════════════════════════════════════
function calcIRR(cfs,g){
  g=g||.15;var r=g;
  for(var i=0;i<2000;i++){
    var n=cfs.reduce(function(a,c,t){return a+c/Math.pow(1+r,t);},0);
    var d=cfs.reduce(function(a,c,t){return a+(-t*c)/Math.pow(1+r,t+1);},0);
    if(Math.abs(d)<1e-12)break;var r2=r-n/d;
    if(Math.abs(r2-r)<1e-8)return r2;r=r2;
  }return r;
}
function calcNPV(rate,cfs){return cfs.reduce(function(a,c,t){return a+c/Math.pow(1+rate/100,t);},0);}
function fmt(n,d){d=d||0;if(typeof n!=='number'||!isFinite(n))return'—';return n.toLocaleString('en',{minimumFractionDigits:d,maximumFractionDigits:d});}
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}

// ══════════════════════════════════════════════════════
// STATION TYPES
// ══════════════════════════════════════════════════════
var TYPES={
  telecom:{n:'Telecom BTS',ico:'🗼',desc:'Cell tower / BTS, generator-only site',col:'#60a5fa',tag:'COMMON',
    p:{mc:1000,pl:10,ps:'Generator Only',gh:0,dl:2000,dp:20,pw:720,pt:'Resin Monocrystalline',np:21,ik:15,it:'Grid-Tied String',ip:'Three-phase',ni:1,psh:6.2,pr:80,bess:0,bk:0,bp:0,mf:20000,cy:3,ct:'ESA',ppw:9,ipr:135000,mpp:1000,dcm:300,dcp:50,acm:60,acp:50,mtr:2500,cmb:7000,dcd:2000,acp2:4000,spd:2500,erth:3500,cnd:3000,mc4:800,la:45000,gc:25000,cng:5,pmpct:3,om:4380,ins_c:1460,mon:660,rdl:100,voc:50,vmp:42,isc:14.5,imp:13.8,lat:31}},
  residential:{n:'Residential',ico:'🏠',desc:'Home rooftop, grid-tied or hybrid',col:'#22c55e',tag:'',
    p:{mc:350,pl:5,ps:'Grid Only',gh:24,dl:0,dp:0,pw:450,pt:'Monocrystalline PERC',np:10,ik:5,it:'Grid-Tied String',ip:'Single-phase',ni:1,psh:5.5,pr:78,bess:0,bk:0,bp:0,mf:2500,cy:5,ct:'ESA',ppw:8,ipr:32000,mpp:800,dcm:80,dcp:40,acm:20,acp:40,mtr:1500,cmb:4000,dcd:1200,acp2:2500,spd:1500,erth:2000,cnd:1500,mc4:500,la:15000,gc:4000,cng:5,pmpct:3,om:1000,ins_c:500,mon:300,rdl:0,voc:37,vmp:31,isc:11,imp:10.5,lat:31}},
  commercial:{n:'Commercial',ico:'🏢',desc:'Office / retail, business hours load',col:'#a78bfa',tag:'',
    p:{mc:8000,pl:60,ps:'Grid Only',gh:24,dl:0,dp:0,pw:550,pt:'Bifacial Monocrystalline',np:120,ik:60,it:'Grid-Tied String',ip:'Three-phase',ni:2,psh:5.5,pr:80,bess:0,bk:0,bp:0,mf:35000,cy:7,ct:'ESA',ppw:8.5,ipr:92000,mpp:900,dcm:500,dcp:50,acm:100,acp:50,mtr:2500,cmb:7000,dcd:2000,acp2:4000,spd:2500,erth:3500,cnd:3000,mc4:800,la:55000,gc:20000,cng:5,pmpct:3,om:6000,ins_c:3000,mon:1200,rdl:0,voc:44,vmp:37,isc:13,imp:12.5,lat:31}},
  industrial:{n:'Industrial',ico:'🏭',desc:'Factory / warehouse, large 3-phase',col:'#fb923c',tag:'HIGH VALUE',
    p:{mc:50000,pl:300,ps:'Grid + Generator',gh:24,dl:8000,dp:20,pw:550,pt:'Bifacial Monocrystalline',np:600,ik:300,it:'Central',ip:'Three-phase',ni:3,psh:5.8,pr:81,bess:0,bk:0,bp:0,mf:180000,cy:10,ct:'ESA',ppw:7.5,ipr:280000,mpp:850,dcm:2000,dcp:55,acm:300,acp:55,mtr:5000,cmb:15000,dcd:4000,acp2:8000,spd:5000,erth:7000,cnd:8000,mc4:2000,la:180000,gc:60000,cng:5,pmpct:3,om:25000,ins_c:12000,mon:3600,rdl:500,voc:44,vmp:37,isc:13,imp:12.5,lat:31}},
  agricultural:{n:'Agricultural',ico:'🌾',desc:'Farm / irrigation pump, daytime load',col:'#84cc16',tag:'',
    p:{mc:2500,pl:22,ps:'Generator Only',gh:0,dl:1800,dp:20,pw:500,pt:'Monocrystalline PERC',np:55,ik:25,it:'Grid-Tied String',ip:'Three-phase',ni:1,psh:6.0,pr:79,bess:0,bk:0,bp:0,mf:9000,cy:5,ct:'ESA',ppw:8,ipr:55000,mpp:800,dcm:400,dcp:50,acm:80,acp:50,mtr:2500,cmb:7000,dcd:2000,acp2:4000,spd:2500,erth:3500,cnd:3000,mc4:800,la:35000,gc:20000,cng:5,pmpct:3,om:3000,ins_c:1500,mon:600,rdl:100,voc:40,vmp:34,isc:12.5,imp:12,lat:31}},
  water:{n:'Water Pumping',ico:'💧',desc:'Off-grid borehole / pump station',col:'#22d3ee',tag:'',
    p:{mc:900,pl:8,ps:'Generator Only',gh:0,dl:1400,dp:20,pw:400,pt:'Monocrystalline PERC',np:25,ik:10,it:'Hybrid',ip:'Three-phase',ni:1,psh:6.0,pr:78,bess:1,bk:25,bp:1800,mf:6000,cy:5,ct:'ESA',ppw:8,ipr:50000,mpp:800,dcm:200,dcp:50,acm:60,acp:50,mtr:2500,cmb:5000,dcd:2000,acp2:3500,spd:2500,erth:3500,cnd:2500,mc4:600,la:30000,gc:8000,cng:5,pmpct:3,om:2500,ins_c:1200,mon:480,rdl:50,voc:36,vmp:30,isc:12,imp:11.5,lat:31}},
  school:{n:'School / Clinic',ico:'🏫',desc:'Community facility, reliable power',col:'#f472b6',tag:'SOCIAL',
    p:{mc:1800,pl:16,ps:'Grid + Generator',gh:12,dl:1000,dp:20,pw:400,pt:'Monocrystalline PERC',np:50,ik:20,it:'Hybrid',ip:'Three-phase',ni:1,psh:5.8,pr:79,bess:1,bk:40,bp:1800,mf:7500,cy:5,ct:'ESA',ppw:8,ipr:60000,mpp:800,dcm:250,dcp:50,acm:70,acp:50,mtr:2500,cmb:6000,dcd:2000,acp2:4000,spd:2500,erth:3500,cnd:3000,mc4:700,la:32000,gc:10000,cng:5,pmpct:3,om:2800,ins_c:1400,mon:560,rdl:80,voc:36,vmp:30,isc:12,imp:11.5,lat:31}},
  offgrid:{n:'Remote Off-Grid',ico:'🌍',desc:'Full BESS, diesel backup, no grid',col:'#f59e0b',tag:'',
    p:{mc:700,pl:6,ps:'Generator Only',gh:0,dl:1600,dp:20,pw:400,pt:'Monocrystalline PERC',np:28,ik:10,it:'Off-Grid',ip:'Single-phase',ni:1,psh:6.0,pr:78,bess:1,bk:60,bp:1800,mf:9000,cy:5,ct:'ESA',ppw:8.5,ipr:55000,mpp:900,dcm:220,dcp:50,acm:50,acp:50,mtr:2500,cmb:5000,dcd:2000,acp2:3500,spd:2500,erth:3500,cnd:2500,mc4:600,la:35000,gc:5000,cng:5,pmpct:3,om:3200,ins_c:1600,mon:640,rdl:60,voc:36,vmp:30,isc:12,imp:11.5,lat:31}},
  utility:{n:'Utility Scale',ico:'⚡',desc:'Large ground-mount MW+ PPA project',col:'#fbbf24',tag:'ENTERPRISE',
    p:{mc:600000,pl:1500,ps:'Grid Only',gh:24,dl:0,dp:0,pw:720,pt:'Bifacial Monocrystalline',np:2500,ik:1500,it:'Central',ip:'Three-phase',ni:6,psh:6.0,pr:82,bess:0,bk:0,bp:0,mf:1200000,cy:20,ct:'PPA',ppw:6.5,ipr:500000,mpp:700,dcm:15000,dcp:55,acm:2000,acp:55,mtr:15000,cmb:50000,dcd:15000,acp2:25000,spd:15000,erth:20000,cnd:25000,mc4:8000,la:800000,gc:400000,cng:4,pmpct:3,om:180000,ins_c:90000,mon:36000,rdl:0,voc:50,vmp:42,isc:14.5,imp:13.8,lat:27}},
  ev:{n:'EV Charging Hub',ico:'🚗',desc:'Solar canopy + BESS + EV chargers',col:'#34d399',tag:'GROWING',
    p:{mc:12000,pl:100,ps:'Grid Only',gh:24,dl:0,dp:0,pw:550,pt:'Bifacial Monocrystalline',np:200,ik:100,it:'Hybrid',ip:'Three-phase',ni:2,psh:5.5,pr:80,bess:1,bk:150,bp:1600,mf:45000,cy:7,ct:'ESA',ppw:8,ipr:120000,mpp:950,dcm:800,dcp:55,acm:150,acp:55,mtr:5000,cmb:12000,dcd:4000,acp2:6000,spd:4000,erth:5000,cnd:6000,mc4:1500,la:80000,gc:40000,cng:5,pmpct:3,om:9000,ins_c:4500,mon:1800,rdl:0,voc:44,vmp:37,isc:13,imp:12.5,lat:31}},
  hotel:{n:'Hotel / Resort',ico:'🏨',desc:'24/7 hospitality, rooftop + ground',col:'#e879f9',tag:'',
    p:{mc:25000,pl:180,ps:'Grid + Generator',gh:24,dl:3000,dp:20,pw:550,pt:'Bifacial Monocrystalline',np:350,ik:180,it:'Grid-Tied String',ip:'Three-phase',ni:3,psh:5.6,pr:80,bess:0,bk:0,bp:0,mf:85000,cy:8,ct:'ESA',ppw:8,ipr:150000,mpp:900,dcm:1200,dcp:55,acm:200,acp:55,mtr:5000,cmb:12000,dcd:4000,acp2:7000,spd:4000,erth:5000,cnd:6000,mc4:1500,la:100000,gc:35000,cng:5,pmpct:3,om:14000,ins_c:7000,mon:2800,rdl:200,voc:44,vmp:37,isc:13,imp:12.5,lat:31}},
};

// ══════════════════════════════════════════════════════
// STATE
// ══════════════════════════════════════════════════════
var S={
  tab:'type',stype:'telecom',
  name:'',ref:'',by:'SolarPM Pro',country:'',city:'',sites:1,mount:'Ground-mount elevated',
  util:'',gt:2.5,nm:'Available',gconn:'New connection required',
  cur:'EGP',xr:50,lp:'Flat 24/7',hasbat:0,batcap:'',mgb:0,
  // transport
  tr_dist:150,tr_trucks:2,tr_cpm:15,tr_fuel:500,
  tr_crew:6,tr_days:7,tr_perdiem:200,tr_accom:3000,
  tr_siteprep:5000,tr_security:2000,tr_customs:0,
  // engineering
  voc:50,vmp:42,isc:14.5,imp:13.8,lat:31,
};
Object.assign(S,TYPES.telecom.p);

// ══════════════════════════════════════════════════════
// CALCULATIONS
// ══════════════════════════════════════════════════════
function calc(){
  var s=S;
  var kw=(s.np*s.pw)/1000;
  var dg=kw*s.psh*(s.pr/100);
  var mg=dg*30,ag=dg*365;
  var mc=s.mc||1;
  var exp=Math.max(0,mg-mc);
  var nmc=exp*(s.gt||0);
  var cov=(mg/mc)*100;

  var pt=s.np*s.pw*(s.ppw||0);
  var it=s.ni*(s.ipr||0);
  var mt=s.np*(s.mpp||0);
  var dc=(s.dcm||0)*(s.dcp||0);
  var ac=(s.acm||0)*(s.acp||0);
  var bt=s.bess?(s.bk||0)*(s.bp||0):0;
  var eq=pt+it+mt+dc+ac+(s.mtr||0)+(s.cmb||0)+(s.dcd||0)+(s.acp2||0)+(s.spd||0)+(s.erth||0)+(s.cnd||0)+(s.mc4||0)+bt;

  // transport
  var tr_equip=(s.tr_dist||0)*(s.tr_trucks||0)*(s.tr_cpm||0)*2;
  var tr_crew_cost=(s.tr_crew||0)*(s.tr_days||0)*(s.tr_perdiem||0);
  var tr_total=tr_equip+tr_crew_cost+(s.tr_accom||0)+(s.tr_siteprep||0)+(s.tr_security||0)+(s.tr_customs||0)+(s.tr_fuel||0);

  var ins_sub=(s.la||0)+(s.gc||0);
  var dir=eq+ins_sub+tr_total;
  var cng=dir*(s.cng||0)/100;
  var pmv=dir*(s.pmpct||0)/100;
  var capex=dir+cng+pmv;
  var cpkw=kw>0?capex/kw:0;

  var diesel=(s.dl||0)*(s.dp||0);
  var gb=s.mgb||0;
  var cur=diesel+gb;
  var rd=(s.rdl||0)*(s.dp||0);
  var ng=Math.max(0,mc-mg)*(s.gt||0);
  var post=s.mf+rd+Math.max(0,ng-nmc);
  var sav=cur-post;
  var savpct=cur>0?(sav/cur)*100:0;
  var totsav=sav*12*(s.cy||1);

  var ar=(s.mf||0)*12;
  var ao=(s.om||0)+(s.ins_c||0)+(s.mon||0);
  var an=ar-ao;
  var pb=an>0?capex/an:Infinity;

  var cfs=[-capex];
  for(var y=1;y<=Math.min(s.cy||1,25);y++) cfs.push(ar*Math.pow(1+(s.esc||0)/100,y-1)-ao);
  var ir=calcIRR(cfs)*100;
  var nv=calcNPV(s.dr||20,cfs);
  var tot=cfs.slice(1).reduce(function(a,b){return a+b;},0);
  var np2=tot-capex;
  var te=ag*(s.cy||1);
  var lcoe=te>0?(capex+ao*(s.cy||1))/te:0;

  // monthly yield
  var lat=Math.abs(s.lat||30);
  var N_factors=[.65,.72,.87,.97,1.06,1.12,1.12,1.07,.98,.87,.71,.63];
  var S_factors=[1.12,1.07,.98,.87,.71,.63,.65,.72,.87,.97,1.06,1.12];
  var mf=(s.lat||0)>=0?N_factors:S_factors;
  var months=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  var mdays=[31,28,31,30,31,30,31,31,30,31,30,31];
  var monthly=months.map(function(m,i){
    var gen=kw*s.psh*mf[i]*(s.pr/100)*mdays[i];
    return{m:m,gen:gen,days:mdays[i],factor:mf[i]};
  });

  // engineering
  var voc=s.voc||50,vmp=s.vmp||42,isc=s.isc||14.5,imp=s.imp||13.8;
  var inv_vmax=s.it==='Central'?1500:1000;
  var max_series=Math.floor(inv_vmax/voc);
  var rec_series=Math.min(max_series,Math.max(4,Math.floor(inv_vmax*0.85/vmp)));
  var strings_total=s.np>0&&rec_series>0?Math.ceil(s.np/rec_series):0;
  var str_voc=rec_series*voc;
  var str_vmp=rec_series*vmp;
  var dc_current=imp*Math.ceil(strings_total/s.ni);
  var dc_ac_ratio=kw>0&&s.ik>0?kw/(s.ik*s.ni):0;
  var spec_yield=kw>0?ag/kw:0;
  var rec_tilt=Math.round(lat*0.87+3.1);
  var dc_cable_size=dc_current>20?10:dc_current>14?6:4;
  var ac_power=s.ik*s.ni;
  var ac_current_kva=s.ip==='Three-phase'?(ac_power*1000)/(Math.sqrt(3)*400):(ac_power*1000)/230;
  var ac_cable_size=ac_current_kva>100?70:ac_current_kva>63?35:ac_current_kva>32?16:10;

  return{kw:kw,dg:dg,mg:mg,ag:ag,exp:exp,nmc:nmc,cov:cov,
    pt:pt,it:it,mt:mt,dc:dc,ac:ac,bt:bt,eq:eq,ins_sub:ins_sub,
    tr_equip:tr_equip,tr_crew_cost:tr_crew_cost,tr_total:tr_total,
    dir:dir,cng:cng,pmv:pmv,capex:capex,cpkw:cpkw,
    diesel:diesel,gb:gb,cur:cur,rd:rd,post:post,sav:sav,savpct:savpct,totsav:totsav,
    ar:ar,ao:ao,an:an,pb:pb,cfs:cfs,ir:ir,nv:nv,np2:np2,lcoe:lcoe,
    monthly:monthly,
    max_series:max_series,rec_series:rec_series,strings_total:strings_total,
    str_voc:str_voc,str_vmp:str_vmp,dc_current:dc_current,dc_ac_ratio:dc_ac_ratio,
    spec_yield:spec_yield,rec_tilt:rec_tilt,dc_cable_size:dc_cable_size,
    ac_cable_size:ac_cable_size,ac_current_kva:ac_current_kva};
}

// ══════════════════════════════════════════════════════
// ARCHITECTURE: metrics update vs full render
// Input changes → updateMetrics() only (NO form re-render = no focus loss)
// Tab switch → renderTab() + updateMetrics()
// Structural toggles (BESS, hasbat) → rerenderCurrentTab()
// ══════════════════════════════════════════════════════
function C(){return S.cur||'EGP';}
function XR(){return S.xr||50;}
function usd(n){return'$'+fmt(n/XR());}

function updateMetrics(){
  var c=calc();
  var T=TYPES[S.stype];
  var chip=document.getElementById('hdr-chip');
  if(chip){chip.textContent=T.ico+' '+T.n;chip.style.background=T.col+'18';chip.style.borderColor=T.col+'40';chip.style.color=T.col;}
  var kwEl=document.getElementById('hdr-kwp');
  if(kwEl)kwEl.textContent=fmt(c.kw,2)+' kWp';
  
  var tc=document.getElementById('ticker');
  if(!tc)return;
  tc.innerHTML='';
  var tks=[
    {l:'CapEx',v:C()+' '+fmt(c.capex),cl:c.tr_total>0?'var(--ora)':'var(--t1)'},
    {l:'Transport',v:C()+' '+fmt(c.tr_total),cl:'var(--ora)'},
    {l:'Fee/mo',v:C()+' '+fmt(S.mf),cl:'var(--amb)'},
    {l:'Payback',v:isFinite(c.pb)?fmt(c.pb,1)+' yrs':'—',cl:'var(--blu)'},
    {l:'IRR',v:isFinite(c.ir)?fmt(c.ir,1)+'%':'—',cl:c.ir>20?'var(--grn)':c.ir>10?'var(--amb)':'var(--red)'},
    {l:'NPV@'+(S.dr||20)+'%',v:C()+' '+fmt(c.nv),cl:c.nv>0?'var(--grn)':'var(--red)'},
    {l:'Saves/mo',v:C()+' '+fmt(c.sav),cl:'var(--grn)'},
    {l:'Coverage',v:fmt(c.cov,0)+'%',cl:c.cov>=100?'var(--grn)':'var(--amb)'},
    {l:'LCOE',v:C()+' '+fmt(c.lcoe,2)+'/kWh',cl:'var(--t2)'},
  ];
  tks.forEach(function(t){
    var d=document.createElement('div');d.className='tick';
    d.innerHTML='<div class="tick-l">'+t.l+'</div><div class="tick-v" style="color:'+t.cl+'">'+t.v+'</div>';
    tc.appendChild(d);
  });

  // right panel
  var rp=document.getElementById('rpanel');
  if(!rp)return;
  rp.innerHTML='';
  function rpsec(ttl){var d=document.createElement('div');d.className='rp-sec';d.textContent=ttl;rp.appendChild(d);}
  function rprow(l,v,cl){var d=document.createElement('div');d.className='rp-row';d.innerHTML='<span class="rp-l">'+l+'</span><span class="rp-v" style="color:'+(cl||'var(--amb)')+'">'+v+'</span>';rp.appendChild(d);}
  rpsec('System');
  rprow('kWp',fmt(c.kw,2)+' kWp','var(--t1)');
  rprow('Monthly',fmt(c.mg,0)+' kWh');
  rprow('Coverage',fmt(c.cov,0)+'%',c.cov>=100?'var(--grn)':'var(--amb)');
  rprow('Export',fmt(c.exp,0)+' kWh/mo','var(--cyn)');
  rpsec('CapEx');
  rprow('Equip.',C()+' '+fmt(c.eq),'var(--t2)');
  rprow('Transport',C()+' '+fmt(c.tr_total),'var(--ora)');
  rprow('Total',C()+' '+fmt(c.capex),'var(--t1)');
  rprow('/kWp',C()+' '+fmt(c.cpkw,0),'var(--t2)');
  rpsec('Returns');
  rprow('Payback',isFinite(c.pb)?fmt(c.pb,1)+' yrs':'—','var(--blu)');
  rprow('IRR',isFinite(c.ir)?fmt(c.ir,1)+'%':'—',c.ir>20?'var(--grn)':c.ir>10?'var(--amb)':'var(--red)');
  rprow('NPV@'+(S.dr||20)+'%',C()+' '+fmt(c.nv),c.nv>0?'var(--grn)':'var(--red)');
  rprow('Net Profit',C()+' '+fmt(c.np2),'var(--grn)');
  rprow('LCOE',C()+' '+fmt(c.lcoe,2)+'/kWh');
  rpsec('Client');
  rprow('Before',C()+' '+fmt(c.cur)+'/mo','var(--red)');
  rprow('After',C()+' '+fmt(c.post)+'/mo','var(--amb)');
  rprow('Saves/mo',C()+' '+fmt(c.sav),'var(--grn)');
  rprow('Saves %',fmt(c.savpct,0)+'%','var(--grn)');
  var cpbtn=document.createElement('button');
  cpbtn.style.cssText='width:100%;margin-top:12px;padding:8px 0;border-radius:6px;border:1px solid var(--amb);background:#f59e0b15;color:var(--amb);font-family:inherit;font-size:11px;font-weight:900;cursor:pointer;letter-spacing:.06em;text-transform:uppercase;';
  cpbtn.textContent='⬇ Copy Prompt';
  cpbtn.onclick=copyPrompt;
  rp.appendChild(cpbtn);
}

// ══════════════════════════════════════════════════════
// INPUT HELPERS — fire updateMetrics only, no form re-render
// ══════════════════════════════════════════════════════
function numInp(key,opts){
  opts=opts||{};
  var i=document.createElement('input');
  i.type='number';i.className='inp';
  i.value=S[key]!==undefined?S[key]:'';
  if(opts.min!=null)i.min=opts.min;
  if(opts.max!=null)i.max=opts.max;
  if(opts.step!=null)i.step=opts.step;
  i.addEventListener('input',function(){
    var v=this.value===''?0:parseFloat(this.value)||0;
    S[key]=v;
    updateMetrics();
    // live hint update if present
    if(opts.liveHint){var el=document.getElementById(opts.liveHint);if(el)el.textContent=opts.liveHintFn();}
  });
  return i;
}
function txtInp(key,ph){
  var i=document.createElement('input');
  i.type='text';i.className='inp';
  i.value=S[key]||'';if(ph)i.placeholder=ph;
  i.addEventListener('input',function(){S[key]=this.value;updateMetrics();});
  return i;
}
function selInp(key,opts,onChange){
  var s=document.createElement('select');s.className='sel';
  opts.forEach(function(o){var op=document.createElement('option');op.value=o;op.textContent=o;if(S[key]===o)op.selected=true;s.appendChild(op);});
  s.addEventListener('change',function(){S[key]=this.value;if(onChange)onChange();else updateMetrics();});
  return s;
}
function chkInp(key,lbl,onChange){
  var d=document.createElement('div');d.className='chkrow';
  var box=document.createElement('div');box.className='chkbox'+(S[key]?' on':'');box.textContent='✓';
  var sp=document.createElement('span');sp.className='chk-l';sp.textContent=lbl;
  d.appendChild(box);d.appendChild(sp);
  d.addEventListener('click',function(){S[key]=S[key]?0:1;if(onChange)onChange();else updateMetrics();});
  return d;
}
function fld(lbl,hint,child,opts){
  opts=opts||{};
  var d=document.createElement('div');d.className='fld';
  if(opts.full)d.style.gridColumn='1/-1';
  d.innerHTML='<div class="fld-l">'+lbl+'</div>'+(hint?'<div class="fld-h">'+hint+'</div>':'');
  d.appendChild(child);
  return d;
}
function secH(ico,ttl){
  var d=document.createElement('div');d.className='sec-hd';
  d.innerHTML='<span class="sec-ico">'+ico+'</span><span class="sec-ttl">'+ttl+'</span>';
  return d;
}
function div2(cls,html){var d=document.createElement('div');if(cls)d.className=cls;if(html)d.innerHTML=html;return d;}
function grid(cols){var d=document.createElement('div');d.className=cols||'g2';return d;}
function mcard(lbl,val,sub,col,hi){
  col=col||'var(--amb)';
  var d=div2('mcard'+(hi?' hi':''));d.style.borderLeftColor=col;
  d.innerHTML='<div class="mc-l">'+esc(lbl)+'</div><div class="mc-v" style="color:'+col+'">'+esc(String(val))+'</div>'+(sub?'<div class="mc-s">'+esc(String(sub))+'</div>':'');
  return d;
}

// re-render current tab (for structural changes)
function rerenderCurrentTab(){
  renderTab(S.tab);
  updateMetrics();
}

// ══════════════════════════════════════════════════════
// TAB RENDERER
// ══════════════════════════════════════════════════════
var TABS=[
  {id:'type',ico:'🔷',lbl:'Type'},
  {id:'site',ico:'📌',lbl:'Site'},
  {id:'solar',ico:'☀️',lbl:'Solar'},
  {id:'bom',ico:'🏷️',lbl:'BOM'},
  {id:'transport',ico:'🚚',lbl:'Transport'},
  {id:'fin',ico:'📈',lbl:'Finance'},
  {id:'eng',ico:'🔬',lbl:'Engineering'},
  {id:'results',ico:'🎯',lbl:'Results'},
  {id:'help',ico:'❓',lbl:'Help'},
];

function switchTab(id){
  S.tab=id;
  // update nav buttons
  document.querySelectorAll('.snbtn,.bnbtn').forEach(function(b){
    b.classList.toggle('on',b.dataset.tab===id);
  });
  renderTab(id);
  updateMetrics();
}

function renderNav(){
  var sn=document.getElementById('sidenav');
  var bni=document.getElementById('bnav-inner');
  sn.innerHTML='';bni.innerHTML='';
  TABS.forEach(function(t){
    var b=document.createElement('button');
    b.className='snbtn'+(S.tab===t.id?' on':'');b.dataset.tab=t.id;
    b.innerHTML='<span class="sn-ico">'+t.ico+'</span><span>'+t.lbl+'</span>';
    b.addEventListener('click',function(){switchTab(t.id);});
    sn.appendChild(b);
    var bb=document.createElement('button');
    bb.className='bnbtn'+(S.tab===t.id?' on':'');bb.dataset.tab=t.id;
    bb.innerHTML='<span class="bn-ico">'+t.ico+'</span>'+t.lbl;
    bb.addEventListener('click',function(){switchTab(t.id);});
    bni.appendChild(bb);
  });
}

function renderTab(tab){
  var con=document.getElementById('content');
  con.innerHTML='';
  con.classList.remove('fi');
  void con.offsetWidth;
  con.classList.add('fi');
  var c=calc();
  var T=TYPES[S.stype];
  if(tab==='type')renderType(con,c,T);
  else if(tab==='site')renderSite(con,c,T);
  else if(tab==='solar')renderSolar(con,c,T);
  else if(tab==='bom')renderBOM(con,c,T);
  else if(tab==='transport')renderTransport(con,c,T);
  else if(tab==='fin')renderFin(con,c,T);
  else if(tab==='eng')renderEng(con,c,T);
  else if(tab==='results')renderResults(con,c,T);
  else if(tab==='help')renderHelp(con);
}

// ══════════════════════════════════════════════════════
// TAB: TYPE
// ══════════════════════════════════════════════════════
function renderType(con,c,T){
  con.appendChild(secH('🔷','Select Station Type'));
  var p=div2('',''); p.style.cssText='font-size:11px;color:var(--t3);margin-bottom:14px;line-height:1.6;';
  p.textContent='Choose your installation type. All defaults load automatically — customise everything in the next tabs.';
  con.appendChild(p);
  var sg=div2('st-grid');
  Object.keys(TYPES).forEach(function(key){
    var TT=TYPES[key];
    var card=div2('stcard'+(S.stype===key?' on':''));
    card.style.borderColor=S.stype===key?TT.col:'var(--brd)';
    var glow=div2('st-glow');glow.style.background=TT.col;card.appendChild(glow);
    var kwp=fmt((TT.p.np*TT.p.pw)/1000,1);
    card.innerHTML+='<div class="st-ico">'+TT.ico+'</div><div class="st-nm" style="color:'+(S.stype===key?TT.col:'var(--t1)')+'">'+TT.n+'</div><div class="st-desc">'+TT.desc+'</div><div class="st-kw">'+kwp+' kWp typical</div>'+(TT.tag?'<div class="st-tag" style="background:'+TT.col+'22;color:'+TT.col+'">'+TT.tag+'</div>':'');
    card.addEventListener('click',(function(k){return function(){pickType(k);};})(key));
    sg.appendChild(card);
  });
  con.appendChild(sg);
  var ib=div2('ibox mt12');
  ib.style.cssText='margin-top:12px;background:'+T.col+'08;border-color:'+T.col+'40;';
  ib.className='ibox';
  ib.innerHTML='✔ Selected: <span style="color:'+T.col+';font-weight:700">'+T.ico+' '+T.n+'</span> — '+T.desc+'. Next: <span style="color:var(--amb);font-weight:700">📌 Site tab</span>';
  con.appendChild(ib);
}
function pickType(key){
  var TT=TYPES[key];var prev={name:S.name,ref:S.ref,by:S.by,country:S.country,city:S.city,sites:S.sites,mount:S.mount,cur:S.cur,xr:S.xr,util:S.util,gt:S.gt,hasbat:S.hasbat,batcap:S.batcap,tr_dist:S.tr_dist,tr_trucks:S.tr_trucks,tr_cpm:S.tr_cpm,tr_fuel:S.tr_fuel,tr_crew:S.tr_crew,tr_days:S.tr_days,tr_perdiem:S.tr_perdiem,tr_accom:S.tr_accom,tr_siteprep:S.tr_siteprep,tr_security:S.tr_security,tr_customs:S.tr_customs};
  Object.assign(S,TT.p,prev);S.stype=key;
  if(!S.name)S.name=TT.n+' — Phase 1';
  switchTab('site');
}

// ══════════════════════════════════════════════════════
// TAB: SITE
// ══════════════════════════════════════════════════════
function renderSite(con){
  con.appendChild(secH('📌','Project Identity'));
  var g=grid('g2');con.appendChild(g);
  g.appendChild(fld('Project Name',null,txtInp('name','e.g. Matrouh BTS Phase 1')));
  g.appendChild(fld('Reference No.',null,txtInp('ref','SOL-EGY-2026-001')));
  g.appendChild(fld('Country',null,txtInp('country','e.g. Egypt')));
  g.appendChild(fld('City / Region',null,txtInp('city','e.g. Matrouh')));
  g.appendChild(fld('Number of Sites (Phase 1)',null,numInp('sites',{min:1})));
  g.appendChild(fld('Prepared By',null,txtInp('by','')));
  g.appendChild(fld('Mounting Type',null,selInp('mount',['Ground-mount elevated','Ground-mount flat','Rooftop flat','Rooftop tilted','Carport / canopy','Both ground+roof'])));

  con.appendChild(div2('mt20'));con.appendChild(secH('⚡','Power & Load'));
  var g2=grid('g2');con.appendChild(g2);
  g2.appendChild(fld('Monthly Consumption','kWh/month',numInp('mc',{min:0})));
  g2.appendChild(fld('Daily Consumption (approx.)','kWh/day — for reference',numInp('daily_c',{min:0})));
  g2.appendChild(fld('Peak Load','Maximum kW demand',numInp('pl',{min:0,step:0.5})));
  g2.appendChild(fld('Load Profile',null,selInp('lp',['Flat 24/7','Higher daytime','Higher night','Business hours only','Seasonal / variable'])));
  g2.appendChild(fld('Current Power Source',null,selInp('ps',['Generator Only','Grid Only','Grid + Generator','Off-grid Battery','Other'])));
  g2.appendChild(fld('Grid Hours/Day','0 = no existing grid',numInp('gh',{min:0,max:24})));
  g2.appendChild(fld(C()+' Monthly Grid Bill','0 if no grid',numInp('mgb',{min:0})));
  var batF=div2('fld');batF.innerHTML='<div class="fld-l">Existing Battery / UPS</div>';
  batF.appendChild(chkInp('hasbat','Yes, site has existing battery bank',rerenderCurrentTab));
  if(S.hasbat){var bci=numInp('batcap',{min:0});bci.placeholder='Capacity kWh (optional)';batF.appendChild(div2('mt8'));batF.lastChild.appendChild(bci);}
  g2.appendChild(batF);

  con.appendChild(div2('mt20'));con.appendChild(secH('⛽','Diesel / Generator'));
  var g3=grid('g3');con.appendChild(g3);
  g3.appendChild(fld('Monthly Diesel (Liters)','0 if no diesel',numInp('dl',{min:0})));
  g3.appendChild(fld(C()+' per Liter',null,numInp('dp',{min:0,step:0.5})));
  g3.appendChild(fld('Residual Diesel Post-Solar','Emergency backup L/month',numInp('rdl',{min:0})));
  var c=calc();
  if(c.diesel>0){var ib=div2('ibox mt8');ib.className='ibox bad';ib.innerHTML='Current diesel: <span class="r">'+C()+' '+fmt(c.diesel)+'/mo</span> · Annual: <span class="r">'+C()+' '+fmt(c.diesel*12)+'</span> · <span class="v">'+usd(c.diesel*12)+'/yr</span>';con.appendChild(ib);}

  con.appendChild(div2('mt20'));con.appendChild(secH('🔌','Grid & Utility'));
  var g4=grid('g2');con.appendChild(g4);
  g4.appendChild(fld('Utility / Grid Operator',null,txtInp('util','EEHC, KPLC, NERC…')));
  g4.appendChild(fld(C()+'/kWh Grid Tariff',null,numInp('gt',{min:0,step:0.01})));
  g4.appendChild(fld('Net Metering',null,selInp('nm',['Available','Not Available','Under Review'])));
  g4.appendChild(fld('Grid Connection',null,selInp('gconn',['Existing connection','New connection required'])));

  con.appendChild(div2('mt20'));con.appendChild(secH('💱','Currency & Exchange'));
  var g5=grid('g2');con.appendChild(g5);
  g5.appendChild(fld('Local Currency','EGP, NGN, KES, SAR, USD…',txtInp('cur','EGP')));
  g5.appendChild(fld('Exchange Rate (local per USD)',null,numInp('xr',{min:0.01,step:0.01})));
}

// ══════════════════════════════════════════════════════
// TAB: SOLAR
// ══════════════════════════════════════════════════════
function renderSolar(con){
  var c=calc();
  con.appendChild(secH('☀️','Solar System Design'));
  var g=grid('g3');con.appendChild(g);
  g.appendChild(fld('Panel Wattage (Wp)',null,numInp('pw',{min:50})));
  g.appendChild(fld('Number of Panels',null,numInp('np',{min:1})));
  g.appendChild(fld('Panel Type',null,selInp('pt',['Resin Monocrystalline','Monocrystalline PERC','Bifacial Monocrystalline','Polycrystalline','Thin Film','HJT','TOPCon'])));
  g.appendChild(fld('Inverter Size (kW per unit)',null,numInp('ik',{min:0.5,step:0.5})));
  g.appendChild(fld('Number of Inverters',null,numInp('ni',{min:1})));
  g.appendChild(fld('Inverter Type',null,selInp('it',['Grid-Tied String','Hybrid','Central','Microinverter','Off-Grid'])));
  g.appendChild(fld('Inverter Phase Configuration',null,selInp('ip',['Single-phase','Three-phase'])));
  g.appendChild(fld('Peak Sun Hours/day','From solar resource map',numInp('psh',{min:1,max:10,step:0.1})));
  g.appendChild(fld('Performance Ratio %','75–85% typical',numInp('pr',{min:50,max:100})));

  var bessRow=div2('mt14');bessRow.appendChild(chkInp('bess','Include Battery Energy Storage System (BESS)',rerenderCurrentTab));con.appendChild(bessRow);
  if(S.bess){
    var gb=grid('g3');gb.className='g3 mt12';
    gb.appendChild(fld('BESS Capacity (kWh)',null,numInp('bk',{min:0})));
    gb.appendChild(fld(C()+'/kWh BESS Price',null,numInp('bp',{min:0})));
    var bti=div2('fld');bti.innerHTML='<div class="fld-l">BESS Cost</div><div class="ibox"><span class="v">'+C()+' '+fmt(c.bt)+'</span></div>';
    gb.appendChild(bti);con.appendChild(gb);
  }

  var live=div2('');live.style.cssText='margin-top:20px;background:var(--s3);border:1px solid var(--brd2);border-radius:9px;padding:14px;';
  live.innerHTML='<div style="font-size:10px;color:var(--amb);font-weight:700;letter-spacing:.08em;text-transform:uppercase;margin-bottom:12px;">⚡ Live Design Output</div>';
  var mg=div2('mgrid');
  var cov_ok=c.cov>=100;
  [
    {l:'System kWp',v:fmt(c.kw,2)+' kWp',cl:'var(--amb)',hi:0},
    {l:'Daily Generation',v:fmt(c.dg,1)+' kWh',cl:'var(--amb)',hi:0},
    {l:'Monthly Generation',v:fmt(c.mg,0)+' kWh',cl:'var(--amb)',hi:0},
    {l:'Solar Coverage',v:fmt(c.cov,0)+'%',cl:cov_ok?'var(--grn)':'var(--amb)',hi:cov_ok},
    {l:'Monthly Export',v:fmt(c.exp,0)+' kWh',cl:'var(--cyn)',hi:0},
    {l:'NM Credit/month',v:C()+' '+fmt(c.nmc,0),cl:'var(--grn)',hi:0},
  ].forEach(function(m){mg.appendChild(mcard(m.l,m.v,null,m.cl,m.hi));});
  live.appendChild(mg);
  if(c.kw>0&&S.pl>0){
    var clipping=c.dc_ac_ratio>1.35;
    var rb=div2('ibox warn mt12');rb.style.marginTop='10px';
    rb.innerHTML='DC/AC Ratio: <span class="v">'+fmt(c.dc_ac_ratio,2)+'×</span> · Inv/Load: <span class="v">'+fmt(S.ik/S.pl,2)+'×</span> · Specific Yield: <span class="v">'+fmt(c.spec_yield,0)+' kWh/kWp/yr</span>'+(clipping?'<span class="r"> ⚠ High clipping (>1.35) — consider larger inverter</span>':'');
    live.appendChild(rb);
  }
  con.appendChild(live);
}

// ══════════════════════════════════════════════════════
// TAB: BOM
// ══════════════════════════════════════════════════════
function renderBOM(con){
  var c=calc();
  con.appendChild(secH('🏷️','Equipment Prices'));
  var g=grid('g2');con.appendChild(g);
  var pHint=div2('');pHint.id='p-hint';pHint.textContent='→ '+C()+' '+fmt(S.pw*(S.ppw||0))+' per panel';
  g.appendChild(fld('Panel Price ('+C()+'/Wp)',null,(function(){var w=div2('');w.appendChild(numInp('ppw',{min:0,step:0.1}));w.appendChild(pHint);return w;})()));
  g.appendChild(fld('Inverter ('+C()+'/unit)',null,numInp('ipr',{min:0})));
  g.appendChild(fld('Mounting Structure ('+C()+'/panel)',null,numInp('mpp',{min:0})));
  g.appendChild(fld('DC Cable — length (m)',null,numInp('dcm',{min:0})));
  g.appendChild(fld('DC Cable — price ('+C()+'/m)',null,numInp('dcp',{min:0})));
  g.appendChild(fld('AC Cable — length (m)',null,numInp('acm',{min:0})));
  g.appendChild(fld('AC Cable — price ('+C()+'/m)',null,numInp('acp',{min:0})));
  g.appendChild(fld('Smart Bidirectional Meter ('+C()+')',null,numInp('mtr',{min:0})));
  g.appendChild(fld('DC Combiner Box ('+C()+')',null,numInp('cmb',{min:0})));
  g.appendChild(fld('DC Disconnect Switch ('+C()+')',null,numInp('dcd',{min:0})));
  g.appendChild(fld('AC Protection Panel + MCBs ('+C()+')',null,numInp('acp2',{min:0})));
  g.appendChild(fld('Surge Protection Device — SPD ('+C()+')',null,numInp('spd',{min:0})));
  g.appendChild(fld('Earthing / Grounding System ('+C()+')',null,numInp('erth',{min:0})));
  g.appendChild(fld('Conduit, Trunking & Fittings ('+C()+')',null,numInp('cnd',{min:0})));
  g.appendChild(fld('MC4 Connectors & Lugs ('+C()+')',null,numInp('mc4',{min:0})));
  g.appendChild(fld('EPC Labor ('+C()+'/site)',null,numInp('la',{min:0})));
  g.appendChild(fld('Grid Connection + Permits ('+C()+')',null,numInp('gc',{min:0})));
  g.appendChild(fld('Contingency %','Applied to all direct costs',numInp('cng',{min:0,max:30})));
  g.appendChild(fld('Project Management %','Applied to all direct costs',numInp('pmpct',{min:0,max:20})));

  var bom=div2('bom');
  bom.innerHTML='<div class="bom-hd"><span>Item</span><span>'+C()+'</span></div>';
  var rows=[
    ['Panels ('+S.np+'×'+S.pw+'Wp @ '+S.ppw+' '+C()+'/W)',c.pt,0],
    ['Inverter ('+S.ni+'×'+S.ik+'kW)',c.it,0],
    ['Mounting Structure',c.mt,0],['DC Cable ('+S.dcm+'m)',c.dc,0],
    ['AC Cable ('+S.acm+'m)',c.ac,0],['Smart Meter',(S.mtr||0),0],
    ['Combiner + Disconnect + AC Panel',(S.cmb||0)+(S.dcd||0)+(S.acp2||0),0],
    ['SPD + Earthing + Conduit + MC4',(S.spd||0)+(S.erth||0)+(S.cnd||0)+(S.mc4||0),0],
  ];
  if(S.bess)rows.push(['BESS ('+S.bk+'kWh @ '+S.bp+' '+C()+'/kWh)',c.bt,0]);
  rows.push(['— Equipment Subtotal',c.eq,1]);
  rows.push(['EPC Labor',(S.la||0),0],['Grid Connection + Permits',(S.gc||0),0]);
  rows.push(['— Installation Subtotal',c.ins_sub,1]);
  rows.push(['Transport & Logistics (see Transport tab)',c.tr_total,0,1]);
  rows.push(['Contingency ('+S.cng+'%)',c.cng,0],['Project Mgmt ('+S.pmpct+'%)',c.pmv,0]);
  rows.forEach(function(r,i){
    var row=div2('bom-row'+(r[2]?' sub':''));
    if(!r[2]&&i%2===0)row.style.background='var(--s2)';
    var valColor=r[3]?'color:var(--ora);font-weight:700':'';
    row.innerHTML='<span class="bl'+(r[2]?' b':'')+'">'+r[0]+'</span><span class="bv'+(r[2]?' a':'')+'" style="'+valColor+'">'+fmt(r[1])+'</span>';
    bom.appendChild(row);
  });
  var tot=div2('bom-row tot');
  tot.innerHTML='<span class="bl b" style="color:var(--grn)">TOTAL PROJECT CAPEX</span><div style="text-align:right"><div class="bv g">'+C()+' '+fmt(c.capex)+'</div><div style="font-size:9px;color:var(--t3)">'+usd(c.capex)+'</div></div>';
  bom.appendChild(tot);
  con.appendChild(bom);
}

// ══════════════════════════════════════════════════════
// TAB: TRANSPORT
// ══════════════════════════════════════════════════════
function renderTransport(con){
  var c=calc();
  con.appendChild(secH('🚚','Transport & Logistics Costs'));
  var ib=div2('ibox');ib.innerHTML='Transport costs are calculated and <span class="v">automatically added to CapEx</span>. Leave fields at 0 if not applicable to your project.';
  con.appendChild(ib);

  con.appendChild(div2('mt16'));con.appendChild(secH('📦','Equipment Transport'));
  var g=grid('g2');con.appendChild(g);
  g.appendChild(fld('Distance from Warehouse','km (one-way)',numInp('tr_dist',{min:0})));
  g.appendChild(fld('Number of Trucks Required','for equipment delivery',numInp('tr_trucks',{min:0})));
  g.appendChild(fld(C()+' per km per Truck','transport cost',numInp('tr_cpm',{min:0,step:0.5})));
  g.appendChild(fld('Extra Fuel / Misc. Transport ('+C()+')','flat allowance',numInp('tr_fuel',{min:0})));
  g.appendChild(fld('Customs / Import Clearance ('+C()+')','if equipment is imported',numInp('tr_customs',{min:0})));

  var tb=div2('ibox mt8');
  tb.innerHTML='Equipment transport cost: <span class="v">'+C()+' '+fmt(c.tr_equip)+'</span> ('+S.tr_dist+'km × '+S.tr_trucks+' trucks × '+C()+S.tr_cpm+'/km × 2-way + fuel)';
  con.appendChild(tb);

  con.appendChild(div2('mt20'));con.appendChild(secH('👷','Installation Crew'));
  var g2=grid('g3');con.appendChild(g2);
  g2.appendChild(fld('Number of Crew Members',null,numInp('tr_crew',{min:0})));
  g2.appendChild(fld('Days On-Site',null,numInp('tr_days',{min:0})));
  g2.appendChild(fld(C()+' Per Diem per Person/day','meals + transport allowance',numInp('tr_perdiem',{min:0})));
  g2.appendChild(fld('Accommodation Cost ('+C()+' total)','hotel/camp for full duration',numInp('tr_accom',{min:0})));
  g2.appendChild(fld('Site Preparation ('+C()+')','civil works, fencing, access road',numInp('tr_siteprep',{min:0})));
  g2.appendChild(fld('Site Security ('+C()+')','guards, cameras during install',numInp('tr_security',{min:0})));

  var tb2=div2('ibox mt8');
  tb2.innerHTML='Crew cost: <span class="v">'+C()+' '+fmt(c.tr_crew_cost)+'</span> ('+S.tr_crew+' people × '+S.tr_days+' days × '+C()+S.tr_perdiem+')';
  con.appendChild(tb2);

  // Summary
  var sum=div2('trans-summary');
  sum.innerHTML='<div style="font-size:10px;color:var(--ora);font-weight:900;letter-spacing:.1em;text-transform:uppercase;margin-bottom:12px;">📊 Transport Summary</div>';
  var rows=[
    ['Equipment Transport (round trip)',c.tr_equip],
    ['Crew Per Diem',c.tr_crew_cost],
    ['Accommodation',(S.tr_accom||0)],
    ['Site Preparation',(S.tr_siteprep||0)],
    ['Security',(S.tr_security||0)],
    ['Customs / Import',(S.tr_customs||0)],
    ['Extra Fuel / Misc.',(S.tr_fuel||0)],
  ];
  rows.forEach(function(r){
    if(r[1]>0){
      var pct=c.capex>0?r[1]/c.capex*100:0;
      var d=div2('');d.style.cssText='display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--brd);font-size:11px;';
      d.innerHTML='<span style="color:var(--t2)">'+r[0]+'</span><span style="color:var(--ora);font-weight:700">'+C()+' '+fmt(r[1])+'</span>';
      sum.appendChild(d);
    }
  });
  var tot=div2('');tot.style.cssText='display:flex;justify-content:space-between;padding:10px 0 4px;font-size:13px;font-weight:900;';
  tot.innerHTML='<span style="color:var(--t1)">TOTAL TRANSPORT</span><div style="text-align:right"><div style="color:var(--ora)">'+C()+' '+fmt(c.tr_total)+'</div><div style="font-size:9px;color:var(--t3)">'+usd(c.tr_total)+' · '+fmt(c.capex>0?c.tr_total/c.capex*100:0,1)+'% of CapEx</div></div>';
  sum.appendChild(tot);
  var pbar_wrap=div2('pbar-wrap');var pbar=div2('pbar');
  pbar.style.cssText='width:'+Math.min(100,c.capex>0?c.tr_total/c.capex*100:0)+'%;background:var(--ora);';
  pbar_wrap.appendChild(pbar);sum.appendChild(pbar_wrap);
  con.appendChild(sum);
}

// ══════════════════════════════════════════════════════
// TAB: FINANCE
// ══════════════════════════════════════════════════════
function renderFin(con){
  var c=calc();
  con.appendChild(secH('📈','Contract & Financial Terms'));
  var g=grid('g3');con.appendChild(g);
  g.appendChild(fld('Contract Type',null,selInp('ct',['ESA','PPA','Hybrid','Lease','Direct Sale'])));
  g.appendChild(fld('Contract Duration (Years)','0 = direct sale / no contract',numInp('cy',{min:0,max:25})));
  g.appendChild(fld('Monthly Service Fee ('+C()+')',null,numInp('mf',{min:0})));
  g.appendChild(fld('Discount Rate %','Your hurdle / required return',numInp('dr',{min:0,max:100})));
  g.appendChild(fld('Annual Escalator %','0 = fixed / 5 = CPI-linked',numInp('esc',{min:0,max:30})));

  con.appendChild(div2('mt20'));con.appendChild(secH('🔧','Annual OpEx — Your Operating Costs'));
  var g2=grid('g3');con.appendChild(g2);
  g2.appendChild(fld('O&M ('+C()+'/year)','Maintenance & repairs',numInp('om',{min:0})));
  g2.appendChild(fld('Insurance ('+C()+'/year)','System insurance',numInp('ins_c',{min:0})));
  g2.appendChild(fld('Monitoring ('+C()+'/year)','Remote monitoring subscription',numInp('mon',{min:0})));
  var ib=div2('ibox mt8');ib.innerHTML='Total OpEx: <span class="v">'+C()+' '+fmt(c.ao)+'/yr</span> · Monthly: <span class="v">'+C()+' '+fmt(c.ao/12)+'/mo</span> · Annual Net CF: <span class="g">'+C()+' '+fmt(c.an)+'/yr</span>';
  con.appendChild(ib);

  con.appendChild(div2('mt20'));con.appendChild(secH('💰','Cash Flow Projection'));
  var yrs=Math.min(S.cy||1,10);
  var hdrs=['Item','Year 0'];for(var y=1;y<=yrs;y++)hdrs.push('Y'+y);
  var cfRows=[
    {l:'CapEx',vs:[-c.capex].concat(Array(yrs).fill(0)),bold:0},
    {l:'Revenue',vs:[0].concat(Array.from({length:yrs},function(_,i){return(S.mf||0)*12*Math.pow(1+(S.esc||0)/100,i);})),bold:0},
    {l:'OpEx',vs:[0].concat(Array(yrs).fill(-c.ao)),bold:0},
    {l:'Net CF',vs:c.cfs.slice(0,yrs+1),bold:1},
  ];
  var wrap=div2('tbl-wrap');
  var tbl=document.createElement('table');tbl.className='tbl';
  var th='<thead><tr>'+hdrs.map(function(h,i){return'<th'+(i>0?' style="text-align:right"':'')+'>'+h+'</th>';}).join('')+'</tr></thead><tbody>';
  cfRows.forEach(function(row){
    th+='<tr class="'+(row.bold?'bold':'')+'"><td>'+row.l+'</td>';
    row.vs.slice(0,yrs+1).forEach(function(v){th+='<td class="'+(v<0?'neg':v>0?'pos':'')+'">'+(v===0?'—':(v<0?'('+fmt(Math.abs(v))+')':fmt(v)))+'</td>';});
    th+='</tr>';
  });
  th+='</tbody>';tbl.innerHTML=th;wrap.appendChild(tbl);con.appendChild(wrap);

  con.appendChild(div2('mt20'));con.appendChild(secH('🎯','Fee Sensitivity — Pricing Tiers'));
  var tiers=div2('tiers');
  [['Conservative',0.75,'Low fee, max client savings'],['Base ✓',1.0,'Balanced — recommended'],['Premium',1.3,'High IRR'],['Custom',null,null]].forEach(function(t,i){
    if(t[1]===null)return;
    var fee=Math.round((S.mf||0)*t[1]);
    var fcfs=[-c.capex].concat(Array(S.cy||1).fill(fee*12-c.ao));
    var tIRR=calcIRR(fcfs)*100;
    var tNPV=calcNPV(S.dr||20,fcfs);
    var tsave=c.cur-fee-(c.rd||0);
    var tc=div2('tc'+(i===1?' on':''));
    tc.innerHTML='<div style="font-size:9px;color:'+(i===1?'var(--grn)':'var(--t3)')+';font-weight:700;letter-spacing:.06em;text-transform:uppercase;margin-bottom:4px;">'+t[0]+'</div>'+
      '<div style="font-size:14px;font-weight:900;color:var(--t1)">'+C()+' '+fmt(fee)+'/mo</div>'+
      '<div style="font-size:11px;font-weight:700;color:'+(tIRR>20?'var(--grn)':tIRR>10?'var(--amb)':'var(--red)')+';margin:3px 0">IRR '+(isFinite(tIRR)?fmt(tIRR,0)+'%':'—')+'</div>'+
      '<div style="font-size:10px;color:'+(tNPV>0?'var(--grn)':'var(--red)')+'">NPV '+(tNPV>0?'+':'')+C()+' '+fmt(tNPV)+'</div>'+
      '<div style="font-size:9px;color:var(--t3);margin-top:4px;line-height:1.4">'+t[2]+'</div>';
    tiers.appendChild(tc);
  });
  con.appendChild(tiers);
}

// ══════════════════════════════════════════════════════
// TAB: ENGINEERING
// ══════════════════════════════════════════════════════
function renderEng(con){
  var c=calc();
  con.appendChild(secH('🔬','Engineering Study'));
  var ib=div2('ibox');ib.innerHTML='This tab provides a simplified engineering analysis. For final design, commission a certified electrical engineer.';
  con.appendChild(ib);

  // Panel electrical specs
  con.appendChild(div2('mt16'));con.appendChild(secH('⚡','Panel Electrical Parameters (STC)'));
  var g=grid('g4');con.appendChild(g);
  g.appendChild(fld('Voc (V)','Open circuit voltage',numInp('voc',{min:1,step:0.1})));
  g.appendChild(fld('Vmp (V)','Max power voltage',numInp('vmp',{min:1,step:0.1})));
  g.appendChild(fld('Isc (A)','Short circuit current',numInp('isc',{min:0.1,step:0.1})));
  g.appendChild(fld('Imp (A)','Max power current',numInp('imp',{min:0.1,step:0.1})));

  con.appendChild(div2('mt20'));con.appendChild(secH('📐','Site & Tilt'));
  var g2=grid('g2');con.appendChild(g2);
  g2.appendChild(fld('Site Latitude (°)','Positive = North, Negative = South',numInp('lat',{min:-90,max:90,step:0.1})));
  g2.appendChild(fld('Inverter Max Input Voltage','Auto-derived from type',div2('ibox','<span class="v">'+(S.it==='Central'?'1500V':'1000V')+'</span> — '+S.it)));

  // String Design
  var sd=div2('eng-box');
  sd.innerHTML='<div class="eng-title">🔗 String Design</div>';
  var inv_vmax=S.it==='Central'?1500:1000;
  var valid_str=c.str_voc<inv_vmax;
  var voc_warn=c.str_voc>(inv_vmax*0.9);
  var srows=[
    ['Max panels per string (Voc limit)',c.max_series+' panels ('+C()+' based on Voc='+S.voc+'V)','var(--t2)'],
    ['Recommended panels per string',c.rec_series+' panels','var(--amb)'],
    ['Total strings (parallel)',c.strings_total+' strings','var(--amb)'],
    ['String Voc (temp derating needed)',fmt(c.str_voc,1)+' V'+(valid_str?' ✔':' ✖'),valid_str?'var(--grn)':'var(--red)'],
    ['String Vmp',fmt(c.str_vmp,1)+' V','var(--t2)'],
    ['DC current per MPPT (Imp × strings/MPPT)',fmt(c.dc_current,1)+' A','var(--t2)'],
    ['DC/AC Array Ratio',fmt(c.dc_ac_ratio,3)+'×'+(c.dc_ac_ratio>1.35?' ⚠ Clipping risk':c.dc_ac_ratio<0.8?' ⚠ Undersized':' ✔ Good'),c.dc_ac_ratio>1.35||c.dc_ac_ratio<0.8?'var(--amb)':'var(--grn)'],
    ['Recommended DC cable size',c.dc_cable_size+' mm²','var(--cyn)'],
    ['Recommended AC cable size',c.ac_cable_size+' mm²','var(--cyn)'],
    ['AC current (estimated)',fmt(c.ac_current_kva,1)+' A ('+S.ip+')','var(--t2)'],
  ];
  srows.forEach(function(r){
    var d=div2('');d.style.cssText='display:grid;grid-template-columns:1fr 1fr;gap:8px;padding:5px 0;border-bottom:1px solid var(--brd);font-size:11px;';
    d.innerHTML='<span style="color:var(--t3)">'+r[0]+'</span><span style="font-weight:700;color:'+r[2]+'">'+r[1]+'</span>';
    sd.appendChild(d);
  });
  con.appendChild(sd);

  // Tilt & Orientation
  var to=div2('eng-box');
  to.innerHTML='<div class="eng-title">🧭 Tilt & Orientation Recommendations</div>';
  var lat=Math.abs(S.lat||31);
  var summer_tilt=Math.max(10,Math.round(lat-15));
  var winter_tilt=Math.min(75,Math.round(lat+15));
  var trows=[
    ['Site Latitude',fmt(S.lat,1)+'° '+(S.lat>=0?'N':'S'),'var(--amb)'],
    ['Optimal annual tilt',c.rec_tilt+'°','var(--grn)'],
    ['Summer tilt (max energy Jun-Aug)',summer_tilt+'°','var(--t2)'],
    ['Winter tilt (max energy Dec-Feb)',winter_tilt+'°','var(--t2)'],
    ['Azimuth (orientation)',S.lat>=0?'180° True South (Northern hemisphere)':'0° True North (Southern hemisphere)','var(--t2)'],
    ['Inter-row spacing (rule of thumb)','≥ '+fmt(0.6*Math.cos(c.rec_tilt*Math.PI/180)*1,2)+'m to avoid row shading','var(--t2)'],
  ];
  trows.forEach(function(r){
    var d=div2('');d.style.cssText='display:grid;grid-template-columns:1fr 1fr;gap:8px;padding:5px 0;border-bottom:1px solid var(--brd);font-size:11px;';
    d.innerHTML='<span style="color:var(--t3)">'+r[0]+'</span><span style="font-weight:700;color:'+r[2]+'">'+r[1]+'</span>';
    to.appendChild(d);
  });
  con.appendChild(to);

  // Monthly Yield
  var my=div2('eng-box');
  my.innerHTML='<div class="eng-title">📅 Estimated Monthly Energy Yield</div>';
  var ywrap=div2('tbl-wrap');ywrap.style.marginTop='8px';
  var ytbl=document.createElement('table');ytbl.className='tbl';
  var maxGen=Math.max.apply(null,c.monthly.map(function(m){return m.gen;}));
  ytbl.innerHTML='<thead><tr><th>Month</th><th>Days</th><th>Gen (kWh)</th><th>% of Annual</th><th>Visual</th></tr></thead>';
  var tb='<tbody>';
  var totalCheck=0;
  c.monthly.forEach(function(m){
    totalCheck+=m.gen;
    var pct=c.ag>0?m.gen/c.ag*100:0;
    var barw=maxGen>0?Math.round(m.gen/maxGen*80):0;
    var col=m.factor>=1.05?'var(--amb)':m.factor<=0.70?'var(--blu)':'var(--t2)';
    tb+='<tr><td style="color:'+col+';font-weight:700">'+m.m+'</td><td>'+m.days+'</td><td class="pos">'+fmt(m.gen,0)+'</td><td>'+fmt(pct,1)+'%</td><td><div style="background:var(--amb);height:4px;width:'+barw+'px;border-radius:2px;display:inline-block;"></div></td></tr>';
  });
  tb+='<tr class="bold"><td>TOTAL</td><td>365</td><td class="pos">'+fmt(totalCheck,0)+'</td><td>100%</td><td></td></tr>';
  tb+='</tbody>';ytbl.innerHTML+=tb;ywrap.appendChild(ytbl);my.appendChild(ywrap);
  con.appendChild(my);

  // Site Checklist
  var cl=div2('eng-box');
  cl.innerHTML='<div class="eng-title">✅ Site Assessment Checklist</div>';
  var checks=[
    {ok:c.kw>0,t:'System sized',d:'System capacity is defined ('+fmt(c.kw,2)+' kWp)'},
    {ok:c.dc_ac_ratio>=0.8&&c.dc_ac_ratio<=1.35,t:'DC/AC ratio',d:'Ratio is '+fmt(c.dc_ac_ratio,2)+'× (ideal: 0.80–1.35)'},
    {ok:c.str_voc<(S.it==='Central'?1500:1000),t:'String Voc within inverter limit',d:'String Voc = '+fmt(c.str_voc,0)+'V vs max '+(S.it==='Central'?1500:1000)+'V'},
    {ok:S.nm==='Available',t:'Net metering available',d:'Utility net metering policy: '+S.nm},
    {ok:(S.gconn==='Existing connection')||(S.gc>0),t:'Grid connection planned',d:S.gconn},
    {ok:c.capex>0,t:'CapEx calculated',d:'Total project cost: '+C()+' '+fmt(c.capex)},
    {ok:isFinite(c.ir)&&c.ir>0,t:'Positive IRR',d:isFinite(c.ir)?'IRR = '+fmt(c.ir,1)+'%':'IRR not calculable — check inputs'},
    {ok:c.nv>0,t:'Positive NPV',d:(c.nv>0?'NPV = '+C()+' '+fmt(c.nv):'Negative NPV — increase fee or reduce cost')},
    {ok:c.pb<(S.cy||3),t:'Payback within contract period',d:isFinite(c.pb)?'Payback = '+fmt(c.pb,1)+' yrs vs '+S.cy+' yr contract':'Payback longer than contract'},
    {ok:S.voc>0&&S.vmp>0,t:'Panel specs entered',d:'Voc='+S.voc+'V, Vmp='+S.vmp+'V, Isc='+S.isc+'A'},
  ];
  var clDiv=div2('checklist');
  checks.forEach(function(ck){
    var d=div2('chk-item');
    d.style.background=ck.ok?'#22c55e08':'#f8717108';
    d.innerHTML='<span class="ico">'+(ck.ok?'✅':'⚠️')+'</span><div><div style="font-weight:700;color:'+(ck.ok?'var(--grn)':'var(--amb)')+'">'+ck.t+'</div><div>'+ck.d+'</div></div>';
    clDiv.appendChild(d);
  });
  cl.appendChild(clDiv);con.appendChild(cl);
}

// ══════════════════════════════════════════════════════
// TAB: RESULTS
// ══════════════════════════════════════════════════════
function renderResults(con){
  var c=calc();var T=TYPES[S.stype];
  con.appendChild(secH('🎯','Results Dashboard'));
  var mg=div2('mgrid');con.appendChild(mg);
  [
    {l:'Total CapEx',v:C()+' '+fmt(c.capex),s:usd(c.capex),cl:'var(--amb)'},
    {l:'Simple Payback',v:isFinite(c.pb)?fmt(c.pb,1)+' yrs':'—',s:isFinite(c.pb)?'Month '+Math.round(c.pb*12):'',cl:'var(--blu)'},
    {l:'IRR',v:isFinite(c.ir)?fmt(c.ir,1)+'%':'—',s:null,cl:c.ir>20?'var(--grn)':c.ir>10?'var(--amb)':'var(--red)',hi:c.ir>20},
    {l:'NPV @ '+(S.dr||20)+'%',v:C()+' '+fmt(c.nv),s:usd(c.nv),cl:c.nv>0?'var(--grn)':'var(--red)',hi:c.nv>0},
    {l:(S.cy||1)+'-Yr Net Profit',v:C()+' '+fmt(c.np2),s:usd(c.np2),cl:'var(--grn)',hi:c.np2>0},
    {l:'LCOE',v:C()+' '+fmt(c.lcoe,2)+'/kWh',s:'Grid: '+C()+' '+(S.gt||0)+'/kWh',cl:c.lcoe<(S.gt||99)?'var(--grn)':'var(--amb)'},
  ].forEach(function(m){mg.appendChild(mcard(m.l,m.v,m.s,m.cl,m.hi));});

  con.appendChild(div2('mt20'));con.appendChild(secH('👤','Client Savings'));
  var mg2=div2('mgrid');con.appendChild(mg2);
  [
    {l:'Current Monthly Cost',v:C()+' '+fmt(c.cur),s:null,cl:'var(--red)'},
    {l:'Post-Solar Monthly Cost',v:C()+' '+fmt(c.post),s:null,cl:'var(--amb)'},
    {l:'Monthly Saving',v:C()+' '+fmt(c.sav),s:fmt(c.savpct,0)+'% reduction',cl:'var(--grn)',hi:c.sav>0},
    {l:(S.cy||1)+'-Year Saving',v:C()+' '+fmt(c.totsav),s:usd(c.totsav),cl:'var(--grn)'},
    {l:'Net Metering Credit/mo',v:C()+' '+fmt(c.nmc),s:null,cl:'var(--cyn)'},
    {l:'CapEx per kWp',v:C()+' '+fmt(c.cpkw,0),s:usd(c.cpkw)+'/kWp',cl:'var(--t2)'},
  ].forEach(function(m){mg2.appendChild(mcard(m.l,m.v,m.s,m.cl,m.hi));});

  // Transport in results
  if(c.tr_total>0){
    con.appendChild(div2('mt12'));
    var trb=div2('ibox');trb.style.borderColor='var(--ora)44';
    trb.innerHTML='Transport & Logistics: <span style="color:var(--ora);font-weight:700">'+C()+' '+fmt(c.tr_total)+'</span> ('+fmt(c.capex>0?c.tr_total/c.capex*100:0,1)+'% of total CapEx)';
    con.appendChild(trb);
  }

  con.appendChild(div2('mt20'));con.appendChild(secH('📋','Generate AI Prompt'));
  var pp=div2('');pp.style.cssText='font-size:11px;color:var(--t3);margin-bottom:12px;line-height:1.7;';
  pp.textContent='Copies a complete, fully-calculated prompt with all engineering data. Paste into any AI — then request: Business Plan, Client Proposal, SLD, Financial Model (XLSX), ESA Contract, Pitch Deck, Feasibility Study, and more.';
  con.appendChild(pp);
  var pb=document.createElement('button');pb.id='pbtn';pb.className='pbtn idle';pb.textContent='⬇  COPY COMPLETE PROJECT PROMPT';pb.onclick=copyPrompt;
  con.appendChild(pb);
  var prev=div2('ppreview');prev.innerHTML='<pre id="ptext"></pre>';
  con.appendChild(prev);
  var c2=calc();setTimeout(function(){var el=document.getElementById('ptext');if(el)el.textContent=buildPrompt(c2,T).slice(0,900)+'...';},0);
}

// ══════════════════════════════════════════════════════
// TAB: HELP
// ══════════════════════════════════════════════════════
function renderHelp(con){
  con.appendChild(secH('❓','Help & Glossary'));
  var ib=div2('ibox ok');ib.innerHTML='Use this reference when filling in the configurator or reviewing your results. Click any tab to continue configuring your project.';
  con.appendChild(ib);

  var terms=[
    {term:'kWp',abbr:'Kilowatt-peak',def:'The rated power output of a solar panel or system under Standard Test Conditions (STC: 1000 W/m² irradiance, 25°C cell temp). It is the nameplate capacity of your array.',ex:'21 panels × 720 Wp = 15.12 kWp system'},
    {term:'kWh',abbr:'Kilowatt-hour',def:'A unit of energy. One kWh = 1 kW consumed or generated for 1 hour. Your electricity bill is measured in kWh.',ex:'Daily generation: 15 kWp × 6.2 PSH × 80% PR = 74.4 kWh/day'},
    {term:'PSH',abbr:'Peak Sun Hours',def:'The number of hours per day when solar irradiance averages 1,000 W/m². It is NOT actual daylight hours — it is equivalent full-sun hours. Higher PSH = more energy per kWp.',ex:'Matrouh, Egypt = 6.2 PSH/day (very high, excellent for solar)'},
    {term:'PR',abbr:'Performance Ratio',def:'The ratio of actual energy output vs. theoretical maximum. Accounts for temperature losses, wiring losses, shading, dust, inverter efficiency, mismatch, etc.',ex:'80% PR is typical. Bifacial panels in a clean desert can reach 83–85%'},
    {term:'IRR',abbr:'Internal Rate of Return',def:'The annualised return on your investment. It is the discount rate that makes NPV = 0. Higher IRR = better project. Compare to your hurdle rate (required return).',ex:'IRR 28% vs hurdle 20% → project beats target by 8 percentage points'},
    {term:'NPV',abbr:'Net Present Value',def:'The value of all future cash flows discounted back to today\'s money, minus your initial investment. Positive NPV = project creates value at your required return rate.',ex:'NPV +EGP 54,000 @ 20% → project earns 20% AND creates 54k extra value'},
    {term:'LCOE',abbr:'Levelised Cost of Energy',def:'Total lifetime cost of the system (CapEx + OpEx) divided by total energy generated over the contract period. Compare to grid tariff — if LCOE < tariff, solar is cheaper.',ex:'LCOE EGP 1.62/kWh vs grid EGP 2.50/kWh → solar saves EGP 0.88/kWh'},
    {term:'ESA',abbr:'Energy Service Agreement',def:'Contract where you (investor) own the solar system, install it at the client\'s site, and charge a fixed monthly service fee. Client pays for the service, not the asset. Different from a PPA.',ex:'Client pays EGP 20,000/month for 3 years. You own the system.'},
    {term:'PPA',abbr:'Power Purchase Agreement',def:'Contract where the client pays per kWh generated (like a utility tariff) rather than a fixed monthly fee. Better for large/variable-generation systems. Common for utility-scale.',ex:'Client pays EGP 1.80/kWh for every kWh the solar produces'},
    {term:'CapEx',abbr:'Capital Expenditure',def:'Total upfront cost to design, procure, and install the solar system. Includes equipment, installation, transport, contingency, and project management.',ex:'EGP 438,000 for 15 kWp BTS site'},
    {term:'OpEx',abbr:'Operating Expenditure',def:'Annual running costs after installation: O&M (maintenance), insurance, remote monitoring. Typically 1–2% of CapEx per year.',ex:'EGP 6,500/year = O&M 4,380 + Insurance 1,460 + Monitoring 660'},
    {term:'Net Metering',abbr:'Export Credit Billing',def:'A utility policy that credits you (or your client) for excess solar electricity exported to the grid. Each kWh exported earns a credit at the grid tariff rate, reducing the bill.',ex:'Export 1,250 kWh × EGP 2.50/kWh = EGP 3,125/month credit'},
    {term:'DC/AC Ratio',abbr:'Array-to-Inverter Ratio',def:'The ratio of your DC array capacity (kWp) to your inverter AC capacity (kW). Slightly over 1.0 is normal and acceptable (reduces inverter cost). Over 1.35 causes clipping losses.',ex:'15.12 kWp ÷ 15 kW inverter = 1.008 DC/AC ratio — ideal'},
    {term:'Voc',abbr:'Open Circuit Voltage',def:'The maximum voltage a panel produces when no current flows. Used to calculate maximum string voltage — which must be below the inverter\'s maximum input voltage (typically 1000V for string, 1500V for central).',ex:'5 panels × 50V Voc = 250V string Voc (well within 1000V limit)'},
    {term:'String',abbr:'Series-connected panels',def:'A group of solar panels connected in series. Series = voltage adds up. Parallel = current adds up. String design determines voltage at the inverter MPPT input.',ex:'4 strings × 5 panels = 20 panels wired to one inverter MPPT'},
    {term:'BESS',abbr:'Battery Energy Storage System',def:'A battery bank that stores excess solar energy for use at night or during grid outages. Adds resilience but increases CapEx significantly. Critical for off-grid sites.',ex:'60 kWh BESS provides ~8 hours backup at 7.5 kW average load'},
    {term:'Payback',abbr:'Simple Payback Period',def:'Total CapEx divided by annual net cash flow (revenue minus OpEx). Tells you how many years until your investment is fully recovered. Simpler than IRR but ignores time value of money.',ex:'EGP 438,000 ÷ EGP 233,500/year = 1.9 year payback'},
    {term:'Specific Yield',abbr:'kWh/kWp/year',def:'Annual energy output per kWp of installed capacity. A measure of system quality and location. Higher = better. Good desert systems: 1,600–2,200 kWh/kWp/year.',ex:'27,000 kWh/year ÷ 15.12 kWp = 1,786 kWh/kWp/year'},
  ];

  var hg=div2('help-grid');hg.style.marginTop='16px';
  terms.forEach(function(t){
    var card=div2('help-card');
    card.innerHTML='<div class="help-term">'+t.term+'</div><div class="help-abbr">'+t.abbr+'</div><div class="help-def">'+t.def+'</div><div class="help-ex">→ '+t.ex+'</div>';
    hg.appendChild(card);
  });
  con.appendChild(hg);
}

// ══════════════════════════════════════════════════════
// PROMPT BUILDER
// ══════════════════════════════════════════════════════
function buildPrompt(c,T){
  return'# ☀️ SOLARPM PRO v3 — PROJECT PROMPT\n## '+( S.name||'Unnamed')+' | '+T.n+' | '+new Date().toLocaleDateString('en-GB',{month:'long',year:'numeric'})+'\n\n'+
'## AGENT ROLE\nSolarPM Pro — elite Solar-as-a-Service advisor (Engineering + Finance + Legal + Strategy).\nUse ONLY the data below. Flag unknowns before calculating.\n\n'+
'## IDENTITY\nProject: '+(S.name||'—')+' | Ref: '+(S.ref||'—')+' | By: '+S.by+'\nDate: '+new Date().toLocaleDateString('en-GB',{day:'numeric',month:'long',year:'numeric'})+'\nStation: '+T.n+' ('+T.desc+')\nLocation: '+(S.city||'—')+', '+(S.country||'—')+' | Sites: '+S.sites+' | Mounting: '+S.mount+'\n\n'+
'## SITE & LOAD\nMonthly: '+S.mc+' kWh | Peak: '+S.pl+' kW | Profile: '+S.lp+'\nPower source: '+S.ps+' | Grid: '+S.gh+'h/day | Tariff: '+C()+' '+S.gt+'/kWh | Grid bill: '+C()+' '+fmt(S.mgb||0)+'/mo\nDiesel: '+S.dl+' L/mo @ '+C()+' '+S.dp+'/L = '+C()+' '+fmt(c.diesel)+'/mo | Annual: '+C()+' '+fmt(c.diesel*12)+'\nBattery/UPS: '+(S.hasbat?'Yes'+(S.batcap?' — '+S.batcap+'kWh':''):'No')+'\nNet Metering: '+S.nm+' | Grid Connection: '+S.gconn+'\n\n'+
'## SOLAR SYSTEM\nCapacity: '+fmt(c.kw,2)+' kWp ('+S.np+' × '+S.pw+'Wp '+S.pt+')\nInverter: '+S.ni+' × '+S.ik+'kW '+S.it+' ('+S.ip+')\nBESS: '+(S.bess?'Yes — '+S.bk+'kWh @ '+C()+S.bp+'/kWh':'No')+'\nPSH: '+S.psh+'h/day | PR: '+S.pr+'% | Tilt: '+c.rec_tilt+'° (recommended)\nDaily: '+fmt(c.dg,1)+' kWh | Monthly: '+fmt(c.mg,0)+' kWh | Annual: '+fmt(c.ag,0)+' kWh\nCoverage: '+fmt(c.cov,0)+'% | DC/AC ratio: '+fmt(c.dc_ac_ratio,2)+'× | Specific yield: '+fmt(c.spec_yield,0)+' kWh/kWp/yr\nExport: '+fmt(c.exp,0)+' kWh/mo | NM Credit: '+C()+' '+fmt(c.nmc,0)+'/mo\n\n'+
'## STRING DESIGN\nPanel: Voc='+S.voc+'V, Vmp='+S.vmp+'V, Isc='+S.isc+'A, Imp='+S.imp+'A\nRec. panels/string: '+c.rec_series+' | Total strings: '+c.strings_total+'\nString Voc: '+fmt(c.str_voc,1)+'V | String Vmp: '+fmt(c.str_vmp,1)+'V\nRec. DC cable: '+c.dc_cable_size+'mm² | Rec. AC cable: '+c.ac_cable_size+'mm²\n\n'+
'## CAPEX & BOM\n'+
'Equipment subtotal: '+C()+' '+fmt(c.eq)+'\nInstallation: '+C()+' '+fmt(c.ins_sub)+'\nTransport & logistics: '+C()+' '+fmt(c.tr_total)+(c.tr_total>0?' (dist:'+S.tr_dist+'km, '+S.tr_trucks+' trucks, '+S.tr_crew+' crew, '+S.tr_days+' days)':'')+'\nContingency '+S.cng+'% + PM '+S.pmpct+'%: '+C()+' '+fmt(c.cng+c.pmv)+'\nTOTAL CAPEX: '+C()+' '+fmt(c.capex)+' ('+usd(c.capex)+') | '+C()+' '+fmt(c.cpkw,0)+'/kWp\n\n'+
'## FINANCIAL MODEL\nContract: '+S.ct+', '+S.cy+' years @ '+C()+' '+fmt(S.mf)+'/month | Escalator: '+(S.esc||0)+'%/yr\nDiscount Rate: '+(S.dr||20)+'% | Annual Revenue: '+C()+' '+fmt(c.ar)+' | Annual OpEx: '+C()+' '+fmt(c.ao)+'\nClient: '+C()+' '+fmt(c.cur)+'/mo → '+C()+' '+fmt(c.post)+'/mo (saves '+fmt(c.savpct,0)+'%, '+C()+' '+fmt(c.sav)+'/mo)\n'+S.cy+'-Year Client Saving: '+C()+' '+fmt(c.totsav)+' ('+usd(c.totsav)+')\n\n'+
'## KEY METRICS\nPayback: '+fmt(c.pb,1)+' yrs | IRR: '+fmt(c.ir,1)+'% | NPV@'+(S.dr||20)+'%: '+C()+' '+fmt(c.nv)+'\nNet Profit ('+S.cy+'yr): '+C()+' '+fmt(c.np2)+' ('+usd(c.np2)+')\nLCOE: '+C()+' '+fmt(c.lcoe,2)+'/kWh vs grid '+C()+' '+(S.gt||0)+'/kWh\n\n'+
'## REQUESTED OUTPUT (choose):\n'+
'☐ Business Plan (DOCX)  ☐ Client Proposal  ☐ ESA/PPA Contract\n'+
'☐ Financial Model+Sensitivity (XLSX)  ☐ BOM (XLSX)  ☐ SLD Diagram\n'+
'☐ Monthly Yield Study  ☐ Pitch Deck (PPTX)  ☐ Feasibility Study\n\n'+
'*SolarPM Pro v3 | '+new Date().toLocaleDateString()+'*';
}
function copyPrompt(){
  var c=calc();var T=TYPES[S.stype];var text=buildPrompt(c,T);
  var btn=document.getElementById('pbtn');
  var fallback=function(){var ta=document.createElement('textarea');ta.value=text;ta.style.cssText='position:fixed;opacity:0;';document.body.appendChild(ta);ta.select();try{document.execCommand('copy');}catch(e){}document.body.removeChild(ta);if(btn){btn.className='pbtn done';btn.textContent='✓  COPIED!';setTimeout(function(){btn.className='pbtn idle';btn.textContent='⬇  COPY COMPLETE PROJECT PROMPT';},3000);}};
  if(navigator.clipboard){navigator.clipboard.writeText(text).then(function(){if(btn){btn.className='pbtn done';btn.textContent='✓  COPIED — PASTE INTO YOUR AI AGENT';setTimeout(function(){btn.className='pbtn idle';btn.textContent='⬇  COPY COMPLETE PROJECT PROMPT';},3000);}}).catch(fallback);}else{fallback();}
}

// ══════════════════════════════════════════════════════
// INIT
// ══════════════════════════════════════════════════════
renderNav();
renderTab(S.tab);
updateMetrics();
</script>
</body>
</html>
