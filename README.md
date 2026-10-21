<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#08111f">
<title>TradingFloor AI — Market Signals</title>
<style>
:root{--bg:#07111d;--panel:#0e1b2b;--panel2:#122337;--line:#23384d;--text:#eef5ff;--muted:#91a4b9;--gold:#f5bd4f;--green:#31d6a0;--red:#ff687d;--blue:#69a9ff;--radius:18px}
*{box-sizing:border-box}body{margin:0;background:radial-gradient(ellipse at 15% 0%,#132943 0,transparent 42%),var(--bg);color:var(--text);font:15px/1.5 Inter,system-ui,-apple-system,Segoe UI,Arial,sans-serif}button,select{font:inherit}button{cursor:pointer;transition:transform .18s,filter .18s}button:hover{filter:brightness(1.08);transform:translateY(-1px)}button:disabled{opacity:.55;cursor:wait;transform:none}.wrap{max-width:1250px;margin:auto;padding:24px}.top{display:flex;justify-content:space-between;align-items:center;gap:16px;margin-bottom:24px}.brand{font-weight:900;letter-spacing:1.5px;font-size:20px}.brand span{color:var(--gold)}.eyebrow{font-size:10px;letter-spacing:2.5px;text-transform:uppercase;color:var(--gold);font-weight:800}.subtitle{color:var(--muted);font-size:12px;margin-top:4px}.status{display:inline-flex;align-items:center;gap:8px;border:1px solid var(--line);background:#102235;border-radius:999px;padding:9px 13px;font-size:11px;color:#d8e4f2}.dot{height:8px;width:8px;background:var(--gold);border-radius:50%;box-shadow:0 0 12px currentColor}.dot.live{background:var(--green)}.hero{display:flex;align-items:flex-end;justify-content:space-between;gap:18px;margin:12px 0 18px}.hero h1{font-size:clamp(27px,4vw,42px);line-height:1.08;margin:7px 0}.hero p{margin:8px 0 0;color:var(--muted);max-width:600px;font-size:13px}.controls{display:flex;gap:9px;flex-wrap:wrap;align-items:center}.select,.btn{border:1px solid var(--line);border-radius:11px;padding:11px 13px;color:var(--text);background:#122338;font-size:12px}.select{min-width:130px}.btn-primary{background:linear-gradient(135deg,#ffd878,var(--gold));border-color:var(--gold);color:#17202a;font-weight:900}.btn-secondary{background:#13283d}.grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:13px}.card{background:linear-gradient(145deg,rgba(19,39,59,.97),rgba(12,25,39,.98));border:1px solid var(--line);border-radius:var(--radius);padding:18px;min-width:0;box-shadow:0 10px 28px #00000016}.metric-label{font-size:11px;color:var(--muted);display:flex;justify-content:space-between;gap:8px}.metric-value{font-size:clamp(22px,2.5vw,30px);font-weight:850;letter-spacing:-.7px;margin:9px 0 4px;overflow-wrap:anywhere}.small{font-size:11px;color:var(--muted)}.positive{color:var(--green)!important}.negative{color:var(--red)!important}.gold{color:var(--gold)}.cols{display:grid;grid-template-columns:1.15fr .85fr;gap:13px;margin-top:13px}.card-head{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-bottom:15px}.card-head h2{font-size:15px;margin:0}.tag{font-size:10px;padding:6px 9px;border:1px solid var(--line);border-radius:8px;color:#c4d4e5;background:#102236;white-space:nowrap}.chart{height:230px;width:100%;display:block}.chart svg{width:100%;height:100%;display:block}.signal-box{border:1px solid #28465a;background:linear-gradient(135deg,#102b31,#112333);border-radius:15px;padding:17px}.signal-top{display:flex;align-items:center;justify-content:space-between;gap:10px}.signal-direction{font-size:21px;font-weight:950;letter-spacing:.4px}.pill{border-radius:999px;padding:6px 10px;font-size:10px;font-weight:850;border:1px solid var(--line);background:#172b3d;color:#c9d9e9}.pill.buy{color:var(--green);border-color:#256e5a;background:#12372f}.pill.sell{color:var(--red);border-color:#81404a;background:#3a202b}.pill.wait{color:var(--gold);border-color:#80672e;background:#332a19}.signal-box h3{font-size:16px;margin:12px 0 5px}.signal-box p{font-size:12px;color:#b6c8d8;margin:0}.levels{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:15px}.level{background:#0b1b29;border:1px solid #263c4e;border-radius:11px;padding:10px;min-width:0}.level span{display:block;font-size:10px;color:var(--muted);margin-bottom:4px}.level strong{font-size:13px;overflow-wrap:anywhere}.level.entry{border-color:#80672e}.level.sl{border-color:#753a48}.level.tp{border-color:#256e5a}.bar{height:6px;background:#23384a;border-radius:999px;overflow:hidden;margin:9px 0}.bar i{display:block;height:100%;width:0;background:linear-gradient(90deg,var(--blue),var(--green));border-radius:999px;transition:width .4s}.confluences{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:8px;margin-top:13px}.confluence{display:flex;gap:8px;align-items:flex-start;border:1px solid var(--line);background:#0c1c2b;border-radius:10px;padding:9px;font-size:11px;color:#c3d1df}.check{font-weight:900;color:var(--green)}.cross{font-weight:900;color:var(--muted)}.bottom-grid{display:grid;grid-template-columns:1fr 1fr;gap:13px;margin-top:13px}.rows .item{display:flex;justify-content:space-between;align-items:center;gap:12px;padding:12px 0;border-bottom:1px solid #22374a}.rows .item:last-child{border:0}.rows b{font-size:12px}.rows small{display:block;color:var(--muted);font-size:11px;margin-top:2px}.table-wrap{overflow:auto}table{width:100%;border-collapse:collapse;font-size:11px;white-space:nowrap}th,td{text-align:left;border-bottom:1px solid #23384a;padding:11px 7px}th{font-weight:700;color:var(--muted)}.notice{padding:12px 14px;border-left:3px solid var(--gold);background:#1c2530;color:#b9c7d4;border-radius:0 10px 10px 0;font-size:11px;margin-top:14px}.foot{text-align:center;color:#71869a;font-size:10px;margin:24px 0 6px}.spinner{display:inline-block;width:12px;height:12px;border:2px solid #1d394b;border-top-color:var(--gold);border-radius:50%;animation:spin .7s linear infinite;vertical-align:middle}@keyframes s 70pin{to{transform:rotate(360deg)}}.flash{animation:flash .55s ease}@keyframes flash{0%{opacity:.45;transform:translateY(2px)}100%{opacity:1;transform:none}}
@media(max-width:850px){.grid{grid-template-columns:repeat(2,minmax(0,1fr))}.cols,.bottom-grid{grid-template-columns:1fr}.hero{align-items:flex-start;flex-direction:column}.controls{width:100%}.select,.btn{flex:1}.top{align-items:flex-start}.status{max-width:150px}}
@media(max-width:430px){.wrap{padding:13px}.card{padding:14px}.grid{gap:9px}.metric-value{font-size:22px}.levels{gap:5px}.level{padding:8px}.level strong{font-size:11px}.confluences{grid-template-columns:1fr}.brand{font-size:17px}.hero h1{font-size:30px}}
</style>
</head>
<body>
<main class="wrap">
<header class="top"><div><div class="brand">TRADING<span>FLOOR AI</span></div><div class="subtitle">Market intelligence · Technical confluence · Signal workspace</div></div><div class="status"><span class="dot" id="status-dot"></span><span id="feed-status">FEED NOT CHECKED</span></div></header>
<section class="hero"><div><div class="eyebrow">Live market terminal</div><h1>Trade the setup.<br><span class="gold">Not the noise.</span></h1><p>Market candles, trend structure, supply and demand, breakouts, retests and candlestick-pattern checks in one clean dashboard.</p></div><div class="controls"><select id="market" class="select" aria-label="Market"><option value="BTCUSDT">Bitcoin · BTC/USDT</option><option value="PAXGUSDT">Gold proxy · PAXG/USDT</option></select><select id="interval" class="select" aria-label="Timeframe"><option value="1m">1 minute</option><option value="5m">5 minutes</option><option value="15m">15 minutes</option><option value="30m">30 minutes</option><option value="1h" selected>1 hour</option><option value="4h">4 hours</option></select><select id="poll-rate" class="select" aria-label="Signal refresh interval"><option value="5000">Refresh every 5 seconds</option><option value="15000">Refresh every 15 seconds</option></select><button id="generate" class="btn btn-primary">✦ Generate Signal</button><a class="btn btn-secondary" href="./TradingFloorAI_SignalEA.mq5" download="TradingFloorAI_SignalEA.mq5" style="display:inline-flex;align-items:center;justify-content:center;text-decoration:none">⬇ Download MT5 Bot</a></div></section>
<section class="grid">
<div class="card"><div class="metric-label">Latest market price <span class="gold">● LIVE</span></div><div class="metric-value" id="price">—</div><div class="small" id="price-sub">Waiting for market candles</div></div>
<div class="card"><div class="metric-label">24-candle change <span>↗</span></div><div class="metric-value" id="change">—</div><div class="small" id="change-sub">Selected timeframe</div></div>
<div class="card"><div class="metric-label">Market bias <span>◈</span></div><div class="metric-value" id="bias">WAIT</div><div class="small" id="bias-sub">Awaiting analysis</div></div>
<div class="card"><div class="metric-label">Confluence score <span>◎</span></div><div class="metric-value" id="score">—</div><div class="bar"><i id="score-bar"></i></div><div class="small">Rule-based score, not a win probability</div></div>
</section>
<section class="cols">
<article class="card"><div class="card-head"><div><h2>Price action</h2><div class="small" id="chart-sub">Recent exchange candles</div></div><span class="tag" id="symbol-tag">BTCUSDT · 1H</span></div><div class="chart"><svg id="chart" viewBox="0 0 760 250" preserveAspectRatio="none" role="img" aria-label="Candlestick chart"><text x="380" y="125" fill="#91a4b9" text-anchor="middle">Loading market candles…</text></svg></div><div class="small" id="candle-meta">Candles are fetched from the signal service.</div><div class="notice">The chart is indicative market data, not your broker’s execution price. Verify prices in MT5 before trading.</div></article>
<article class="card"><div class="card-head"><div><h2>Signal generator</h2><div class="small">Entry · invalidation · targets</div></div><span class="tag" id="signal-tf">1H</span></div><div class="signal-box"><div class="signal-top"><div class="signal-direction" id="signal-dir">WAIT</div><span class="pill wait" id="signal-pill">NO SETUP</span></div><h3 id="setup-title">Waiting for a valid setup</h3><p id="signal-reason">Configure the signal service, then press Generate Signal.</p><div class="levels"><div class="level entry"><span>ENTRY</span><strong id="entry">—</strong></div><div class="level sl"><span>STOP LOSS</span><strong id="stop">—</strong></div><div class="level tp"><span>TAKE PROFIT</span><strong id="target">—</strong></div></div><div class="small" style="margin-top:12px" id="rr">Risk/reward: —</div></div><div class="card-head" style="margin-top:18px;margin-bottom:8px"><h2>Confluence checklist</h2><span class="tag" id="checks-count">0 / 6</span></div><div class="confluences" id="confluences"><div class="confluence">Run analysis to evaluate conditions.</div></div></article>
</section>
<section class="bottom-grid"><article class="card"><div class="card-head"><h2>Market structure</h2><span class="tag">Auto-detected</span></div><div class="rows" id="structure"><div class="item"><div><b>Trend</b><small>Waiting for candles</small></div><span class="tag">—</span></div></div></article><article class="card"><div class="card-head"><h2>Recent signal history</h2><span class="tag">This browser</span></div><div class="table-wrap"><table><thead><tr><th>Time</th><th>Market</th><th>TF</th><th>Signal</th><th>Score</th></tr></thead><tbody id="history"><tr><td colspan="5">No generated signals yet.</td></tr></tbody></table></div><div class="small" style="margin-top:9px">History stays in this browser only; it is not the MT5 signal queue.</div></article></section>
<section class="card" style="margin-top:13px" id="mt5-setup">
<div class="card-head"><div><h2>Connect TradingFloor AI to MetaTrader 5</h2><div class="small">Cloudflare Worker signal bridge · authenticated MT5 requests</div></div><span class="tag">SETUP REQUIRED</span></div>
<p class="small">The Download MT5 Bot button downloads the Expert Advisor source (.mq5). Compile it in MetaEditor to create the executable .ex5 file. The bot requests the same signal service used by this website; the website itself does not execute trades.</p>
<div class="rows">
<div class="item"><div><b>1. Deploy the signal service</b><small>In Cloudflare, create a Worker and paste the supplied worker.js code. Deploy it, then create a Worker secret named MT5_API_KEY using a long random value. Keep this secret private.</small></div><span class="tag">Cloudflare</span></div>
<div class="item"><div><b>2. Set the website endpoint</b><small>In this HTML, replace DEFAULT_ENDPOINT with your exact https://…workers.dev base URL. Do not put MT5_API_KEY in website code. Upload this index.html and TradingFloorAI_SignalEA.mq5 together to the website root.</small></div><span class="tag">Website</span></div>
<div class="item"><div><b>3. Compile the bot</b><small>In MT5, press F4 to open MetaEditor. Open TradingFloorAI_SignalEA.mq5 and press F7. Use the generated .ex5 file only if compilation succeeds without errors.</small></div><span class="tag">MetaEditor</span></div>
<div class="item"><div><b>4. Allow web requests in MT5</b><small>MT5 → Tools → Options → Expert Advisors → tick “Allow WebRequest for listed URL” → add only your Worker base URL, e.g. https://your-worker.your-subdomain.workers.dev (no endpoint path).</small></div><span class="tag">WebRequest</span></div>
<div class="item"><div><b>5. Configure the EA on a DEMO account</b><small>Attach it to a chart. Set InpWorkerBaseURL to the Worker URL, InpApiKey to the same secret, InpSignalSymbol to BTCUSDT or PAXGUSDT, and InpBrokerSymbol to the exact symbol in Market Watch. Keep InpAllowLiveTrading=false while testing.</small></div><span class="tag">Demo first</span></div>
<div class="item"><div><b>6. Verify before enabling orders</b><small>Check the Experts tab for HTTP 200 and fresh signal logs. Confirm broker symbol pricing, contract size, stop levels, spread and lot sizing. Only enable live trading after separate, extended demo validation.</small></div><span class="tag">Verify</span></div>
</div>
<div class="notice"><b>Security and trading warning:</b> Never publish the Worker API key in the website, GitHub repository, or a screenshot. Anyone who has the key can query the authenticated endpoint. Signals are experimental and not guaranteed profitable. PAXG/USDT is not the same instrument as XAU/USD; do not map them for automated trading unless you have verified the pricing and contract behavior.</div>
</section>
<div class="notice"><b>Risk note:</b> Experimental rule-based signals are not a validated profitable strategy. Scores are not win probabilities. Test on a demo account first. PAXG/USDT is a gold-backed token proxy, not XAU/USD. Signals expire quickly and may be rejected if stale.</div>
<footer class="foot">TradingFloor AI · Market data · Signal-only website · No performance guarantee</footer>
</main>
<script>
(()=>{
'use strict';
const $=id=>document.getElementById(id);
const DEFAULT_ENDPOINT='https://YOUR-WORKER-NAME.YOUR-SUBDOMAIN.workers.dev';
const ENDPOINT=(new URLSearchParams(location.search).get('signalApi')||DEFAULT_ENDPOINT).replace(/\/+$/,'');
const fmt=n=>Number.isFinite(Number(n))?Number(n).toLocaleString('en-US',{minimumFractionDigits:2,maximumFractionDigits:Number(n)<1?5:2}):'—';
let busy=false, timer=null, lastSignalId='';
const stateKey='tradingfloor_ai_history_v2';
function setStatus(text,live=false){$('feed-status').textContent=text;$('status-dot').className='dot'+(live?' live':'')}
function drawChart(cs){
 const svg=$('chart');if(!Array.isArray(cs)||cs.length<2){svg.innerHTML='<text x="380" y="125" fill="#91a4b9" text-anchor="middle">Waiting for candles…</text>';return}
 const data=cs.slice(-55),min=Math.min(...data.map(c=>c.l)),max=Math.max(...data.map(c=>c.h)),span=max-min||1,xstep=760/data.length,bodyW=Math.max(3,xstep*.52);let s='';
 for(let j=0;j<5;j++){const y=10+j*55;s+='<line x1="0" y1="'+y+'" x2="760" y2="'+y+'" stroke="#23384d" stroke-dasharray="4 6"/>'}
 data.forEach((c,i)=>{const x=i*xstep+xstep/2,y=v=>235-(v-min)/span*215,up=c.c>=c.o,color=up?'#31d6a0':'#ff687d',top=Math.min(y(c.o),y(c.c)),height=Math.max(2,Math.abs(y(c.o)-y(c.c)));s+='<line x1="'+x+'" y1="'+y(c.h)+'" x2="'+x+'" y2="'+y(c.l)+'" stroke="'+color+'" stroke-width="1.4"/><rect x="'+(x-bodyW/2)+'" y="'+top+'" width="'+bodyW+'" height="'+height+'" rx="1" fill="'+color+'"/>'});
 svg.innerHTML=s;
}
function renderStructure(a){
 const rows=[['Trend',a.trend,a.trend==='Bullish'?'positive':a.trend==='Bearish'?'negative':''],['Supply zone',a.inSupply?'Price near resistance/supply':'No nearby supply zone',a.inSupply?'negative':''],['Demand zone',a.inDemand?'Price near support/demand':'No nearby demand zone',a.inDemand?'positive':''],['Breakout',a.breakoutUp?'Bullish breakout':a.breakoutDown?'Bearish breakdown':'No fresh breakout',a.breakoutUp?'positive':a.breakoutDown?'negative':''],['Retest',a.retestUp?'Bullish retest':a.retestDown?'Bearish retest':'No confirmed retest',a.retestUp?'positive':a.retestDown?'negative':''],['Structure',a.higherHigh&&a.higherLow?'Higher highs / higher lows':a.lowerHigh&&a.lowerLow?'Lower highs / lower lows':'Mixed swing structure','']];
 $('structure').innerHTML=rows.map(r=>'<div class="item"><div><b>'+r[0]+'</b><small>'+r[1]+'</small></div><span class="tag '+r[2]+'">'+(r[2]==='positive'?'Bullish':r[2]==='negative'?'Bearish':'Checked')+'</span></div>').join('');
}
function renderSignal(a){
 const buy=a.dir==='BUY',sell=a.dir==='SELL',waiting=a.dir!=='BUY'&&a.dir!=='SELL';
 $('bias').textContent=a.dir;$('bias').className='metric-value '+(buy?'positive':sell?'negative':'');$('bias-sub').textContent=buy?'Bullish confluence':sell?'Bearish confluence':'No high-confluence setup';
 $('signal-dir').textContent=a.dir;$('signal-dir').className='signal-direction '+(buy?'positive':sell?'negative':'');$('signal-pill').textContent=buy?'BUY SETUP':sell?'SELL SETUP':'NO TRADE';$('signal-pill').className='pill '+(buy?'buy':sell?'sell':'wait');
 $('setup-title').textContent=buy?'Bullish technical confluence':sell?'Bearish technical confluence':'Wait for clearer confluence';
 $('signal-reason').textContent=waiting?(a.reason||'No direction reached the candidate threshold. Stay flat rather than inventing direction.'):(a.reason||'Rule-based candidate only; this is not a performance prediction.');
 $('entry').textContent=a.entry?fmt(a.entry):'—';$('stop').textContent=a.stop?fmt(a.stop):'—';$('target').textContent=a.target?fmt(a.target):'—';$('rr').textContent=a.rr?'Risk/reward target: 1 : '+Number(a.rr).toFixed(2)+' · ATR-based levels':'Risk/reward: not available';
 const labels=['Trend alignment','Supply / demand zone','Swing structure','Candlestick pattern','Breakout / retest','Momentum direction'],checks=Array.isArray(a.checks)?a.checks:[false,false,false,false,false,false];
 $('confluences').innerHTML=labels.map((label,i)=>'<div class="confluence"><span class="'+(checks[i]?'check':'cross')+'">'+(checks[i]?'✓':'○')+'</span><span>'+label+'<br><span class="small">'+(checks[i]?'Condition detected':'Condition not confirmed')+'</span></span></div>').join('');
 $('checks-count').textContent=checks.filter(Boolean).length+' / 6';$('score').textContent=Number.isFinite(Number(a.score))?Math.round(a.score)+' / 100':'—';$('score-bar').style.width=Math.max(0,Math.min(100,Number(a.score)||0))+'%';
 $('score-bar').style.background=buy?'linear-gradient(90deg,#2a9b7a,#31d6a0)':sell?'linear-gradient(90deg,#bc4a5b,#ff687d)':'linear-gradient(90deg,#b48b35,#f5bd4f)';
}
function renderHistory(){
 let h=[];try{h=JSON.parse(localStorage.getItem(stateKey)||'[]')}catch{}
 $('history').innerHTML=h.length?h.slice(0,10).map(x=>'<tr><td>'+new Date(x.t).toLocaleString()+'</td><td>'+x.symbol+'</td><td>'+x.tf+'</td><td class="'+(x.dir==='BUY'?'positive':x.dir==='SELL'?'negative':'')+'">'+x.dir+'</td><td>'+x.score+'/100</td></tr>').join(''):'<tr><td colspan="5">No generated signals yet.</td></tr>';
}
function saveHistory(s){
 if(!s||!s.signalId||s.signalId===lastSignalId)return;
 lastSignalId=s.signalId;
 let h=[];try{h=JSON.parse(localStorage.getItem(stateKey)||'[]')}catch{}
 h.unshift({t:s.generatedAt||Date.now(),symbol:s.symbol,tf:s.timeframe,dir:s.dir,score:Math.round(s.score||0)});
 try{localStorage.setItem(stateKey,JSON.stringify(h.slice(0,25)))}catch{}renderHistory();
}
async function generate(silent=false){
 if(busy)return;busy=true;if(!silent){$('generate').disabled=true;$('generate').innerHTML='<span class="spinner"></span> Checking…'}
 setStatus('CHECKING SIGNAL SERVICE');
 try{
  const symbol=$('market').value,interval=$('interval').value;
  const u=ENDPOINT+'/public-signal?symbol='+encodeURIComponent(symbol)+'&interval='+encodeURIComponent(interval);
  const res=await fetch(u,{cache:'no-store',headers:{'Accept':'application/json'}});
  if(!res.ok)throw Error('Signal service returned HTTP '+res.status+'. Check the Worker URL and deployment.');
  const payload=await res.json();
  if(!payload||!payload.signal||!Array.isArray(payload.candles))throw Error('Signal service response is incomplete.');
  const s=payload.signal,cs=payload.candles;
  if(!cs.length)throw Error('No closed candles returned by the signal service.');
  const now=Date.now();
  if(!Number.isFinite(Number(s.generatedAt))||!Number.isFinite(Number(s.expiresAt))||Number(s.expiresAt)<=now)throw Error('Signal is expired. Waiting for a fresh signal.');
  $('price').textContent=fmt(cs[cs.length-1].c);$('price-sub').textContent=symbol+' · candle close '+new Date(s.candleTime).toLocaleString();
  const first=cs[Math.max(0,cs.length-24)].c,last=cs[cs.length-1].c,change=first?(last-first)/first*100:0;
  $('change').textContent=(change>=0?'+':'')+change.toFixed(2)+'%';$('change').className='metric-value '+(change>=0?'positive':'negative');$('change-sub').textContent='Change across recent closed candles';
  $('symbol-tag').textContent=symbol+' · '+interval.toUpperCase();$('signal-tf').textContent=interval.toUpperCase();$('chart-sub').textContent='Signal service · '+interval.toUpperCase();
  $('candle-meta').textContent=cs.length+' closed candles · candle '+new Date(s.candleTime).toLocaleString()+' · expires '+new Date(s.expiresAt).toLocaleTimeString();
  drawChart(cs);renderStructure(s);renderSignal(s);saveHistory(s);setStatus('SIGNAL SERVICE CONNECTED',true);
 }catch(e){
  setStatus('SIGNAL SERVICE ERROR');$('price-sub').textContent=e.message;
  if(!silent){$('signal-reason').textContent=e.message;$('setup-title').textContent='Signal service unavailable';$('signal-dir').textContent='WAIT';$('signal-pill').textContent='FEED ERROR';$('signal-pill').className='pill wait';$('bias').textContent='WAIT';$('bias-sub').textContent='Could not analyse market';$('entry').textContent='—';$('stop').textContent='—';$('target').textContent='—';$('rr').textContent='Risk/reward unavailable';$('score').textContent='—';$('score-bar').style.width='0%';$('confluences').innerHTML='<div class="confluence">Signal service unavailable. No new trade signal should be used.</div>'}
  console.error(e);
 }finally{busy=false;$('generate').disabled=false;$('generate').textContent='✦ Generate Signal'}
}
function restartPolling(){if(timer)clearInterval(timer);generate(false);timer=setInterval(()=>generate(true),Number($('poll-rate').value)||5000)}
$('generate').addEventListener('click',()=>generate(false));
$('market').addEventListener('change',restartPolling);
$('interval').addEventListener('change',()=>{$('signal-tf').textContent=$('interval').value.toUpperCase();restartPolling()});
$('poll-rate').addEventListener('change',restartPolling);
renderHistory();
if(ENDPOINT.includes('YOUR-WORKER-NAME')){setStatus('SET WORKER URL');$('signal-reason').textContent='Deploy worker.js, then replace DEFAULT_ENDPOINT in index.html with your deployed Workers URL.'}
else restartPolling();
})();
</script>
</body>
</html>
