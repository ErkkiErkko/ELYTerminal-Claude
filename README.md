# ELYTerminal · Claude

**简体中文** | [English](README.en.md)

<img src="assets/icons/elyterminal.svg" width="160" alt="Claude 抱着终端的 Q 版图标">

基于 [ELYTerminal](https://git.zacharyzhang.com/Zacharyzhang-NY/ELYTerminal) 的 Claude 娘化定制版。沿用原版 Q 版画风，将窗口上的动画人物和应用图标换成橘色长发、琥珀眼睛、花饰与黑白缎带的 Claude 形象。

终端使用 Rust、GPUI 和 Ely 组件构建，布局为左侧会话、中间终端、右侧 Git 或文件面板。各项设置均可在设置窗口中调整。

## 下载与运行

[下载最新版本](https://github.com/ErkkiErkko/ELYTerminal-Claude/releases/latest)

当前提供 **Windows x64** 定制版：

1. 下载 `ELYTerminal-Claude.exe`，或下载并解压 `ELYTerminal-Claude-windows-x64.zip`。
2. 双击 `ELYTerminal-Claude.exe` 启动，使用时不需要安装 Rust。
3. 在 **Settings → Terminal → Claude** 中开启或关闭动画人物。

发布页也提供源码包、相对上游的补丁和 `SHA256SUMS.txt` 校验文件。便携压缩包包含项目及第三方许可证。

本定制版已在本机 Windows x64 环境中完成 Release 构建、216 项 Rust 测试、格式与 clippy 检查、启动检查和内嵌图标核对。启动检查以隐藏窗口运行，确认角色与 PowerShell 提示符正常加载。

源码保留了 macOS 和 Linux 支持，但本定制版尚未在这两个平台验证，也未提供对应的定制安装包。上游发布的安装包仍使用原版 Ely 形象。

## Claude 定制内容

- **人物外观：**橘色长发、琥珀眼睛、花朵头饰、黑白缎带、流苏耳饰和花朵胸针，保持原版 Q 版比例与扁平色块画风。
- **动画与状态：**保留呼吸、眨眼、发丝摆动、工作、等待、出错、庆祝、犯困和点击回应。点击人物会眨眼回应，也能将她从犯困状态唤醒。
- **窗口位置：**保留上游逻辑——上方空间足够时位于窗口顶部；空间不足时移到终端内部的底部，避免显示到屏幕外。
- **应用图标：**使用同一 Claude 形象抱着终端的构图。Windows exe 内嵌 16、24、32、48、64、128、256 像素七种透明背景图标。
- **Windows 修复：**延后角色窗口的边框刷新，修复初始化时同步回调导致的借用错误，并补充回归验证。
- **设置兼容：**显示名称改为 Claude，原来的 `ely` 配置键继续有效。

## 终端功能

- **终端显示：**基于 `alacritty_terminal`，支持 256 色、真彩色、粗体、斜体、暗色、五种下划线样式、宽字符和组合字符。框线、块状字符和 Powerline 分隔符采用几何绘制，减少单元格间的缝隙。
- **输入与链接：**支持 xterm 和 kitty 键盘协议、Windows 的 win32-input-mode、输入法、鼠标报告、括号粘贴、OSC 8 链接、普通网址识别和滚动历史搜索。通过下方快捷键打开链接；在 herdr 中，链接由 herdr 处理，加按 Shift 可由终端直接打开。
- **Shell 集成：**支持 zsh、bash、fish 和 PowerShell，报告当前目录、标题、提示符、命令及退出状态。
- **会话管理：**创建、关闭和切换会话；状态标记显示工作进度、等待输入、完成或错误等状态。悬停可查看详细报告，后台会话的响铃会留下视觉标记而不播放声音。
- **文件与 Git：**文件树显示当前会话目录及 Git 状态；Git 面板支持查看分支、暂存、取消暂存、丢弃修改、提交、历史记录和差异。在 herdr 中，目录跟随其当前聚焦的面板。
- **布局：**侧栏可隐藏或调整宽度，窗口尺寸和侧栏宽度会保存。Windows 和 Linux 可通过齿轮按钮打开设置。
- **通知与导航：**支持后台会话的系统通知，可点击返回对应会话；可跳转到上一个或下一个提示符。macOS 系统通知需要从应用包运行，`cargo run` 不支持。
- **主题：**内置 Ely Dark/Light、Catppuccin Mocha/Macchiato/Frappé/Latte、Tokyo Night、Dracula、Nord、Gruvbox Dark、Rosé Pine、Solarized Light、One Light 和 Kanagawa Wave，可设置随系统深色模式切换的主题。在 Omarchy 4 上可跟随系统主题。
- **透明与模糊：**macOS 使用 NSVisualEffectView，Windows 使用亚克力效果，Wayland/X11 使用合成器提供的模糊接口。透明度低于 100% 时才显示模糊，Linux 还需要合成器开启相应功能。

## 快捷键

设置窗口的 **Settings → Terminal** 页面会列出当前平台的快捷键。

| 操作 | macOS | Windows / Linux |
|---|---|---|
| 新建会话 | Cmd-T | Ctrl-Shift-T |
| 关闭会话 | Cmd-W | Ctrl-Shift-W |
| 会话 1–8 / 最后一个 | Cmd-1 至 Cmd-8 / Cmd-9 | Alt-1 至 Alt-8 / Alt-9 |
| 下一个 / 上一个会话 | Ctrl-Tab / Ctrl-Shift-Tab | Ctrl-Tab / Ctrl-Shift-Tab |
| 显示或隐藏会话栏 | Cmd-B | Ctrl-Shift-B |
| 显示或隐藏右侧栏 | Cmd-Alt-B | Ctrl-Shift-Alt-B |
| 复制 / 粘贴 | Cmd-C / Cmd-V | Ctrl-Shift-C / Ctrl-Shift-V；Windows 也支持 Ctrl-V |
| 全选 | Cmd-A | Ctrl-Shift-A |
| 搜索 | Cmd-F | Ctrl-Shift-F |
| 放大 / 缩小 / 重置字号 | Cmd-= / Cmd-minus / Cmd-0 | Ctrl-= / Ctrl-minus / Ctrl-0 |
| 打开链接 | Cmd-单击 | Ctrl-单击 |
| 上一个 / 下一个提示符 | Cmd-Up / Cmd-Down | Ctrl-Shift-Up / Ctrl-Shift-Down |
| 设置 | Cmd-, | Ctrl-, |
| 最小化 | Cmd-M | — |
| 退出 | Cmd-Q | Ctrl-Shift-Q |

## 从源码构建

### Windows

需要 Rust 1.95.0、Visual Studio C++ Build Tools 和 Windows SDK。`rust-toolchain.toml` 固定了 Rust 版本，rustup 会按该文件选择工具链。

在已配置 C++ 工具链的 **Developer PowerShell for Visual Studio** 中运行：

```powershell
git clone https://github.com/ErkkiErkko/ELYTerminal-Claude.git
cd ELYTerminal-Claude
cargo build --release --locked
.\target\release\elyterminal.exe
```

本地构建生成的程序名为 `elyterminal.exe`；发布页中的程序重命名为 `ELYTerminal-Claude.exe`。

### macOS 和 Linux

源码构建命令：

```sh
cargo run --release --locked
```

Debian / Ubuntu 需先安装构建依赖：

```sh
sudo apt-get install pkg-config libwayland-dev libxkbcommon-dev libxkbcommon-x11-dev \
  libxcb1-dev libx11-xcb-dev libfontconfig-dev libfreetype-dev
```

仓库保留了上游的打包脚本，产物写入 `target/release`：

| 脚本 | 用途 |
|---|---|
| `scripts/windows-zip.ps1` | 构建 Windows exe 并打包 ZIP |
| `scripts/mac-app.sh` | 构建 macOS 应用包和磁盘映像；签名、公证需要自行配置 |
| `scripts/linux-tar.sh` | 在 Docker 中构建 Linux 程序并打包桌面入口和图标 |

这些脚本沿用上游的产物命名方式；macOS 和 Linux 定制产物尚未验证。

### 日志

日志输出到标准错误流。`RUST_LOG=elyterminal=debug` 可增加日志，`trace` 会记录每次绘制。Windows Release 程序不会打开控制台窗口，可将日志保存到文件：

```powershell
$env:RUST_LOG = "elyterminal=debug"
.\target\release\elyterminal.exe 2> log.txt
```

## 设置文件

设置窗口会将修改自动保存到对应平台的 `settings.json`：

| 平台 | 路径 |
|---|---|
| Windows | `%APPDATA%\ELYTerminal\settings.json` |
| macOS | `~/Library/Application Support/ELYTerminal/settings.json` |
| Linux | `$XDG_CONFIG_HOME/ELYTerminal/settings.json`；未设置时使用 `~/.config/ELYTerminal/settings.json` |

配置文件无法解析或包含越界值时，程序会报告错误并停止启动，不会覆盖原文件。Claude 定制版沿用 ELYTerminal 的配置位置。

## 开发与检查

- `scripts/check.sh` 执行格式检查、clippy、测试和每个手写文件不超过 500 行的检查。
- [AGENTS.md](AGENTS.md) 说明项目结构、开发规则和设计记录。
- [GitHub Actions](https://github.com/ErkkiErkko/ELYTerminal-Claude/actions) 在推送和拉取请求时检查、测试并构建 Windows 版本，也支持手动运行。
- Actions 的构建产物可在对应运行页面下载；正式发布文件位于 [Releases](https://github.com/ErkkiErkko/ELYTerminal-Claude/releases)。

## 上游与许可证

本定制版基于上游 `0.1.5`，基准提交为 `3759cf882553561d9dc4d10825f63b6b9c5d457e`，保留了上游提交历史和版权声明。

**本定制版及新增代码继续使用 MIT 许可证**，详见 [LICENSE](LICENSE)。第三方代码和资源继续遵循各自许可证：

- 框线绘制和键盘编码参考 Ghostty，采用 MIT，见 [LICENSE-GHOSTTY](LICENSE-GHOSTTY)。
- 主题来自 iTerm2-Color-Schemes，采用 MIT，见 [主题许可证](assets/themes/LICENSE)。
- JetBrains Mono 及其 Nerd Font 版本采用 SIL Open Font License，见 [JetBrains Mono 许可证](assets/fonts/JetBrainsMono-LICENSE.txt)和 [Nerd Font 许可证](assets/fonts/JetBrainsMonoNerdFont-LICENSE.txt)。
