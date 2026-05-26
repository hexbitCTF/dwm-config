# dwm

My personal build of [dwm](https://dwm.suckless.org/) 6.6 — the dynamic window manager for X.

## Patches Applied

| Patch | Description |
| :--- | :--- |
| [attachbottom](https://dwm.suckless.org/patches/attachbottom/) | New windows attach at the bottom of the stack |
| [splitstatus](https://dwm.suckless.org/patches/splitstatus/) | Splits status text at a delimiter for modular bar |
| [statuscmd](https://dwm.suckless.org/patches/statuscmd/) | Adds clickability to status bar (used by dwmblocks) |
| [swapfocus](https://dwm.suckless.org/patches/swapfocus/) | `Alt+Tab` toggles between the two most recent clients |
| [vanitygaps](https://dwm.suckless.org/patches/vanitygaps/) | Configurable gaps between and around windows |

## Custom Config

- **Font:** JetBrainsMono Nerd Font (16px) + Noto Color Emoji
- **Color scheme:** Dark blue ocean (`#011423` bg, `#0FC5ED` accent)
- **4 tags:** 🏠 🔒 📖 📝 (house, lock, book, pencil)
- **Gaps:** 7px inner, 5px outer, smart gaps enabled
- **Scratchpad:** Floating `st` terminal toggled with `Super+grave`
- **Status bar:** `dwmblocks` (set via `STATUSBAR` macro)
- **Keybindings:** Super key as MODKEY, dmenu for app launcher, vim-style navigation

## Installation

```sh
sudo make clean install
```

## Requirements

- Xlib headers
- libXinerama (optional, for multi-monitor)
- libXft + fontconfig (for font rendering)
