<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">

<title>Trading Terminal</title>

<style>
:root {
  --blue: #2878d0;
  --red: #e64b4b;
  --green: #159b83;
  --text: #171717;
  --muted: #777;
  --line: #e5e5e5;
  --bg: #fff;
}

* {
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}

body {
  margin: 0;
  font-family: Roboto, Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
  font-size: 15px;
}

button, input, select {
  font: inherit;
}

button {
  cursor: pointer;
}

.topbar {
  height: 62px;
  display: flex;
  align-items: center;
  padding: 0 17px;
  gap: 20px;
  background: #fff;
  border-bottom: 1px solid #f0f0f0;
  position: sticky;
  top: 0;
  z-index: 5;
}

.hamburger {
  border: 0;
  background: none;
  font-size: 29px;
  padding: 0;
  width: 35px;
}

.top-title {
  font-size: 21px;
  font-weight: 500;
  flex: 1;
}

.icon-btn {
  border: 0;
  background: none;
  font-size: 24px;
  color: #555;
}

.page {
  display: none;
  padding-bottom: 85px;
}

.page.active {
  display: block;
}

.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 75px;
  display: flex;
  justify-content: space-around;
  background: white;
  border-top: 1px solid #ddd;
  z-index: 8;
  padding-bottom: env(safe-area-inset-bottom);
}

.nav-item {
  flex: 1;
  border: 0;
  background: white;
  color: #555;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 5px;
  font-size: 12px;
}

.nav-item .nav-icon {
  font-size: 24px;
  line-height: 27px;
}

.nav-item.active {
  color: var(--blue);
  font-weight: bold;
}

/* QUOTES */

.quote-row {
  padding: 17px 13px;
  border-bottom: 1px solid #f1f1f1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
}

.quote-name {
  font-size: 17px;
  font-weight: bold;
}

.quote-sub {
  color: var(--muted);
  font-size: 12px;
  margin-top: 5px;
}

.quote-change {
  font-size: 12px;
  color: var(--blue);
  margin-bottom: 5px;
}

.quote-price {
  display: flex;
  gap: 12px;
  font-size: 19px;
  font-weight: bold;
}

.bid { color: var(--red); }
.ask { color: var(--blue); }

/* CHART */

.trade-controls {
  display: flex;
  align-items: stretch;
  height: 55px;
}

.sell-btn, .buy-btn {
  color: white;
  border: 0;
  width: 30%;
  font-size: 16px;
}

.sell-btn { background: #3483f6; }
.buy-btn { background: #e94c4c; }

.lot-control {
  display: flex;
  flex: 1;
  align-items: center;
  justify-content: space-around;
  background: white;
}

.lot-control button {
  border: 0;
  background: white;
  font-size: 23px;
}

.lot-control input {
  width: 48px;
  border: 0;
  text-align: center;
  outline: none;
}

.chart-info {
  padding: 10px;
  font-size: 14px;
  font-weight: bold;
}

.tv-container {
  height: 58vh;
  min-height: 340px;
  position: relative;
}

#tradingview_chart {
  width: 100%;
  height: 100%;
}

/* TRADE */

.account-summary {
  padding: 15px 16px;
}

.account-heading {
  color: var(--blue);
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 16px;
}

.summary-row {
  display: flex;
  justify-content: space-between;
  padding: 8px 0;
  gap: 8px;
  font-weight: bold;
}

.summary-row span:first-child {
  color: #333;
}

.section-heading {
  padding: 14px;
  background: #f6f6f6;
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
  font-weight: bold;
  color: #777;
}

.position {
  padding: 13px;
  border-bottom: 1px solid var(--line);
}

.position-line {
  display: flex;
  justify-content: space-between;
  gap: 10px;
}

.position-symbol {
  font-weight: bold;
}

.position-detail {
  color: #777;
  margin-top: 5px;
  font-size: 13px;
}

.pnl {
  font-size: 17px;
  font-weight: bold;
}

.positive { color: var(--blue); }
.negative { color: var(--red); }

.close-position {
  margin-top: 10px;
  padding: 7px 12px;
  background: white;
  border: 1px solid #bbb;
  border-radius: 4px;
}

/* HISTORY */

.history-summary {
  padding: 15px;
  border-bottom: 1px solid var(--line);
}

.history-item {
  padding: 13px;
  border-bottom: 1px solid var(--line);
}

.history-item small {
  color: var(--muted);
}

.history-top {
  display: flex;
  justify-content: space-between;
  gap: 8px;
}

/* DRAWER */

.overlay {
  display: none;
  position: fixed;
  inset: 0;
  background: #0008;
  z-index: 20;
}

.overlay.open {
  display: block;
}

.drawer {
  width: min(86%, 350px);
  height: 100%;
  background: white;
  overflow-y: auto;
  padding-bottom: 20px;
}

.drawer-header {
  padding: 25px 20px;
  border-bottom: 1px solid var(--line);
}

.avatar {
  width: 52px;
  height: 52px;
  background: var(--blue);
  color: white;
  border-radius: 4px;
  display: grid;
  place-items: center;
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 12px;
}

.drawer-header strong {
  display: block;
  font-size: 18px;
}

.drawer-header small {
  display: block;
  color: #777;
  margin-top: 6px;
}

.drawer-link {
  display: flex;
  width: 100%;
  padding: 15px 22px;
  align-items: center;
  gap: 20px;
  border: 0;
  background: white;
  text-align: left;
  font-size: 16px;
  font-weight: 500;
}

.drawer-link:active {
  background: #f0f0f0;
}

.drawer-link span {
  width: 26px;
  text-align: center;
  font-size: 21px;
}

/* FORMS AND ABOUT */

.form-card {
  padding: 16px;
}

.form-card label {
  display: block;
  margin: 15px 0 6px;
  font-weight: bold;
}

.form-card input,
.form-card select {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background: white;
}

.primary-btn {
  background: var(--blue);
  color: white;
  border: 0;
  padding: 13px 16px;
  border-radius: 4px;
  width: 100%;
  margin-top: 18px;
  font-weight: bold;
}

.secondary-btn {
  background: white;
  color: var(--blue);
  border: 1px solid var(--blue);
  padding: 10px 14px;
  border-radius: 4px;
}

.card {
  margin: 14px;
  padding: 17px;
  border: 1px solid var(--line);
  border-radius: 5px;
  line-height: 1.6;
}

.muted {
  color: var(--muted);
}

.empty {
  text-align: center;
  color: #888;
  padding: 35px 15px;
}

.notice {
  background: #fff8e1;
  border-left: 4px solid #e5a000;
  padding: 12px;
  font-size: 13px;
  line-height: 1.5;
}

@media (max-width: 360px) {
  .topbar { gap: 12px; }
  .quote-price { font-size: 16px; gap: 7px; }
  .summary-row { font-size: 13px; }
}
</style>
</head>

<body>

<header class="topbar">
  <button class="hamburger" onclick="openDrawer()">☰</button>
  <div class="top-title" id="topTitle">Quotes</div>
  <button class="icon-btn" id="headerAction"
          onclick="headerAction()">＋</button>
</header>

<!-- QUOTES -->

<section id="quotesPage" class="page active">
  <div id="quotesList"></div>
</section>

<!-- CHARTS -->

<section id="chartsPage" class="page">

  <div class="trade-controls">
    <button class="sell-btn" onclick="openOrder('SELL')">
      SELL<br><strong id="sellPrice">--</strong>
    </button>

    <div class="lot-control">
      <button onclick="adjustLot(-0.01)">−</button>
      <input id="chartLot" type="number"
             min="0.01" max="100" step="0.01" value="0.01">
      <button onclick="adjustLot(0.01)">＋</button>
    </div>

    <button class="buy-btn" onclick="openOrder('BUY')">
      BUY<br><strong id="buyPrice">--</strong>
    </button>
  </div>

  <div class="chart-info">
    <select id="chartSymbol" onchange="loadChart()">
      <option value="OANDA:XAUUSD">XAUUSD · Gold</option>
      <option value="OANDA:EURUSD">EURUSD · Euro vs US Dollar</option>
    </select>

    <select id="chartInterval" onchange="loadChart()">
      <option value="15">M15</option>
      <option value="30">M30</option>
      <option value="60">H1</option>
      <option value="240">H4</option>
      <option value="D">D1</option>
      <option value="W">W1</option>
    </select>
  </div>

  <div class="tv-container">
    <div id="tradingview_chart"></div>
  </div>

  <div class="card">
    <strong>Trading controls</strong>
    <p class="muted">
      Orders opened here are simulated locally. The TradingView chart
      is a separate market-data display and does not execute trades.
    </p>
    <button class="secondary-btn"
            onclick="showPage('trade')">View positions</button>
  </div>
</section>

<!-- TRADE -->

<section id="tradePage" class="page">

  <div class="account-summary">
    <div class="account-heading" id="floatingTotal">0.00 USD</div>

    <div class="summary-row">
      <span>Balance:</span><span id="balance">10,000.00</span>
    </div>

    <div class="summary-row">
      <span>Equity:</span><span id="equity">10,000.00</span>
    </div>

    <div class="summary-row">
      <span>Margin:</span><span id="margin">0.00</span>
    </div>

    <div class="summary-row">
      <span>Free margin:</span><span id="freeMargin">10,000.00</span>
    </div>

    <div class="summary-row">
      <span>Margin Level (%):</span><span id="marginLevel">—</span>
    </div>

    <div style="margin-top:14px">
      <button class="secondary-btn"
              onclick="showPage('charts')">＋ New order</button>
    </div>
  </div>

  <div class="section-heading">
    Positions <span style="float:right" id="positionCount">0</span>
  </div>

  <div id="positionsList">
    <div class="empty">No open positions</div>
  </div>
</section>

<!-- HISTORY -->

<section id="historyPage" class="page">

  <div class="history-summary">
    <div class="summary-row">
      <span>Profit:</span><span id="historyProfit">0.00</span>
    </div>
    <div class="summary-row">
      <span>Deposits:</span><span id="deposits">10,000.00</span>
    </div>
    <div class="summary-row">
      <span>Balance:</span><span id="historyBalance">10,000.00</span>
    </div>
  </div>

  <div class="section-heading">Closed trades and transactions</div>
  <div id="historyList">
    <div class="empty">No closed trades yet</div>
  </div>
</section>

<!-- MESSAGES -->

<section id="messagesPage" class="page">
  <div class="card">
    <h3>Messages</h3>
    <p class="muted">
      There are no broker messages because this application
      does not connect to a broker.
    </p>
  </div>
</section>

<!-- SETTINGS -->

<section id="settingsPage" class="page">
  <div class="card">
    <h3>Settings</h3>

    <label for="startingBalance">Starting balance (USD)</label>
    <input id="startingBalance" type="number"
           min="1" value="10000"
           style="width:100%;padding:12px">

    <label for="leverage">Simulated leverage</label>
    <select id="leverage" style="width:100%;padding:12px">
      <option value="50">1:50</option>
      <option value="100" selected>1:100</option>
      <option value="200">1:200</option>
      <option value="500">1:500</option>
    </select>

    <button class="primary-btn" onclick="saveSettings()">
      Save settings
    </button>

    <p class="muted">
      Changing the starting balance resets the simulated account.
      Open positions will be closed first.
    </p>

    <button class="secondary-btn" onclick="resetAccount()">
      Reset simulated account
    </button>
  </div>
</section>

<!-- ABOUT -->

<section id="aboutPage" class="page">

  <div class="card">
    <h2>About</h2>
    <p><strong>Trading Terminal</strong></p>
    <p>Version 1.0 · Educational trading simulator</p>

    <div class="notice">
      <strong>Disclaimer</strong><br><br>
      This application is an independent educational trading simulator.
      Account balances, account labels, orders, positions, margin,
      equity, profit and loss, and trade history are simulated locally
      using JavaScript.
      <br><br>
      No broker is connected. No real orders are sent, and no real
      deposits, withdrawals, or financial transactions are performed.
      Displaying a balance in USD does not mean the funds are real.
      <br><br>
      Charts are provided by TradingView when an internet connection
      is available. Chart prices may differ from prices used by a
      broker or from the simulated prices used in this application.
      <br><br>
      This project is not an official MetaTrader 5 or MetaQuotes
      application and is not affiliated with, endorsed by, or sponsored
      by MetaQuotes Ltd. or any broker. Product names and trademarks
      belong to their respective owners.
      <br><br>
      This application is for learning and testing only. Do not use
      its simulated results as evidence of real trading performance.
    </div>

    <h3>Account information</h3>
    <p>Account type: Live-style interface</p>
    <p>Execution: Local simulation only</p>
    <p>Broker connection: None</p>
    <p>Storage: Browser local storage</p>
  </div>
</section>

<!-- OTHER MENU PAGES -->

<section id="newsPage" class="page">
  <div class="card">
    <h3>News</h3>
    <p class="muted">No broker news feed is connected.</p>
  </div>
</section>

<section id="mailboxPage" class="page">
  <div class="card">
    <h3>Mailbox</h3>
    <p class="muted">No broker mailbox is connected.</p>
  </div>
</section>

<section id="journalPage" class="page">
  <div class="card">
    <h3>Journal</h3>
    <div id="journalList"></div>
  </div>
</section>

<section id="calendarPage" class="page">
  <div class="card">
    <h3>Economic calendar</h3>
    <p class="muted">
      An economic calendar requires a supported external data source.
    </p>
  </div>
</section>

<section id="communityPage" class="page">
  <div class="card">
    <h3>Traders Community</h3>
    <p class="muted">
      Community features require an external service.
    </p>
  </div>
</section>

<section id="guidePage" class="page">
  <div class="card">
    <h3>User guide</h3>
    <p>1. Choose XAUUSD or EURUSD.</p>
    <p>2. Select the chart timeframe.</p>
    <p>3. Set your simulated lot size.</p>
    <p>4. Tap Buy or Sell to open a simulated position.</p>
    <p>5. Visit Trade to monitor positions and close trades.</p>
    <p>6. Visit History to review closed trades.</p>
  </div>
</section>

<!-- BOTTOM NAVIGATION -->

<nav class="bottom-nav">
  <button class="nav-item active" data-page="quotes"
          onclick="showPage('quotes')">
    <span class="nav-icon">↕</span>Quotes
  </button>

  <button class="nav-item" data-page="charts"
          onclick="showPage('charts')">
    <span class="nav-icon">▥</span>Charts
  </button>

  <button class="nav-item" data-page="trade"
          onclick="showPage('trade')">
    <span class="nav-icon">⌁</span>Trade
  </button>

  <button class="nav-item" data-page="history"
          onclick="showPage('history')">
    <span class="nav-icon">◷</span>History
  </button>

  <button class="nav-item" data-page="messages"
          onclick="showPage('messages')">
    <span class="nav-icon">▢</span>Messages
  </button>
</nav>

<!-- SIDE DRAWER -->

<div class="overlay" id="overlay" onclick="closeDrawer(event)">
  <aside class="drawer" onclick="event.stopPropagation()">

    <div class="drawer-header">
      <div class="avatar">TT</div>
      <strong>Trading Terminal</strong>
      <small>Local simulated account</small>
      <p><a href="#" onclick="goMenu('settings');return false">
        Manage account settings
      </a></p>
    </div>

    <button class="drawer-link" onclick="goMenu('trade')">
      <span>⌁</span> Trade
    </button>

    <button class="drawer-link" onclick="goMenu('news')">
      <span>▤</span> News
    </button>

    <button class="drawer-link" onclick="goMenu('mailbox')">
      <span>✉</span> Mailbox
    </button>

    <button class="drawer-link" onclick="goMenu('journal')">
      <span>▦</span> Journal
    </button>

    <button class="drawer-link" onclick="goMenu('settings')">
      <span>
