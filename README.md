<p align="center">
  <img src="TrueReplayer.ico" width="80" />
</p>

<h1 align="center">TrueReplayer</h1>

<p align="center">
  A modern macro recorder and replayer for Windows built with WinUI 3.<br/>
  Record mouse clicks, keyboard inputs, and scroll actions — then replay them with precision.
</p>

<p align="center">
  <a href="https://github.com/fatalihue/TrueReplayer-releases/releases/latest">
    <img src="https://img.shields.io/github/v/release/fatalihue/TrueReplayer-releases?style=flat-square&color=60CDFF" alt="Latest Release" />
  </a>
  <img src="https://img.shields.io/badge/platform-Windows%2010%2F11-0078D4?style=flat-square" alt="Platform" />
  <img src="https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square" alt=".NET 8" />
</p>

---

![Main Window](Image%20App/TrueReplayer1.png)

## Download

<a href="https://github.com/fatalihue/TrueReplayer-releases/releases/latest">
  <img src="https://img.shields.io/badge/Download-Latest%20Release-60CDFF?style=for-the-badge&logo=windows" alt="Download" />
</a>

**Installer** — Run `TrueReplayer-win-Setup.exe` for automatic installation with auto-updates.

**Portable** — Extract `TrueReplayer-win-Portable.zip` and run `TrueReplayer.exe` — no installation needed.

> **Requires:** Windows 10 (1809) or later — x64

---

## Features

### Recording & Replay
- Record mouse clicks (left, right, middle), scroll, and keyboard with real or fixed delays
- Insert mode — record new actions at any position in the list
- Looping with repeat count or infinite, with optional interval between iterations
- Live highlighting and auto-scroll during replay
- Raw Input support for games (e.g., Roblox)
- Silent click capture — insert mouse actions manually without triggering the actual click
- International keyboard layout support (ABNT2 and others)

### Action Table
- Inline editing, drag & drop reordering, and multi-selection
- Bulk operations — set delay, duplicate, or delete selected actions
- Color-coded action types and configurable column visibility

### Send Text
- Insert text blocks as typed keystrokes with emoji picker, dynamic variables (`{clipboard}`, `{date}`, `{time}`), special keys, and reusable snippets

### Profiles
- Organize macros into profiles with hotkeys, hotstrings, and folders
- Window targeting — restrict hotkeys to specific windows (process name or title match)
- Import & export as `.trprofile` files with conflict resolution
- Pin favorite profiles to the top

### Command Palette
- **Ctrl+K** — fuzzy search across commands, profiles, and settings

### Theme Editor
- 14 built-in presets (Midnight, Nord, Dracula, Monokai, and more)
- Full color customization with import/export

### Settings
- Execution delays, recording filters, customizable hotkeys
- Always on top, system tray, run on startup, auto-updates

---

## Default Hotkeys

| Action | Key |
|--------|-----|
| Record | `Ctrl+PageUp` |
| Replay | `Ctrl+PageDown` |
| Toggle Profile Keys | `Pause` |
| Bring to Foreground | `Ctrl+Insert` |
| Command Palette | `Ctrl+K` |

All hotkeys can be changed in Settings.
