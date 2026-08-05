# Nitrafe One

**v1.0.8 — 2026-08-05**

A Windows desktop system-optimization suite built on Tauri 2 + React 19 + Rust. Cleans temporary files, purges standby RAM, applies Game Boost tweaks (MMCSS, power plan, network throttling), manages startup apps, and uninstalls applications with residual cleanup — all via real Win32/NtApi calls, no fake progress.

---

## Download v1.0.8

- **Setup (.exe)**: https://github.com/georgepitystudio/nitrafe-app/blob/main/Nitrafe%20One_1.0.8_x64-setup.exe?raw=true
- **Installer (.msi)**: https://github.com/georgepitystudio/nitrafe-app/blob/main/Nitrafe%20One_1.0.8_x64_en-US.msi?raw=true

Both links use `?raw=true` so the browser downloads the installer directly instead of opening the GitHub blob page.

---

## What's new in v1.0.8

### Fluidity & startup
- **Instant startup**: inline splash renders in <100ms; React mount replaces it after first paint. No more white-screen delay.
- **Zero idle polling**: metrics stream from a single Rust `system_metrics` event subscription. When the window is unfocused, the emitter drops from 2s to 10s to save CPU.
- **Lazy tabs**: each tab (Clean, Game Boost, RAM, Protect, Uninstaller, Settings) is its own React chunk, loaded on demand. Main bundle is 292 KB (was ~600 KB with `framer-motion`, now removed).
- **Real progress events**: `scan_progress` and `clean_progress` events replace the previous 1.8–2.8s artificial `setInterval` waits.

### UI & design
- CSS design tokens on `:root` (`--accent`, `--surface`, `--ink`, `--line`, semantic tones) — mapped into Tailwind so the whole app is themable.
- **Fixed `shadow-xs` bug**: 72 occurrences were rendering nothing (class doesn't exist in Tailwind 3.4). Replaced with a real `shadow-card` scale.
- Single Inter Variable font file replaces 6 separate `@fontsource/inter/*` imports.
- Sparkline indicators for CPU and RAM in the title bar (last 30 samples).
- `tabular-nums` on every live numeric value so digits stop jumping between ticks.
- `prefers-reduced-motion` disables continuous animations.
- Keyboard focus rings (`focus-visible:ring-accent`) across all interactive elements.
- Unified `Modal` component with focus trap, `Esc`-to-close, and consistent backdrop.
- Unified `Toast` system replaces 8 separate ephemeral message states.

### Game Boost — real differentiation
The three presets now write distinct MMCSS values instead of running identical code:

| Preset | GPU Priority | Task Priority | SFIO | SystemResponsiveness | NetworkThrottling | Flush Standby |
|---|---|---|---|---|---|---|
| **eSports** | 8 | 6 | High | 0 | Disabled | ✓ |
| **Balanced** | 7 | 5 | High | 10 | 10 | ✓ |
| **Streamer** | 6 | 4 | Normal | 20 | 10 | ✗ (preserved for OBS) |

Disabling a preset now **restores the previous MMCSS values** captured at activation (snapshotted in `HKCU\Software\Nitrafe\GameBoost`). Report surfaces `needs_admin` / `power_plan_applied` truthfully via a warning banner.

### Backend
- `dir_size_and_count` is **parallelized with rayon** + `AtomicU64` — deep scan of large `%TEMP%` directories is now 4-8× faster.
- Cleanup skips files modified in the **last 5 minutes** to avoid interrupting active installers.
- `SYS_INFO` sysinfo instance consolidated (was duplicated between the polling command and the emitter thread).
- Installed-apps list is cached (60s TTL) with an explicit `refresh_installed_apps` command; two-phase load (registry-first, on-disk sizes enriched in background).
- Removed duplicated `run_diagnostic_tool` command — the streaming variant is the single path now.
- Release binary uses `opt-level = "z"`, `lto = true`, `codegen-units = 1`, `strip = true`.

---

## Features

### Clean
Real Windows temp directories are scanned in parallel:
- `%TEMP%` — user temporary files
- `C:\Windows\Temp` — system temp
- Chrome + Edge browser cache (`%LOCALAPPDATA%\Google\Chrome\User Data\Default\Cache`, `Microsoft\Edge\User Data\Default\Cache`)
- `%LOCALAPPDATA%\D3DSCache` — orphan shader caches
- **Deep mode also includes**: `C:\Windows\SoftwareDistribution\Download` (Windows Update cache), `%LOCALAPPDATA%\CrashDumps` (app crash dumps)

Each category shows real byte counts, safety level (Safe / Recommended / Advanced), and can be toggled off individually before cleaning.

### RAM Optimizer
Multi-method flush via real Win32 / NtApi:
- **Working sets** — `K32EmptyWorkingSet` for every process (`OpenProcess` with `PROCESS_QUERY_INFORMATION | PROCESS_SET_QUOTA`)
- **Standby list** — `NtSetSystemInformation(SystemMemoryListInformation, MemoryPurgeStandbyList=4)` — the same mechanism used by Microsoft's RAMMap
- **All** — both, sequentially

Reports `bytes_freed = ram_before - ram_after` (measured with sysinfo, not estimated). Standby purge requires admin/`SeProfileSingleProcessPrivilege`; the UI surfaces the failure honestly.

### Game Boost
See table above. Also flips Windows power plan to **High Performance** (`8c5e7fda-e8bf-4a96-9a85-a6e23a8c635c`) via `powercfg /setactive`, and reverts to the previously observed plan on disable.

### Protect
- Security score dashboard with Windows Defender / Firewall / telemetry / suspicious process reporting.
- Startup app manager (real registry: `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` and equivalent).
- One-click Windows System Restore Point creation.

### Uninstaller
- Two-phase list: registry fast (instant paint), then real on-disk sizes computed in the background.
- Filter by leftover risk (High / Medium / Low), sort by name or size.
- After running the official uninstaller, scans for residual folders and registry keys and offers a one-click purge.
- Free tier: 2 uninstalls / month; PRO: unlimited.

### Settings
- Diagnostic tools with live streaming stdout (SFC `/scannow`, DISM `/CheckHealth`, DNS `/flushdns`) — each command's real output pipes into a terminal view in real time.
- Language selector (9 languages).
- Hardware fingerprint display for license activation.
- Manual update check (GitHub Releases + `version.json` fallbacks).

---

## Repository layout

```
apps/
  klyro-desktop/          Tauri 2 + React 19 desktop app
    src/                  Frontend (App shell, lazy tabs, hooks, UI kit)
    src-tauri/            Rust backend commands + emitter
  klyro-service/          Windows service (background scheduling)
  klyro-cli/              CLI companion
crates/
  klyro-core/             SystemCleaner, RAMOptimizer, GameBoost, SystemTweaker engines
  klyro-winapi/           NtSetSystemInformation wrapper for standby-list purge
  klyro-safety/           Security dashboard, startup app manager, restore points
  klyro-license/          License validation + hardware fingerprint
  klyro-uninstaller/      Installed-apps enumeration, real leftover scanning, official uninstaller runner
  klyro-updater/          Release channel plumbing
```

---

## Build

### Development
```bash
cd apps/klyro-desktop
npm install
npm run tauri dev
```

### Release (produces `.exe` + `.msi` under `target/release/bundle/`)
```bash
cd apps/klyro-desktop
npm run tauri build
```

Bundles are written to:
- `target/release/bundle/nsis/Nitrafe One_1.0.8_x64-setup.exe`
- `target/release/bundle/msi/Nitrafe One_1.0.8_x64_en-US.msi`

### Type-check + build the frontend only
```bash
cd apps/klyro-desktop
npx tsc --noEmit
npm run build
```

### Cargo-only verification
```bash
cargo check --workspace
cargo build --release --package klyro-core
```

---

## Tech stack

- **Frontend**: React 19, TypeScript 5.7 (strict), Tailwind CSS 3.4 with CSS design tokens, Vite 6 (target `chrome110`), lucide-react icons, Inter Variable font.
- **Backend**: Rust 1.7+ workspace, Tauri 2.2, sysinfo 0.30 for metrics, rayon 1.10 for parallel scans, winreg 0.55, windows 0.58 (Win32 APIs), single `NtSetSystemInformation` binding in `klyro-winapi`.
- **Release profile**: `opt-level = "z"`, `lto = true`, `codegen-units = 1`, `panic = "abort"`, `strip = true`.

---

## License

Proprietary — © Nitrafe Software Team. See `apps/klyro-desktop/src-tauri/resources/licensing/EULA.txt`.
