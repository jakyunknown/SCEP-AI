<div align="center">

<br/>
```
███████╗ ██████╗███████╗██████╗      █████╗ ██╗
██╔════╝██╔════╝██╔════╝██╔══██╗    ██╔══██╗██║
███████╗██║     █████╗  ██████╔╝    ███████║██║
╚════██║██║     ██╔══╝  ██╔═══╝     ██╔══██║██║
███████║╚██████╗███████╗██║         ██║  ██║██║
╚══════╝ ╚═════╝╚══════╝╚═╝         ╚═╝  ╚═╝╚═╝
```

### 🛡️ Security · Cipher · Entropy · Protection — AI Powered

**A professional, phone-framed password security tool built in a single HTML file.**
*No frameworks. No dependencies. No data ever leaves your device.*

<br/>

![HTML](https://img.shields.io/badge/HTML5-Single%20File-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-Animations-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-40D090?style=for-the-badge)
![Privacy](https://img.shields.io/badge/Privacy-100%25%20Local-FF4060?style=for-the-badge&logo=shield&logoColor=white)

<br/>

> **Scan. Check. Encrypt. Protect.**
> SCEP AI gives you instant, real-time insight into how strong — or how vulnerable — your password actually is.

<br/>

---

</div>

## ✨ Features

### 🔐 Core Analysis Engine
- **Real-time Shannon entropy calculation** — measures password strength in bits as you type
- **Character pool detection** — identifies lowercase, uppercase, digits, and symbols in use
- **5-tier strength rating** — Critical · Weak · Fair · Strong · Excellent
- **GPU crack-time estimation** — calculates how long a 1 billion guesses/sec attack would take
- **Animated score ring** — circular progress indicator that updates live

### 🚨 Vulnerability Detection
Automatically flags the following weaknesses:

| Issue | Example |
|---|---|
| Common / dictionary word | `password`, `sunshine`, `dragon` |
| Sequential characters | `1234`, `abcd`, `qwer` |
| Repeated characters | `aaa`, `111` |
| Low character diversity | `aaabbbccc` |
| Too short | Under 8 characters |
| Marginally short | Under 12 characters |

### 🔍 Breach Check *(Offline Mock — API-Ready)*
- Checks the entered password against a local dataset of commonly breached passwords
- Displays **"Exposed"** in red or **"Not found"** in green with clear visual styling
- **100% local** — no data is ever sent anywhere
- Clean, swappable architecture: one function to replace when connecting a real API (e.g. HaveIBeenPwned)

### ♻️ Password Reuse Warning
- Tracks the **last 5 passwords** checked in the current session (in-memory only)
- Warns you if you type a password you've already analyzed: *"Password reused recently"*
- Uses a **400ms debounce** — only triggers after you pause typing, not on every keystroke
- Automatically clears on page reload — nothing is ever persisted

### 💡 Password Generator
- Generates **3 random 20-character passwords** on load and on demand
- Generates a **memorable passphrase** (Adjective + Verb + Noun + Number + Symbol)
- All suggestions display their own entropy score
- One-tap **copy to clipboard** with toast confirmation

### 📱 Phone Frame UI
- Realistic **iPhone-style frame** with side buttons, Dynamic Island, and home indicator
- Scrollable app screen with live status bar (clock, signal, WiFi, battery)
- Spring-animated **phone entry animation** on load
- Ambient background glow that pulses behind the device
- Fully responsive — adapts to full-page layout on smaller screens

<br/>

---

## 🚀 Getting Started

### Option 1 — Just Open It
```bash
# Download the file, then:
double-click password-entropy-checker.html
```
Opens instantly in any modern browser. No install, no setup, no server needed.

### Option 2 — VS Code + Live Server
```bash
# 1. Install the Live Server extension in VS Code
# 2. Open the project folder
# 3. Right-click the HTML file → "Open with Live Server"
```

### Option 3 — Clone & Run
```bash
git clone https://github.com/yourusername/scep-ai.git
cd scep-ai
open password-entropy-checker.html   # macOS
start password-entropy-checker.html  # Windows
```

> ✅ **Zero dependencies.** No `npm install`. No build step. No bundler. Just one file.

<br/>

---

## 🔌 Swapping in a Real Breach API

The breach check logic is isolated in one clean function. Find this comment in the `<script>` section:
```javascript
// ── BREACH CHECK ─────────────────────────────────────────────
// ⬇️  SWAP POINT: Replace this function body to use a real API.
// Never log or transmit the plain password — hash it first (SHA-1 k-anonymity).
async function checkBreach(pw) { ... }
```

**To integrate HaveIBeenPwned:**
```javascript
async function checkBreach(pw) {
  const hash = await sha1(pw);                          // implement sha1()
  const prefix = hash.slice(0, 5).toUpperCase();
  const suffix = hash.slice(5).toUpperCase();
  const res = await fetch(`https://api.pwnedpasswords.com/range/${prefix}`);
  const text = await res.text();
  const exposed = text.split('\n').some(line => line.startsWith(suffix));
  renderBreachResult(exposed);
}
```

> 🔒 Only a partial SHA-1 hash prefix is sent. The plain password never leaves the device.

<br/>

---

## 🏗️ Project Structure
```
scep-ai/
│
├── password-entropy-checker.html   ← Entire app (HTML + CSS + JS, single file)
├── README.md                       ← You are here
└── no-bug-icon.svg                 ← App icon asset
```

<br/>

---

## 🧠 How Entropy Is Calculated
```
Entropy (bits) = Length × log₂(Pool Size)
```

| Characters used | Pool size added |
|---|---|
| Lowercase letters (a–z) | +26 |
| Uppercase letters (A–Z) | +26 |
| Digits (0–9) | +10 |
| Symbols (!@#…) | +32 |

A **penalty of 8 bits** is applied per detected weakness. The final penalized score determines the strength tier.

| Tier | Entropy | Crack Time |
|---|---|---|
| 🔴 Critical | < 28 bits | Instantly |
| 🟠 Weak | 28–40 bits | Minutes to hours |
| 🟡 Fair | 40–60 bits | Days to months |
| 🟢 Strong | 60–80 bits | Years |
| 🔵 Excellent | 80+ bits | Centuries+ |

<br/>

---

## 🛡️ Privacy & Security

| Principle | Implementation |
|---|---|
| **Zero network requests** | No password data is ever transmitted |
| **No storage** | Nothing written to `localStorage`, cookies, or any database |
| **Session-only memory** | Reuse history lives in JS memory, cleared on reload |
| **Local breach check** | Mock dataset bundled inside the file |
| **Open source** | Full source visible — audit it yourself |

<br/>

---

## 🗺️ Roadmap

- [ ] Real HaveIBeenPwned API integration (k-anonymity)
- [ ] Dark / Light theme toggle
- [ ] Export analysis report as PDF
- [ ] PWA support — installable on mobile home screen
- [ ] Passphrase generator with custom word lists
- [ ] Accessibility improvements (ARIA labels, keyboard navigation)

<br/>

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!
```bash
git checkout -b feature/your-feature-name
git commit -m "Add: your feature description"
git push origin feature/your-feature-name
```

Please keep all changes **self-contained in the single HTML file** and avoid introducing external runtime dependencies.

<br/>

---

## 📄 License

This project is licensed under the **MIT License** — use it, modify it, ship it.
```
MIT License — Copyright (c) 2025 SCEP AI
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software to use, copy, modify, merge, publish, distribute, sublicense,
and/or sell copies of the Software.
```

<br/>

---

<div align="center">

**Built with 🛡️ by SCEP AI**

*Security · Cipher · Entropy · Protection — one password at a time.*

<br/>

[![GitHub stars](https://img.shields.io/github/stars/yourusername/scep-ai?style=social)](https://github.com/yourusername/scep-ai)
[![GitHub forks](https://img.shields.io/github/forks/yourusername/scep-ai?style=social)](https://github.com/yourusername/scep-ai/fork)

</div>
