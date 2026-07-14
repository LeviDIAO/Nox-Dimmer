# Nox-Dimmer — Taskbar-Covering Patch

> 🇺🇸 English | 🇨🇳 [中文](#中文-readme)

A patched variant of [**YashvardhanG/Nox-Dimmer**](https://github.com/YashvardhanG/Nox-Dimmer) that makes the **Hyper Mode overlay cover the entire screen including the taskbar**, while keeping it visible & clickable underneath (click-through transparent layer).

## What This Patch Changes

The original Nox-Dimmer's Hyper Mode deliberately excludes the taskbar area from its overlay (`rcWork` / work area), leaving the taskbar noticeably brighter than the rest of the screen in low-light environments. This patch:

1. **`Nox.py` line ~199**: Changes `info.rcWork` → `info.rcMonitor` so the black overlay covers the full monitor rectangle, including the taskbar.
2. **`Nox.py` line ~234**: Adds `-toolwindow` attribute to prevent the overlay window from briefly appearing in the taskbar on first activation.
3. UI label updated: "Hyper Mode (Taskbar Visible)" → "Hyper Mode (Covers Taskbar)".

**Total: 3 lines changed.** Everything else — hotkeys, multi-monitor support, tray icon, gamma enforcement — is identical to upstream v1.4.

## Why

When using an external monitor (e.g., HKC P272U Pro) in a low-light environment, even at minimum hardware brightness + Twinkle Tray DDC/CI control, the screen can still feel too bright. The original Hyper mode gets close to OLED-level darkness but leaves the taskbar glowing. This patch fixes that gap.

## Building From Source

```bash
git clone https://github.com/LeviDIAO/Nox-Dimmer.git
cd Nox-Dimmer
pip install -r requirements.txt
pyinstaller --noconfirm --onefile --windowed --icon=nox_icon.ico \
  --add-data "nox_icon.ico;." \
  --hidden-import pystray --hidden-import pystray._win32 \
  --hidden-import screeninfo --hidden-import keyboard \
  --hidden-import PIL --hidden-import PIL.ImageDraw --hidden-import PIL.ImageTk \
  --name "Nox-Dimmer-Patched" Nox.py
```

## Download

Pre-built single-file executable (v2 — taskbar-covering Hyper mode + taskbar-flash fix): [`dist/Nox-Dimmer-Patched.exe`](dist/Nox-Dimmer-Patched.exe). No install needed — just run it. Built from the `Nox.py` in this repo.

## Credits & License

- **Original author**: [Yashvardhan Gupta](https://github.com/YashvardhanG) ([@YashvardhanG](https://github.com/YashvardhanG))
- **Original project**: https://github.com/YashvardhanG/Nox-Dimmer
- **Patch maintainer**: LeviDIAO
- **License**: MIT (see [`LICENSE`](LICENSE) — original license preserved unchanged)

---

# 中文 README

> 🇨🇳 中文 | 🇺🇸 [English](#nox-dimmer--taskbar-covering-patch)

本项目是 [**YashvardhanG/Nox-Dimmer**](https://github.com/YashvardhanG/Nox-Dimmer) 的一个**修改版**，让 **Hyper 模式的黑色遮罩覆盖整个屏幕（含任务栏）**，同时保持任务栏**仍然可见、仍然可点击**（遮罩是点击穿透的半透明层）。

## 这个补丁改了什么

原版 Nox-Dimmer 的 Hyper 模式刻意把任务栏区域排除在遮罩之外（用的是 `rcWork` / 工作区），导致在光线较暗的环境下，任务栏比屏幕其余部分明显更亮。本补丁做了三处修改：

1. **`Nox.py` 约第 199 行**：把 `info.rcWork` 改为 `info.rcMonitor`，让黑色遮罩覆盖整块显示器（含任务栏）。
2. **`Nox.py` 约第 234 行**：增加 `-toolwindow` 属性，防止遮罩窗口在首次开启时短暂出现在任务栏上。
3. 界面文案更新："Hyper Mode (Taskbar Visible)" → "Hyper Mode (Covers Taskbar)"（覆盖任务栏）。

**总共只改了 3 行。** 其余功能——快捷键、多显示器独立控制、托盘图标、伽马值强制——都与原版 v1.4 完全一致。

## 为什么需要它

在光线较暗的环境中使用外接显示器（例如 HKC P272U Pro）时，即便把硬件亮度拉到最低、再用 Twinkle Tray 走 DDC/CI 控制，屏幕依然太亮。原版的 Hyper 模式已经接近 OLED 级的纯黑，却唯独留下任务栏在发光。这个补丁填补了这个缺口。

## 从源码构建

```bash
git clone https://github.com/LeviDIAO/Nox-Dimmer.git
cd Nox-Dimmer
pip install -r requirements.txt
pyinstaller --noconfirm --onefile --windowed --icon=nox_icon.ico \
  --add-data "nox_icon.ico;." \
  --hidden-import pystray --hidden-import pystray._win32 \
  --hidden-import screeninfo --hidden-import keyboard \
  --hidden-import PIL --hidden-import PIL.ImageDraw --hidden-import PIL.ImageTk \
  --name "Nox-Dimmer-Patched" Nox.py
```

## 下载

预编译的单文件可执行程序（v2——覆盖任务栏的 Hyper 模式 + 修复任务栏闪烁）：[`dist/Nox-Dimmer-Patched.exe`](dist/Nox-Dimmer-Patched.exe)。无需安装，直接运行即可。由本仓库中的 `Nox.py` 构建而来。

## 致谢与许可

- **原作者**：[Yashvardhan Gupta](https://github.com/YashvardhanG)（[@YashvardhanG](https://github.com/YashvardhanG)）
- **原项目**：https://github.com/YashvardhanG/Nox-Dimmer
- **补丁维护者**：LeviDIAO
- **许可协议**：MIT（见 [`LICENSE`](LICENSE)——原始许可证内容未作改动，完整保留）
