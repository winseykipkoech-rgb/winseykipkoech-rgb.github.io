
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#07111d">
<title>TradingFloor AI | Live Market Signals</title>

<style>
:root {
  --bg:#07111d;
  --panel:#101f30;
  --panel2:#14283b;
  --line:#263c50;
  --text:#eff6ff;
  --muted:#91a4b9;
  --gold:#f5bd4f;
  --green:#32d6a0;
  --red:#ff7082;
  --blue:#76aaff;
}
*{box-sizing:border-box}
body{
  margin:0;background:radial-gradient(ellipse at top,#142c45 0%,var(--bg) 52%);
  color:var(--text);font:14px/1.5 Arial,Helvetica,sans-serif;
}
button,select{font:inherit}
button{cursor:pointer;transition:.2s}
button:hover{filter:brightness(1.12);transform:translateY(-1px)}
button:disabled{opacity:.6;cursor:wait;transform:none}
.wrap{max-width:1250px;margin:auto;padding:22px}
header,.flex,.heading,.signal-top{
  display:flex;justify-content:space-between;align-items:center;gap:12px
}
header{margin-bottom:30px}
.brand{font-weight:900;letter-spacing:1.5px;font-size:21px}
.brand span,.gold{color:var(--gold)}
.eyebrow{color:var(--gold);font-size:10px;letter-spacing:2px;font-weight:bold}
.muted,.small{color:var(--muted);font-size:11px}
.status,.tag,.pill{
  display:inline-block;border:1px solid var(--line);border-radius:9px;
  background:#122438;padding:7px 10px;font-size:10px
}
.status{border-radius:30px}
.dot{display:inline-block;width:7px;height:7px;border-radius:50%;background:var(--gold);margin-right:6px}
.dot.live{background:var(--green)}
.hero{display:flex;justify-content:space-between;align-items:flex-end;gap:22px;margin-bottom:20px}
h1{font-size:clamp(30px,4vw,44px);line-height:1.08;margin:8px 0}
h2{font-size:15px;margin:0}
p{color:var(--muted)}
.controls{display:flex;flex-wrap:wrap;gap:9px}
select,button{
  background:#14283b;color:var(--text);border:1px solid var(--line);
  border-radius:10px;padding:11px 13px;font-size:12px
}
select{min-width:145px}
.primary{background:linear-gradient(120deg,#ffda80,var(--gold));color:#17202a;border-color:var(--gold);font-weight:bold}
.grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:13px}
.cols{display:grid;grid-template-columns:1.15fr .85fr;gap:13px;margin-top:13px}
.card{
  min-width:0;padding:18px;border:1px solid var(--line);border-radius:17px;
  background:linear-gradient(145deg,#14283b,#0d1a29);
  box-shadow:0 12px 28px #0002
}
.heading{margin-bottom:15px}
.metric-label{color:var(--muted);font-size:11px}
.metric-value{font-size:clamp(23px,3vw,31px);font-weight:850;margin:8px 0}
.positive{color:var(--green)!important}
.negative{color:var(--red)!important}
.chart{width:100%;height:260px}
.chart svg{width:100%;height:100%;display:block}
.signal-box{
  border:1px solid #2b465a;border-radius:14px;padding:16px;
  background:linear-gradient(135deg,#102c32,#112234)
}
.signal-direction{font-size:24px;font-weight:900}
.pill.buy{color:var(--green);border-color:#26755c;background:#10372d}
.pill.sell{color:var(--red);border-color:#793e4b;background:#3a202b}
.pill.wait{color:var(--gold)}
.levels{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:7px;margin-top:15px}
.level{padding:10px 8px;border:1px solid var(--line);border-radius:10px;background:#091925;min-width:0}
.level span{display:block;color:var(--muted);font-size:10px;margin-bottom:5px}
.level strong{font-size:12px;overflow-wrap:anywhere}
.entry{border-color:#80672f}.stop{border-color:#783c49}.target{border-color:#26745b}
.bar{height:6px;background:#263c50;border-radius:10px;overflow:hidden;margin:9px 0}
.bar i{display:block;height:100%;width:0;background:var(--gold);transition:width .4s}
.checks{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:8px;margin-top:13px}
.check{border:1px solid var(--line);border-radius:10px;padding:10px;background:#0b1a28;font-size:11px}
.yes{color:var(--green);font-weight:bold}.no{color:var(--muted)}
.bottom{display:grid;grid-template-columns:1fr 1fr;gap:13px;margin-top:13px}
.item{display:flex;justify-content:space-between;gap:10px;padding:12px 0;border-bottom:1px solid var(--line)}
.item:last-child{border-bottom:0}
.item b{font-size:12px}.item small{display:block;color:var(--muted);font-size:11px;margin-top:3px}
table{width:100%;border-collapse:collapse;font-size:11px}
th,td{text-align:left;padding:10px 6px;border-bottom:1px solid var(--line)}
th{color:var(--muted)}
.table-wrap{overflow-x:auto}
.notice{margin-top:14px;padding:12px;border-left:3px solid var(--gold);background:#1b2733;border-radius:0 9px 9px 0;color:#bac8d6;font-size:11px}
footer{text-align:center;color:#71869a;font-size:10px;margin:24px 0 6px}
.spinner{display:inline-block;width:12px;height:12px;border:2px solid #34495b;border-top-color:var(--gold);border-radius:50%;animation:spin .7s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
@media(max-width:850px){
 .grid{grid-template-columns:repeat(2,minmax(0,1fr))}
 .cols,.bottom{grid-template-columns:1fr}
 .hero{align-items:flex-start;flex-direction:column}
 .controls{width:100%}.controls select,.controls button{flex:1}
}
@media(max-width:450px){
 .wrap{padding:12px}header{align-items:flex-start}
 .brand{font-size:17px}.card{padding:13px}
 .grid{gap:8px}.levels{gap:5px}.level{padding:7px 5px}
 .checks{grid-template-columns:1fr}.chart{height:210px}
}
</style>
</head>

<body>
<main class="wrap">

<header>
  <div>
    <div class="brand">TRADING<span>FLOOR AI</span></div>
    <div class="muted">Live market data · Technical confluence · Signal dashboard</div>
  </div>
  <div class="status"><span class="dot" id="dot"></span><span id="status">CONNECTING</span></div>
</header>

<section class="hero">
  <div>
    <div class="eyebrow">MARKET INTELLIGENCE TERMINAL</div>
    <h1>Trade the setup.<br><span class="gold">Not the noise.</span></h1>
    <p>Spot-market candles, trend lines, supply and demand, breakouts, retests and candlestick analysis.</p>
  </div>
  <div class="controls">
    <select id="market" aria-label="Market">
      <option value="BTCUSDT">Bitcoin · BTC/USDT Spot</option>
      <option value="PAXGUSDT">Gold proxy · PAXG/USDT Spot</option>
    </select>
    <select id="tf" aria-label="Timeframe">
      <option value="15m">15 minutes</option>
      <option value="30m">30 minutes</option>
      <option value="1h" selected>1 hour</option>
      <option value="4h">4 hours</option>
    </select>
    <button class="primary" id="generate">✦ Generate Signal</button>
  </div>
</section>

<section class="grid">
  <div class="card">
    <div class="metric-label">LATEST PRICE <span class="gold">● LIVE</span></div>
    <div class="metric-value" id="price">—</div>
    <div class="small" id="priceInfo">Waiting for market data</div>
  </div>
  <div class="card">
    <div class="metric-label">RECENT PRICE CHANGE</div>
    <div class="metric-value" id="change">—</div>
    <div class="small">Last 24 candles</div>
  </div>
  <div class="card">
    <div class="metric-label">MARKET DIRECTION</div>
    <div class="metric-value" id="bias">WAIT</div>
    <div class="small" id="biasInfo">Awaiting analysis</div>
  </div>
  <div class="card">
    <div class="metric-label">CONFLUENCE SCORE</div>
    <div class="metric-value" id="score">—</div>
    <div class="bar"><i id="scoreBar"></i></div>
    <div class="small">Rule score, not win probability</div>
  </div>
</section>

<section class="cols">
  <article class="card">
    <div class="heading">
      <div><h2>Live candlestick chart</h2><div class="small" id="chartInfo">Binance Spot candles</div></div>
      <span class="tag" id="symbol">BTCUSDT</span>
    </div>
    <div class="chart">
      <svg id="chart" viewBox="0 0 760 260" preserveAspectRatio="none">
        <text x="380" y="130" fill="#91a4b9" text-anchor="middle">Loading candles…</text>
      </svg>
    </div>
    <div class="small" id="candleInfo">Waiting for exchange data.</div>
    <div class="notice">PAXG/USDT is a gold-backed token proxy, not the official XAU/USD index. Availability depends on Binance Spot listing and regional access.</div>
  </article>

  <article class="card">
    <div class="heading">
      <div><h2>Signal generator</h2><div class="small">Entry · stop-loss · take-profit</div></div>
      <span class="tag" id="timeTag">1H</span>
    </div>
    <div class="signal-box">
      <div class="signal-top">
        <div class="signal-direction" id="direction">WAIT</div>
        <span class="pill wait" id="signalPill">NO SETUP</span>
      </div>
      <h2 id="setup" style="margin:12px 0 6px">Waiting for analysis</h2>
      <p id="reason" style="font-size:12px">Press Generate Signal to analyze the latest candles.</p>
      <div class="levels">
        <div class="level entry"><span>ENTRY</span><strong id="entry">—</strong></div>
        <div class="level stop"><span>STOP LOSS</span><strong id="sl">—</strong></div>
        <div class="level target"><span>TAKE PROFIT</span><strong id="tp">—</strong></div>
      </div>
      <div class="small" id="rr" style="margin-top:12px">Risk/reward: —</div>
    </div>
    <div class="heading" style="margin-top:18px;margin-bottom:8px">
      <h2>Confluence checklist</h2><span class="tag" id="checkCount">0 / 6</span>
    </div>
    <div class="checks" id="checks"></div>
  </article>
</section>

<section class="bottom">
  <article class="card">
    <div class="heading"><h2>Market structure</h2><span class="tag">Auto-detected</span></div>
    <div id="structure">
      <div class="item"><div><b>Trend</b><small>Waiting for candles</small></div></div>
    </div>
  </article>
  <article class="card">
    <div class="heading"><h2>Signal history</h2><span class="tag">This browser</span></div>
    <div class="table-wrap">
      <table>
        <thead><tr><th>Time</th><th>Market</th><th>TF</th><th>Signal</th><th>Score</th></tr></thead>
        <tbody id="history"><tr><td colspan="5">No signals recorded yet.</td></tr></tbody>
      </table>
    </div>
    <div class="small" style="margin-top:10px">History is stored on this device only.</div>
  </article>
</section>

<div class="notice">
  <b>Risk notice:</b> Signals are experimental rule-based analysis, not financial advice. A 70/100 confluence score does not mean a 70% win rate. Backtest and paper-trade before using real money.
</div>

<footer>TradingFloor AI · Public spot market data · No trade execution · No guaranteed performance</footer>
</main>

<script>
(() => {
"use strict";

const $ = id => document.getElementById(id);
const API = "https://api.binance.com/api/v3/klines";
const HISTORY_KEY = "tradingfloor_spot_history_v1";
let candles = [];
let busy = false;

function fmt(n) {
  if (!Number.isFinite(n)) return "—";
  return n.toLocaleString("en-US", {
    minimumFractionDigits: 2,
    maximumFractionDigits: n < 1 ? 6 : 2
  });
}

function setStatus(text, live=false) {
  $("status").textContent = text;
  $("dot").className = "dot" + (live ? " live" : "");
}

async function getCandles() {
  const symbol = $("market").value;
  const interval = $("tf").value;
  const url = API + "?symbol=" + encodeURIComponent(symbol) +
    "&interval=" + encodeURIComponent(interval) + "&limit=180";

  const response = await fetch(url, {cache:"no-store"});
  if (!response.ok) {
    let message = "HTTP " + response.status;
    try {
      const error = await response.json();
      if (error.msg) message += ": " + error.msg;
    } catch (_) {}
    throw new Error(message + ". This spot pair may not be available.");
  }

  const raw = await response.json();
  if (!Array.isArray(raw) || raw.length < 60) {
    throw new Error("Not enough candles were returned for analysis.");
  }

  return raw.map(k => ({
    t:+k[0], o:+k[1], h:+k[2], l:+k[3], c:+k[4], v:+k[5]
  })).filter(c => [c.o,c.h,c.l,c.c,c.v].every(Number.isFinite));
}

function ema(values, period) {
  if (!values.length) return 0;
  const k = 2 / (period + 1);
  let result = values[0];
  for (let i=1; i<values.length; i++) {
    result = values[i] * k + result * (1-k);
  }
  return result;
}

function atr(cs, period=14) {
  const tr = [];
  for (let i=1; i<cs.length; i++) {
    tr.push(Math.max(
      cs[i].h-cs[i].l,
      Math.abs(cs[i].h-cs[i-1].c),
      Math.abs(cs[i].l-cs[i-1].c)
    ));
  }
  const recent = tr.slice(-period);
  return recent.reduce((a,b)=>a+b,0) / Math.max(1,recent.length);
}

function pivots(cs) {
  const highs=[], lows=[];
  for (let i=2; i<cs.length-2; i++) {
    const c=cs[i];
    if (c.h>cs[i-1].h && c.h>cs[i-2].h &&
        c.h>=cs[i+1].h && c.h>=cs[i+2].h) {
      highs.push({i,p:c.h});
    }
    if (c.l<cs[i-1].l && c.l<cs[i-2].l &&
        c.l<=cs[i+1].l && c.l<=cs[i+2].l) {
      lows.push({i,p:c.l});
    }
  }
  return {highs,lows};
}

function patterns(cs) {
  const a=cs[cs.length-1], b=cs[cs.length-2];
  const body=Math.abs(a.c-a.o) || 1e-9;
  const range=Math.max(a.h-a.l,1e-9);
  const lower=Math.min(a.o,a.c)-a.l;
  const upper=a.h-Math.max(a.o,a.c);

  return {
    bullEngulf: b.c<b.o && a.c>a.o && a.o<=b.c && a.c>=b.o,
    bearEngulf: b.c>b.o && a.c<a.o && a.o>=b.c && a.c<=b.o,
    hammer: lower>body*2 && upper<body && a.c>a.o,
    shooting: upper>body*2 && lower<body && a.c<a.o,
    doji: body/range < .1
  };
}

function analyze(cs) {
  const last=cs[cs.length-1], prev=cs[cs.length-2];
  const ranges=atr(cs);
  const closes=cs.map(c=>c.c);
  const e20=ema(closes.slice(-80),20);
  const e50=ema(closes.slice(-120),50);

  const trend = e20>e50 && last.c>e20 ? "Bullish" :
                e20<e50 && last.c<e20 ? "Bearish" : "Mixed";

  const {highs,lows}=pivots(cs);
  const recentHighs=highs.filter(x=>x.i>cs.length-45);
  const recentLows=lows.filter(x=>x.i>cs.length-45);
  const resistance=recentHighs[recentHighs.length-1];
  const support=recentLows[recentLows.length-1];

  const near = level => level && Math.abs(last.c-level.p)<=ranges*1.2;
  const supply=near(resistance) && last.c<=resistance.p;
  const demand=near(support) && last.c>=support.p;

  const breakoutUp=!!resistance && prev.c<=resistance.p && last.c>resistance.p;
  const breakoutDown=!!support && prev.c>=support.p && last.c<support.p;

  const retestUp=!!resistance && last.l<=resistance.p+ranges*.25 &&
    last.c>resistance.p && last.c>last.o;
  const retestDown=!!support && last.h>=support.p-ranges*.25 &&
    last.c<support.p && last.c<last.o;

  const hh=highs.length>1 && highs.at(-1).p>highs.at(-2).p;
  const hl=lows.length>1 && lows.at(-1).p>lows.at(-2).p;
  const lh=highs.length>1 && highs.at(-1).p<highs.at(-2).p;
  const ll=lows.length>1 && lows.at(-1).p<lows.at(-2).p;

  const candle=patterns(cs);
  const bull=[
    trend==="Bullish",
    demand || breakoutUp || retestUp,
    hh || hl,
    candle.bullEngulf || candle.hammer,
    breakoutUp || retestUp,
    last.c>prev.c
  ];
  const bear=[
    trend==="Bearish",
    supply || breakoutDown || retestDown,
    lh || ll,
    candle.bearEngulf || candle.shooting,
    breakoutDown || retestDown,
    last.c<prev.c
  ];

  const bullScore=bull.filter(Boolean).length;
  const bearScore=bear.filter(Boolean).length;
  let direction="WAIT";
  let score=Math.max(bullScore,bearScore)/6*100;

  if (bullScore>=4 && bullScore>bearScore) direction="BUY";
  else if (bearScore>=4 && bearScore>bullScore) direction="SELL";

  let stop=null,target=null,rr=null;
  const entry=last.c;

  if (direction==="BUY") {
    stop=Math.min(entry-ranges*1.25,
      support ? support.p-ranges*.15 : entry-ranges*1.25);
    target=entry+Math.max(entry-stop,ranges)*1.8;
    rr=(target-entry)/(entry-stop);
  } else if (direction==="SELL") {
    stop=Math.max(entry+ranges*1.25,
      resistance ? resistance.p+ranges*.15 : entry+ranges*1.25);
    target=entry-Math.max(stop-entry,ranges)*1.8;
    rr=(entry-target)/(stop-entry);
  }

  return {
    last,prev,ranges,trend,resistance,support,supply,demand,
    breakoutUp,breakoutDown,retestUp,retestDown,hh,hl,lh,ll,candle,
    bullScore,bearScore,direction,score,entry,stop,target,rr,
    checks:direction==="BUY" ? bull :
      direction==="SELL" ? bear :
      [trend==="Bullish",trend==="Bearish",demand,supply,
       breakoutUp||breakoutDown,retestUp||retestDown]
  };
}

function drawChart(cs) {
  const svg=$("chart"), data=cs.slice(-55);
  const low=Math.min(...data.map(c=>c.l));
  const high=Math.max(...data.map(c=>c.h));
  const span=high-low || 1;
  const step=760/data.length, bodyW=Math.max(3,step*.52);
  const y=v=>245-(v-low)/span*225;
  let out="";

  for(let i=0;i<5;i++){
    const gy=12+i*55;
    out+='<line x1="0" y1="'+gy+'" x2="760" y2="'+gy+
      '" stroke="#263c50" stroke-dasharray="4 6"/>';
  }

  data.forEach((c,i)=>{
    const x=i*step+step/2;
    const up=c.c>=c.o;
    const color=up?"#32d6a0":"#ff7082";
    const top=Math.min(y(c.o),y(c.c));
    const height=Math.max(2,Math.abs(y(c.o)-y(c.c)));

    out+='<line x1="'+x+'" y1="'+y(c.h)+'" x2="'+x+
      '" y2="'+y(c.l)+'" stroke="'+color+'" stroke-width="1.4"/>';
    out+='<rect x="'+(x-bodyW/2)+'" y="'+top+'" width="'+bodyW+
      '" height="'+height+'" rx="1" fill="'+color+'"/>';
  });
  svg.innerHTML=out;
}

function renderStructure(a) {
  const rows=[
    ["Trend",a.trend,a.trend==="Bullish"?"positive":a.trend==="Bearish"?"negative":""],
    ["Supply zone",a.supply?"Price near resistance":"No confirmed nearby supply",a.supply?"negative":""],
    ["Demand zone",a.demand?"Price near support":"No confirmed nearby demand",a.demand?"positive":""],
    ["Breakout",a.breakoutUp?"Bullish breakout":a.breakoutDown?"Bearish breakdown":"No fresh breakout",a.breakoutUp?"positive":a.breakoutDown?"negative":""],
    ["Retest",a.retestUp?"Bullish retest":a.retestDown?"Bearish retest":"No confirmed retest",a.retestUp?"positive":a.retestDown?"negative":""],
    ["Swing structure",a.hh&&a.hl?"Higher highs / higher lows":a.lh&&a.ll?"Lower highs / lower lows":"Mixed swing structure",""]
  ];

  $("structure").innerHTML=rows.map(r=>
    '<div class="item"><div><b>'+r[0]+'</b><small>'+r[1]+
    '</small></div><span class="tag '+r[2]+'">'+
    (r[2]==="positive"?"Bullish":r[2]==="negative"?"Bearish":"Checked")+
    '</span></div>'
  ).join("");
}

function renderSignal(a) {
  const buy=a.direction==="BUY", sell=a.direction==="SELL";
  $("bias").textContent=a.direction;
  $("bias").className="metric-value "+(buy?"positive":sell?"negative":"");
  $("biasInfo").textContent=buy?"Bullish confluence":sell?"Bearish confluence":"No high-confluence setup";

  $("direction").textContent=a.direction;
  $("direction").className="signal-direction "+(buy?"positive":sell?"negative":"");
  $("signalPill").textContent=buy?"BUY SETUP":sell?"SELL SETUP":"NO TRADE";
  $("signalPill").className="pill "+(buy?"buy":sell?"sell":"wait");

  $("setup").textContent=buy?"Bullish technical setup":
    sell?"Bearish technical setup":"Wait for clearer confluence";

  $("reason").textContent=buy || sell
    ? "Conditions agree across trend, structure, zones, candles and momentum. Confirm the setup before trading."
    : "The six checks have not produced a clear direction with at least four agreeing conditions.";

  $("entry").textContent=fmt(a.entry);
  $("sl").textContent=a.stop ? fmt(a.stop) : "—";
  $("tp").textContent=a.target ? fmt(a.target) : "—";
  $("rr").textContent=a.rr ? "Risk/reward target: 1 : "+a.rr.toFixed(2) : "Risk/reward: unavailable";

  const labels=["Trend alignment","Supply / demand","Swing structure",
    "Candlestick pattern","Breakout / retest","Momentum direction"];

  $("checks").innerHTML=labels.map((label,i)=>
    '<div class="check"><span class="'+(a.checks[i]?"yes":"no")+'">'+
    (a.checks[i]?"✓ ":"○ ")+label+'</span><div class="small">'+
    (a.checks[i]?"Condition detected":"Not confirmed")+'</div></div>'
  ).join("");

  $("checkCount").textContent=a.checks.filter(Boolean).length+" / 6";
  $("score").textContent=Math.round(a.score)+" / 100";
  $("scoreBar").style.width=Math.round(a.score)+"%";
  $("scoreBar").style.background=buy?"var(--green)":sell?"var(--red)":"var(--gold)";
}

function saveHistory(a) {
  if(a.direction==="WAIT") ret
