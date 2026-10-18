<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MT5 Terminal — Local Shell</title>
<script type="text/javascript" src="https://s3.tradingview.com/tv.js"></script>
<style>
  :root{
    --bg:#131722; --panel:#1e222d; --panel2:#2a2e39; --border:#2a2e39;
    --text:#d1d4dc; --muted:#787b86; --green:#26a69a; --red:#ef5350;
    --blue:#2962ff; --yellow:#ffd166; --accent:#4a90d9;
  }
  *{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',Tahoma,sans-serif;}
  body{background:var(--bg);color:var(--text);height:100vh;overflow:hidden;display:flex;flex-direction:column;}
  header{height:36px;background:#0d1117;border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 10px;gap:14px;font-size:12px;}
  header .logo{font-weight:700;color:var(--accent);letter-spacing:.5px;}
  header .acc-switch{display:flex;gap:4px;margin-left:auto;}
  header .acc-btn{background:var(--panel2);border:1px solid var(--border);color:var(--muted);padding:3px 10px;border-radius:3px;cursor:pointer;font-size:11px;}
  header .acc-btn.active{background:var(--blue);color:#fff;border-color:var(--blue);}
  header .acc-btn:hover{color:var(--text);}
  header .broker{color:var(--muted);font-size:11px;}
  .main{flex:1;display:flex;min-height:0;}
  .left{width:210px;background:var(--panel);border-right:1px solid var(--border);display:flex;flex-direction:column;min-height:0;}
  .left .tabs{display:flex;border-bottom:1px solid var(--border);}
  .left .tabs div{flex:1;text-align:center;padding:6px;font-size:11px;color:var(--muted);cursor:pointer;border-bottom:2px solid transparent;}
  .left .tabs div.active{color:var(--text);border-bottom-color:var(--blue);}
  .left .search{padding:6px;border-bottom:1px solid var(--border);}
  .left .search input{width:100%;background:var(--panel2);border:1px solid var(--border);color:var(--text);padding:4px 6px;border-radius:3px;font-size:11px;outline:none;}
  .sym-list{flex:1;overflow-y:auto;font-size:11px;}
  .sym-row{display:flex;justify-content:space-between;padding:4px 8px;cursor:pointer;border-bottom:1px solid #1a1e27;}
  .sym-row:hover{background:var(--panel2);}
  .sym-row.selected{background:#243447;}
  .sym-row .bid{color:var(--green);}
  .sym-row .ask{color:var(--red);}
  .center{flex:1;display:flex;flex-direction:column;min-width:0;}
  .chart-box{flex:1;min-height:0;position:relative;background:#000;}
  .chart-box iframe,.chart-box > div{width:100%;height:100%;border:0;}
  .chart-toolbar{height:30px;background:var(--panel);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 8px;gap:8px;font-size:11px;}
  .chart-toolbar .pair{font-weight:700;color:var(--accent);}
  .chart-toolbar button{background:var(--panel2);border:1px solid var(--border);color:var(--muted);padding:2px 8px;border-radius:3px;cursor:pointer;font-size:11px;}
  .chart-toolbar button:hover{color:var(--text);}
  .right{width:300px;background:var(--panel);border-left:1px solid var(--border);display:flex;flex-direction:column;min-height:0;}
  .trade-panel{padding:8px;border-bottom:1px solid var(--border);}
  .trade-panel h4{font-size:11px;color:var(--muted);margin-bottom:6px;text-transform:uppercase;letter-spacing:.5px;}
  .trade-panel .row{display:flex;gap:6px;margin-bottom:6px;align-items:center;}
  .trade-panel label{font-size:11px;color:var(--muted);width:52px;}
  .trade-panel input,.trade-panel select{flex:1;background:var(--panel2);border:1px solid var(--border);color:var(--text);padding:4px 6px;border-radius:3px;font-size:11px;outline:none;}
  .trade-panel .calc{font-size:11px;color:var(--yellow);padding:4px 0;}
  .btn-buy{background:var(--green);color:#fff;border:0;padding:7px;border-radius:3px;cursor:pointer;font-weight:700;font-size:12px;flex:1;}
  .btn-sell{background:var(--red);color:#fff;border:0;padding:7px;border-radius:3px;cursor:pointer;font-weight:700;font-size:12px;flex:1;}
  .btn-buy:hover{filter:brightness(1.1);} .btn-sell:hover{filter:brightness(1.1);}
  .account-info{padding:8px;font-size:11px;border-bottom:1px solid var(--border);}
  .account-info .line{display:flex;justify-content:space-between;padding:2px 0;}
  .account-info .val{font-weight:600;}
  .account-info .val.pos{color:var(--green);} .account-info .val.neg{color:var(--red);}
  .bottom{height:210px;background:var(--panel);border-top:1px solid var(--border);display:flex;flex-direction:column;min-height:0;}
  .bottom .tabs{display:flex;border-bottom:1px solid var(--border);}
  .bottom .tabs div{padding:5px 14px;font-size:11px;color:var(--muted);cursor:pointer;border-bottom:2px solid transparent;}
  .bottom .tabs div.active{color:var(--text);border-bottom-color:var(--blue);}
  .bottom .content{flex:1;overflow:auto;font-size:11px;}
  table{width:100%;border-collapse:collapse;}
  th{text-align:left;padding:4px 8px;color:var(--muted);font-weight:500;border-bottom:1px solid var(--border);position:sticky;top:0;background:var(--panel);}
  td{padding:4px 8px;border-bottom:1px solid #1a1e27;}
  .close-btn{background:var(--red);color:#fff;border:0;padding:2px 6px;border-radius:2px;cursor:pointer;font-size:10px;}
  .close-btn:hover{filter:brightness(1.15);}
  ::-webkit-scrollbar{width:8px;height:8px;}
  ::-webkit-scrollbar-thumb{background:#3a3e4a;border-radius:4px;}
  .toast{position:fixed;bottom:20px;right:20px;background:var(--panel2);border:1px solid var(--border);color:var(--text);padding:8px 14px;border-radius:4px;font-size:12px;opacity:0;transition:opacity .3s;z-index:99;}
  .toast.show{opacity:1;}
</style>
</head>
<body>
<header>
  <span class="logo">MT5</span>
  <span class="broker">Broker: LocalShell Demo · No live feed</span>
  <div class="acc-switch" id="accSwitch"></div>
</header>
<div class="main">
  <div class="left">
    <div class="tabs"><div class="active" onclick="switchLeftTab(0)">Symbols</div><div onclick="switchLeftTab(1)">Watchlist</div></div>
    <div class="search"><input id="symSearch" placeholder="Search symbol..." oninput="filterSymbols()"></div>
    <div class="sym-list" id="symList"></div>
  </div>
  <div class="center">
    <div class="chart-toolbar">
      <span class="pair" id="chartPair">EURUSD</span>
      <button onclick="setTf('1')">1m</button><button onclick="setTf('5')">5m</button><button onclick="setTf('15')">15m</button>
      <button onclick="setTf('60')">1h</button><button onclick="setTf('240')">4h</button><button onclick="setTf('D')">D</button>
      <button onclick="setTf('W')">W</button>
      <span style="margin-left:auto;color:var(--muted)">Chart: TradingView Advanced</span>
    </div>
    <div class="chart-box" id="chartBox"></div>
  </div>
  <div class="right">
    <div class="trade-panel">
      <h4>New Order</h4>
      <div class="row"><label>Symbol</label><input id="ordSymbol" readonly></div>
      <div class="row"><label>Volume</label><input id="ordLots" type="number" value="0.10" step="0.01" min="0.01" oninput="recalcOrder()"></div>
      <div class="row"><label>Stop</label><input id="ordSL" type="number" step="0.0001" placeholder="optional" oninput="recalcOrder()"></div>
      <div class="row"><label>Limit</label><input id="ordTP" type="number" step="0.0001" placeholder="optional" oninput="recalcOrder()"></div>
      <div class="calc" id="ordCalc">Margin: — · Pip value: —</div>
      <div class="row"><button class="btn-sell" onclick="placeOrder('sell')">SELL</button><button class="btn-buy" onclick="placeOrder('buy')">BUY</button></div>
    </div>
    <div class="account-info" id="accInfo"></div>
  </div>
</div>
<div class="bottom">
  <div class="tabs"><div class="active" onclick="switchBotTab(0)">Trade History</div><div onclick="switchBotTab(1)">Open Positions</div><div onclick="switchBotTab(2)">Journal</div></div>
  <div class="content" id="botContent"></div>
</div>
<div class="toast" id="toast"></div>
<script>
const PAIRS = ["EURUSD","GBPUSD","USDJPY","USDCHF","AUDUSD","USDCAD","NZDUSD","EURGBP","EURJPY","GBPJPY","CHFJPY","AUDJPY","CADJPY","NZDJPY","EURCHF","GBPCHF","AUDCHF","CADCHF","NZDCHF","EURAUD","GBPAUD","AUDNZD","EURNZD","GBPNZD","USDSEK","USDNOK","USDTRY","USDZAR","USDMXN","USDINR","USDBRL","USDIDR","USDTHB","USDSGD","USDHKD","USDKRW","USDPLN","USDCZK","USDHUF","USDILS","USDCLP","USDCOP","USDPEN","USDARS","USDEGP","USDNGN","USDVND","USDMYR","USDPKR","USDPHP","USDQAR","USDSAR","USDAED"];
const CONTRACT = 100000;
const DEFAULT_LEVERAGE = 100;
const BASE = {EURUSD:1.0842,GBPUSD:1.2745,USDJPY:149.82,USDCHF:0.8810,AUDUSD:0.6520,USDCAD:1.3680,NZDUSD:0.5980,EURGBP:0.8510,EURJPY:162.40,GBPJPY:190.90,CHFJPY:170.10,AUDJPY:97.70,CADJPY:109.50,NZDJPY:89.60,EURCHF:0.9550,GBPCHF:1.1220,AUDCHF:0.5740,CADCHF:0.6430,NZDCHF:0.5260,EURAUD:1.6630,GBPAUD:1.9550,AUDNZD:1.0900,EURNZD:1.8130,GBPNZD:2.1310,USDSEK:10.42,USDNOK:10.68,USDTRY:34.10,USDZAR:17.85,USDMXN:18.60,USDINR:83.40,USDBRL:5.05,USDIDR:15600,USDTHB:35.20,USDSGD:1.345,USDHKD:7.82,USDKRW:1340,USDPLN:3.95,USDCZK:23.10,USDHUF:355,USDILS:3.72,USDCLP:920,USDCOP:4050,USDPEN:3.75,USDARS:980,USDEGP:48.5,USDNGN:1600,USDVND:25400,USDMYR:4.72,USDPKR:278,USDPHP:56.5,USDQAR:3.64,USDSAR:3.75,USDAED:3.67};
function makeAccount(id,name,balance){ return {id,name,balance,equity:balance,margin:0,freeMargin:balance,marginLevel:0,leverage:DEFAULT_LEVERAGE,positions:[   makeAccount(1,"Demo Account 1",10000), makeAccount(2,"Demo Account 2",5000), makeAccount(3,"Demo Account 3",25000), makeAccount(4,"Demo Account 4",1000), makeAccount(5,"Demo Account 5",50000) ];
let activeAcc = 0, selectedPair = "EURUSD", currentTf = "60", leftTab = 0, botTab = 0, prices = {};
function seedPrices(){ PAIRS.forEach(p=>{ prices = {bid:BASE , ask:BASE +(BASE >20?0.02:0.00015)}; }); }
function tick(){ PAIRS.forEach(p=>{ let spread = (p.startsWith("USD") && BASE >20)?0.02:0.00015; let ch = (Math.random()-0.5)*(BASE >20?0.05:0.0004); prices .bid = Math.max(0.0001, prices .bid+ch); prices .ask = prices .bid+spread; }); renderSymList(); updateFloating(); recalcOrder(); }
seedPrices(); setInterval(tick, 1500);
function pipSize(pair){ return pair.includes("JPY")?0.01:0.0001; }
function pipValue(pair,lots){ let ps = pipSize(pair); if(pair.startsWith("USD")) return lots*CONTRACT*ps; if(pair.endsWith("USD")) return lots*CONTRACT*ps; let mid = (prices .bid+prices .ask)/2; return lots*CONTRACT*ps*mid; }
function marginRequired(pair,lots,lev){ let price = (prices .bid+prices .ask)/2; return (lots*CONTRACT*price)/lev; }
function pnlOf(pos){ let cur = pos.side==="buy"?prices .bid:prices .ask; let diff = pos.side==="buy"? (cur-pos.open): (pos.open-cur); return diff/pipSize(pos.pair)*pipValue(pos.pair,pos.lots); }
function renderSymList(){ let q = document.getElementById("symSearch").value.toUpperCase(); let list = PAIRS.filter(p=>p.includes(q)); let html = ""; list.forEach(p=>{ let sel = p===selectedPair?" selected":""; html += `<div class="sym-row${sel}" onclick="selectPair('${p}')"><span>${p}</span><span><span class="bid">${prices .bid.toFixed(p.includes("JPY")?2:5)}</span> / <span class="ask">${prices .ask.toFixed(p.includes("JPY")?2:5)}</span></span></div>`; }); document.getElementById("symList").innerHTML = html; }
function selectPair(p){ selectedPair=p; renderSymList(); renderChart(); recalcOrder(); document.getElementById("ordSymbol").value=p; }
function filterSymbols(){ renderSymList(); }
function tvSymbol(pair){ return "FX:" + pair; }
function renderChart(){ let box = document.getElementById("chartBox"); box.innerHTML = ""; let sym = tvSymbol(selectedPair); new TradingView.widget({ autosize:true, symbol:sym, interval:currentTf, container_id:"chartBox", theme:"dark", style:"1", locale:"en", toolbar_bg:"#1e222d", enable_publishing:false, hide_top_toolbar:false, hide_legend:false, save_image:false, studies:["RSI@tv-basicstudies","MACD@tv-basicstudies"], show_popup_button:true, popup_width:"1000", popup_height:"650" }); document.getElementById("chartPair").textContent = selectedPair + " · " + currentTf; }
function setTf(tf){ currentTf=tf; renderChart(); }
function renderAccInfo(){ let a = accounts ; let ml = a.margin>0? (a.equity/a.margin*100):0; let html = `<div class="line"><span>Account</span><span class="val">${a.name}</span></div><div class="line"><span>Balance</span><span class="val">$${(a.balance).toFixed(2)}</span></div><div class="line"><span>Equity</span><span class="val ${a.equity>=a.balance?'pos':'neg'}">$${(a.equity).toFixed(2)}</span></div><div class="line"><span>Margin</span><span class="val">$${(a.margin).toFixed(2)}</span></div><div class="line"><span>Free Margin</span><span class="val">$${(a.freeMargin).toFixed(2)}</span></div><div class="line"><span>Margin Level</span><span class="val ${ml<100&&ml>0?'neg':''}">${ml?ml.toFixed(0)+'%':'—'}</span></div><div class="line"><span>Leverage</span><span class="val">1:${a.leverage}</span></div><div class="line"><span>Open Pos</span><span class="val">${a.positions.length}</span></div><div class="line"><span>Floating P&L</span><span class="val ${floatingTotal(a)>=0?'pos':'neg'}">$${(floatingTotal(a)).toFixed(2)}</span></div>`; document.getElementById("accInfo").innerHTML = html; }
function floatingTotal(a){ return a.positions.reduce((s,p)=>s+pnlOf(p),0); }
function updateFloating(){ accounts.forEach(a=>{ let fl = floatingTotal(a); a.equity = a.balance + fl; a.margin = a.positions.reduce((s,p)=>s+marginRequired(p.pair,p.lots,a.leverage),0); a.freeMargin = a.equity - a.margin; a.marginLevel = a.margin>0? a.equity/a.margin*100 : 0; }); renderAccInfo(); if(botTab===1) renderBottom(); }
function renderBottom(){ let a = accounts ; let html = ""; if(botTab===0){ html = `<table><tr><th>Time</th><th>Pair</th><th>Side</th><th>Lots</th><th>Open</th><th>Close</th><th>P&L</th></tr>`; a.history.slice().reverse().forEach(h=>{ html += `<tr><td>${h.time}</td><td>${h.pair}</td><td style="color:${h.side==='buy'?'var(--green)':'var(--red)'}">${h.side.toUpperCase()}</td><td>${h.lots}</td><td>${h.open.toFixed(5)}</td><td>${h.close.toFixed(5)}</td><td style="color:${h.pnl>=0?'var(--green)':'var(--red)'}">$${(h.pnl).toFixed(2)}</td></tr>`; }); html += `</table>`; } else if(botTab===1){ html = `<table><tr><th>Pair</th><th>Side</th><th>Lots</th><th>Open</th><th>Current</th><th>P&L</th><th>Margin</th><th></th></tr>`; a.positions.forEach((p,i)=>{ let cur = p.side==="buy"?prices .bid:prices .ask; let pl = pnlOf(p); html += `<tr><td>${p.pair}</td><td style="color:${p.side==='buy'?'var(--green)':'var(--red)'}">${p.side.toUpperCase()}</td><td>${p.lots}</td><td>${p.open.toFixed(5)}</td><td>${cur.toFixed(5)}</td><td style="color:${pl>=0?'var(--green)':'var(--red)'}">$${(pl).toFixed(2)}</td><td>$${(marginRequired(p.pair,p.lots,a.leverage)).toFixed(2)}</td><td><button class="close-btn" onclick="closePos(${i})">X</button></td></tr>`; }); html += `</table>`; } else { html = `<table><tr><th>Time</th><th>Event</th></tr>`; a.journal.slice().reverse().forEach(j=>{ html += `<tr><td>${j.time}</td><td>${j.msg}</td></tr>`; }); html += `</table>`; } document.getElementById("botContent").innerHTML = html; }
function switchBotTab(i){ botTab=i; document.querySelectorAll(".bottom .tabs div").forEach((d,idx)=>d.classList.toggle("active",idx===i)); renderBottom(); }
function switchLeftTab(i){ leftTab=i; document.querySelectorAll(".left .tabs div").forEach((d,idx)=>d.classList.toggle("active",idx===i)); }
function recalcOrder(){ let lots = parseFloat(document.getElementById("ordLots").value)||0; let sl = parseFloat(document.getElementById("ordSL").value); let tp = parseFloat(document.getElementById("ordTP").value); let m = marginRequired(selectedPair,lots,accounts .leverage); let pv = pipValue(selectedPair,lots); let txt = `Margin: ${m.toFixed(2)} USD · Pip value: ${pv.toFixed(2)} USD/pip`; if(!isNaN(sl)){ let diff = Math.abs(((prices .bid+prices .ask)/2)-sl)/pipSize(selectedPair); txt += ` · SL risk: ${(diff*pv).toFixed(2)} USD`; } if(!isNaN(tp)){ let diff = Math.abs(((prices .bid+prices .ask)/2)-tp)/pipSize(selectedPair); txt += ` · TP reward: ${(diff*pv).toFixed(2)} USD`; } document.getElementById("ordCalc").textContent = txt; }
function placeOrder(side){ let a = accounts ; let lots = parseFloat(document.getElementById("ordLots").value)||0.01; let m = marginRequired(selectedPair,lots,a.leverage); if(m > a.freeMargin){ toast("Not enough free margin"); return; } let price = side==="buy"?prices .ask:prices .bid; let pos = {pair:selectedPair,side,lots,open:price,time:nowStr(),sl:parseFloat(document.getElementById("ordSL").value)||null,tp:parseFloat(document.getElementById("ordTP").value)||null}; a.positions.push(pos); a.journal.push({time:nowStr(),msg:`Opened ${side.toUpperCase()} ${lots} ${selectedPair} @ ${price.toFixed(5)} · margin ${m.toFixed(2)}`}); updateFloating(); renderBottom(); toast(`${side.toUpperCase()} ${lots} ${selectedPair} opened`); monitorPos(a.positions.length-1); }
function monitorPos(idx){ let a = accounts ; let iv = setInterval(()=>{ if(idx>=a.positions.length){ clearInterval(iv); return; } let p = a.positions ; let cur = p.side==="buy"?prices .bid:prices .ask; if(p.sl && ((p.side==="buy" && cur<=p.sl) || (p.side==="sell" && cur>=p.sl))) closePos(idx,true); else if(p.tp && ((p.side==="buy" && cur>=p.tp) || (p.side==="sell" && cur<=p.tp))) closePos(idx,true); },1000); }
function closePos(idx,auto){ let a = accounts ; let p = a.positions ; if(!p) return; let cur = p.side==="buy"?prices .bid:prices .ask; let pl = pnlOf(p); a.balance += pl; a.history.push({pair:p.pair,side:p.side,lots:p.lots,open:p.open,close:cur,pnl:pl,time:nowStr()}); a.journal.push({time:nowStr(),msg:`Closed ${p.side.toUpperCase()} ${p.lots} ${p.pair} @ ${cur.toFixed(5)} · P&L ${(pl>=0?'+':'')+pl.toFixed(2)} ${auto?'(TP/SL hit)':''}`}); a.positions.splice(idx,1); updateFloating(); renderBottom(); if(!auto) toast(`Closed · P&L ${(pl>=0?'+':'')+pl.toFixed(2)} USD`); }
function nowStr(){ return new Date().toLocaleTimeString(); }
function renderAccSwitch(){ let html = ""; accounts.forEach((a,i)=>{ html += `<button class="acc-btn${i===activeAcc?' active':''}" onclick="switchAcc(${i})">${a.name.replace('Demo ','D')} · ${a.balance.toFixed(0)}</button>`; }); document.getElementById("accSwitch").innerHTML = html; }
function switchAcc(i){ activeAcc=i; renderAccSwitch(); renderAccInfo(); renderBottom(); recalcOrder(); toast("Switched to "+accounts .name); }
function toast(msg){ let t=document.getElementById("toast"); t.textContent=msg; t.classList.add("show"); setTimeout(()=>t.classList.remove("show"),2200); }
document.getElementById("ordSymbol").value = selectedPair; renderSymList(); renderChart(); renderAccSwitch(); renderAccInfo(); renderBottom(); recalcOrder(); toast("Local MT5 shell ready — 5 demo accounts, simulated ticks, no broker");
</script>
</body>
</html>
