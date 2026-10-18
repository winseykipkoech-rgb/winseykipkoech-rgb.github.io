<!doctype html>





Trading Flow AI — Gold Signals

<style>
:root {
  --bg: #08131f;
  --card: #112333;
  --line: #294052;
  --text: #edf4fb;
  --muted: #9aabba;
  --gold: #f5bd4f;
  --green: #39d5a0;
  --red: #ff7880;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font: 15px/1.5 Arial, sans-serif;
}
.wrap { max-width: 1120px; margin: auto; padding: 22px; }
.top, .row, .head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}
.top { margin-bottom: 18px; }
.brand { font-weight: 850; letter-spacing: 1px; }
.brand span, .gold { color: var(--gold); }
.badge, .tag {
  border: 1px solid #80652f;
  color: #f6d99b;
  background: #2b261c;
  border-radius: 8px;
  padding: 7px 10px;
  font-size: 11px;
}
.eyebrow {
  font-size: 10px;
  letter-spacing: 2px;
  color: var(--gold);
  text-transform: uppercase;
}
.muted { color: var(--muted); font-size: 12px; }
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
}
.cols {
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: 12px;
  margin-top: 12px;
}
.card {
  background: linear-gradient(145deg, #14283a, #0f1d2a);
  border: 1px solid var(--line);
  border-radius: 14px;
  padding: 17px;
  min-width: 0;
}
.label { color: var(--muted); font-size: 12px; }
.value { font-size: 26px; font-weight: 800; margin: 7px 0; }
.head { margin-bottom: 14px; }
.head h2 { font-size: 15px; margin: 0; }
.chart { height: 190px; width: 100%; }
.chart svg { width: 100%; height: 100%; }
.signal {
  padding: 14px;
  border: 1px solid #365344;
  border-radius: 11px;
  background: #142f2a;
}
.signal h3 { font-size: 16px; margin: 12px 0 5px; }
.signal p { font-size: 12px; color: #b6c9c4; }
.stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;
  margin-top: 12px;
}
.stats div { border-top: 1px solid #365344; padding-top: 8px; }
.stats small {
  display: block;
  color: #9cb6aa;
  font-size: 10px;
}
.stats strong { font-size: 12px; }
.select, button {
  border: 1px solid var(--line);
  border-radius: 8px;
  padding: 10px;
  background: #182e40;
  color: var(--text);
  font: inherit;
  font-size: 12px;
}
.controls {
  display: flex;
  gap: 9px;
  align-items: center;
  flex-wrap: wrap;
  margin: 13px 0;
}
.primary {
  background: var(--gold);
  color: #17212b;
  border-color: var(--gold);
  font-weight: 700;
  cursor: pointer;
}
.notice {
  margin-top: 14px;
  padding: 11px 13px;
  border-left: 3px solid var(--gold);
  background: #1a222a;
  border-radius: 0 8px 8px 0;
  color: #bbc7d1;
  font-size: 11px;
}
.rows .row { padding: 10px 0; border-bottom: 1px solid #26394a; }
.rows .row:last-child { border: 0; }
.rows b { font-size: 12px; }
.rows small { display: block; color: var(--muted); font-size: 11px; }
table { border-collapse: collapse; width: 100%; font-size: 11px; }
td, th { text-align: left; border-bottom: 1px solid #26394a; padding: 9px 5px; }
th { color: var(--muted); }
.foot { text-align: center; color: #718597; font-size: 10px; margin: 20px 0; }
.good { color: var(--green); }
.bad { color: var(--red); }

@media (max-width: 750px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
  .cols { grid-template-columns: 1fr; }
  .wrap { padding: 13px; }
  .top { align-items: flex-start; }
  .badge { max-width: 145px; }
  .chart { height: 155px; }
}
</style>



<main class="wrap">

<header class="top">
  <div>
    <div class="brand">TRADING <span>FLOW AI</span></div>
    <div class="eyebrow">Gold market dashboard</div>
    <h1 style="font-size:26px;margin:5px 0">XAU/USD signals</h1>
    <div class="muted">English · Website-only updates · No Telegram alerts</div>
  </div>
  <div class="badge" id="feed-badge">CONNECTING TO PRICE FEED</div>
</header>

<section class="grid">
  <div class="card">
    <div class="label">Gold spot price</div>
    <div class="value" id="price">Loading…</div>
    <div class="muted" id="price-status">Connecting to public API</div>
  </div>
  <div class="card">
    <div class="label">Current indicator</div>
    <div class="value" id="direction">WAIT</div>
    <div class="muted" id="signal-time">Collecting price snapshots</div>
  </div>
  <div class="card">
    <div class="label">Timeframes</div>
    <div class="value">15m+</div>
    <div class="muted">15m · 25m · 30m · 1H · 4H</div>
  </div>
  <div class="card">
    <div class="label">Signal engine</div>
    <div class="value" style="font-size:20px" id="feed-status">Connecting…</div>
    <div class="muted">Browser-side analysis</div>
  </div>
</section>

<section class="cols">
  <article class="card">
    <div class="head">
      <div>
        <h2>Spot-price snapshots</h2>
        <div class="muted">Collected while this page is open</div>
      </div>
      <span class="tag">XAU/USD</span>
    </div>
    <div class="row">
      <strong id="chart-price">$—</strong>
      <span id="chart-change" class="muted">Waiting for samples</span>
    </div>
    <div class="chart">
      <svg id="chart" viewbox="0 0 700 220" preserveaspectratio="none">
        <text x="350" y="110" fill="#9aabba" text-anchor="middle">Collecting price snapshots…</text>
      </svg>
    </div>
    <div class="notice">
      This is an indicative spot-price feed, not necessarily a broker's executable XAU/USD quote. The chart uses browser snapshots, not historical exchange candles.
    </div>
  </article>

  <article class="card">
    <div class="head">
      <div>
        <h2>Latest signal indicator</h2>
        <div class="muted">Basic price-momentum rules, not AI</div>
      </div>
      <span class="tag">Indicative</span>
    </div>

    <div class="signal">
      <div class="row">
        <strong id="signal-badge">WAIT · COLLECTING DATA</strong>
        <span class="muted" id="tf-label">Multiple timeframes</span>
      </div>
      <h3 id="setup">Not enough local price history</h3>
      <p id="reason">Keep the page open to collect snapshots. A timeframe cannot be analysed until enough time has passed.</p>
      <div class="stats">
        <div>
          <small>Latest entry reference</small>
          <strong id="entry">—</strong>
        </div>
        <div>
          <small>Stop-loss</small>
          <strong>Not calculated</strong>
        </div>
        <div>
          <small>Take-profit</small>
          <strong>Not calculated</strong>
        </div>
      </div>
    </div>

    <div class="controls">
      <label for="tf" class="muted">Analyse:</label>
      <select class="select" id="tf">
        <option value="multi" />Multiple timeframes
        <option value="15" />15 minutes
        <option value="25" />25 minutes
        <option value="30" />30 minutes
        <option value="60" />1 hour
        <option value="240" />4 hours
      </select>
      <button class="primary" id="refresh">Refresh price</button>
    </div>

    <div class="muted">
      The browser polls around once per minute. Initial timeframe analysis needs older snapshots first.
    </div>
  </article>
</section>

<section class="cols">
  <article class="card">
    <div class="head">
      <h2>Signal history</h2>
      <span class="tag">This browser only</span>
    </div>
    <table>
      <thead>
        <tr><th>Time</th><th>Timeframe</th><th>Indicator</th></tr>
      </thead>
      <tbody id="history">
        <tr><td colspan="3">No indicator changes recorded yet.</td></tr>
      </tbody>
    </table>
    <div class="muted" style="margin-top:10px">
      History is stored in this browser only, not shared with other members or devices.
    </div>
  </article>

  <article class="card">
    <div class="head"><h2>What this version can do</h2></div>
    <div class="rows">
      <div class="row">
        <div>
          <b>Public spot-price API</b>
          <small>Fetched directly in the browser without an API key.</small>
        </div>
        <span class="tag">Attempting</span>
      </div>
      <div class="row">
        <div>
          <b>Multi-timeframe snapshots</b>
          <small>15m, 25m, 30m, 1H and 4H if the page stays open.</small>
        </div>
        <span class="tag">Local</span>
      </div>
      <div class="row">
        <div>
          <b>Shared live signals</b>
          <small>Requires a hosted backend/database for all members.</small>
        </div>
        <span class="tag">Not included</span>
      </div>
    </div>
    <div class="notice">
      No backend is needed to try this single-file demo. Signals are simple snapshot-momentum indicators, not validated trading advice. Do not trade real money based on them. Public API availability and freshness can change.
    </div>
  </article>
</section>

<div class="foot">
  Trading Flow AI · Browser-side prototype · Not financial advice · No trading performance is guaranteed.
</div>
</main>

<script>
(() => {
  const $ = id => document.getElementById(id);
  const key = 'tfai_samples_v1';
  const hkey = 'tfai_history_v1';

  let samples = [];
  try {
    samples = JSON.parse(localStorage.getItem(key) || '[]');
  } catch (e) {}

  samples = samples.filter(s =>
    s.t > Date.now() - 8 * 86400000 && Number.isFinite(s.p)
  );

  const money = n => '$' + n.toLocaleString('en-US', {
    minimumFractionDigits: 2,
    maximumFractionDigits: 2
  });

  function chart() {
    const svg = $('chart');
    const a = samples.slice(-100).map(s => s.p);

    if (a.length < 2) {
      svg.innerHTML =
        '<text x="350" y="110" fill="#9aabba" text-anchor="middle">Collecting price snapshots…</text>';
      return;
    }

    const lo = Math.min(...a);
    const hi = Math.max(...a);
    const r = hi - lo || 1;
    const pts = a.map((p, i) =>
      (700 * i / (a.length - 1)).toFixed(1) + ',' +
      (195 - (p - lo) / r * 170).toFixed(1)
    ).join(' ');

    svg.innerHTML =
      '<g stroke="#294052" stroke-dasharray="4 5">' +
      '<path d="M0 25H700M0 67H700M0 109H700M0 151H700M0 193H700"/>' +
      '</g><polyline points="' + pts +
      '" fill="none" stroke="#f5bd4f" stroke-width="3" stroke-linejoin="round" stroke-linecap="round"/>';
  }

  function history(dir) {
    let arr = [];
    try {
      arr = JSON.parse(localStorage.getItem(hkey) || '[]');
    } catch (e) {}

    if (!arr.length || arr[0].d !== dir) {
      arr.unshift({
        t: Date.now(),
        d: dir,
        tf: $('tf').value
      });
      localStorage.setItem(hkey, JSON.stringify(arr.slice(0, 20)));
    }

    $('history').innerHTML = arr.slice(0, 10).map(x =>
      '<tr><td>' + new Date(x.t).toLocaleString() +
      '</td><td>' + (x.tf === 'multi' ? 'Multi' : x.tf + 'm') +
      '</td><td>' + x.d + '</td></tr>'
    ).join('');
  }

  function analyse() {
    const tf = $('tf').value;
    const periods = tf === 'multi'
      ? [15, 25, 30, 60, 240]
      : [Number(tf)];

    const moves = [];
    const now = Date.now();
    const latest = samples[samples.length - 1];

    for (const m of periods) {
      const old = samples.filter(s => s.t <= now - m * 60000).pop();
      if (old && latest) {
        moves.push({
          m,
          change: (latest.p - old.p) / old.p * 100
        });
      }
    }

    const need = tf === 'multi' ? 3 : 1;
    let dir = 'WAIT';
    let title = 'Not enough local price history';
    let reason = 'Keep this page open until older snapshots exist for the selected timeframe.';

    if (moves.length >= need) {
      const up = moves.filter(x => x.change > .03).length;
      const down = moves.filter(x => x.change < -.03).length;

      dir = up >= need && up > down
        ? 'BUY'
        : down >= need && down > up
          ? 'SELL'
          : 'NO TRADE';

      title = dir === 'BUY'
        ? 'Indicative upward momentum'
        : dir === 'SELL'
          ? 'Indicative downward momentum'
          : 'Timeframes do not agree';

      reason = moves.map(x =>
        x.m + 'm ' + (x.change >= 0 ? '+' : '') +
        x.change.toFixed(3) + '%'
      ).join(' · ') +
      ' — simple spot snapshots, not broker candles or a tested strategy.';
    }

    $('direction').textContent = dir;
    $('signal-badge').textContent = dir + ' · INDICATIVE';
    $('signal-badge').className =
      dir === 'BUY' ? 'good' : dir === 'SELL' ? 'bad' : '';
    $('setup').textContent = title;
    $('reason').textContent = reason;
    $('entry').textContent = latest ? money(latest.p) : '—';
    $('signal-time').textContent = 'Samples saved locally: ' + samples.length;
    $('tf-label').textContent = tf === 'multi'
      ? '15m + 25m + 30m + 1H + 4H'
      : tf + ' minute(s)';

    if (dir !== 'WAIT') history(dir);
  }

  async function update() {
    try {
      $('price-status').textContent = 'Requesting spot price…';

      const r = await fetch(
        'https://api.gold-api.com/price/XAU',
        { cache: 'no-store' }
      );

      if (!r.ok) throw Error('HTTP ' + r.status);

      const d = await r.json();
      const p = Number(d.price);

      if (!Number.isFinite(p) || p <= 0) {
        throw Error('No valid price returned');
      }

      const now = Date.now();

      if (!samples.length || now - samples[samples.length - 1].t >= 50000) {
        samples.push({ t: now, p });
      }

      samples = samples
        .filter(s => s.t > now - 8 * 86400000)
        .slice(-12000);

      localStorage.setItem(key, JSON.stringify(samples));

      $('price').textContent = money(p);
      $('chart-price').textContent = money(p);
      $('price-status').textContent =
        'Spot API · ' +
        (d.updatedAt ? new Date(d.updatedAt).toLocaleTimeString() : 'time not supplied');

      $('feed-badge').textContent = 'PRICE API CONNECTED';
      $('feed-status').textContent = 'Price connected';
      $('feed-status').className = 'value good';

      $('chart-change').textContent = samples.length > 1
        ? ((p - samples[samples.length - 2].p >= 0 ? '+' : '') +
           (p - samples[samples.length - 2].p).toFixed(2) +
           ' since previous sample')
        : 'Waiting for next sample';

      chart();
      analyse();

    } catch (e) {
      $('price-status').textContent = 'Price API unavailable: ' + e.message;
      $('feed-badge').textContent = 'PRICE FEED UNAVAILABLE';
      $('feed-status').textContent = 'Unavailable';
      $('feed-status').className = 'value bad';
    }
  }

  $('refresh').addEventListener('click', update);
  $('tf').addEventListener('change', analyse);

  chart();
  analyse();
  update();
  setInterval(update, 60000);
})();
</script>

</!doctype>
