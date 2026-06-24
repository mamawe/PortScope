# 🔍 PortScope

<p align="center">
  <strong>See what's running on your ports, then decide what to kill.</strong><br>
  <strong>看清每个端口在干什么，再决定怎么处理。</strong><br>
  <em>A blazing-fast macOS menu bar app for port management — built with Tauri + React + Rust.</em><br>
  <em>一款极速 macOS 菜单栏端口管理工具 —— 基于 Tauri + React + Rust 构建。</em>
</p>

<p align="center">
  <a href="#-功能特性-features">Features</a> •
  <a href="#-为什么不用终端命令-why-not-terminal">Why Not Terminal?</a> •
  <a href="#-安装-installation">Installation</a> •
  <a href="#-技术栈-tech-stack">Tech Stack</a> •
  <a href="#%EF%B8%8f-roadmap">Roadmap</a> •
  <a href="#-参与贡献-contributing">Contributing</a> •
  <a href="#-许可证-license">License</a>
</p>

---

## ✨ 功能特性 (Features)

### 👁 SEE — 看透每个端口
Click any port entry to reveal full details:
点击任意端口条目，展开完整详情：

- Process name & PID — 进程名与 PID
- Full startup command line — 完整启动命令
- CPU / Memory usage — CPU 与内存占用
- Running duration — 运行时长
- Network connection info — 网络连接信息

### 🌐 OPEN — 一键直达
One-click open `http://localhost:<port>` in your browser — instantly see what service is running without memorizing port numbers or digging through config files.
一键在浏览器打开 `http://localhost:<port>` —— 无需记忆端口号或翻配置文件，直接看到跑的是什么服务。

### ⚡ KILL — 安全释放
Confirm and kill with confidence:
确认无误后，放心释放：

- Single process termination — 单个进程终止
- Batch cleanup with global shortcut — 全局快捷键批量清理
- Safety warnings for system-critical processes — 关键进程安全警告
- Undo support (process restarts if killed by mistake) — 误杀撤销支持

---

## 🤔 为什么不用终端命令？(Why Not Terminal?)

| | `lsof` + `kill` (终端) | **PortScope** |
|---|---|---|
| **时间 / Time** | ~30 秒 (查找 → 定位 PID → 验证 → 杀进程) | **~3 秒** |
| **风险 / Risk** | 容易杀错进程（没有可视化上下文） | 先看详情再做决定 |
| **发现 / Discovery** | 必须提前知道端口号 | 所有活跃端口自动列出 |
| **预览 / Preview** | 无法预览正在运行的服务 | 一键浏览器预览 |
| **记忆 / Memory** | 需要记住命令和参数 | 零命令行知识要求 |

> 💡 **PortScope 不只是杀进程工具 —— 它的核心价值是让你在动手之前，先看懂每个端口在干什么。**
>
> 💡 **PortScope isn't just about killing processes — it's about understanding what's running on your machine before you make a decision.**

---

## 📦 安装 (Installation)

### 前置要求 (Prerequisites)

- macOS 12+ (Monterey 或更高版本)
- [Rust 工具链](https://rustup.rs/)（仅源码构建需要）
- [Node.js](https://nodejs.org/) 18+（仅源码构建需要）

### Homebrew（推荐 / Recommended）

```bash
brew install --cask portscope
```

### 源码构建 (Build from Source)

```bash
# 克隆仓库
git clone https://github.com/mamawe/PortScope.git
cd PortScope

# 安装依赖
npm install

# 开发模式运行
npm run tauri dev

# 生产环境构建
npm run tauri build
```

生产构建产物位于 `src-tauri/target/release/bundle/`。

---

## 🛠 技术栈 (Tech Stack)

| 层 / Layer | 技术 / Technology | 为什么选它 / Why? |
|---|---|---|
| **前端 Frontend** | React 18 + TypeScript | 快速迭代，生态丰富 |
| **桌面壳 Desktop Shell** | [Tauri v2](https://tauri.app/) | ~5MB 包体，<0.3s 启动，Rust 后端 |
| **系统调用 System Calls** | Rust | 直接 BSD 系统调用，内存安全 |
| **样式 Styling** | Tailwind CSS | 极小运行时，原子化 CSS |
| **构建 Build** | Vite | 极速热更新 |

### 架构图 (Architecture)

```
┌─────────────────────────────────────┐
│         Menu Bar (macOS Native)      │
│         菜单栏 (macOS 原生)           │
├─────────────────────────────────────┤
│         React Frontend              │
│    ┌──────────┬──────────┐          │
│    │ PortList │ DetailView│          │
│    │ 端口列表  │ 详情面板   │          │
│    └──────────┴──────────┘          │
├─────────────────────────────────────┤
│       Tauri IPC Bridge              │
├─────────────────────────────────────┤
│        Rust Backend                 │
│  ┌─────────┬─────────┬─────────┐   │
│  │lsof parse│kill proc│net info │   │
│  │端口解析  │进程终止  │网络信息  │   │
│  └─────────┴─────────┴─────────┘   │
└─────────────────────────────────────┘
```

---

## 🗺 发展路线图 (Roadmap)

### ✅ v0.1 — 最小可用产品 MVP (当前 / Current)
- [x] 菜单栏图标 + 端口数量角标
- [x] 活跃端口列表（端口、进程、PID）
- [x] 单个进程 Kill 功能
- [x] 基础详情查看

### 🔄 v0.2 — 即将推出 (Coming Soon)
- [ ] 一键「在浏览器中打开」
- [ ] 进程详情面板（CPU、内存、命令、运行时长）
- [ ] 端口搜索 / 过滤
- [ ] 深色模式支持

### 🎯 v1.0 — 正式发布 (Launch)
- [ ] 全局快捷键快速查看端口
- [ ] 可配置间隔自动刷新
- [ ] 收藏常用端口（固定置顶）
- [ ] 新端口出现时通知
- [ ] Homebrew Cask 正式发布

### 💎 Pro 版（未来付费功能 / Future Paid Tier）
- [ ] 端口占用历史 & 时间线分析
- [ ] iCloud 跨 Mac 同步配置
- [ ] 团队工作区（共享端口配置）
- [ ] 优先技术支持

---

## 🤝 参与贡献 (Contributing)

我们非常欢迎贡献！入门步骤：
We love contributions! Here's how to get started:

1. Fork 本仓库
2. 创建功能分支：`git checkout -b feature/amazing-feature`
3. 进行开发并测试：`npm run tauri dev`
4. 提交代码：`git commit -m 'Add amazing feature'`
5. 推送分支：`git push origin feature/amazing-feature`
6. 发起 Pull Request

### 开发提示 (Development Tips)

- 使用 `npm run tauri dev` 进行前端热重载开发
- Rust 后端修改需要重启 Tauri
- 发 Issue 前请先搜索已有 issue
- 遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范

---

## 📊 项目数据 (Stats)

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

## 🙏 致谢 (Acknowledgments)

- [Tauri](https://tauri.app/) — 出色的轻量级应用框架
- [Portia](https://www.portia.app/) — 证明了市场需求确实存在
- 每一个曾经输入过 `lsof -i :3000` 然后叹气的开发者 😤

---

## 📄 许可证 (License)

本项目基于 [MIT License](LICENSE) 开源。

---

<p align="center">
  <strong>Made with ☕ by <a href="https://github.com/mamawe">mamawe</a></strong><br>
  <strong>☕ 由 <a href="https://github.com/mamawe">mamawe</a> 用心制作</strong><br>
  <em>If you find PortScope useful, give it a ⭐ — it helps more developers discover it!</em><br>
  <em>如果你觉得 PortScope 有用，欢迎点个 ⭐ —— 让更多开发者发现它！</em>
</p>
