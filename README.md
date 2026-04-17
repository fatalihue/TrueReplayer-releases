<p align="center">
  <img src="TrueReplayer.ico" width="84" alt="TrueReplayer" />
</p>

<h1 align="center">TrueReplayer</h1>

<p align="center">
  <b>Macro recorder and replayer for Windows.</b><br/>
  Record mouse, keyboard, scroll, and browser actions — then replay with precision.
</p>

<p align="center">
  <a href="https://github.com/fatalihue/TrueReplayer-releases/releases/latest">
    <img src="https://img.shields.io/github/v/release/fatalihue/TrueReplayer-releases?style=flat-square&color=60CDFF&label=release" alt="Latest Release" />
  </a>
  <img src="https://img.shields.io/badge/windows-10%20%2F%2011-0078D4?style=flat-square" alt="Windows 10/11" />
  <img src="https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square" alt=".NET 8" />
  <img src="https://img.shields.io/badge/arch-x64-6bcb77?style=flat-square" alt="x64" />
</p>

<p align="center">
  <img src="Image%20App/MainWindow.png" alt="TrueReplayer main window" width="900" />
</p>

---

## Download

<a href="https://github.com/fatalihue/TrueReplayer-releases/releases/latest">
  <img src="https://img.shields.io/badge/Download-Latest%20Release-60CDFF?style=for-the-badge&logo=windows" alt="Download" />
</a>

| Package | Use |
|---|---|
| `TrueReplayer-win-Setup.exe` | Installs the app and enables **auto-updates** (recommended) |
| `TrueReplayer-win-Portable.zip` | Extract and run — no install, no auto-update |
| `TrueReplayer-ChromeExtension-1.2.0.zip` | Enables browser automation actions (load unpacked in `chrome://extensions`) |

> **Requires** Windows 10 (1809+) or Windows 11 — x64

---

## Highlights

- 🎯 **Precise replay** with Raw Input support — works with games like Roblox
- 🪟 **Window-aware** — lock size, position, and auto-focus a target window before replay
- 🌐 **Browser automation** — click, type, and navigate with CSS selectors (Chrome extension)
- ⌨️ **Hotkeys & hotstrings** to trigger any profile from anywhere
- 📁 **Profiles & folders** with inherited window targets
- 🎨 **Fluent dark UI** with 14 theme presets and full custom colors

---

## Recording & Replay

- **Mouse** — left / right / middle clicks, scroll, drag (press and release captured separately)
- **Keyboard** — all keys including modifiers, function keys, numpad, and symbols
- **Delays** — capture real timing or use a fixed delay; optional **random delay (jitter)**
- **Insert mode** — click any row to record new actions at that position
- **Looping** — repeat count (or infinite) with optional delay between iterations
- **Live replay feedback** — current action highlights, status bar shows progress and elapsed time
- **Clicker mode** — autoclicker with selectable button (left / right / middle)

## Action Table

- **Inline editing** — double-click any cell to edit delay, coordinates, key, or notes
- **Sheet panel** — double-click a row to open a detailed side editor
- **Drag & drop** — reorder single or multiple rows with grip handles
- **Multi-selection** — `Ctrl`+click, `Shift`+click, or `Ctrl`+A
- **Bulk operations** — update delay, coordinates, or notes across all selected rows
- **Select Similar** — select every action of the same type with one click
- **Column visibility** — show/hide columns from the toolbar
- **Copy & Paste between profiles** — transfer actions between any two profiles
- **Undo / Redo** — full history with `Ctrl+Z` / `Ctrl+Y`

## Window Target

Lock a profile to a specific application window for reliable, stateless replay.

<p align="center">
  <img src="Image%20App/TargetConfig.png" alt="Target Configuration dialog" width="780" />
</p>

- **Click-to-detect** — click any window to capture its process and title
- **Match modes** — `Contains` or regex against the window title
- **Relative Coordinates** — record clicks relative to the window, so it replays correctly even if the window moves
- **Lock Size** — saves the window's width/height on recording and restores them before replay
- **Lock Position** — saves the window's X/Y and restores it alongside the size *(new in 1.9.41)*
- **Bring to Focus** — auto-focus the target window before replaying, preserving maximized/fullscreen state
- **Update Window Size & Position** — recapture geometry without re-recording
- **Convert Coordinates** — bulk-convert actions between absolute and window-relative

## Profiles & Folders

- **JSON profile files** — stored under `Documents\TrueReplayer\Profiles`
- **Folders** — group profiles visually with custom colors; collapse / disable whole folders
- **Inherited settings** — folders can define the window target, relative coords, and bring-to-focus — all profiles inside inherit automatically
- **Hotkeys** — assign a keyboard shortcut to instantly trigger a profile
- **Hotstrings** — type a sequence (e.g. `/hello`) to auto-fire a profile (instant or terminator mode)
- **Import / Export** — share profiles as `.trprofile` files, with folder organization and images preserved
- **Search** — filter profiles by name instantly
- **Unsaved changes guard** — prompts before switching or closing

## Send Text

Insert blocks of text as typed keystrokes with dynamic content.

<p align="center">
  <img src="Image%20App/SendText.png" alt="Send Text dialog" width="780" />
</p>

- **Emoji picker** — search and insert any emoji
- **Dynamic variables** — `{clipboard}`, `{date}`, `{time}`, `{datetime}`
- **Special keys** — `{enter}`, `{tab}`, `{backspace}`
- **Snippets** — save and reuse frequent text blocks

## Browser Automation

Drive Chrome-based browsers with the TrueReplayer extension. Uses CSS selectors instead of fragile screen coordinates.

| Action | What it does |
|---|---|
| **Browser Click / Right Click** | Click an element by CSS selector or visible text |
| **Browser Input Text** | Type into an input, with `{clipboard}` / `{date}` / `{time}` / `{datetime}` placeholders |
| **Browser Wait** | Wait for an element to appear before proceeding |
| **Browser Navigate** | Open a URL in the current tab or a new tab |

- **Visual Pick Element** — click anywhere in the page to capture a robust CSS selector
- **Text Match** — match by visible text (e.g. `Submit`) as an alternative to selectors
- **Auto-detect inputs** — clicking an input field during recording creates an Input Text action automatically
- **Reliable reconnect** — alarm-based keep-alive, reconnects cleanly after Chrome idles

> 📘 Setup guide: see [`docs/extension-setup/`](docs/extension-setup/)

## Appearance

Personalize the interface with 14 presets or fully custom colors.

<p align="center">
  <img src="Image%20App/Themes.png" alt="Theme Editor" width="780" />
</p>

- **Presets** — Midnight, Carbon, Amethyst, Emerald, Rose, Ocean, Amber, Slate, Nord, Dracula, Monokai, Copper, Sakura, Neon
- **Custom colors** — accent, semantic (recording red, replay green), action-type pill colors
- **Mono font** — Consolas, Cascadia Mono, Cascadia Code, Courier New, Lucida Console
- **Import / Export** themes as JSON

## Command Palette

Press `Ctrl+K` for fuzzy search across commands, profiles, and settings — everything reachable without the mouse.

## Settings

| Section | Options |
|---|---|
| **Execution** | Fixed delay, loop count, loop interval, random delay (jitter), clicker button |
| **Recording** | Toggle mouse clicks, scroll, keyboard, profile keys, browser actions |
| **Hotkeys** | Recording, replay, profile-keys toggle, bring-to-foreground |
| **Window** | Always on top, system tray, run on startup, start minimized, run as administrator |
| **Updates** | Auto-check on launch, manual check |

## Quality of Life

- **Auto-updates** — checks and installs in the background on launch *(installer builds)*
- **Multi-monitor** — coordinates work across all displays
- **System tray** — minimize to tray; global **Bring to Foreground** hotkey restores from tray *(new in 1.9.41)*
- **Auto-recovery** — if the UI crashes, the app reloads itself within 5 seconds
- **Escape closes menus** — context menus and dropdowns dismiss with `Esc`
- **Toast notifications** — stacked success / error / info messages
- **Unsaved changes guard** — never lose work to an accidental close
- **WebView2 runtime check** — prompts to install if missing

---

## Default Hotkeys

| Action | Key |
|---|---|
| Start / Stop Recording | `Ctrl+PageUp` |
| Start / Stop Replay | `Ctrl+PageDown` |
| Toggle Profile Keys | `Pause` |
| Bring to Foreground | `Ctrl+Insert` |
| Command Palette | `Ctrl+K` |
| Undo / Redo | `Ctrl+Z` / `Ctrl+Y` |

All hotkeys can be remapped in **Settings → Hotkeys**.

---

## System Requirements

- Windows 10 version 1809 or later / Windows 11 — x64 only
- [Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/) (bundled on Windows 11; prompted on Windows 10)
- ~500 MB disk space (self-contained .NET 8 runtime — no install required)
