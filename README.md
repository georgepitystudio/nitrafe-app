<div align="center">

# 🚀 Nitrafe One v1.0.8

![Version](https://img.shields.io/badge/version-1.0.8--stable-blue.svg?style=for-the-badge)
![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011%20x64-0078D4.svg?style=for-the-badge&logo=windows)
![Built With](https://img.shields.io/badge/architecture-Native%20Win32%20Engine-orange.svg?style=for-the-badge&logo=windows)
![License](https://img.shields.io/badge/license-Proprietary-red.svg?style=for-the-badge)
![Security](https://img.shields.io/badge/telemetry-Zero--Tracking-success.svg?style=for-the-badge)

**The Ultimate Next-Generation Windows Optimization, Game Booster & Security Suite.**

<<<<<<< HEAD
[📥 Download Executable Setup (.exe)](#-official-release-installers) • [📦 Download Windows Installer (.msi)](#-official-release-installers)
=======
[🌐 Official Website (Coming Soon)](#) • [📥 Download Executable Setup (.exe)](#-official-release-installers) • [📦 Download Windows Installer (.msi)](#-official-release-installers)
>>>>>>> a3e4dff956bdc5f3166762950aa6c3e35552e39a

</div>

---

## 🎉 What's New in v1.0.8

- **Instant startup, fluid UI** — inline boot splash (<100ms), lazy-loaded tabs, GPU-accelerated animations, no idle polling. Metrics stream from a single Rust subscription that slows to 10s when the window is unfocused.
- **Real Game Boost differentiation** — the three presets no longer share code. Each writes distinct MMCSS + network throttling values, and disabling restores your previous settings from a snapshot.
- **Refined design system** — CSS design tokens (`--accent`, `--surface`, `--ink`), real depth shadows (`shadow-xs` bug fixed — 72 invisible shadows now visible), Inter Variable font, tabular numerals, keyboard focus rings, reduced-motion support.
- **Honest scan & clean progress** — event-driven `scan_progress` / `clean_progress` replace the previous 1.8–2.8s fake wait. Cleaner now skips files modified in the last 5 minutes.
- **Faster backend** — directory sizing parallelized with rayon (4-8× faster on large %TEMP%), installed-apps list cached with TTL, release binary uses LTO + opt-level="z".
- **Two-phase installed-apps load** — registry-first for instant paint, on-disk sizes enriched in the background.

---

## 📥 Official Release Installers

Select your preferred installation format below for direct download:

| Package Type | File Name | Direct Download Link | Format | Size |
| :--- | :--- | :--- | :---: | :---: |
| 🚀 **Executable Setup (Recommended)** | `Nitrafe One_1.0.8_x64-setup.exe` | [⬇️ **Download Setup (.exe)**](./Nitrafe%20One_1.0.8_x64-setup.exe?raw=true) | `.exe` | **~3.1 MB** |
| 📦 **Windows Installer Package** | `Nitrafe One_1.0.8_x64_en-US.msi` | [⬇️ **Download Package (.msi)**](../msi/Nitrafe%20One_1.0.8_x64_en-US.msi?raw=true) | `.msi` | **~3.8 MB** |

> 💡 **Note:** Click the direct download links above or select the file from the repository list and click **"Download raw"**.

---

## ✨ System Capabilities & Product Overview

Nitrafe One is engineered for Windows power users, competitive gamers, and workstations requiring peak hardware responsiveness and system cleanliness.

### 🧹 1. Deep System & Storage Purge
- **System Cache & Temporary Cleanup**: Safely scans and removes Windows `%TEMP%`, `C:\Windows\Temp`, browser web caches (Chrome, Edge), Windows Update download cache (deep mode), application crash dumps (deep mode) and orphan D3D shader cache leftovers.
- **Rayon-Parallel Scan**: Every category is sized concurrently, and directory recursion itself is parallel. Deep scans of huge `%TEMP%` directories are now several times faster.
- **Safety Window**: Files modified in the last 5 minutes are skipped, avoiding interference with active installers or app writes.

### ⚡ 2. Real-Time RAM & Memory Working Set Optimizer
- **Working Set Trimming**: `K32EmptyWorkingSet` called for every process (via `OpenProcess` with `PROCESS_QUERY_INFORMATION | PROCESS_SET_QUOTA`).
- **Standby List Defragmentation**: `NtSetSystemInformation(SystemMemoryListInformation, MemoryPurgeStandbyList=4)` — the same NtApi mechanism used by Microsoft's own RAMMap.
- **Measured Reclaim**: Reports `bytes_freed = ram_before − ram_after` (measured with sysinfo, never estimated).

### 💽 3. Multi-Partition Disk Health & Capacity Monitor
- **Live Drive Diagnostics**: Monitors storage partition health across all mounted drives with dynamic status indicators:
  - 🟢 **Optimal Capacity (<60% Used)**: High available storage buffer.
  - 🟡 **Moderate Load (60% - 85% Used)**: Storage warning threshold.
  - 🔴 **Critical Storage (>85% Used)**: High capacity utilization alert.

### 🎮 4. Low-Latency Game Booster Engine (Now Truly Differentiated)

| Preset | GPU Priority | Task Priority | SFIO | SystemResponsiveness | NetworkThrottling | Flush Standby |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| 🏆 **eSports** | 8 | 6 | High | 0 (max headroom) | Disabled | ✓ |
| ⚖️ **Balanced** | 7 | 5 | High | 10 | 10 | ✓ |
| 🎥 **Streamer** | 6 | 4 | Normal | 20 (aer pt encoder) | 10 | ✗ (preserved for OBS) |

Disabling now **restores your previous MMCSS values**, snapshotted in `HKCU\Software\Nitrafe\GameBoost` at activation. When admin rights are missing, the UI surfaces a warning honestly instead of silently failing.

### 🛡️ 5. Windows Security Guard & Autostart Manager
- **Startup Impact Evaluation**: Identifies background autostart software impacting boot times.
- **System Health Audit**: Verifies real-time Windows Defender, Firewall, and telemetry protection states.
- **One-Click Restore Point**: Creates a real Windows System Restore Point before major operations.

### 🧾 6. Smart Uninstaller
- **Two-Phase Load**: Registry entries render instantly, then real on-disk sizes enrich in the background via a parallel scan.
- **Residual Trace Cleanup**: After the official uninstaller finishes, scans `%ProgramData%`, `%LocalAppData%`, and HKCU for residual folders and registry keys and offers a one-click purge.

---

## ⚙️ Installation & Deployment

### Standard Executable Installation
<<<<<<< HEAD
1. Download [`Nitrafe One_1.0.8_x64-setup.exe`](./Nitrafe%20One_1.0.8_x64-setup.exe?raw=true).
=======
1. Download [`Nitrafe One_1.0.7_x64-setup.exe`](./Nitrafe%20One_1.0.7_x64-setup.exe?raw=true).
>>>>>>> a3e4dff956bdc5f3166762950aa6c3e35552e39a
2. Double-click the installer executable to launch the NSIS Setup Wizard.
3. Follow the onscreen wizard steps and launch **Nitrafe One**.

### Enterprise & Silent MSI Deployment
To deploy silently across enterprise systems via Command Prompt or PowerShell:
```powershell
<<<<<<< HEAD
msiexec /i "Nitrafe One_1.0.8_x64_en-US.msi" /qb
=======
msiexec /i "Nitrafe One_1.0.7_x64_en-US.msi" /qb
>>>>>>> a3e4dff956bdc5f3166762950aa6c3e35552e39a
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

Nitrafe only performs actions that are required for system optimization and maintenance. The application **will never delete or modify important files without your permission.** The v1.0.8 cleaner skips any file modified in the last five minutes — active installers, currently-open browser sessions, and running games stay untouched.

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
To report bugs, and make suggestions contact @georgepity on discord or @georgepityc on instagram.

© 2026 **Nitrafe Technologies Inc.** All rights reserved.  
<<<<<<< HEAD
Contact Support: [support@nitrafe.one](mailto:support@nitrafe.one)
=======
Official Website: [Coming Soon](#) | Contact Support: [Coming Soon](mailto:#)
>>>>>>> a3e4dff956bdc5f3166762950aa6c3e35552e39a

</div>
