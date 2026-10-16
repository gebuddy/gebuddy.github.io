# ⚔️ G.E. Buddy

**A lightweight, fast, and privacy-focused Old School RuneScape (OSRS) Grand Exchange merchanting and alchemy calculator.**

🔗 **Live Demo:** [gebuddy.github.io](https://gebuddy.github.io)

G.E. Buddy is a single-file, zero-dependency web application designed to help OSRS players find profitable merchanting flips and high-alchemy items. It fetches real-time data directly from the OSRS Wiki Price API, calculates accurate profits (including GE tax exemptions), and provides a seamless, responsive experience on both desktop and mobile devices.

---

## ✨ Features

- 📊 **Dual Modes:** Dedicated tabs for **Merch / Flip** (margin & ROI) and **Alch Items** (High Alchemy profit).
- 💰 **Accurate Calculations:** Automatically factors in the 2% Grand Exchange tax, including exemptions for utility items (e.g., *Chisel, Gardening trowel, Secateurs*).
- 📱 **Fully Responsive:** Adaptive UI featuring a clean card-based list for mobile devices and a detailed, sortable data table for desktop.
- 🌓 **Dark & Light Themes:** Easy on the eyes, with a system-aware theme toggle.
- ⭐ **Watchlist & Hiding:** Star items to track them closely or hide items you never want to see again.
- ⚙️ **Advanced Filtering:** Filter by F2P/P2P, minimum profit, minimum ROI, minimum volume, trade limit, and data age.
- 💾 **Custom Presets:** Save and load your favorite filter configurations instantly.
- 🔗 **Device Sync (No Account Needed):** Export and import your settings, watchlist, and hidden items using a compact, compressed "Settings Code". No server or database required.
- ⚡ **Performance:** Caches item mappings for 24 hours to ensure lightning-fast load times and minimize API strain. Auto-refresh capabilities with configurable intervals.

---

## 🚀 How to Use

1. **Browse:** Select either the "Merch / Flip" or "Alch Items" tab.
2. **Filter:** Use the search bar, F2P toggle, or open the "Filters" panel to set minimum profit, ROI, or volume thresholds.
3. **Sort:** Click the sort dropdown (or column headers on desktop) to rank items by Profit, ROI, Volume, or Potential Profit.
4. **Interact:** Tap or click on any item to open a detail sheet. From here, you can:
   - View full price history on the OSRS Wiki.
   - Open the official RuneScape Wiki page.
   - Copy the item name to your clipboard.
   - Add to your Watchlist or Hide the item.
5. **Sync:** Click the ⚙️ (Settings) icon to generate a **Settings Code**. Copy this code and paste it into G.E. Buddy on another device to instantly restore your preferences.

---

## 🛠️ Local Development

Because this project uses the `fetch` API to retrieve data from the OSRS Wiki, modern browser security (CORS) will block it if opened directly as a `file://` URL. You must serve it via a local HTTP server.

**Option 1: Python (Recommended)**
```bash
# Navigate to the project directory
cd gebuddy.github.io

# Python 3
python -m http.server 8000
```
Then open `http://localhost:8000` in your browser.

**Option 2: VS Code**
1. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension.
2. Right-click `index.html` and select "Open with Live Server".

**Option 3: Node.js**
```bash
npx serve .
```

---

## 🏗️ Technical Architecture

G.E. Buddy is intentionally built to be as simple and portable as possible:
- **Zero Dependencies:** No React, Vue, jQuery, or build tools (Webpack/Vite). Just pure, modern Vanilla JavaScript (ES6+).
- **Single File:** All HTML, CSS, and JavaScript (including embedded base64 SVG/WebP assets) reside in a single `index.html` file for effortless deployment.
- **Styling:** Modern CSS using Custom Properties (Variables), CSS Grid, Flexbox, and `color-mix()` for glassmorphism effects.
- **Data Source:** [OSRS Wiki Price API](https://prices.runescape.wiki/) (Unofficial, but the community standard).
- **Storage:** Uses `localStorage` for caching and saving user preferences locally.

---

## 🛡️ Privacy

G.E. Buddy is **100% client-side**. 
- No analytics, trackers, or cookies are used.
- No data is ever sent to a backend server.
- Your watchlist and hidden items stay on your device unless you explicitly choose to export them via the Settings Code.

---

## ⚠️ Disclaimer

*G.E. Buddy is a fan-made project and is **not** affiliated with, endorsed by, or connected to Jagex Ltd. in any way. "Old School RuneScape" and "RuneScape" are registered trademarks of Jagex Ltd. All item data and icons are sourced from the [OSRS Wiki](https://oldschool.runescape.wiki/) under their respective licenses.*

---

## 🤝 Contributing

Found a bug or have a feature request? Feel free to open an [Issue](https://github.com/gebuddy/gebuddy.github.io/issues) or submit a [Pull Request](https://github.com/gebuddy/gebuddy.github.io/pulls). Since it's a single file, making quick tweaks and testing them is incredibly straightforward!

---

## 📜 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 📄 Source Code (`index.html`)

Save the following code as `index.html` in your repository.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#141517">
<title>G.E. Buddy</title>
<style>
/* ============ theme tokens ============ */
:root {
  --bg: #f1f0ec;
  --panel: #fff;
  --line: #d9d6cd;
  --fg: #1d1c19;
  --dim: #7a766b;
  --acc: #9a6b00;
  --accfg: #fff;
  --good: #0a6b2e;
  --bad: #c42b2b;
  --warn: #a85d00;
  --sel: #e9e6dc;
  --c-rune: #007777;
  --c-mithril: #0000cc;
  --c-adamant: #006600;
  --c-gilded: #b8860b;
  --c-ring: #cc6600;
  --c-necklace: #cc6600;
}
:root[data-theme=dark] {
  --bg: #141517;
  --panel: #1d1f23;
  --line: #2f3238;
  --fg: #e8e6df;
  --dim: #8b8e96;
  --acc: #e0b13c;
  --accfg: #1a1400;
  --good: #6fcf8f;
  --bad: #ff6b6b;
  --warn: #e5c07b;
  --sel: #272a30;
  --c-rune: #4ec9b0;
  --c-mithril: #569cd6;
  --c-adamant: #6a9955;
  --c-gilded: #dcdcaa;
  --c-ring: #ce9178;
  --c-necklace: #ce9178;
}

/* ============ base ============ */
* { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
[hidden] { display: none !important; }
html, body {
  margin: 0;
  background: var(--bg);
  color: var(--fg);
  font: 15px/1.35 system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
}
body {
  padding: env(safe-area-inset-top, 0) env(safe-area-inset-right, 0)
           env(safe-area-inset-bottom, 0) env(safe-area-inset-left, 0);
  max-width: 720px;
  margin: 0 auto;
}

/* ============ header ============ */
/* The header artwork is a data URI injected by JS via --hdrimg (see EMBEDDED ASSETS). */
header {
  flex-wrap: wrap;
  position: sticky;
  top: 0;
  z-index: 5;
  display: flex;
  gap: 6px;
  padding: 8px 10px;
  border-bottom: 2px solid var(--acc);
  align-items: center;
  background-image: linear-gradient(rgba(12,12,14,.50), rgba(12,12,14,.32)), var(--hdrimg);
  background-position: 50% 45%;
  background-size: cover;
  background-color: #1d1f23;
  box-shadow: 0 4px 14px rgba(0,0,0,.35);
}
.brand { order: -1; flex: 0 0 100%; display: flex; justify-content: center; }
.brand img {
  height: 58px;
  width: auto;
  max-width: 100%;
  display: block;
  filter: drop-shadow(0 2px 6px rgba(0,0,0,.55));
}
.tabs {
  display: flex;
  flex: 1;
  background: color-mix(in srgb, var(--panel) 84%, transparent);
  -webkit-backdrop-filter: blur(6px);
  backdrop-filter: blur(6px);
  border: 1px solid var(--line);
  border-radius: 10px;
  padding: 3px;
  gap: 3px;
}
.tabs button {
  flex: 1;
  border: 0;
  background: none;
  color: var(--dim);
  font: inherit;
  font-weight: 600;
  padding: 8px;
  border-radius: 7px;
}
.tabs button.on { background: var(--acc); color: var(--accfg); }
.ib {
  border: 1px solid var(--line);
  background: color-mix(in srgb, var(--panel) 84%, transparent);
  -webkit-backdrop-filter: blur(6px);
  backdrop-filter: blur(6px);
  color: var(--fg);
  border-radius: 10px;
  width: 42px;
  height: 42px;
  font-size: 16px;
}
header #theme { margin-left: auto; }

/* ============ controls ============ */
#ctl { padding: 10px; display: grid; gap: 8px; }
.row { display: flex; gap: 6px; flex-wrap: wrap; align-items: center; }
.in, select, .b {
  font: inherit;
  color: var(--fg);
  background: var(--panel);
  border: 1px solid var(--line);
  border-radius: 9px;
  padding: 9px 11px;
  min-height: 40px;
}
.in { width: 100%; }
.in.sm { width: 64px; padding: 9px 8px; }
.in.bad { border-color: var(--bad); }
select { max-width: 46vw; }
.b { font-weight: 600; }
.b.pri { background: var(--acc); color: var(--accfg); border-color: var(--acc); margin-left: auto; }
.b:disabled { opacity: .5; }
.sw { display: flex; gap: 7px; align-items: center; min-height: 40px; }
.sw input { width: 20px; height: 20px; accent-color: var(--acc); }
.dim { color: var(--dim); }
#adv {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  background: var(--panel);
  border: 1px solid var(--line);
  border-radius: 12px;
  padding: 10px;
}
#adv label { display: grid; gap: 3px; font-size: 13px; color: var(--dim); }
#adv .full { grid-column: 1/-1; }

/* ============ status line ============ */
#st { padding: 2px 12px 6px; font-size: 13px; display: grid; gap: 2px; }
#st .bad { color: var(--bad); }
#st .warn { color: var(--warn); }
#st .info { color: var(--acc); }

/* ============ mobile card list ============ */
#list { list-style: none; margin: 0; padding: 0 10px; display: grid; gap: 7px; transition: opacity .15s; }
#list.dim { opacity: .45; }
.card { background: var(--panel); border: 1px solid var(--line); border-radius: 12px; padding: 10px 12px; cursor: pointer; }
.card:active { background: var(--sel); }
.top { display: flex; gap: 11px; align-items: center; }
.mid { flex: 1; min-width: 0; display: grid; gap: 3px; }
.mid .nm { display: block; }
.meta {
  display: flex;
  flex-wrap: wrap;
  gap: 2px 12px;
  font-size: 13px;
  font-variant-numeric: tabular-nums;
  align-items: center;
}
.meta i, .gr i { font-style: normal; color: var(--dim); font-size: 12px; }
.meta .up { color: var(--good); }
.meta .dn { color: var(--bad); }
.pill { border: 1px solid var(--line); border-radius: 6px; padding: 0 5px; font-size: 11px; color: var(--dim); }
.rt { text-align: right; display: grid; gap: 2px; flex: none; }
.roi { font-size: 12px; color: var(--dim); font-variant-numeric: tabular-nums; }
.card.neg .roi { color: var(--bad); }
.nm { font-weight: 650; overflow-wrap: anywhere; display: flex; align-items: center; gap: 9px; min-width: 0; }
.pf { font-size: 17px; font-weight: 700; font-variant-numeric: tabular-nums; white-space: nowrap; color: var(--good); }
.card.neg .pf, .card.neg .nm { color: var(--bad); }
.card.old .nm { color: var(--dim); }
.n-rune { color: var(--c-rune); }
.n-mithril { color: var(--c-mithril); }
.n-adamant { color: var(--c-adamant); }
.n-gilded { color: var(--c-gilded); }
.n-ring { color: var(--c-ring); }
.n-necklace { color: var(--c-necklace); }
.gr {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(88px, 1fr));
  gap: 6px 10px;
  margin-top: 9px;
  padding-top: 9px;
  border-top: 1px solid var(--line);
}
.gr span { display: grid; font-variant-numeric: tabular-nums; font-size: 14px; }
.sk {
  height: 78px;
  border-radius: 12px;
  background: linear-gradient(90deg, var(--panel), var(--sel), var(--panel));
  background-size: 200% 100%;
  animation: sh 1.2s linear infinite;
}
@keyframes sh { to { background-position: -200% 0; } }
@media (prefers-reduced-motion: reduce) { .sk { animation: none; } }

/* ============ pagination ============ */
#pg { display: flex; gap: 8px; align-items: center; justify-content: space-between; padding: 12px 10px 28px; }
#pg .in { width: 64px; }

/* ============ bottom sheet / dialog ============ */
#ov { position: fixed; inset: 0; background: #0008; z-index: 20; display: flex; align-items: flex-end; justify-content: center; }
#sh {
  background: var(--panel);
  width: 100%;
  max-width: 720px;
  max-height: 82vh;
  overflow: auto;
  border-radius: 16px 16px 0 0;
  padding: 16px 16px calc(18px + env(safe-area-inset-bottom, 0));
  display: grid;
  gap: 8px;
}
#sh h3 { margin: 0 0 4px; font-size: 17px; overflow-wrap: anywhere; }
.kv {
  display: flex;
  justify-content: space-between;
  padding: 6px 0;
  border-bottom: 1px solid var(--line);
  font-variant-numeric: tabular-nums;
}
.kv span:first-child { color: var(--dim); }
.act { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 6px; }
.act .b, .act a { text-align: center; text-decoration: none; color: var(--fg); display: flex; align-items: center; justify-content: center; }
.chk { display: flex; gap: 10px; align-items: center; padding: 8px 0; border-bottom: 1px solid var(--line); }
.chk input { width: 20px; height: 20px; accent-color: var(--acc); }
#sh .code {
  font: 700 30px/1 ui-monospace, Menlo, Consolas, monospace;
  letter-spacing: .3em;
  text-align: center;
  padding: 16px 0 16px .3em;
  background: var(--bg);
  border: 1px solid var(--line);
  border-radius: 10px;
  color: var(--acc);
  user-select: all;
}
#sh .err { color: var(--bad); font-size: 14px; }
#sh .sec { display: grid; gap: 8px; padding: 10px 0; border-bottom: 1px solid var(--line); }
#sh p { margin: 0; font-size: 14px; }

/* ============ desktop table ============ */
#tbl { padding: 0 10px; }
#tbl.dim { opacity: .45; }
table { width: 100%; border-collapse: separate; border-spacing: 0; font-variant-numeric: tabular-nums; font-size: 14px; }
th {
  position: sticky;
  top: 59px;
  z-index: 2;
  background: var(--bg);
  text-align: right;
  font-weight: 600;
  color: var(--dim);
  padding: 9px 10px;
  border-bottom: 1px solid var(--line);
  cursor: pointer;
  white-space: nowrap;
  user-select: none;
}
th:hover { color: var(--fg); }
th.on { color: var(--acc); }
th.l { text-align: left; cursor: default; }
td { padding: 5px 10px; border-bottom: 1px solid var(--line); text-align: right; white-space: nowrap; }
td.l { text-align: left; white-space: normal; }
tbody tr { cursor: pointer; }
tbody tr:nth-child(odd) { background: var(--panel); }
tbody tr:hover { background: var(--sel); }
tr.neg td { color: var(--bad); }
tr.old .nm { color: var(--dim); }
td.pos { color: var(--good); font-weight: 650; }
td.up { color: var(--good); }
td.dn { color: var(--bad); }
.ic { width: 40px; height: 40px; object-fit: contain; flex: none; image-rendering: pixelated; }
.ic.big { width: 44px; height: 44px; }
.ic.sm { width: 28px; height: 28px; }

/* ============ toast ============ */
#toast {
  position: fixed;
  left: 50%;
  bottom: calc(24px + env(safe-area-inset-bottom, 0));
  transform: translateX(-50%);
  background: var(--fg);
  color: var(--bg);
  padding: 9px 16px;
  border-radius: 20px;
  z-index: 30;
  font-size: 14px;
}

/* ============ wide layout (>=900px) ============ */
@media (min-width: 900px) {
  body { max-width: 1500px; }
  header { padding: 10px 16px; flex-wrap: nowrap; background-position: 50% 14%; }
  .tabs { flex: none; width: 340px; order: 0; }
  .brand { order: 1; flex: 1 1 auto; justify-content: center; padding-left: 12%; }
  .brand img { height: 48px; }
  header .ib { order: 2; }
  header #theme { margin-left: 0; }
  th { top: 70px; }
  #ctl { display: flex; flex-wrap: wrap; align-items: center; gap: 8px 14px; padding: 12px 16px; }
  #ctl > .row { display: contents; }
  #ctl > .in { width: 280px; }
  select { max-width: none; }
  #adv { flex-basis: 100%; grid-template-columns: repeat(6, 1fr); }
  #adv .full { grid-column: span 2; }
  #st { padding: 2px 16px 8px; display: flex; flex-wrap: wrap; gap: 2px 22px; }
  #tbl { padding: 0 16px; }
  #pg { padding: 14px 16px 32px; }
  #ov { align-items: center; }
  #sh { border-radius: 16px; max-width: 460px; }
}
</style>
</head>
<body>
<header>
  <div class="brand"><img id="logo" alt="G.E. Buddy"></div>
  <div class="tabs"><button data-t="merch">Merch / Flip</button><button data-t="alch">Alch Items</button></div>
  <button class="ib" id="theme" aria-label="Toggle theme"></button>
  <button class="ib" id="cfgb" aria-label="Save or load settings">⚙</button>
  <button class="ib" id="info" aria-label="Help">?</button>
</header>
<div id="ctl"></div>
<div id="st"></div>
<ul id="list"></ul>
<div id="tbl" hidden></div>
<div id="pg"></div>
<div id="ov" hidden><div id="sh" role="dialog"></div></div>
<div id="toast" hidden></div>

<script>
'use strict';
window.onerror = (m, u, l) => {
  const d = document.createElement('div');
  d.style.cssText = 'padding:10px;color:#f66;font:13px monospace';
  d.textContent = 'Script error: ' + m + ' (line ' + l + ')';
  document.body.prepend(d);
};

/* ---------- tiny helpers ---------- */
const $ = (s, e = document) => e.querySelector(s);
const LS = {
  get(k, d) { try { const v = localStorage.getItem(k); return v ? JSON.parse(v) : d } catch { return d } },
  set(k, v) { try { localStorage.setItem(k, JSON.stringify(v)) } catch {} },
};
const esc = s => String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const fmt = n => Number(n).toLocaleString('en-US');
const SUF = { k: 1e3, m: 1e6, b: 1e9 };
function parseNum(t, suffix = true, float = false) {
  let s = String(t).trim().toLowerCase().replace(/[,_]/g, '');
  let m = 1;
  if (suffix && SUF[s.slice(-1)]) { m = SUF[s.slice(-1)]; s = s.slice(0, -1); }
  const v = Number(s) * m;
  if (!s || !isFinite(v)) throw 0;
  return float ? v : Math.round(v);
}
function fmtAge(ts, now = Date.now() / 1e3) {
  if (!ts) return 'N/A';
  const s = Math.max(0, Math.floor(now - ts));
  return s < 60 ? s + 's ago' : s < 3600 ? Math.floor(s / 60) + 'm ago'
       : s < 86400 ? Math.floor(s / 3600) + 'h ago' : Math.floor(s / 86400) + 'd ago';
}

/* ---------- embedded assets ---------- */
/* The header background and logo are huge base64 data URIs (the bulk of this
   file). They are kept here as constants and wired in below so the CSS and
   markup at the top of the file stay readable. */
const HDR_IMG = 'data:image/webp;base64,UklGRjCEAABXRUJQVlA4ICSEAACw2wKdASroA6wBPqFInkumJCmqJbG8YUAUCWdtJ92Y/FDwhMhTIG2NLqM9R/dya/7x+qXk39dP9r1L2CYiKPEc0JpFU+57i+VUPcgWKg349/Gd6xg89OX9t9LvpPeZDzdvTT/bOmy9YX0UvOp9aH/MY9LMq6c5Xe8X9jta/8N1Thl/kOSjlu+r/2H7P+w7iv2qOzeYp7Q/fv/76eU5L821AvPHwgKCH9O9HrwG/dH73fAx+6W+7kES9H61L2B5JlcXppVDn2UJkUP
