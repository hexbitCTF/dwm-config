# dwm

My personal build of [dwm](https://dwm.suckless.org/) 6.6 — the dynamic window manager for X.

## Patches Applied

| Patch | Description |
| :--- | :--- |
| [attachbottom](https://dwm.suckless.org/patches/attachbottom/) | New windows attach at the bottom of the stack instead of the top |
| [splitstatus](https://dwm.suckless.org/patches/splitstatus/) | Splits status text at a delimiter (`;`) to prevent block overlap with modular bars |
| [statuscmd](https://dwm.suckless.org/patches/statuscmd/) | Passes mouse button and x-coordinate to the status script, enabling clickable blocks in dwmblocks |
| [swapfocus](https://dwm.suckless.org/patches/swapfocus/) | `Alt+Tab` toggles focus between the two most recently used clients |
| [vanitygaps](https://dwm.suckless.org/patches/vanitygaps/) | Configurable inner/outer gaps between windows and screen edges, with smart gap auto-hide |

## Bar Transparency (Super+T)

This build implements a **per-pixel alpha transparency effect** for the dwm bar using a 32-bit ARGB visual. When an ARGB-compatible compositor (like picom) is running:

- **`Super+T`** toggles bar transparency on/off
- The bar background uses 60% opacity (`alpha = 0x9999`) — dark enough to be readable, transparent enough to see wallpaper
- Transparency is **smart**: the bar only becomes transparent when no windows occupy the current tag, or when the floating layout (`><>`) is active. This keeps the bar opaque over tiled windows for readability
- The effect is purely visual — it does not affect window borders, only the bar background (`SchemeBarNorm`)

The implementation works by:
1. Detecting a 32-bit ARGB visual at startup via `XMatchVisualInfo`
2. Creating the bar window with that visual and a transparent background pixel
3. Applying an XRender color with `alpha = 0x9999` (60%) to the bar background scheme
4. Toggling a `transparentbar` flag on `Super+T` that controls whether the alpha value is used during draw

## Tags

The workspace system uses 9 tag slots, with 8 currently named:

| Slot | Tag | Primary Use |
| :--: | :-: | :---------- |
| 1 | 🏠 | Home — general desktop, personal apps |
| 2 | 🛡️ | Security — pentesting tools, CTF, cybersecurity lab |
| 3 | 🎮 | Gaming — Steam, Lutris, game launchers |
| 4 | 📖 | Study — notes, ebooks, research papers |
| 5 | 🌐 | Browse — Firefox, web browsing |
| 6 | 💻 | Dev — code editors, terminals, IDE |
| 7 | 🔒 | Private — encrypted/secure applications |
| 8 | 📝 | Docs — documents, writing, office |
| 9 | | Available for custom use |

Tags are navigated with `Super+[1-9]`. Windows can be moved between tags with `Super+Shift+[1-9]`. Applications can be assigned to specific tags via the `rules[]` array in `config.h`.

## Layouts

| Key | Layout | Description |
| :-: | :----- | :---------- |
| `Super+Shift+T` | `[]=` (tile) | Master-stack layout (default) |
| `Super+Shift+F` | `><>` (floating) | All windows float freely |
| `Super+Shift+M` | `[M]` (monocle) | All windows maximized |

## Custom Config

- **Font:** JetBrainsMono Nerd Font (14px) + Noto Color Emoji (14px)
- **Color scheme:** Dark blue ocean (`#011423` bg, `#0FC5ED` blue accent, `#CBE0F0` text, `#214969` inactive border)
- **Border width:** 2px
- **Gaps:** 7px inner, 5px outer, smart gaps enabled (auto-hide outer gaps when only one window)
- **Master factor:** 0.55 (55% of screen for master area)
- **Scratchpad:** Floating `st` terminal (120x34) toggled with `Super+grave`
- **Status bar:** `dwmblocks` (set via `STATUSBAR` macro, statuscmd-aware clickable blocks)
- **dmenu:** Dark theme matching dwm (`col_bg`, `col_fg`, `col_accent` passed as flags)
- **Keybindings:** Super key as MODKEY, vim-style `h/l` for focus, `Super+Shift+Up/Down` for master count

## Installation

```sh
sudo make clean install
```

## Requirements

- Xlib headers
- libXinerama (optional, multi-monitor support)
- libXft + fontconfig (font rendering)
- XRender (for bar alpha transparency)
- A compositor like picom (to see transparency effects)
