# 🏃‍♀️ LiveSplit Remote Viewer 🏃‍♂️

> A lightweight, mobile‑friendly web viewer for LiveSplit speedrun timers

![LiveSplit Viewer Screenshot](https://raw.githubusercontent.com/RandomTick/livesplit-viewer/refs/heads/main/assets/screenshot.png)

## ✨ Features

* 📱 View your LiveSplit timer on any device with a web browser
* 🔄 Real‑time updates of split times and comparisons
* 📊 See current and completed splits at a glance
* 🎮 Perfect companion for single‑monitor or couch‑stream setups
* 🌐 No external dependencies — just HTML, CSS, and vanilla JS

---

## 🚀 Quick Start (choose one)

### Option A – "Double‑click & go" *(PC‑only)*

1. **Download** the latest `livesplit‑viewer.zip` from [Releases](https://github.com/RandomTick/livesplit-viewer/releases).
2. **Extract** the zip and **double‑click `index.html`**.
3. In LiveSplit **Right‑click → Control → Start Server** (default port **16834**).
4. Leave the viewer's address box at **`localhost:16834`** (or type your own LAN IP).

> This works because a file opened via `file://` is considered an *insecure* context, so the browser allows a plain WebSocket (`ws://…`).

---

### Option B – "Serve over your LAN" *(PC + phone/tablet)*

If you want to read the timer on a second screen:

1. **Install Python 3** (if you don't have it). It comes pre‑installed on macOS/Linux; Windows users can grab it from [https://python.org](https://python.org).
2. **Clone or download** this repository.
3. In a terminal **`cd` into the folder** that contains `index.html` and run:

   ```bash
   python -m http.server 8080 --bind 0.0.0.0
   ```

   This starts a tiny static server reachable on your LAN at **`http://<your‑PC‑name>:8080`**.
4. *(Windows only)* Allow port 8080 through the firewall the first time:

   ```powershell
   New-NetFirewallRule -DisplayName "LiveSplit Viewer HTTP" `
     -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow
   ```
5. **On your phone/tablet** open a browser to **`http://<your‑PC‑name>:8080`**.
6. Type in the ip **`<your‑PC‑name>:<port>`** — tap **Connect** and enjoy!

> Because the page itself is served over plain HTTP, browsers are happy to open a `ws://` connection to your LiveSplit Server without extra TLS setup.

---

## ⚙️ Technical Notes

| Item             | Details                                                                            |
| ---------------- | ---------------------------------------------------------------------------------- |
| LiveSplit port   | WebSocket server listens on **16834** (`Right‑click → Control → Start Server`).    |
| Web technologies | Vanilla JS, `requestAnimationFrame` interpolation for smooth timer, no frameworks. |
| Security         | Runs entirely on your machine/LAN. No data is sent to any third‑party server.      |
| File size        | ≈30 kB total (HTML + CSS + JS).                                                    |

---

## ❓ Troubleshooting

| Symptom                         | Fix                                                                                                                                  |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **"Disconnected" instantly**    | LiveSplit Server not running, wrong IP, or firewall blocking port 16834.                                                             |
| **Mixed‑content error**         | You're loading the page over **HTTPS** but using **`ws://…`**. Use HTTP/`file://` *or* change to `wss://` with your own TLS wrapper. |
| **Site not reachable on phone** | Make sure PC and phone are on the same Wi‑Fi, and open port 8080 in Windows Firewall.                                                |

---

## 💖 Credits

Created with love for the speedrunning community.

*Note: This is not an official LiveSplit project. LiveSplit is developed by [CryZe](https://github.com/CryZe) and the LiveSplit team.*
