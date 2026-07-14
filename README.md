# Nox-Dimmer — Taskbar-Covering Patch

A patched variant of [**YashvardhanG/Nox-Dimmer**](https://github.com/YashvardhanG/Nox-Dimmer) that makes the **Hyper Mode overlay cover the entire screen including the taskbar**, while keeping it visible & clickable underneath (click-through transparent layer).

## What This Patch Changes

The original Nox-Dimmer's Hyper Mode deliberately excludes the taskbar area from its overlay (`rcWork` / work area), leaving the taskbar noticeably brighter than the rest of the screen in low-light use cases. This patch:

1. **`Nox.py` line ~199**: Changes `info.rcWork` → `info.rcMonitor` so the black overlay covers the full monitor rectangle, including the taskbar.
2. **`Nox.py` line ~234**: Adds `-toolwindow` attribute to prevent the overlay window from briefly appearing in the taskbar on first activation.
3. UI label updated: "Hyper Mode (Taskbar Visible)" → "Hyper Mode (Covers Taskbar)".

**Total: 3 lines changed.** Everything else — hotkeys, multi-monitor support, tray icon, gamma enforcement — is identical to upstream v1.4.

## Why

When using an external monitor (e.g., HKC P272U Pro) in a low-light environment, even at minimum hardware brightness + Twinkle Tray DDC/CI control, the screen is still too bright. The original Hyper mode gets close to OLED-level darkness but leaves the taskbar glowing. This patch fixes that gap.

## Building From Source

```bash
git clone https://github.com/YashvardhanG/Nox-Dimmer.git
# Apply the 3-line patch above, or use this fork's Nox.py
pip install -r requirements.txt
pyinstaller --noconfirm --onefile --windowed --icon=nox_icon.ico \
  --add-data "nox_icon.ico;." \
  --hidden-import pystray --hidden-import pystray._win32 \
  --hidden-import screeninfo --hidden-import keyboard \
  --hidden-import PIL --hidden-import PIL.ImageDraw --hidden-import PIL.ImageTk \
  --name "Nox-Dimmer-Patched" Nox.py
```

## Download

Grab the pre-built executable from [Releases](../../releases). Single-file, no install needed.

## Credits & License

- **Original author**: [Yashvardhan Gupta](https://github.com/YashvardhanG) ([@YashvardhanG](https://github.com/YashvardhanG))
- **Original project**: https://github.com/YashvardhanG/Nox-Dimmer
- **Patch maintainer**: LeviDIAO
- **License**: MIT (see [`LICENSE`](LICENSE) — original license preserved unchanged)
