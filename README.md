<div align="center">

# 🛡️ CC Version Guard

**Take control of your version. Lock your preferred release and block unwanted auto-updates.**

[![Rust](https://img.shields.io/badge/Rust-2021-orange?style=flat-square&logo=rust)](https://www.rust-lang.org/)
[![Platform](https://img.shields.io/badge/Platform-Windows-blue?style=flat-square&logo=windows)](https://www.microsoft.com/windows)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![MCAF](https://img.shields.io/badge/Follows-MCAF-purple?style=flat-square)](https://mcaf.managed-code.com/)

[Download](#-quick-start) • [Features](#-features) • [How It Works](#-how-it-works) • [Build](#-building-from-source) • [Documentation](#-documentation)

</div>

---

## 🎯 The Problem

Automatic updates frequently:
- Remove features (free Auto-Captions → paid subscription)
- Add paywalls to previously free exports
- Increase cloud dependency and telemetry
- Break workflows by changing the UI

**You shouldn't be forced to update software you already own.**

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| **Version Detection** | Automatically scans your system for all installed CapCut versions |
| **Version Selection** | Choose exactly which version to keep — the rest are safely removed |
| **Download Manager** | Curated links to legacy versions from [ProjectBukkit](https://github.com/ProjectBukkit/CapcutVersions) |
| **Update Blocking** | Locks configuration files and creates blocker files to prevent auto-updates |
| **Guided Wizard** | Step-by-step flow — no technical knowledge required |

### Persona-Based Version Recommendations

| Persona | Version | Best For |
|---------|---------|----------|
| 🖥️ **Offline Purist** | 1.5.0 | Clean UI, unrestricted 4K export, zero cloud dependency |
| 🔊 **Audio Engineer** | 2.5.4 | Multi-track audio editing, stable mixer, keyframe support |
| ✨ **Creator** | 3.9.0 | Last version with free Auto-Captions (API-dependent) |

---

## 🚀 Quick Start

### Option 1: Download Release
1. Download `capcut_guard_rust.exe` from [Releases](https://github.com/Zendevve/capcut-version-guard/releases)
2. Run the executable
3. Follow the wizard

> **⚠️ Windows SmartScreen Warning**
>
> You may see "Windows protected your PC" when running. This is normal for unsigned executables.
>
> **To run anyway:**
> 1. Click **"More info"**
> 2. Click **"Run anyway"**
>
> The app is open-source — [inspect the code yourself](src/main.rs) if you're concerned.

### Option 2: Build from Source
```bash
git clone https://github.com/Zendevve/capcut-version-guard.git
cd capcut-version-guard
cargo build --release
```

The binary will be at `target/release/capcut_guard_rust.exe`

---

## 🔧 How It Works

```mermaid
flowchart LR
    subgraph Main Flow
        A[Welcome] --> B{PreCheck}
        B -->|CapCut Found| C[Version Select]
        C --> D[Running]
        D --> E[Complete]
    end

    subgraph Alternative
        A -->|Download Legacy| F[Download Manager]
        F -->|Opens Browser| G[ProjectBukkit]
    end

    subgraph Protection Steps
        D -->|Step 1| H[Delete Other Versions]
        D -->|Step 2| I[Lock Config Files]
        D -->|Step 3| J[Create Blockers]
    end
```

### Protection Mechanisms

1. **Version Cleanup** — Removes all versions except your selected one from `%LOCALAPPDATA%\CapCut\Apps\`
2. **Config Locking** — Sets critical configuration files to read-only
3. **Blocker Files** — Creates backup files (`updater.exe.bak`) that prevent the updater from running
4. **Directory Blockers** — Creates blocking folders (`CapCutUpdater.bak/`) that occupy updater paths

---

## 🏗️ Architecture

### Tech Stack

| Technology | Purpose |
|-----------|---------|
| **Rust 2021** | Memory-safe systems programming |
| **eframe/egui** | Immediate-mode GUI framework |
| **egui-phosphor** | Professional icon set |
| **walkdir** | Directory traversal |
| **sysinfo** | Process detection |

### Project Structure

```
capcut_guard_rust/
├── src/
│   └── main.rs           # Single-file application (~1100 lines)
├── docs/
│   ├── Features/         # Feature specifications
│   ├── ADR/              # Architecture Decision Records
│   ├── Development/      # Setup guides
│   └── Testing/          # Test strategy
├── AGENTS.md             # AI agent instructions (MCAF)
├── Cargo.toml            # Dependencies
└── README.md
```

### Design Decisions

- **Single executable** — No installer, no runtime dependencies
- **Wizard UX pattern** — Guides users through multi-step process
- **Responsive layout** — Dynamic spacing adapts to window size (20px–80px)
- **60-30-10 color rule** — Professional enterprise aesthetic

> See [docs/ADR/](docs/ADR/) for detailed Architecture Decision Records.

---

## 📖 Documentation

| Document | Description |
|----------|-------------|
| [AGENTS.md](AGENTS.md) | AI coding rules and project conventions |
| [Version Protection](docs/Features/version-protection.md) | Core feature specification |
| [Download Manager](docs/Features/download-manager.md) | Legacy version download flow |
| [GUI Framework ADR](docs/ADR/001-gui-framework.md) | Why eframe/egui |
| [Wizard UX ADR](docs/ADR/002-wizard-ux.md) | Why wizard pattern |
| [Development Setup](docs/Development/setup.md) | Build instructions |
| [Testing Strategy](docs/Testing/strategy.md) | How we test |

---

## 🛠️ Building from Source

### Prerequisites
- [Rust](https://rustup.rs/) 1.70 or later
- Windows 10/11

### Commands

```bash
# Build optimized release
cargo build --release

# Run directly
cargo run --release

# Format code
cargo fmt

# Lint
cargo clippy
```

---

## 🤝 Contributing

This project follows [MCAF](https://mcaf.managed-code.com/) (Managed Code AI Framework).

Before contributing:
1. Read [AGENTS.md](AGENTS.md)
2. Check [docs/](docs/) for context
3. Follow the coding rules and UI preferences documented there

---

## ⚠️ Disclaimer

This tool modifies files in your CapCut installation directory. While it's designed to be safe:
- **Back up your projects** before running
- Use at your own risk
- Not affiliated with ByteDance or CapCut

---

## 💬 A Note from the Developer

Hey! I'm a college student building this in my free time as a hobby project — and hopefully a portfolio piece to land my first dev job.

**Why the SmartScreen warning?** Code signing certificates cost $200-400/year, which is... a lot when you're living on instant noodles. The app is fully open-source, so you can [read every line of code](src/main.rs) before running it.

If you find this useful:
- ⭐ **Star the repo** — it helps with visibility
- 🐛 **Report bugs** — I actually fix them
- 💼 **Hiring?** — [Let's talk](https://github.com/Zendevve)

---

## 📄 License

MIT © [Zendevve](https://github.com/Zendevve)

---

<div align="center">

**Built with Rust 🦀 and instant noodles 🍜**

*Made with love by a broke college student who just wants to help people keep their software.*

</div>
