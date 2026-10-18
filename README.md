
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, viewport-fit=cover">
<title>MT5 Style Trading Simulator</title>
<style>
:root{--blue:#2878d7;--green:#168b55;--red:#c62828;--ink:#171717;--muted:#777;--line:#e5e5e5;--paper:#fff;--soft:#f6f7f8}
*{box-sizing:border-box}
html,body{margin:0;min-height:100%;font-family:Roboto,"Arial",sans-serif;background:#fff;color:var(--ink)}
button,input,select{font:inherit}
button{cursor:pointer}
.app{max-width:760px;margin:auto;min-height:100vh;background:#fff;padding-bottom:78px}
.topbar{height:66px;display:flex;align-items:center;gap:16px;padding:0 18px;background:#fff;position:sticky;top:0;z-index:5}
.hamb{border:0;background:none;font-size:29px;padding:0 3px}
.top-title{font-size:22px;font-weight:500;flex:1}
.top-action{border:0;background:none;font-size:26px;color:#555;padding:7px}
.subhead{padding:0 20px 12px;color:#888;font-size:19px}
.tabs{display:flex;border-bottom:1px solid #eee;position:sticky;top:66px;background:#fff;z-index:4}
.tab{flex:1;border:0;background:#fff;padding:17px 4px 14px;font-size:14px;color:#777;border-bottom:3px solid transparent}
.tab.active{color:#111;border-bottom-color:#4285f4;font-weight:600}
.content{padding:0 16px}
.screen{display:none}
.screen.active{display:block}
.summary{padding:18px 12px 14px;border-bottom:1px solid #e7e7e7}
.metric{display:flex;justify-content:space-between;align-items:center;font-weight:700;padding:7px 2px}
.metric span:first-child{font-size:15px}
.metric strong{font-size:16px}
.hint{color:#777;font-size:12px;line-height:1.5}
.quote{display:grid;grid-template-columns:1fr auto;gap:10px;padding:15px 2px;border-bottom:1px solid #eee;align-items:center}
.qname{font-weight:700;font-size:17px}
.qsub{color:#888;font-size:12px;margin-top:5px}
.qprices{display:flex;gap:10px;text-align:right}
.qprice{font-size:19px;font-weight:700;white-space:nowrap}
.up{color:#c62828}.down{color:#2476cc}
.card{border:1px solid #e5e5e5;border-radius:10px;margin:14px 0;padding:14px}
.card h3{font-size:16px;margin:0 0 13px}
.row{display:flex;gap:10px;align-items:center}
.row>*{flex:1;min-width:0}
.field{margin:10px 0}
.field label{display:block;font-size:13px;color:#555;margin-bottom:6px}
.field input,.field select{width:100%;padding:12px;border:1px solid #d5d5d5;border-radius:6px;background:white}
.btn{border:0;border-radius:5px;padding:12px 15px;background:#e9eef5;color:#222;font-weight:600}
.btn.primary{background:var(--blue);color:white}
.btn.buy{background:#168b55;color:white}
.btn.sell{background:#c62828;color:white}
.position{border-bottom:1px solid #e8e8e8;padding:14px 2px}
.poshead{display:flex;justify-content:space-between;gap:10px;font-weight:700}
.posdetail{color:#777;font-size:12px;margin-top:6px;line-height:1.6}
.posactions{display:flex;gap:8px;margin-top:10px}
.posactions button{padding:8px 12px}
.empty{text-align:center;padding:65px 12px;color:#999}
.emptyicon{font-size:58px;color:#ddd;margin-bottom:12px}
.bottomnav{position:fixed;z-index:10;bottom:0;left:50%;transform:translateX(-50%);width:min(760px,100%);height:72px;display:flex;background:#fff;border-top:1px solid #ddd;box-shadow:0 -2px 7px #0001;padding-bottom:env(safe-area-inset-bottom)}
.navbtn{flex:1;border:0;background:white;color:#444;font-size:12px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:5px}
.navbtn .ico{font-size:24px;line-height:1}
.navbtn.active{color:var(--blue);font-weight:700}
.drawerbg{position:fixed;inset:0;background:#0006;z-index:20;display:none}
.drawerbg.open{display:block}
.drawer{height:100%;width:min(330px,86vw);background:#fff;padding:22px 0;box-shadow:4px 0 20px #0002}
.accountbox{padding:8px 22px 22px;border-bottom:1px solid #ddd}
.avatar{display:inline-flex;width:45px;height:45px;background:#2865df;color:white;align-items:center;justify-content:center;font-weight:bold;font-size:21px;margin-right:12px;vertical-align:middle}
.accountname{display:inline-block;vertical-align:middle;font-weight:600}
.accountname small{display:block;color:#777;font-weight:400;margin-top:4px}
.draweritem{display:block;width:100%;text-align:left;padding:15px 24px;border:0;background:#fff;font-weight:600;font-size:15px}
.draweritem:active,.draweritem:hover{background:#f4f6f8}
.chartwrap{height:440px;width:100%;margin-top:12px}
.chartwrap iframe{width:100%;height:100%;border:0}
.pill{font-size:10px;color:#8a5b00;background:#fff1c7;border-radius:4px;padding:4px 7px;font-weight:700}
.smallmuted{font-size:12px;color:#777}
.historyitem{padding:12px 2px;border-bottom:1px solid #eee;display:flex;justify-content:space-between;gap:12px}
.positive{color:#168b55}.negative{color:#c62828}
.notice{background:#fff8e5;border:1px solid #f2dfaa;color:#725a20;border-radius:7px;padding:10px;font-size:12px;line-height:1.45;margin:12px 0}
.chatbox{border:1px solid #eee;border-radius:8px;padding:14px;min-height:100px;color:#777;font-size:13px;line-height:1.5}
@media(min-width:600px){.content{padding:0 24px}.qprice{font-size:21px}.topbar{padding:0 24px}}
</style>
</head>
<body>
<div class="app">
<header class="topbar">
<button class="hamb" onclick="toggleDrawer(true)">☰</button>
<div class="top-title" id="pageTitle">Quotes</div>
<button class="top-action" onclick="tickPrices()">↻</button>
<button class="top-action" onclick="showScreen('trade')">⊞</button>
</header>
<div class="subhead" id="pageSubtitle">All symbols <span class="pill">SIMULATED</span></div>

<section id="quotes" class="screen active">
<div class="content">
<div id="quotesList"></div>
<div class="notice">SIMULATOR ONLY — prices are generated locally, not live Exness quotes.</div>
</div>
</section>

<section id="charts" class="screen">
<div class="content"><div class="card">
<h3>Chart</h3><div class="row">
<div class="field"><label>Symbol</label><select id="chartSymbol" onchange="loadChart()"><option value="OANDA:XAUUSD">XAU/USD</option><option value="OANDA:EURUSD">EUR/USD</option></select></div>
<div class="field"><label>Timeframe</label><select id="chartTf" onchange="loadChart()"><option value="15">15 minutes</option><option value="30">30 minutes</option><option value="60">1 hour</option><option value="240">4 hours</option><option value="D">1 day</option><option value="W">1 week</option></select></div>
</div>
<div class="chartwrap" id="chartContainer"><div class="empty">Open this tab to load TradingView.</div></div>
<p class="hint">TradingView prices may differ from simulated execution prices.</p>
</div></div>
</section>

<section id="trade" class="screen">
<div class="summary">
<div class="metric"><span>Balance:</span><strong id="balance">1,000.00 USD</strong></div>
<div class="metric"><span>Equity:</span><strong id="equity">1,000.00 USD</strong></div>
<div class="metric"><span>Used margin:</span><strong id="usedMargin">0.00 USD</strong></div>
<div class="metric"><span>Free margin:</span><strong id="freeMargin">1,000.00 USD</strong></div>
<div class="metric"><span>Floating P/L:</span><strong id="floating">0.00 USD</strong></div>
</div>
<div class="content"><div class="card">
<h3>New Order <span class="pill">SIMULATED</span></h3>
<div class="field"><label>Symbol</label><select id="orderSymbol" onchange="updateOrderEstimate()"><option value="XAUUSD">XAU/USD</option><option value="EURUSD">EUR/USD</option></select></div>
<div class="field"><label>Volume (lots)</label><input id="lots" type="number" min="0.01" max="10" step="0.01" value="0.01" oninput="updateOrderEstimate()"></div>
<div class="row">
<div class="field"><label>Stop Loss (optional price)</label><input id="sl" type="number" step="any" placeholder="Optional"></div>
<div class="field"><label>Take Profit (optional price)</label><input id="tp" type="number" step="any" placeholder="Optional"></div>
</div>
<p class="smallmuted" id="orderEstimate">Estimated margin: —</p>
<div class="row"><button class="btn buy" onclick="openPosition('BUY')">BUY</button><button class="btn sell" onclick="openPosition('SELL')">SELL</button></div>
<p class="hint">Practice only. No orders are sent to MetaTrader or Exness.</p>
</div>
<div class="card"><h3>Open Positions (<span id="positionCount">0</span>)</h3><div id="positionsList"></div></div>
</div>
</section>

<section id="history" class="screen">
<div class="tabs">
<button class="tab active" onclick="historyTab('positions',this)">POSITIONS</button>
<button class="tab" onclick="historyTab('orders',this)">ORDERS</button>
<button class="tab" onclick="historyTab('deals',this)">DEALS</button>
</div>
<div class="content"><div id="historyList"></div></div>
</section>

<section id="messages" class="screen">
<div class="content"><div class="card">
<h3>Messages & TradingView</h3>
<div class="chatbox">Trading chat area<br>Open a chart for XAU/USD or EUR/USD.</div>
<div class="row" style="margin-top:12px">
<button class="btn primary" onclick="showScreen('charts')">Open TradingView Chart</button>
<button class="btn" onclick="showScreen('trade')">New Order</button>
</div>
</div></div>
</section>
</div>

<nav class="bottomnav">
<button class="navbtn active" data-screen="quotes" onclick="showScreen('quotes',this)"><span class="ico">↕</span>Quotes</button>
<button class="navbtn" data-screen="charts" onclick="showScreen('charts',this)"><span class="ico">▯</span>Charts</button>
<button class="navbtn" data-screen="trade" onclick="showScreen('trade',this)"><span class="ico">⌁</span>Trade</button>
<button class="navbtn" data-screen="history" onclick="showScreen('history',this)"><span class="ico">◴</span>History</button>
<button class="navbtn" data-screen="messages" onclick="showScreen('messages',this)"><span class="ico">▢</span>Messages</button>
</nav>

<div class="drawerbg" id="drawerbg" onclick="toggleDrawer(false)">
<aside class="drawer" onclick="event.stopPropagation()">
<div class="accountbox">
<span class="avatar">MT</span><span class="accountname">Trading Simulator<small>Practice Account · USD</small></span>
<p><span class="pill">SIMULATED ACCOUNT</span></p><strong id="drawerBalance">1,000.00 USD</strong>
</div>
<button class="draweritem" onclick="drawerGo('trade')">⌁ &nbsp; Trade</button>
<button class="draweritem" onclick="drawerGo('charts')">▯ &nbsp; Charts</button>
<button class="draweritem" onclick="drawerGo('history')">◴ &nbsp; History</button>
<button class="draweritem" onclick="drawerGo('messages')">▢ &nbsp; Messages / TradingView</button>
<button class="draweritem" onclick="resetAccount()">↻ &nbsp; Reset simulated account</button>
<button class="draweritem" onclick="showInfo()">⚙ &nbsp; Settings / Account info</button>
<div style="padding:16px 22px;color:#777;font-size:12px">No real broker account is connected.</div>
</aside>
</div>

<script>
const START_BALANCE = 1000;
const specs = {
 XAUUSD:{name:'XAU/USD',price:2650.00,spread:0.30,contract:100,leverage:100},
 EURUSD:{name:'EUR/USD',price:1.08000,spread:0.00012,contract:100000,leverage:100}
};
let prices={XAUUSD:specs.XAUUSD.price,EURUSD:specs.EURUSD.price};
let balance=START_BALANCE,nextId=1,positions=[],history=[],orderHistory=[];
let historyMode='positions';

function fmt(n,digits=2){
 return Number(n).toLocaleString('en-US',{minimumFractionDigits:digits,maximumFractionDigits:digits});
}
function digitsFor(sym){return sym==='XAUUSD'?2:5;}
function pnl(p){
 const diff=p.type==='BUY'?prices[p.symbol]-p.openPrice:p.openPrice-prices[p.symbol];
 return diff*specs[p.symbol].contract*p.lots;
}
function margin(p){
 return p.openPrice*specs[p.symbol].contract*p.lots/specs[p.symbol].leverage;
}
function totalFloating(){return positions.reduce((sum,p)=>sum+pnl(p),0);}
function totalMargin(){return positions.reduce((sum,p)=>sum+margin(p),0);}

function updateAccount(){
 const floating=totalFloating(),used=totalMargin(),equity=balance+floating;
 document.getElementById('balance').textContent=fmt(balance)+' USD';
 document.getElementById('equity').textContent=fmt(equity)+' USD';
 document.getElementById('usedMargin').textContent=fmt(used)+' USD';
 document.getElementById('freeMargin').textContent=fmt(equity-used)+' USD';
 const f=document.getElementById('floating');
 f.textContent=(floating>0?'+':'')+fmt(floating)+' USD';
 f.className=floating>=0?'positive':'negative';
 document.getElementById('drawerBalance').textContent=fmt(balance)+' USD';
 renderPositions();renderQuotes();updateOrderEstimate();
}

function renderQuotes(){
 const root=document.getElementById('quotesList');
 root.innerHTML=Object.keys(specs).map(sym=>{
  const s=specs[sym],mid=prices[sym],d=digitsFor(sym);
  const bid=mid-s.spread/2,ask=mid+s.spread/2;
  const change=((mid-s.price)/s.price)*100;
  return `<div class="quote" onclick="quickChart('${sym}')">
  <div><div style="font-size:12px;color:${change>=0?'#2476cc':'#c62828'}">${change>=0?'+':''}${fmt(change,2)}%</div>
  <div class="qname">${s.name}</div>
  <div class="qsub">SIMULATED · L: ${fmt(mid-Math.abs(s.spread)*4,d)} · H: ${fmt(mid+Math.abs(s.spread)*4,d)}</div></div>
  <div class="qprices"><div class="qprice up">${fmt(bid,d)}</div><div class="qprice down">${fmt(ask,d)}</div></div></div>`;
 }).join('');
}

function renderPositions(){
 const root=document.getElementById('positionsList');
 document.getElementById('positionCount').textContent=positions.length;
 if(!positions.length){
  root.innerHTML='<div class="empty"><div class="emptyicon">▱</div>No open positions</div>';return;
 }
 root.innerHTML=positions.map(p=>{
  const value=pnl(p),d=digitsFor(p.symbol);
  return `<div class="position">
  <div class="poshead"><span class="${p.type==='BUY'?'positive':'negative'}">${p.type} ${p.symbol} · ${fmt(p.lots,2)} lot</span>
  <span class="${value>=0?'positive':'negative'}">${value>=0?'+':''}${fmt(value)}</span></div>
  <div class="posdetail">Open: ${fmt(p.openPrice,d)} · Current: ${fmt(prices[p.symbol],d)}<br>
  SL: ${p.sl?fmt(p.sl,d):'—'} · TP: ${p.tp?fmt(p.tp,d):'—'}<br>
  Ticket: ${p.id} · Margin: ${fmt(margin(p))} USD</div>
  <div class="posactions"><button class="btn" onclick="closePosition(${p.id})">Close position</button></div>
  </div>`;
 }).join('');
}

function updateOrderEstimate(){
 const sym=document.getElementById('orderSymbol').value;
 const lots=Math.max(0,Number(document.getElementById('lots').value)||0);
 const est=prices[sym]*specs[sym].contract*lots/specs[sym].leverage;
 const free=balance+totalFloating()-totalMargin();
 document.getElementById('orderEstimate').textContent=
 'Estimated margin: '+fmt(est)+' USD · Free margin: '+fmt(free)+' USD';
}
</script>

<script>
function openPosition(type){
 const sym=document.getElementById('orderSymbol').value;
 const lots=Number(document.getElementById('lots').value);
 const sl=Number(document.getElementById('sl').value)||0;
 const tp=Number(document.getElementById('tp').value)||0;

 if(!Number.isFinite(lots)||lots<0.01||lots>10){
  alert('Enter a lot size from 0.01 to 10.00.');return;
 }
 const price=prices[sym]+(type==='BUY'?specs[sym].spread/2:-specs[sym].spread/2);
 const p={id:nextId++,symbol:sym,type,lots,openPrice:price,
  openTime:new Date().toISOString(),sl,tp};
 const required=margin(p),free=balance+totalFloating()-totalMargin();
 if(required>free){alert('Not enough simulated free margin.');return;}

 positions.unshift(p);
 orderHistory.unshift({id:p.id,symbol:sym,type,lots,status:'OPENED',
  price,time:new Date().toISOString()});
 updateAccount();renderHistory();
}

function closePosition(id){
 const index=positions.findIndex(p=>p.id===id);
 if(index<0)return;
 const p=positions[index],result=pnl(p);
 balance+=result;
 history.unshift({...p,closePrice:prices[p.symbol],
  closeTime:new Date().toISOString(),profit:result});
 positions.splice(index,1);
 orderHistory.unshift({id:p.id,symbol:p.symbol,type:p.type,lots:p.lots,
  status:'CLOSED',price:prices[p.symbol],time:new Date().toISOString()});
 updateAccount();renderHistory();
}

function tickPrices(){
 Object.keys(prices).forEach(sym=>{
  const volatility=sym==='XAUUSD'?1.8:0.00035;
  prices[sym]=Math.max(sym==='XAUUSD'?100:0.5,
   prices[sym]+(Math.random()-.5)*volatility);
 });
 [...positions].forEach(p=>{
  const px=prices[p.symbol];
  const hitSL=p.sl&&(p.type==='BUY'?px<=p.sl:px>=p.sl);
  const hitTP=p.tp&&(p.type==='BUY'?px>=p.tp:px<=p.tp);
  if(hitSL||hitTP)closePosition(p.id);
 });
 updateAccount();renderHistory();
}

function showScreen(id,btn){
 document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
 document.getElementById(id).classList.add('active');
 document.querySelectorAll('.navbtn').forEach(b=>
  b.classList.toggle('active',b.dataset.screen===id));
 const titles={quotes:'Quotes',charts:'Charts',trade:'Trade',
  history:'History',messages:'Messages'};
 document.getElementById('pageTitle').textContent=titles[id]||'MT5';
 document.getElementById('pageSubtitle').innerHTML=
 (id==='quotes'?'All symbols':id==='trade'?'Account overview':
 id==='history'?'All symbols':id==='charts'?'XAU/USD · EUR/USD':'Trading chat')
 +' <span class="pill">SIMULATED</span>';
 if(id==='charts')loadChart();
 if(id==='history')renderHistory();
}

function quickChart(sym){
 document.getElementById('chartSymbol').value=
  sym==='XAUUSD'?'OANDA:XAUUSD':'OANDA:EURUSD';
 showScreen('charts');
}

function loadChart(){
 const symbol=document.getElementById('chartSymbol').value;
 const tf=document.getElementById('chartTf').value;
 const container=document.getElementById('chartContainer');
 container.innerHTML=`<iframe title="TradingView chart"
 src="https://www.tradingview.com/widgetembed/?frameElementId=tvframe&symbol=${encodeURIComponent(symbol)}&interval=${encodeURIComponent(tf)}&hidesidetoolbar=0&symboledit=0&saveimage=0&toolbarbg=f1f3f6&theme=light&style=1&timezone=Africa%2FNairobi&withdateranges=1&hideideas=1&locale=en"
 allowfullscreen loading="lazy"></iframe>`;
}

function historyTab(mode,btn){
 historyMode=mode;
 document.querySelectorAll('#history .tab').forEach(t=>t.classList.remove('active'));
 btn.classList.add('active');
 renderHistory();
}

function renderHistory(){
 const root=document.getElementById('historyList');
 if(!root)return;
 let items=[];
 if(historyMode==='positions'){
  items=history.map(p=>({title:`${p.type} ${p.symbol} · ${fmt(p.lots,2)} lot`,
   sub:`Closed ${new Date(p.closeTime).toLocaleString()} · Close ${fmt(p.closePrice,digitsFor(p.symbol))}`,
   value:p.profit}));
 }else if(historyMode==='orders'){
  items=orderHistory.map(o=>({title:`${o.status} · ${o.type} ${o.symbol}`,
   sub:`Ticket ${o.id} · ${new Date(o.time).toLocaleString()} · ${fmt(o.lots,2)} lot`,
   value:null}));
 }else{
  items=history.map(p=>({title:`Deal #${p.id} · ${p.symbol}`,
   sub:`${p.type} · ${fmt(p.openPrice,digitsFor(p.symbol))} → ${fmt(p.closePrice,digitsFor(p.symbol))}`,
   value:p.profit}));
 }
 root.innerHTML=items.length?items.map(i=>
  `<div class="historyitem"><div><strong>${i.title}</strong>
  <div class="smallmuted" style="margin-top:5px">${i.sub}</div></div>
  <strong class="${i.value==null?'':i.value>=0?'positive':'negative'}">
  ${i.value==null?'':(i.value>=0?'+':'')+fmt(i.value)}</strong></div>`
 ).join(''):'<div class="empty"><div class="emptyicon">▱</div>Empty history</div>';
}

function toggleDrawer(open){
 document.getElementById('drawerbg').classList.toggle('open',open);
}
function drawerGo(id){toggleDrawer(false);showScreen(id);}
function resetAccount(){
 if(!confirm('Reset the simulated account to $1,000 and clear all positions and history?'))return;
 balance=START_BALANCE;positions=[];history=[];orderHistory=[];nextId=1;
 prices={XAUUSD:specs.XAUUSD.price,EURUSD:specs.EURUSD.price};
 toggleDrawer(false);updateAccount();renderHistory();
}
function showInfo(){
 alert('MT5-style practice simulator\nStarting balance: 1,000 USD\nSymbols: XAU/USD and EUR/USD\nPrices and trades are simulated locally. No broker is connected.');
}

updateAccount();
renderHistory();
setInterval(tickPrices,3000);
</script>
</body>
</html>
