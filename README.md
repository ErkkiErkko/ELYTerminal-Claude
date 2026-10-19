# ELYTerminal · Claude

<img src="assets/icons/elyterminal.svg" width="160" alt="Claude 抱着终端的 Q 版图标">

基于 [ELYTerminal](https://git.zacharyzhang.com/Zacharyzhang-NY/ELYTerminal) 的 Claude 娘化定制版。沿用原版 Q 版画风，将窗口动画人物与应用图标改为橘发、琥珀眼、花饰和黑白缎带的 Claude 形象。

## 定制内容

- 保留呼吸、眨眼、发丝摆动、工作、等待、出错、庆祝、犯困和点击回应动画。
- 保留原有位置切换：窗口上方空间足够时位于顶部，空间不足时移到终端内部底部。
- 应用图标同步替换，Windows exe 内含 16 至 256 像素的七种尺寸图标。
- 修复 Windows 角色窗口初始化时同步刷新边框导致的借用错误。
- 在 Settings → Terminal → Claude 中开启或关闭角色，沿用原来的 `ely` 配置键。

## Windows 定制版

[下载最新 Windows 版本](https://github.com/ErkkiErkko/ELYTerminal-Claude/releases/latest)

运行文件为 `ELYTerminal-Claude.exe`，双击即可启动，使用时不需要安装 Rust。压缩包名为 `ELYTerminal-Claude-windows-x64.zip`。

自行编译需要 Rust 1.95.0、Visual Studio C++ Build Tools 和 Windows SDK：

```powershell
cargo build --release --locked
.\target\release\elyterminal.exe
```

本定制版已在 Windows x64 上完成构建、216 项测试、代码检查、启动检查和内嵌图标核对。macOS 和 Linux 构建尚未在本定制版中验证。

GitHub Actions 在推送和拉取请求时检查、测试并构建 Windows 版本，也支持手动运行。构建产物可从 Actions 下载；正式发布文件位于 Releases。

基于上游 `0.1.5` / `3759cf882553561d9dc4d10825f63b6b9c5d457e`，保留原项目的 [MIT 许可证](LICENSE) 和第三方许可证。下面是上游功能与使用说明。

## About ELYTerminal

A terminal for macOS, Windows and Linux, in Rust on GPUI and Ely components. Sessions sit on the left, the terminal in the middle, Git or Files on the right. Every setting has a control in the settings window.

## Upstream installation

The original project's releases on Gitea carry the three builds below, with the original Ely character. They are separate from this Claude customization.

- macOS 11 or later, Apple silicon: open `ELYTerminal-VERSION.dmg` and drag ELYTerminal into Applications. The app is signed with Developer ID and notarized.
- Windows 10 or later, x86_64: unzip `ELYTerminal-VERSION-windows-x86_64.zip` and run `elyterminal.exe`. It is unsigned; if SmartScreen stops it, press More info, then Run anyway.
- Linux, x86_64, glibc 2.35 or later, with libxkbcommon, libxkbcommon-x11 and libxcb:

```sh
tar -xzf ELYTerminal-VERSION-linux-x86_64.tar.gz
cd ELYTerminal-VERSION-linux-x86_64
install -Dm755 elyterminal -t ~/.local/bin
install -Dm644 com.zacharyzhang.elyterminal.desktop -t ~/.local/share/applications
install -Dm644 com.zacharyzhang.elyterminal.svg -t ~/.local/share/icons/hicolor/scalable/apps
```

The desktop entry runs `elyterminal`, so `~/.local/bin` must be on `PATH`.

## Build and run

Rust 1.95.0, which `rust-toolchain.toml` pins; rustup installs it on the first build.

```sh
cargo run --release
```

Each platform's script builds its release in `target/release`: on macOS, `scripts/mac-app.sh` builds `ELYTerminal.app`, with its icon, and a disk image of it; on Windows, `scripts/windows-zip.ps1` zips `elyterminal.exe`, its icon inside; on Linux, `scripts/linux-tar.sh` builds in Docker and packs the binary with its desktop entry and icon.

On Linux, install the libraries gpui links first. On Debian and Ubuntu:

```sh
sudo apt-get install pkg-config libwayland-dev libxkbcommon-dev libxkbcommon-x11-dev \
  libxcb1-dev libx11-xcb-dev libfontconfig-dev libfreetype-dev
```

The app writes its log to stderr. `RUST_LOG=elyterminal=debug` writes more; `trace` logs each paint. A Windows release build opens no console: `elyterminal.exe 2> log.txt` keeps its log.

## What it does

- The terminal runs on `alacritty_terminal`: 256 colors and truecolor, bold, dim, italic, five underline styles, wide characters and combining marks. Box drawing, block elements and powerline shapes are drawn as geometry, so lines join across cells. Keys follow xterm and the kitty keyboard protocol, and on Windows win32-input-mode, as Windows Terminal sends them, so herdr's shortcuts work; input methods compose at the cursor; programs can track the mouse; pastes are bracketed when a program asks; OSC 8 and plain links open with the link press below; inside herdr, herdr opens them, web links only, whole where its pane wraps them, and with Shift the terminal opens what it sees; find searches the scrollback.
- Shell integration for zsh, bash, fish and PowerShell: each prompt reports its folder and title, and OSC 133 marks each prompt, each command and its exit status.
- Claude, with copper-orange hair, amber eyes, flower ornaments and ivory-and-black ribbons in Ely's chibi style, peeks over the window's top edge, or up from its bottom left when the window leaves her no room above it, and moves all the time: she breathes, sways and blinks. She follows your sessions: she hops when a program waits on you, shakes at an error, cheers a finish, reads along while a program works, and dozes when all is calm for long. Press her and she winks, waking her from a doze. Settings › Terminal › Claude turns her off. The existing `ely` setting still controls her.
- Sessions: new, close and switch. A bell marks a hidden session's row and makes no sound. A row's mark shows what its programs report through OSC 7501, OSC 9;4 or herdr: waiting on you, an error, work with its progress, done or idle, else a failed last command. The mark is 3 by 3 dots: work ripples and waiting dips while they last. Hover over the mark lists each report.
- Notifications: while the window is in the background or the session hidden, a session that starts waiting, finishes or fails, and a program's OSC 9, 777 or 99, post a system notification, one a session every 3 seconds at most; a press shows the session. On macOS only the app bundle posts them, not `cargo run`.
- Cmd-Up and Cmd-Down, Ctrl-Shift-Up and Ctrl-Shift-Down off macOS, jump to the prompt before or after the view's top.
- A button at each end of the title bar hides or shows its side column, and a drag on the border between a side column and the terminal resizes it; the window opens as it was left, at the size and widths it was left at. On Windows and Linux a gear beside the right one opens Settings.
- Files shows the session's folder as a tree with Git's marks. Inside herdr the folder is that of herdr's focused pane.
- Git shows the branch, stages, unstages, discards, commits, lists recent commits and opens diffs, all through the `git` command line.
- Themes: Ely Dark, Ely Light, Catppuccin Mocha, Macchiato, Frappé and Latte, Tokyo Night, Dracula, Nord, Gruvbox Dark, Rosé Pine, Solarized Light, One Light and Kanagawa Wave. A second theme can take over while the system is dark. On Omarchy 4, an Omarchy theme follows the system's theme as it switches, and is the default there.
- Background opacity and blur: NSVisualEffectView on macOS, acrylic on Windows, `ext_background_effect_v1` or `org_kde_kwin_blur` on Wayland, `_KDE_NET_WM_BLUR_BEHIND_REGION` on X11, which KWin reads. Blur shows only while the opacity is under 100%. Hyprland blurs only while its own `decoration:blur:enabled` is on, and Omarchy 4.0.4 turns it off; to turn it on there, add `hl.config({ decoration = { blur = { enabled = true } } })` to `~/.config/hypr/looknfeel.lua`.

## Keys

Settings › Terminal lists them all, as this platform binds them.

| | macOS | Windows and Linux |
|---|---|---|
| New session | Cmd-T | Ctrl-Shift-T |
| Close session | Cmd-W | Ctrl-Shift-W |
| Session 1 to 8, last | Cmd-1 to Cmd-8, Cmd-9 | Alt-1 to Alt-8, Alt-9 |
| Next, previous session | Ctrl-Tab, Ctrl-Shift-Tab | Ctrl-Tab, Ctrl-Shift-Tab |
| Sessions column | Cmd-B | Ctrl-Shift-B |
| Right column | Cmd-Alt-B | Ctrl-Shift-Alt-B |
| Copy, paste | Cmd-C, Cmd-V | Ctrl-Shift-C, Ctrl-Shift-V; on Windows Ctrl-V pastes too |
| Select all | Cmd-A | Ctrl-Shift-A |
| Find | Cmd-F | Ctrl-Shift-F |
| Bigger, smaller, reset size | Cmd-=, Cmd-minus, Cmd-0 | Ctrl-=, Ctrl-minus, Ctrl-0 |
| Open a link | Cmd-press | Ctrl-press |
| Settings | Cmd-, | Ctrl-, |
| Minimize | Cmd-M | |
| Quit | Cmd-Q | Ctrl-Shift-Q |

## Settings

The settings window saves each change at once to `settings.json` in the platform's config folder:

- macOS: `~/Library/Application Support/ELYTerminal/settings.json`
- Linux: `$XDG_CONFIG_HOME/ELYTerminal/settings.json`, else `~/.config/ELYTerminal/settings.json`
- Windows: `%APPDATA%\ELYTerminal\settings.json`

A file that does not parse, or holds a value out of range, stops the start with an error naming the file and the field. The app never overwrites it.

## Development

`scripts/check.sh` runs fmt, clippy, the tests and the 500-line rule. `AGENTS.md` lists the rest: the layout, the decisions and the tools.

## License

MIT, in `LICENSE`. Box drawing and key encoding follow Ghostty's code, MIT, in `LICENSE-GHOSTTY`. The theme files come from iTerm2-Color-Schemes, MIT, with its license in `assets/themes`. JetBrains Mono and its Nerd Font build are under the SIL Open Font License, in `assets/fonts`.
