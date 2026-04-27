<p align="right">
  <sub><b>English</b> &nbsp;·&nbsp; <a href="README.pt-BR.md">Português (BR)</a></sub>
</p>

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
  <img src="Image%20App/Main%20Window.png" alt="TrueReplayer main window" width="900" />
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
- 🔗 **Profile chaining** — call other profiles inline with cycle detection and repeat count
- ⚡ **Trigger Modes** — OnPress, OnRelease, WhilePressed, Toggle for hotkey behavior
- 🌐 **Browser automation** — click, type, and navigate with CSS selectors (Chrome extension)
- ⌨️ **Hotkeys & hotstrings** to trigger any profile from anywhere
- 📁 **Profiles & folders** with inherited window targets
- 🎨 **Fluent dark UI** with 23 theme presets and full custom colors

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
- **Skip** — temporarily exclude selected actions from replay without deleting them; skipped rows render dimmed and the state is saved with the profile
- **Select Similar** — select every action of the same type with one click
- **Column visibility** — show/hide columns from the toolbar
- **Copy & Paste between profiles** — transfer actions between any two profiles
- **Undo / Redo** — full history with `Ctrl+Z` / `Ctrl+Y`

## Window Target

Lock a profile to a specific application window for reliable, stateless replay.

<p align="center">
  <img src="Image%20App/Target%20Configuration.png" alt="Target Configuration dialog" width="780" />
</p>

- **Click-to-detect** — click any window to capture its process and title
- **Match modes** — `Contains` or regex against the window title
- **Relative Coordinates** — record clicks relative to the window, so it replays correctly even if the window moves
- **Lock Size** — saves the window's width/height on recording and restores them before replay
- **Lock Position** — saves the window's X/Y and restores it alongside the size
- **Bring to Focus** — auto-focus the target window before replaying, preserving maximized/fullscreen state
- **Update Window Size & Position** — recapture geometry without re-recording
- **Convert Coordinates** — bulk-convert actions between absolute and window-relative

## Profiles & Folders

- **JSON profile files** — stored under `Documents\TrueReplayer\Profiles`
- **Folders** — group profiles visually with custom colors; collapse / disable whole folders
- **Inherited settings** — folders can define the window target, relative coords, and bring-to-focus — all profiles inside inherit automatically
- **Hotkeys** — assign a keyboard shortcut to instantly trigger a profile
- **Hotstrings** — type a sequence (e.g. `/hello`) to auto-fire a profile (instant or terminator mode)
- **Trigger Modes** — choose how the hotkey behaves (see below)
- **Import / Export** — share profiles as `.trprofile` files, with folder organization and images preserved
- **Search** — filter profiles by name instantly
- **Unsaved changes guard** — prompts before switching or closing

## Trigger Modes

Each profile chooses how its hotkey actually fires the macro.

<p align="center">
  <img src="Image%20App/Triggers.png" alt="Trigger Modes" width="780" />
</p>

| Mode | Behavior |
|---|---|
| **On Press** | Fires once when the hotkey is pressed (default) |
| **On Release** | Fires once when the hotkey is released — the down event is swallowed |
| **While Pressed** | Holds the hotkey to keep replaying in an infinite loop; releasing cancels |
| **Toggle** | First press starts the replay, second press stops it |

- Combined hotkeys (e.g. `Alt+Q`) are supported in every mode
- Modifier release order doesn't matter for `On Release` (`Alt↓ Q↓ Q↑ Alt↑` and `Alt↓ Q↓ Alt↑ Q↑` both fire correctly)
- Auto-repeat protection prevents the OS keyboard repeat from spamming `On Press` triggers

## Profile Chaining

Reuse profiles as building blocks. The new **Run Profile** action invokes another profile inline at any point in the macro.

<p align="center">
  <img src="Image%20App/Run%20Profile.png" alt="Run Profile dialog" width="780" />
</p>

- **Repeat count** — call the sub-profile 1–999 times back-to-back per action
- **Cycle detection** — `A → B → A` is blocked at runtime with a diagnostic log entry
- **Max depth** of 5 prevents accidental deep recursion
- **Auto-contained context** — sub-profile uses its own window target, lock position, and relative-coordinate metadata if set; otherwise inherits from the caller
- **Caller restore** — after the sub-profile returns, the caller's window is re-focused so the rest of the parent macro runs against the right target
- **Cancel propagation** — Stop ends the entire chain instantly
- **Live status** — the status bar shows `Running A → B → C` while a sub-profile executes

## Edit Text

Insert blocks of text as typed keystrokes with dynamic content and a visual clipboard transformer.

<p align="center">
  <img src="Image%20App/Edit%20Text.png" alt="Edit Text dialog" width="780" />
</p>

- **Emoji picker** — search and insert any emoji
- **Dynamic variables** — `{clipboard}`, `{date}`, `{time}`, `{datetime}`
- **Special keys** — `{enter}`, `{tab}`, `{backspace}`, navigation arrows, repeat suffix `:N`
- **Snippets** — save and reuse frequent text blocks
- **Syntax highlighting** — token recognition for known variables, including chained clipboard modifiers

### Clipboard Transform

Build complex clipboard tokens visually — no syntax to memorize.

<p align="center">
  <img src="Image%20App/Clipboard.png" alt="Clipboard Transform popover" width="420" />
</p>

| Modifier | What it does |
|---|---|
| **Trim** | Strip leading/trailing whitespace |
| **UPPERCASE / lowercase** | Force case |
| **Line #** | Extract a specific line (1-indexed) |
| **Word #** | Extract a specific word |
| **First N / Last N chars** | Slice from the start or the end |

- Modifiers are chained in order (`{clipboard:trim:line:1:first:8}` etc.)
- Live preview shows the actual clipboard content with all transforms applied
- Tokens are highlighted in the editor and round-trip through Edit / Save unchanged

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

Personalize the interface with 23 presets or fully custom colors.

<p align="center">
  <img src="Image%20App/Themes.png" alt="Theme Editor" width="780" />
</p>

- **Theme presets organized by accent hue:**
  - *Neutral* — Carbon, Slate
  - *Pink/Rose* — Rose, Sakura
  - *Orange/Yellow* — Copper, Amber, Gruvbox Dark
  - *Green* — Emerald, Monokai, Neon
  - *Cyan/Blue* — Ocean, Nord, Midnight, One Dark Pro, Night Flat *(default)*, Tokyo Night, GitHub Dark, GitHub Default, Better Solarized
  - *Purple/Violet/Mauve* — Amethyst, Dracula, Catppuccin Mocha, Rosé Pine
- **Custom colors** — accent, semantic (recording red, replay green), every action-type pill (mouse, key, scroll, send-text, wait-image, browser, run-profile)
- **Mono font** — Consolas, Cascadia Mono, Cascadia Code, Courier New, Lucida Console
- **Layout** — font size, border radius, row height, zoom
- **Import / Export** themes as JSON
- **Live preview** — every change applies instantly across the whole UI

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

- **Auto-updates** with changelog preview — see what's new before downloading; nothing installs without your confirmation
- **WebView2 crash recovery** — escalating recovery strategy (Reload → Navigate → Restart) keeps the UI alive even on rare WebView2 failures
- **Diagnostic logs** — file-based session logs in `%LOCALAPPDATA%\TrueReplayer\Logs\` with rotation; quick access via tray menu
- **DevTools shortcut** — open WebView2 DevTools from the tray for inspection
- **Multi-monitor** — coordinates work across all displays
- **System tray** — minimize to tray; global **Bring to Foreground** hotkey restores from tray
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
