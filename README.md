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
