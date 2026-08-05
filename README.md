<div align="center">

# 🚀 Nitrafe One v1.0.8

![Version](https://img.shields.io/badge/version-1.0.8--stable-blue.svg?style=for-the-badge)
![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011%20x64-0078D4.svg?style=for-the-badge&logo=windows)
![Built With](https://img.shields.io/badge/architecture-Native%20Win32%20Engine-orange.svg?style=for-the-badge&logo=windows)
![License](https://img.shields.io/badge/license-Proprietary-red.svg?style=for-the-badge)
![Security](https://img.shields.io/badge/telemetry-Zero--Tracking-success.svg?style=for-the-badge)

**The Ultimate Next-Generation Windows Optimization, Game Booster & Security Suite.**

[📥 Download Executable Setup (.exe)](#-official-release-installers) • [📦 Download Windows Installer (.msi)](#-official-release-installers)

</div>

---

## 📥 Official Release Installers

Select your preferred installation format below for direct download:

| Package Type | File Name | Direct Download Link | Format | Size |
| :--- | :--- | :--- | :---: | :---: |
| 🚀 **Executable Setup (Recommended)** | `Nitrafe One_1.0.8_x64-setup.exe` | [⬇️ **Download Setup (.exe)**](./Nitrafe%20One_1.0.8_x64-setup.exe?raw=true) | `.exe` | **~3.1 MB** |
| 📦 **Windows Installer Package** | `Nitrafe One_1.0.8_x64_en-US.msi` | [⬇️ **Download Package (.msi)**](../msi/Nitrafe%20One_1.0.8_x64_en-US.msi?raw=true) | `.msi` | **~3.8 MB** |

> 💡 **Note:** Click the direct download links above or select the file from the repository list and click **"Download raw"**.

---

## ✨ What's New in v1.0.8

Nitrafe One v1.0.8 is a major fluidity, design, and backend overhaul focused on making the app feel truly instant and professional.

### 🚀 Fluidity & Performance
- **Instant Boot Splash**: Inline HTML splash appears in under 100 ms — no more white-screen delay.
- **Zero Idle Polling**: Live metrics stream from a single Rust event subscription and slow to a 10 s cadence when the window is unfocused.
- **Lazy-Loaded Tabs**: Every tab is its own React chunk (5–9 KB each), loaded only when opened.
- **GPU-Accelerated Animations**: Continuous animations opt into GPU compositing and honor `prefers-reduced-motion`.

### 🎨 Refined Design System
- **CSS Design Tokens**: Full theme on `:root` (`--accent`, `--surface`, `--ink`, `--line`, semantic tones) — mapped into Tailwind.
- **Real Depth Shadows**: Fixed a bug where 72 `shadow-xs` classes rendered nothing — the whole UI has visible elevation now.
- **Inter Variable Font**: One woff2 file replaces six previous font imports.
- **Keyboard-First**: `focus-visible` rings across all interactive elements, `Esc` closes any modal.

### 🎮 Game Boost — Truly Differentiated Presets
Each preset now writes distinct MMCSS + network throttling values (previously all three ran identical code):

| Preset | GPU Priority | Task Priority | SFIO | SystemResponsiveness | Network Throttling | Flush Standby |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| 🏆 **eSports** | 8 | 6 | High | 0 (max headroom) | Disabled | ✓ |
| ⚖️ **Balanced** | 7 | 5 | High | 10 | Enabled (10) | ✓ |
| 🎥 **Streamer** | 6 | 4 | Normal | 20 (encoder headroom) | Enabled (10) | ✗ (preserved for OBS) |

Disabling a preset now **restores your previous MMCSS values** from a snapshot taken at activation.

### 🧹 Honest Scan & Clean
- **Real Progress Events**: The 1.8–2.8 s fake `setInterval` wait is gone — the scan bar starts moving the moment you click.
- **5-Minute Safety Window**: Cleaner skips files modified in the last 5 minutes to avoid interrupting active installers or open browser sessions.
- **Actual Bytes Reported**: Cleanup progress reports real bytes freed per category.

### ⚡ Faster Backend
- **Parallel Directory Scanning**: `dir_size_and_count` is now paralellized with `rayon` + `AtomicU64` — deep scans of large `%TEMP%` directories are 4–8× faster.
- **Two-Phase App List**: Registry entries paint instantly, then real on-disk sizes enrich in the background.
- **Adaptive Emitter**: System metrics push interval scales with window focus (2 s focused → 10 s minimized).
- **Optimized Release Binary**: Built with `opt-level = "z"`, `lto = true`, `codegen-units = 1`, `strip = true`.

---

## 🎯 Product Overview

Nitrafe One is engineered for Windows power users, competitive gamers, and workstations requiring peak hardware responsiveness and system cleanliness.

### 🧹 1. Deep System & Storage Purge
- **System Cache & Temporary Cleanup**: Safely scans and removes Windows `%TEMP%`, `C:\Windows\Temp`, browser web caches (Chrome, Edge), and orphan D3D shader caches.
- **Deep Mode Extras**: Also targets `C:\Windows\SoftwareDistribution\Download` (installed Windows Updates) and `%LocalAppData%\CrashDumps`.
- **Parallelized Scan Engine**: Every category is sized concurrently, and each directory recursion itself runs in parallel via `rayon`.

### ⚡ 2. Real-Time RAM & Memory Working Set Optimizer
- **Working Set Trimming**: Executes `K32EmptyWorkingSet` for every process to reduce active memory pressure.
- **Standby List Defragmentation**: Purges standby memory via `NtSetSystemInformation(SystemMemoryListInformation, MemoryPurgeStandbyList)` — the same NtApi mechanism used by Microsoft's own RAMMap.
- **Measured Reclaim**: Reports `bytes_freed = ram_before − ram_after` (never estimated).

### 💽 3. Multi-Partition Disk Health & Capacity Monitor
Monitors storage partition health across all mounted drives with dynamic status indicators:
- 🟢 **Optimal Capacity (< 60% Used)** — high available storage buffer.
- 🟡 **Moderate Load (60% – 85% Used)** — storage warning threshold.
- 🔴 **Critical Storage (> 85% Used)** — high capacity utilization alert.

### 🎮 4. Low-Latency Game Booster Engine
- **MMCSS & GPU Priority Elevation**: Per-preset Multimedia Class Scheduler tuning (see table above).
- **QoS & Network Latency Tuning**: eSports preset disables Windows Network Throttling for competitive network latency.
- **Power Plan Switching**: Automatically applies High Performance while active, restores the previous plan on disable.

### 🛡️ 5. Windows Security Guard & Autostart Manager
- **Startup Impact Evaluation**: Identifies background autostart software impacting boot times.
- **System Health Audit**: Verifies real-time Windows Defender, Firewall, and telemetry protection states.
- **One-Click System Restore Point**: Creates a Windows System Restore Point before major operations.

### 🧾 6. Smart Uninstaller
- **Two-Phase Load**: Registry list appears instantly; real on-disk sizes enrich in the background.
- **Residual Trace Cleanup**: After the official uninstaller finishes, scans `%ProgramData%`, `%LocalAppData%`, and HKCU for residual folders and registry keys, offering a one-click purge.

---

## ⚙️ Installation & Deployment

### Standard Executable Installation
1. Download [`Nitrafe One_1.0.8_x64-setup.exe`](./Nitrafe%20One_1.0.8_x64-setup.exe?raw=true).
2. Double-click the installer executable to launch the NSIS Setup Wizard.
3. Follow the onscreen wizard steps and launch **Nitrafe One**.

### Enterprise & Silent MSI Deployment
To deploy silently across enterprise systems via Command Prompt or PowerShell:
```powershell
msiexec /i "Nitrafe One_1.0.8_x64_en-US.msi" /qb
```

---

## 🔒 File Integrity Verification (SHA-256 Checksums)

To verify the integrity and authenticity of your downloaded package, check the SHA-256 cryptographic hashes:

| File Name | SHA-256 Hash |
| :--- | :--- |
| **`Nitrafe One_1.0.8_x64-setup.exe`** | `5D8C5BA82506C40C0B0D10AD80B2E61CCDE0A9A8E2C2C80A43BD8ACF50BE9F4E` |
| **`Nitrafe One_1.0.8_x64_en-US.msi`** | `E8E9D4C342228D52CDE4FDA7B8CA7DC04995E4A99B60F3AEF300AECA33FD5717` |

### Verification Command (PowerShell):
```powershell
Get-FileHash "Nitrafe One_1.0.8_x64-setup.exe"
```

---

## 💻 System Requirements

- **Operating System**: Windows 10 (Build 1903 or newer) / Windows 11 (64-bit)
- **Processor**: 1.6 GHz dual-core or faster x64 processor
- **Memory**: Minimum 2 GB RAM (4 GB recommended)
- **Available Disk Space**: 50 MB
- **Privileges**: Administrator privileges required for Win32 memory trimming, standby-list purge, and HKLM MMCSS Game Boost tuning.

---

## 📖 About Nitrafe

**Nitrafe** is an upcoming technology company founded by **Pitigoi George (GeorgePity)**, originally developed under the **GeorgePity Studio** brand.

The software showcased here is a **PC Cleaner & Booster** designed to improve your computer's performance by cleaning unnecessary files, optimizing system resources, and providing maintenance tools in a simple and user-friendly interface.

### Our Commitment

We believe transparency is essential.

- Nitrafe **does not contain viruses, malware, spyware, or any malicious code.**
- We **do not collect, read, or transmit your personal files or private data.**
- Every optimization is performed locally on your computer.

### Safety

The installation process is designed to be safe and straightforward.

Nitrafe only performs actions that are required for system optimization and maintenance. The application **will never delete or modify important files without your permission.**

Starting with v1.0.8, the cleaner also skips any file modified in the last five minutes — active installers, open browser sessions, and running games stay untouched.

For supported features, a **Rollback** system is available, allowing you to restore previous changes if needed. Game Boost specifically snapshots your previous MMCSS values before applying a preset and restores them on disable.

### Liability

While every effort is made to ensure the software is stable and reliable, Nitrafe cannot be held responsible for issues caused by:

- Third-party software
- Windows updates
- Driver conflicts
- User modifications
- Hardware failures
- Other circumstances unrelated to the application

### Feedback & Support

Nitrafe is currently under active development and community feedback plays an important role in improving the software.

If you have suggestions, feature requests, or encounter any issues, feel free to contact us:

**Discord:** @georgepity

**Instagram:** @georgepityc

Thank you for supporting **Nitrafe** from the very beginning.

Our goal is to build modern, secure, and high-performance software that helps Windows users keep their computers clean, fast, and reliable.

---

<div align="center">

© 2026 **Nitrafe Technologies Inc.** All rights reserved.  
Contact Support: [support@nitrafe.one](mailto:support@nitrafe.one)

</div>
