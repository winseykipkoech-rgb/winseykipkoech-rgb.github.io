<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#ffffff">
<title>Trading Terminal - Simulator</title>

<style>
:root {
  --blue:#2878d0;
  --red:#e34b4b;
  --text:#171717;
  --muted:#777;
  --line:#e4e4e4;
}
* { box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
html,body {
  margin:0; min-height:100%;
  font-family:Roboto,Arial,sans-serif;
  color:var(--text); background:#fff;
}
body { padding-bottom:80px; font-size:15px; }
button,input,select { font:inherit; }
button { cursor:pointer; }
.topbar {
  height:60px; display:flex; align-items:center; gap:16px;
  padding:0 15px; border-bottom:1px solid #eee;
  position:sticky; top:0; background:#fff; z-index:5;
}
.hamburger,.icon-btn {
  border:0; background:transparent; color:#333; padding:5px;
}
.hamburger { font-size:27px; width:34px; }
.top-title { font-size:21px; font-weight:500; flex:1; }
.icon-btn { font-size:27px; }
.page { display:none; }
.page.active { display:block; }
.bottom-nav {
  position:fixed; z-index:8; left:0; right:0; bottom:0;
  height:70px; display:flex; background:#fff;
  border-top:1px solid #ddd;
}
.nav-item {
  flex:1; min-width:0; border:0; background:#fff; color:#555;
  display:flex; flex-direction:column; align-items:center;
  justify-content:center; gap:3px; font-size:12px;
}
.nav-item .glyph { font-size:25px; line-height:27px; }
.nav-item.active { color:var(--blue); font-weight:700; }
.status {
  font-size:11px; color:#777; padding:8px 12px;
  border-bottom:1px solid #eee;
}
.quote-row {
  display:flex; justify-content:space-between; align-items:center;
  gap:7px; padding:17px 12px; border-bottom:1px solid #eee;
  min-height:91px;
}
.quote-name { font-weight:700; font-size:17px; }
.quote-sub,.quote-meta {
  font-size:12px; color:var(--muted); margin-top:5px;
}
.quote-prices {
  display:flex; gap:10px; font-size:16px;
  font-weight:700; white-space:nowrap;
}
.bid { color:var(--red); }
.ask { color:var(--blue); }
.small-label { font-size:10px; font-weight:500; margin-bottom:3px; }
.trade-controls { display:flex; height:57px; align-items:stretch; }
.trade-controls>button {
  width:29%; border:0; color:#fff; font-size:14px;
}
.sell-btn { background:#3483f6; }
.buy-btn { background:#e94c4c; }
.lot-control {
  flex:1; display:flex; align-items:center;
  justify-content:space-around; border-bottom:1px solid #ddd;
}
.lot-control button {
  border:0; background:#fff; font-size:22px; padding:0 5px;
}
.lot-control input {
  width:44px; border:0; text-align:center;
  outline:none; background:#fff;
}
.chart-tools {
  display:flex; gap:8px; padding:10px;
  align-items:center; font-weight:700;
}
.chart-tools select {
  border:0; background:#fff; color:#1768b3;
  font-weight:700; max-width:58%; padding:5px;
}
.tv-wrap {
  height:55vh; min-height:330px; max-height:650px;
  width:100%; position:relative;
}
#tvChart { width:100%; height:100%; }
.chart-fallback { padding:20px; text-align:center; color:#777; }
.card {
  margin:13px; padding:15px; border:1px solid var(--line);
  border-radius:4px; line-height:1.5;
}
.muted { color:var(--muted); }
.summary { padding:14px 15px; }
.floating { font-size:21px; font-weight:700; margin-bottom:14px; }
.summary-row {
  display:flex; justify-content:space-between; gap:10px;
  padding:7px 0; font-weight:700;
}
.section-heading {
  padding:13px 14px; background:#f6f6f6;
  border-top:1px solid var(--line);
  border-bottom:1px solid var(--line);
  font-weight:700; color:#777;
}
.position,.history-item { padding:13px; border-bottom:1px solid var(--line); }
.pos-top,.history-top {
  display:flex; justify-content:space-between;
  gap:9px; align-items:flex-start;
}
.pos-symbol { font-weight:700; }
.pos-detail { font-size:13px; color:#777; margin-top:5px; }
.pnl { font-weight:700; font-size:17px; white-space:nowrap; }
.positive { color:var(--blue); }
.negative { color:var(--red); }
.close-btn,.secondary-btn {
  background:#fff; border:1px solid #aaa; border-radius:4px;
  padding:8px 12px; margin-top:10px; color:#333;
}
.empty { text-align:center; padding:30px 14px; color:#888; }
.overlay {
  display:none; position:fixed; inset:0; background:#0007; z-index:20;
}
.overlay.open { display:block; }
.drawer {
  width:min(86vw,350px); height:100%; overflow:auto;
  background:#fff; padding-bottom:20px;
}
.drawer-head { padding:24px 20px; border-bottom:1px solid var(--line); }
.avatar {
  width:48px; height:48px; display:grid; place-items:center;
  background:var(--blue); color:#fff; font-weight:700;
  font-size:21px; margin-bottom:12px;
}
.drawer-head small { display:block; color:#777; margin-top:6px; }
.drawer-link {
  width:100%; border:0; background:#fff; text-align:left;
  display:flex; align-items:center; gap:18px;
  padding:14px 21px; font-size:16px; font-weight:600;
}
.drawer-link .glyph { width:25px; text-align:center; font-size:21px; }
.form-card label { display:block; font-weight:700; margin:14px 0 6px; }
.form-card input,.form-card select {
  width:100%; padding:12px; border:1px solid #ccc;
  border-radius:4px; background:#fff;
}
.primary-btn {
  width:100%; padding:13px; border:0; border-radius:4px;
  background:var(--blue); color:#fff; font-weight:700; margin-top:17px;
}
.notice {
  background:#fff8e5; border-left:4px solid #e5a000;
  padding:13px; font-size:13px; line-height:1.55;
}
@media(max-width:360px) {
  .topbar { gap:10px; }
  .quote-prices { font-size:13px; gap:6px; }
  .nav-item { font-size:11px; }
}
</style>
</head>
<body>

<header class="topbar">
  <button class="hamburger" aria-label="Open menu" onclick="openDrawer()">☰</button>
  <div class="top-title" id="topTitle">Quotes</div>
  <button class="icon-btn" id="headerAction" onclick="headerAction()">＋</button>
</header>

<section class="page active" id="quotesPage">
  <div class="status">Simulated quotes · No broker connected</div>
  <div id="quotesList"></div>
</section>

<section class="page" id="chartsPage">
  <div class="trade-controls">
    <button class="sell-btn" onclick="openOrder('SELL')">
      <span class="small-label">SELL</span><br>
      <strong id="sellPrice">—</strong>
    </button>
    <div class="lot-control">
      <button onclick="adjustLot(-0.01)">−</button>
      <input id="chartLot" type="number" min="0.01" max="100" step="0.01" value="0.01">
      <button onclick="adjustLot(0.01)">＋</button>
    </div>
    <button class="buy-btn" onclick="openOrder('BUY')">
      <span class="small-label">BUY</span><br>
      <strong id="buyPrice">—</strong>
    </button>
  </div>

  <div class="chart-tools">
    <select id="chartSymbol" onchange="loadChart()">
      <option value="OANDA:XAUUSD">XAUUSD</option>
      <option value="OANDA:EURUSD">EURUSD</option>
    </select>
    <select id="chartInterval" onchange="loadChart()">
      <option value="15">M15</option>
      <option value="30">M30</option>
      <option value="60">H1</option>
      <option value="240" selected>H4</option>
      <option value="D">D1</option>
      <option value="W">W1</option>
    </select>
  </div>

  <div class="tv-wrap">
    <div id="tvChart">
      <div class="chart-fallback">Loading TradingView chart…</div>
    </div>
  </div>
  <div class="card">
    <strong>Order controls</strong>
    <p class="muted">The chart is from TradingView. Orders and P/L are simulated locally and are not connected to chart prices.</p>
    <button class="secondary-btn" onclick="showPage('trade')">View positions</button>
  </div>
</section>

<section class="page" id="tradePage">
  <div class="summary">
    <div class="floating" id="floatingTotal">0.00 USD</div>
    <div class="summary-row"><span>Balance:</span><span id="balance">10,000.00</span></div>
    <div class="summary-row"><span>Equity:</span><span id="equity">10,000.00</span></div>
    <div class="summary-row"><span>Margin:</span><span id="margin">0.00</span></div>
    <div class="summary-row"><span>Free margin:</span><span id="freeMargin">10,000.00</span></div>
    <div class="summary-row"><span>Margin Level (%):</span><span id="marginLevel">—</span></div>
    <button class="secondary-btn" onclick="showPage('charts')">＋ New order</button>
  </div>
  <div class="section-heading">Positions <span style="float:right" id="positionCount">0</span></div>
  <div id="positionsList"><div class="empty">No open positions</div></div>
</section>

<section class="page" id="historyPage">
  <div class="summary">
    <div class="summary-row"><span>Profit:</span><span id="historyProfit">0.00</span></div>
    <div class="summary-row"><span>Deposits:</span><span id="deposits">10,000.00</span></div>
    <div class="summary-row"><span>Balance:</span><span id="historyBalance">10,000.00</span></div>
  </div>
  <div class="section-heading">Closed trades</div>
  <div id="historyList"><div class="empty">No closed trades yet</div></div>
</section>

<section class="page" id="messagesPage">
  <div class="card"><h3>Messages</h3><p class="muted">No broker connection or messages are configured.</p></div>
</section>
<section class="page" id="newsPage">
  <div class="card"><h3>News</h3><p class="muted">No broker news feed is connected.</p></div>
</section>
<section class="page" id="mailboxPage">
  <div class="card"><h3>Mailbox</h3><p class="muted">No broker mailbox is connected.</p></div>
</section>
<section class="page" id="journalPage">
  <div class="card"><h3>Journal</h3><div id="journalList"></div></div>
</section>
<section class="page" id="calendarPage">
  <div class="card"><h3>Economic calendar</h3><p class="muted">A live calendar requires an external data source.</p></div>
</section>
<section class="page" id="communityPage">
  <div class="card"><h3>Traders Community</h3><p class="muted">Community features require an external service.</p></div>
</section>
<section class="page" id="guidePage">
  <div class="card">
    <h3>User guide</h3>
    <p>1. Select XAUUSD or EURUSD.</p>
    <p>2. Choose a timeframe and lot size.</p>
    <p>3. Tap Buy or Sell to open a simulated position.</p>
    <p>4. Visit Trade to monitor or close it.</p>
    <p>5. Visit History to review closed trades.</p>
  </div>
</section>
<section class="page" id="settingsPage">
  <div class="card form-card">
    <h3>Settings</h3>
    <label for="startingBalance">Starting balance (USD)</label>
    <input id="startingBalance" type="number" min="1" value="10000">

    <label for="leverage">Simulated leverage</label>
    <select id="leverage">
      <option value="50">1:50</option>
      <option value="100" selected>1:100</option>
      <option value="200">1:200</option>
      <option value="500">1:500</option>
    </select>

    <button class="primary-btn" onclick="saveSettings()">Save settings</button>
    <p class="muted">Changing the balance closes open positions and resets the simulated account balance.</p>
    <button class="secondary-btn" onclick="resetAccount()">Reset account and history</button>
  </div>
</section>

<section class="page" id="aboutPage">
  <div class="card">
    <h2>About</h2>
    <p><strong>Trading Terminal</strong></p>
    <p>Version 1.1 · Educational trading simulator</p>

    <div class="notice">
      <strong>Disclaimer</strong><br><br>
      This is an independent educational simulator. Balances shown in USD, account labels, orders, margin, equity, profit/loss and trade history are simulated locally with JavaScript. No broker is connected; no real orders, deposits, withdrawals or financial transactions occur. A displayed balance is not real money.<br><br>

      TradingView charts load separately over the internet. Their prices are not connected to the simulator's local prices, which are randomly varied demonstration values.<br><br>

      This project is not an official MetaTrader 5 or MetaQuotes application and is not affiliated with, endorsed by or sponsored by MetaQuotes Ltd. or any broker. All third-party names and trademarks belong to their respective owners. This app is for learning and testing only.
    </div>

    <h3>Account information</h3>
    <p>Interface: MT5-inspired</p>
    <p>Execution: Local simulation only</p>
    <p>Broker connection: None</p>
    <p>Persistence: Browser local storage, when available</p>
  </div>
</section>

<nav class="bottom-nav" aria-label="Main navigation">
  <button class="nav-item active" data-page="quotes" onclick="showPage('quotes')">
    <span class="glyph">↕</span>Quotes
  </button>
  <button class="nav-item" data-page="charts" onclick="showPage('charts')">
    <span class="glyph">▥</span>Charts
  </button>
  <button class="nav-item" data-page="trade" onclick="showPage('trade')">
    <span class="glyph">⌁</span>Trade
  </button>
  <button class="nav-item" data-page="history" onclick="showPage('history')">
    <span class="glyph">◷</span>History
  </button>
  <button class="nav-item" data-page="messages" onclick="showPage('messages')">
    <span class="glyph">▢</span>Messages
  </button>
</nav>

<div class="overlay" id="overlay" onclick="closeDrawer(event)">
  <aside class="drawer" onclick="event.stopPropagation()">
    <div class="drawer-head">
      <div class="avatar">TT</div>
      <strong>Trading Terminal</strong>
      <small>Educational simulator · No broker</small>
      <p><a href="#" onclick="goMenu('settings');return false">Manage account settings</a></p>
    </div>

    <button class="drawer-link" onclick="goMenu('trade')"><span class="glyph">⌁</span>Trade</button>
    <button class="drawer-link" onclick="goMenu('news')"><span class="glyph">▤</span>News</button>
    <button class="drawer-link" onclick="goMenu('mailbox')"><span class="glyph">✉</span>Mailbox</button>
    <button class="drawer-link" onclick="goMenu('journal')"><span class="glyph">▦</span>Journal</button>
    <button class="drawer-link" onclick="goMenu('settings')"><span class="glyph">⚙</span>Settings</button>
    <button class="drawer-link" onclick="goMenu('calendar')"><span class="glyph">▣</span>Economic calendar</button>
    <button class="drawer-link" onclick="goMenu('community')"><span class="glyph">♙</span>Traders Community</button>
    <button class="drawer-link" onclick="goMenu('guide')"><span class="glyph">?</span>User guide</button>
    <button class="drawer-link" onclick="goMenu('about')"><span class="glyph">ⓘ</span>About</button>
  </aside>
</div>
<script>
'use strict';

const STORAGE_KEY = 'trading_terminal_sim_v2';

const specs = {
  XAUUSD: {
    name: 'Gold vs US Dollar',
    initial: 4300,
    spread: 0.40,
    contract: 100,
    digits: 2,
    step: 0.5
  },
  EURUSD: {
    name: 'Euro vs US Dollar',
    initial: 1.165,
    spread: 0.00012,
    contract: 100000,
    digits: 5,
    step: 0.00015
  }
};

let account = {
  balance: 10000,
  leverage: 100,
  deposits: 10000,
  positions: [],
  history: [],
  prices: { XAUUSD: 4300, EURUSD: 1.165 }
};

let nextId = 1;
let currentPage = 'quotes';
let journal = [];

function loadState() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return;

    const d = JSON.parse(raw);

    if (
      d &&
      Number.isFinite(d.balance) &&
      d.balance > 0 &&
      d.prices &&
      Array.isArray(d.positions) &&
      Array.isArray(d.history)
    ) {
      account = { ...account, ...d };

      for (const s of Object.keys(specs)) {
        if (!Number.isFinite(account.prices[s])) {
          account.prices[s] = specs[s].initial;
        }
      }

      nextId = Math.max(
        0,
        ...account.positions.map(p => Number(p.id) || 0),
        ...account.history.map(p => Number(p.id) || 0)
      ) + 1;
    }
  } catch (e) {
    console.warn('Saved data unavailable', e);
  }
}

function saveState() {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(account));
  } catch (e) {
    console.warn('Local storage unavailable', e);
  }
}

function money(n) {
  return Number(n).toLocaleString('en-US', {
    minimumFractionDigits: 2,
    maximumFractionDigits: 2
  });
}

function fmt(s, n) {
  return Number(n).toLocaleString('en-US', {
    minimumFractionDigits: specs[s].digits,
    maximumFractionDigits: specs[s].digits
  });
}

function mid(s) {
  return account.prices[s];
}

function quote(s) {
  return {
    bid: mid(s) - specs[s].spread / 2,
    ask: mid(s) + specs[s].spread / 2
  };
}

function pnl(p) {
  const q = quote(p.symbol);
  const out = p.side === 'BUY' ? q.bid : q.ask;

  return (
    (p.side === 'BUY' ? out - p.entry : p.entry - out) *
    specs[p.symbol].contract *
    p.lots
  );
}

function marginFor(p) {
  return (
    p.entry *
    specs[p.symbol].contract *
    p.lots /
    account.leverage
  );
}

function floating() {
  return account.positions.reduce((sum, p) => sum + pnl(p), 0);
}

function usedMargin() {
  return account.positions.reduce((sum, p) => sum + marginFor(p), 0);
}

function equity() {
  return account.balance + floating();
}

function freeMargin() {
  return equity() - usedMargin();
}

function logEvent(message) {
  journal.unshift({
    time: new Date().toLocaleString(),
    message
  });

  journal = journal.slice(0, 100);
  renderJournal();
}

function renderQuotes() {
  const el = document.getElementById('quotesList');

  el.innerHTML = Object.keys(specs).map(s => {
    const q = quote(s);

    return `
      <div class="quote-row"
           role="button"
           tabindex="0"
           onclick="selectChart('${s}')"
           onkeydown="if(event.key==='Enter')selectChart('${s}')">
        <div>
          <div class="quote-name">${s}</div>
          <div class="quote-sub">${specs[s].name}</div>
          <div class="quote-meta">Simulated price · local demo</div>
        </div>
        <div class="quote-prices">
          <div>
            <div class="small-label">BID</div>
            <span class="bid">${fmt(s, q.bid)}</span>
          </div>
          <div>
            <div class="small-label">ASK</div>
            <span class="ask">${fmt(s, q.ask)}</span>
          </div>
        </div>
      </div>`;
  }).join('');
}

function renderTrade() {
  const f = floating();
  const m = usedMargin();
  const e = equity();

  document.getElementById('floatingTotal').textContent =
    money(f) + ' USD';

  document.getElementById('floatingTotal').className =
    'floating ' + (f >= 0 ? 'positive' : 'negative');

  document.getElementById('balance').textContent = money(account.balance);
  document.getElementById('equity').textContent = money(e);
  document.getElementById('margin').textContent = money(m);
  document.getElementById('freeMargin').textContent = money(freeMargin());

  document.getElementById('marginLevel').textContent =
    m > 0 ? money(e / m * 100) : '—';

  document.getElementById('positionCount').textContent =
    account.positions.length;

  const el = document.getElementById('positionsList');

  if (!account.positions.length) {
    el.innerHTML = '<div class="empty">No open positions</div>';
    return;
  }

  el.innerHTML = account.positions.map(p => {
    const q = quote(p.symbol);
    const out = p.side === 'BUY' ? q.bid : q.ask;
    const v = pnl(p);

    return `
      <div class="position">
        <div class="pos-top">
          <div>
            <div class="pos-symbol">
              ${p.symbol},
              <span class="${p.side === 'BUY' ? 'positive' : 'negative'}">
                ${p.side} ${p.lots.toFixed(2)}
              </span>
            </div>
            <div class="pos-detail">
              ${fmt(p.symbol, p.entry)} → ${fmt(p.symbol, out)}
            </div>
          </div>
          <div class="pnl ${v >= 0 ? 'positive' : 'negative'}">
            ${v >= 0 ? '+' : ''}${money(v)}
          </div>
        </div>
        <div class="pos-detail">Opened ${p.openedAt}</div>
        <button class="close-btn" onclick="closePosition(${p.id})">
          Close position
        </button>
      </div>`;
  }).join('');
}

function renderHistory() {
  const closed = account.history;
  const profit = closed.reduce((a, p) => a + p.pnl, 0);

  document.getElementById('historyProfit').textContent = money(profit);
  document.getElementById('deposits').textContent = money(account.deposits);
  document.getElementById('historyBalance').textContent = money(account.balance);

  const el = document.getElementById('historyList');

  if (!closed.length) {
    el.innerHTML = '<div class="empty">No closed trades yet</div>';
    return;
  }

  el.innerHTML = closed.slice().reverse().map(p => `
    <div class="history-item">
      <div class="history-top">
        <strong>
          ${p.symbol},
          <span class="${p.side === 'BUY' ? 'positive' : 'negative'}">
            ${p.side} ${p.lots.toFixed(2)}
          </span>
        </strong>
        <strong class="${p.pnl >= 0 ? 'positive' : 'negative'}">
          ${p.pnl >= 0 ? '+' : ''}${money(p.pnl)}
        </strong>
      </div>
      <div class="pos-detail">
        ${fmt(p.symbol, p.entry)} → ${fmt(p.symbol, p.exit)}
      </div>
      <div class="pos-detail">
        Opened: ${p.openedAt}<br>
        Closed: ${p.closedAt}
      </div>
    </div>
  `).join('');
}

function renderJournal() {
  const el = document.getElementById('journalList');
  if (!el) return;

  el.innerHTML = journal.length
    ? journal.map(j => `
        <p><small>${j.time}</small><br>${j.message}</p>
      `).join('')
    : '<p>No events recorded this session.</p>';
}

function updateChartPrices() {
  const s = document.getElementById('chartSymbol').value.split(':').pop();
  const q = quote(s);

  document.getElementById('sellPrice').textContent = fmt(s, q.bid);
  document.getElementById('buyPrice').textContent = fmt(s, q.ask);
}

function renderAll() {
  renderQuotes();
  renderTrade();
  renderHistory();
  renderJournal();
  updateChartPrices();
  saveState();
}

function adjustLot(delta) {
  const el = document.getElementById('chartLot');
  const n = Number(el.value) || 0.01;

  el.value = Math.min(
    100,
    Math.max(0.01, Math.round((n + delta) * 100) / 100)
  ).toFixed(2);
}

function openOrder(side) {
  const symbol = document.getElementById('chartSymbol').value.split(':').pop();
  const lots = Number(document.getElementById('chartLot').value);

  if (!Number.isFinite(lots) || lots < 0.01 || lots > 100) {
    alert('Lot size must be between 0.01 and 100.');
    return;
  }

  const q = quote(symbol);
  const entry = side === 'BUY' ? q.ask : q.bid;

  const p = {
    id: nextId++,
    symbol,
    side,
    lots,
    entry,
    openedAt: new Date().toLocaleString()
  };

  if (marginFor(p) > freeMargin()) {
    alert('Insufficient free margin for this simulated order.');
    return;
  }

  account.positions.push(p);
  logEvent('Opened simulated ' + side + ' ' + lots.toFixed(2) + ' ' + symbol);

  renderAll();
  showPage('trade');
}

function closePosition(id) {
  const i = account.positions.findIndex(p => p.id === id);
  if (i < 0) return;

  const p = account.positions[i];
  const result = pnl(p);
  const q = quote(p.symbol);
  const out = p.side === 'BUY' ? q.bid : q.ask;

  account.balance += result;

  account.history.push({
    ...p,
    exit: out,
    pnl: result,
    closedAt: new Date().toLocaleString()
  });

  account.positions.splice(i, 1);

  logEvent('Closed simulated ' + p.side + ' ' + p.symbol + ': ' + money(result) + ' USD');

  renderAll();
}

function simulatePrices() {
  for (const s of Object.keys(specs)) {
    const step = specs[s].step;

    account.prices[s] = Math.max(
      0.00001,
      mid(s) + (Math.random() - 0.5) * step
    );
  }

  renderAll();
}

function loadChart() {
  const symbol = document.getElementById('chartSymbol').value;
  const interval = document.getElementById('chartInterval').value;
  const el = document.getElementById('tvChart');

  el.innerHTML = '<div class="chart-fallback">Loading TradingView chart…</div>';

  if (!navigator.onLine) {
    el.innerHTML = '<div class="chart-fallback">No internet connection. Reconnect to load TradingView.</div>';
    return;
  }

  if (!window.TradingView) {
    el.innerHTML = '<div class="chart-fallback">TradingView is not available. Check internet access and reopen Charts.</div>';
    return;
  }

  try {
    el.innerHTML = '';

    new TradingView.widget({
      autosize: true,
      symbol: symbol,
      interval: interval,
      timezone: 'Africa/Nairobi',
      theme: 'light',
      style: '1',
      locale: 'en',
      enable_publishing: false,
      allow_symbol_change: false,
      hide_top_toolbar: false,
      hide_legend: false,
      save_image: false,
      container_id: 'tvChart'
    });
  } catch (e) {
    el.innerHTML = '<div class="chart-fallback">Could not load chart. Check your internet connection.</div>';
    console.warn(e);
  }
}

function selectChart(s) {
  document.getElementById('chartSymbol').value = 'OANDA:' + s;
  showPage('charts');
}

function showPage(name) {
  const target = document.getElementById(name + 'Page');
  if (!target) return;

  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  target.classList.add('active');

  currentPage = name;

  const titles = {
    quotes:'Quotes',
    charts:'Charts',
    trade:'Trade',
    history:'History',
    messages:'Messages',
    settings:'Settings',
    about:'About',
    news:'News',
    mailbox:'Mailbox',
    journal:'Journal',
    calendar:'Economic calendar',
    community:'Traders Community',
    guide:'User guide'
  };

  document.getElementById('topTitle').textContent = titles[name] || name;

  document.getElementById('headerAction').textContent =
    ['quotes', 'trade'].includes(name) ? '＋' : '⋮';

  document.querySelectorAll('.nav-item').forEach(b => {
    b.classList.toggle('active', b.dataset.page === name);
  });

  closeDrawer();

  if (name === 'charts') loadChart();
  if (name === 'trade') renderTrade();
  if (name === 'history') renderHistory();

  window.scrollTo(0, 0);
}

function openDrawer() {
  document.getElementById('overlay').classList.add('open');
}

function closeDrawer(event) {
  if (event && event.target !== document.getElementById('overlay')) return;

  document.getElementById('overlay').classList.remove('open');
}

function goMenu(name) {
  showPage(name);
}

function headerAction() {
  if (currentPage === 'quotes' || currentPage === 'trade') {
    showPage('charts');
    return;
  }

  openDrawer();
}

function saveSettings() {
  const balance = Number(document.getElementById('startingBalance').value);
  const leverage = Number(document.getElementById('leverage').value);

  if (!Number.isFinite(balance) || balance <= 0) {
    alert('Enter a starting balance greater than zero.');
    return;
  }

  if (account.positions.length &&
      !confirm('Close all open positions before changing the account balance?')) {
    return;
  }

  account.positions.forEach(p => {
    const result = pnl(p);
    const q = quote(p.symbol);
    const out = p.side === 'BUY' ? q.bid : q.ask;

    account.balance += result;

    account.history.push({
      ...p,
      exit: out,
      pnl: result,
      closedAt: new Date().toLocaleString()
    });
  });

  account.positions = [];
  account.balance = balance;
  account.deposits = balance;
  account.leverage = leverage;

  logEvent('Updated simulated account settings.');
  renderAll();
  alert('Settings saved.');
}

function resetAccount() {
  if (!confirm('Reset simulated balance and erase all open and closed trades?')) {
    return;
  }

  account = {
    balance: 10000,
    leverage: 100,
    deposits: 10000,
    positions: [],
    history: [],
    prices: { XAUUSD: 4300, EURUSD: 1.165 }
  };

  nextId = 1;
  journal = [];

  document.getElementById('startingBalance').value = 10000;
  document.getElementById('leverage').value = '100';

  saveState();
  renderAll();
  logEvent('Simulated account reset.');
}

/* Start the local simulator */
loadState();

document.getElementById('startingBalance').value = account.balance;
document.getElementById('leverage').value = String(account.leverage);

renderAll();
setInterval(simulatePrices, 2000);

/* Load TradingView from its public widget library */
</script>

<script
  async
  src="https://s3.tradingview.com/tv.js"
  onload="if(currentPage==='charts')loadChart()">
</script>

</body>
</html>
