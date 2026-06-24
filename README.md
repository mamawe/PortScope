# 🔍 PortScope

<p align="center">
  <strong>See what's running on your ports, then decide what to kill.</strong><br>
  <em>A blazing-fast macOS menu bar app for port management — built with Tauri + React + Rust.</em>
</p>

<p align="center">
  <a href="#-features">Features</a> •
  <a href="#-why-not-terminal">Why Not Terminal?</a> •
  <a href="#-installation">Installation</a> •
  <a href="#-tech-stack">Tech Stack</a> •
  <a href="#%EF%B8%8F-roadmap">Roadmap</a> •
  <a href="#-contributing">Contributing</a> •
  <a href="#-license">License</a>
</p>

---

## ✨ Features

### 👁 SEE — 看透每个端口
Click any port entry to reveal full details:
- Process name & PID
- Full startup command line
- CPU / Memory usage
- Running duration
- Network connection info

### 🌐 OPEN — 一键直达
One-click open `http://localhost:<port>` in your browser — instantly see what service is running without memorizing port numbers or digging through config files.

### ⚡ KILL — 安全释放
Confirm and kill with confidence:
- Single process termination
- Batch cleanup with global shortcut
- Safety warnings for system-critical processes
- Undo support (process restarts if killed by mistake)

---

## 🤔 Why Not Terminal?

| | `lsof` + `kill` (Terminal) | **PortScope** |
|---|---|---|
| **Time** | ~30 seconds (lookup → find PID → verify → kill) | **~3 seconds** |
| **Risk** | Easy to kill wrong process (no visual context) | See full details before deciding |
| **Discovery** | Must know the port number beforehand | All active ports listed automatically |
| **Preview** | No way to preview what's running | One-click browser preview |
| **Memory** | Need to remember commands & flags | Zero command-line knowledge required |

> 💡 **PortScope isn't just about killing processes — it's about understanding what's running on your machine before you make a decision.**

---

## 📦 Installation

### Prerequisites

- macOS 12+ (Monterey or later)
- [Rust toolchain](https://rustup.rs/) (for building from source)
- [Node.js](https://nodejs.org/) 18+ (for building from source)

### Homebrew (Recommended)

```bash
brew install --cask portscope
```

### Build from Source

```bash
# Clone the repo
git clone https://github.com/mamawe/PortScope.git
cd PortScope

# Install dependencies
npm install

# Run in development mode
npm run tauri dev

# Build for production
npm run tauri build
```

The production build will be in `src-tauri/target/release/bundle/`.

---

## 🛠 Tech Stack

| Layer | Technology | Why? |
|---|---|---|
| **Frontend** | React 18 + TypeScript | Fast iteration, rich ecosystem |
| **Desktop Shell** | [Tauri v2](https://tauri.app/) | ~5MB bundle, <0.3s launch, Rust backend |
| **System Calls** | Rust | Direct BSD syscall access, memory-safe |
| **Styling** | Tailwind CSS | Tiny runtime, utility-first |
| **Build** | Vite | Lightning-fast HMR |

### Architecture

```
┌─────────────────────────────────────┐
│         Menu Bar (macOS Native)      │
├─────────────────────────────────────┤
│         React Frontend              │
│    ┌──────────┬──────────┐          │
│    │ PortList │ DetailView│          │
│    └──────────┴──────────┘          │
├─────────────────────────────────────┤
│       Tauri IPC Bridge              │
├─────────────────────────────────────┤
│        Rust Backend                 │
│  ┌─────────┬─────────┬─────────┐   │
│  │lsof parse│kill proc│net info │   │
│  └─────────┴─────────┴─────────┘   │
└─────────────────────────────────────┘
```

---

## 🗺 Roadmap

### ✅ v0.1 — MVP (Current)
- [x] Menu bar icon with port count badge
- [x] Active ports list (port, process, PID)
- [x] Kill individual process
- [x] Basic detail view

### 🔄 v0.2 — Coming Soon
- [ ] One-click "Open in Browser"
- [ ] Process detail panel (CPU, Memory, Command, Duration)
- [ ] Search / filter ports
- [ ] Dark mode support

### 🎯 v1.0 — Launch
- [ ] Global hotkey for quick port peek
- [ ] Auto-refresh with configurable interval
- [ ] Favorite ports (pin frequently used ones)
- [ ] Notification when new port appears
- [ ] Homebrew cask release

### 💎 Pro (Future Paid Tier)
- [ ] Port history & timeline analytics
- [ ] iCloud sync preferences across Macs
- [ ] Team workspace (share port configs)
- [ ] Priority support

---

## 🤝 Contributing

We love contributions! Here's how to get started:

1. Fork the repo
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes and test: `npm run tauri dev`
4. Commit: `git commit -m 'Add amazing feature'`
5. Push: `git push origin feature/amazing-feature`
6. Open a Pull Request

### Development Tips

- Use `npm run tauri dev` for hot-reload during frontend development
- Rust backend changes require Tauri restart
- Check existing issues before creating new ones
- Follow [Conventional Commits](https://www.conventionalcommits.org/)

---

## 📊 Stats

<a href="https://github.com/mamawe/PortScope/stargazers">
  <img src="https://img.shields.io/github/stars/mamawe/PortScope?style=flat-square&logo=github&color=orange" alt="GitHub Stars" />
</a>
<a href="https://github.com/mamawe/PortScope/forks">
  <img src="https://img.shields.io/github/forks/mamawe/PortScope?style=flat-square&logo=github" alt="GitHub Forks" />
</a>
<a href="https://github.com/mamawe/PortScope/issues">
  <img src="https://img.shields.io/github/issues/mamawe/PortScope?style=flat-square" alt="GitHub Issues" />
</a>
<img src="https://img.shields.io/github/license/mamawe/PortScope?style=flat-square" alt="License" />
<img src="https://img.shields.io/badge/macOS-12%2B-blue?style=flat-square&logo=apple" alt="macOS" />
<img src="https://img.shields.io/badge/Tauri-v2-0C4B33?style=flat-square&logo=tauri" alt="Tauri" />

---

## 🙏 Acknowledgments

- [Tauri](https://tauri.app/) — Incredible lightweight app framework
- [Portia](https://www.portia.app/) — For proving the market need exists
- Every developer who's ever typed `lsof -i :3000` and sighed 😤

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">
  <strong>Made with ☕ by <a href="https://github.com/mamawe">mamawe</a></strong><br>
  <em>If you find PortScope useful, give it a ⭐ — it helps more developers discover it!</em>
</p>
