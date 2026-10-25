# ELYTerminal · Claude

**简体中文** | [English](README.en.md)

<img src="assets/icons/elyterminal.svg" width="160" alt="Claude 抱着终端的 Q 版图标">

基于 [ELYTerminal](https://github.com/ELY-Open-Source/ELYTerminal) 的 Claude 娘化定制版。沿用原版 Q 版画风，将窗口上的动画人物和应用图标换成橘色长发、琥珀眼睛、花饰与黑白缎带的 Claude 形象。

终端使用 Rust、GPUI 和 Ely 组件构建，布局为左侧会话、中间终端、右侧 Git 或文件面板。各项设置均可在设置窗口中调整。

## 下载与运行

[下载最新版本](https://github.com/ErkkiErkko/ELYTerminal-Claude/releases/latest)

当前提供 **Windows x64** 定制版：

1. 下载 `ELYTerminal-Claude.exe`，或下载并解压 `ELYTerminal-Claude-windows-x64.zip`。
2. 双击 `ELYTerminal-Claude.exe` 启动，使用时不需要安装 Rust。
3. 在 **Settings → Terminal → Claude** 中开启或关闭动画人物。

发布页也提供源码包、相对上游的补丁和 `SHA256SUMS.txt` 校验文件。便携压缩包包含项目及第三方许可证。

本定制版已在本机 Windows x64 环境中完成 Release 构建、279 项 Rust 测试、格式与 clippy 检查、启动检查和内嵌图标核对。启动检查以隐藏窗口运行，确认角色与 PowerShell 提示符正常加载。

源码保留了 macOS 和 Linux 支持，但本定制版尚未在这两个平台验证，也未提供对应的定制安装包。上游发布的安装包仍使用原版 Ely 形象。

## Claude 定制内容

- **人物外观：**橘色长发、琥珀眼睛、花朵头饰、黑白缎带、流苏耳饰和花朵胸针，保持原版 Q 版比例与扁平色块画风。
- **动画与状态：**保留呼吸、眨眼、发丝摆动、工作、等待、出错、庆祝、犯困和点击回应。点击人物会眨眼回应，也能将她从犯困状态唤醒。
- **窗口位置：**保留上游逻辑——上方空间足够时位于窗口顶部；空间不足时移到终端内部的底部，避免显示到屏幕外。
- **应用图标：**使用同一 Claude 形象抱着终端的构图。Windows exe 内嵌 16、24、32、48、64、128、256 像素七种透明背景图标。
- **Windows 修复：**延后角色窗口的边框刷新，修复初始化时同步回调导致的借用错误，并补充回归验证。
- **设置兼容：**显示名称改为 Claude，原来的 `ely` 配置键继续有效。

## 0.1.9 更新

- **中文界面：**在 Settings → Appearance → Language 选择简体中文；菜单、设置和更新提示随语言切换，人物名称保持 Claude。
- **Windows 终端：**修复输出有时要按键才刷新的问题，以及擦除、插入或删除宽字符时残留的中文字符；滚轮遵循系统滚动设置。
- **Shell 状态：**改进嵌套 bash、zsh、fish、PowerShell 和 Nushell 的交互模式识别，避免程序自己的提示符标记误清除运行状态；也合入了 0.1.9 发布后的相关修复。
- **目录与布局：**Git Bash 和 sh 支持目录联动；新会话可选择固定起始目录，WSL 的 Home 使用发行版自己的主目录。可分别关闭会话拖动和右键菜单，侧栏显示状态会保存。
- **更新通知：**每条更新通知保留对应版本的下载页，手动重新检查不会让旧通知失效；下载仍来自本 Claude 仓库。
- **其他平台：**合入 macOS 输入法下的 Option 键修复、Linux 中文输入与最大化窗口点击修复，以及 Wayland 人物窗口修复。新增 Linux 四种格式的打包脚本与自动构建流程。

## 0.1.8 更新

- **Windows 环境与 Shell：**新会话重新读取系统和用户环境变量，展开变量引用并去重 PATH。未指定 Shell 时依次寻找 PowerShell 7、Windows PowerShell 和 cmd，跳过不可用的应用执行别名。
- **WSL：**Shell 设置为 `wsl` 时，bash、zsh 或 fish 会报告当前目录，文件树和 Git 面板随之更新；WSL 共享目录中的 Git 在对应发行版内运行。拖入文件仍会输入 Windows 路径。
- **会话操作：**右键会话可在同一 Shell 和目录中复制会话或关闭会话；拖动会话行可调整顺序，当前选中的会话保持不变。重命名输入框内的拖动仍用于选择文字。
- **键盘输入：**按键的重复与释放沿用按下时的输入方式，避免中途改变修饰键造成不匹配。macOS 新增可选的 Natural text editing，支持 Option 按词、Command 按行编辑，默认关闭。
- **完成通知：**后台命令只有运行至少 5 秒才发送结束通知，减少短命令和提示符工具带来的重复通知。

## 0.1.7 更新

- **拖动人物：**按住 Claude 可沿窗沿左右拖动，位置自动保存；Wayland 在松开后更新位置。跳跃时衣服和后发继续覆盖窗沿，修复人物下方的空隙。
- **滚动与输入：**新增可拖动的历史滚动条；支持点击 Shell 当前输入行移动光标，具体效果取决于 Shell 和行编辑器。
- **拖入文件：**将文件拖到终端会粘贴路径，按当前会话启动的 Shell 转义。
- **字体与会话：**可按顺序添加回退字体；双击会话名称进行重命名，清空名称可恢复程序标题。
- **Windows：**合入 Windows 10 拖动或缩放窗口时暂时关闭亚克力模糊的优化，并保留 Claude 版的角色初始化修复。
- **检查更新：**Settings → Terminal 可手动检查，自动检查默认在启动时和每天执行。仅检查本 Claude 仓库的发布版，支持 `-claude.N` 修订号；发现新版后打开下载页，不会自动替换程序。检查依赖系统的 `curl`。

## 终端功能

- **终端显示：**基于 `alacritty_terminal`，支持 256 色、真彩色、粗体、斜体、暗色、五种下划线样式、宽字符和组合字符。框线、块状字符和 Powerline 分隔符采用几何绘制，减少单元格间的缝隙。
- **输入与链接：**支持 xterm 和 kitty 键盘协议、Windows 的 win32-input-mode、输入法、鼠标报告、括号粘贴、OSC 8 链接、普通网址识别和滚动历史搜索。通过下方快捷键打开链接；在 herdr 中，链接由 herdr 处理，加按 Shift 可由终端直接打开。
- **Shell 集成：**支持 zsh、bash、fish、PowerShell，以及 Windows 上由 `wsl` 启动的 bash、zsh 或 fish，报告当前目录、标题、提示符、命令及退出状态。
- **会话管理：**创建、复制、关闭和切换会话，支持拖动排序；状态标记显示工作进度、等待输入、完成或错误等状态。悬停可查看详细报告，后台会话的响铃会留下视觉标记而不播放声音。
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
| `scripts/linux-packages.sh` | 在 Ubuntu 22.04 容器中构建 tar.gz、DEB、RPM 和 AppImage |
| `scripts/linux-tar.sh` | 单独构建 Linux tar.gz 包 |

这些脚本沿用上游的产物命名方式；Linux 包版本将 `0.1.9-claude.1` 写为 `0.1.9.claude.1`，兼容各格式。详见 [Linux 打包说明](packaging/linux/README.md)。macOS 和 Linux 定制产物尚未验证。

### 日志

日志输出到标准错误流。`RUST_LOG=elyterminal=debug,ely_gpui_component=info` 可增加日志，`trace` 会记录每次绘制。Windows Release 程序不会打开控制台窗口，可将日志保存到文件：

```powershell
$env:RUST_LOG = "elyterminal=debug,ely_gpui_component=info"
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
- Linux packages 工作流构建并检查四种 Linux 包，仅保存 Actions 产物，不自动发布 Release。
- Actions 的构建产物可在对应运行页面下载；正式发布文件位于 [Releases](https://github.com/ErkkiErkko/ELYTerminal-Claude/releases)。

## 上游与许可证

本定制版基于上游 `0.1.9` 及其后续修复，基准提交为 `6280fd4c3d0b5733efed09d88d41c00703dc6914`，保留了上游提交历史和版权声明。

**本定制版及新增代码继续使用 MIT 许可证**，详见 [LICENSE](LICENSE)。第三方代码和资源继续遵循各自许可证：

- 框线绘制和键盘编码参考 Ghostty，采用 MIT，见 [LICENSE-GHOSTTY](LICENSE-GHOSTTY)。
- 主题来自 iTerm2-Color-Schemes，采用 MIT，见 [主题许可证](assets/themes/LICENSE)。
- JetBrains Mono 及其 Nerd Font 版本采用 SIL Open Font License，见 [JetBrains Mono 许可证](assets/fonts/JetBrainsMono-LICENSE.txt)和 [Nerd Font 许可证](assets/fonts/JetBrainsMonoNerdFont-LICENSE.txt)。

- Linux 复合文本解码表来自 libX11，保留 SunSoft 和 Bruno Haible 的[许可声明](vendor/xim-ctext/tables/LICENSE)。
