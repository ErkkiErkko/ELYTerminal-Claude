# ELYTerminal · Claude

[简体中文](README.md) | **English**

<img src="assets/icons/elyterminal.svg" width="160" alt="A chibi Claude character holding a terminal">

A Claude character customization of [ELYTerminal](https://git.zacharyzhang.com/Zacharyzhang-NY/ELYTerminal). It keeps the original chibi style and replaces the animated window companion and application icon with a feminine Claude design featuring long orange hair, amber eyes, flower ornaments, and black-and-ivory ribbons.

The terminal is built with Rust, GPUI, and Ely components. Sessions sit on the left, the terminal in the middle, and Git or Files on the right. Every setting has a control in the settings window.

## Download and run

[Download the latest release](https://github.com/ErkkiErkko/ELYTerminal-Claude/releases/latest)

Customized binaries are currently available for **Windows x64**:

1. Download `ELYTerminal-Claude.exe`, or download and extract `ELYTerminal-Claude-windows-x64.zip`.
2. Double-click `ELYTerminal-Claude.exe` to start. Rust is not required to use the program.
3. Enable or disable the companion under **Settings → Terminal → Claude**.

The release page also provides a source archive, a patch against upstream, and `SHA256SUMS.txt`. The portable ZIP includes the project and third-party licenses.

This customization has been verified locally on Windows x64 with a Release build, 216 Rust tests, formatting and clippy checks, a startup check, and embedded-icon verification. The startup check used hidden windows and confirmed that the companion loaded and PowerShell reached its prompt.

The source retains macOS and Linux support, but this customization has not been verified on either platform and does not provide customized installers for them. Upstream installers still use the original Ely character.

## Claude customization

- **Character design:** long orange hair, amber eyes, a flower hair ornament, black-and-ivory ribbons, a tassel earring, and a flower brooch, with the original chibi proportions and flat colors.
- **Animation and states:** preserves breathing, blinking, swaying hair, working, waiting, errors, celebrations, dozing, and click reactions. Clicking the companion makes her wink and wakes her from a doze.
- **Window placement:** preserves upstream behavior. The companion stays above the window when there is enough room and moves inside its bottom edge when space is limited, keeping her on screen.
- **Application icon:** uses the same Claude design holding a terminal. The Windows executable embeds seven transparent icon sizes: 16, 24, 32, 48, 64, 128, and 256 pixels.
- **Windows fix:** defers the companion window's frame refresh to prevent synchronous callbacks from causing a borrow error during initialization, with regression coverage.
- **Settings compatibility:** the displayed name is Claude; the existing `ely` configuration key remains valid.

## Terminal features

- **Rendering:** powered by `alacritty_terminal`, with 256 colors, true color, bold, italic, dim text, five underline styles, wide characters, and combining marks. Box drawing, block characters, and Powerline separators are drawn as geometry to keep adjacent cells connected.
- **Input and links:** supports xterm and kitty keyboard protocols, Windows win32-input-mode, input methods, mouse reporting, bracketed paste, OSC 8 links, plain URL detection, and scrollback search. Use the link shortcut below to open links. Inside herdr, herdr handles links; hold Shift as well to let the terminal open them directly.
- **Shell integration:** supports zsh, bash, fish, and PowerShell, reporting the current directory, title, prompts, commands, and exit status.
- **Sessions:** create, close, and switch sessions. Status indicators show progress, waiting for input, completion, or errors. Hover for detailed reports; a bell in a background session leaves a visual mark without playing a sound.
- **Files and Git:** the file tree shows the current session's directory and Git status. The Git panel supports branches, staging, unstaging, discarding changes, commits, history, and diffs. Inside herdr, the directory follows its focused pane.
- **Layout:** hide or resize sidebars; window size and sidebar widths are saved. On Windows and Linux, a gear button opens Settings.
- **Notifications and navigation:** background sessions can post system notifications that open the relevant session when clicked. Jump to the previous or next prompt. On macOS, system notifications require the application bundle and do not work through `cargo run`.
- **Themes:** includes Ely Dark/Light, Catppuccin Mocha/Macchiato/Frappé/Latte, Tokyo Night, Dracula, Nord, Gruvbox Dark, Rosé Pine, Solarized Light, One Light, and Kanagawa Wave. A second theme can follow the system's dark mode. On Omarchy 4, the terminal can follow the system theme.
- **Transparency and blur:** uses NSVisualEffectView on macOS, acrylic on Windows, and compositor blur interfaces on Wayland/X11. Blur is visible only below 100% opacity, and Linux compositors must enable the corresponding effect.

## Keyboard shortcuts

The **Settings → Terminal** page lists the shortcuts for the current platform.

| Action | macOS | Windows / Linux |
|---|---|---|
| New session | Cmd-T | Ctrl-Shift-T |
| Close session | Cmd-W | Ctrl-Shift-W |
| Sessions 1–8 / last session | Cmd-1 through Cmd-8 / Cmd-9 | Alt-1 through Alt-8 / Alt-9 |
| Next / previous session | Ctrl-Tab / Ctrl-Shift-Tab | Ctrl-Tab / Ctrl-Shift-Tab |
| Toggle sessions sidebar | Cmd-B | Ctrl-Shift-B |
| Toggle right sidebar | Cmd-Alt-B | Ctrl-Shift-Alt-B |
| Copy / paste | Cmd-C / Cmd-V | Ctrl-Shift-C / Ctrl-Shift-V; Windows also supports Ctrl-V |
| Select all | Cmd-A | Ctrl-Shift-A |
| Find | Cmd-F | Ctrl-Shift-F |
| Increase / decrease / reset font size | Cmd-= / Cmd-minus / Cmd-0 | Ctrl-= / Ctrl-minus / Ctrl-0 |
| Open a link | Cmd-click | Ctrl-click |
| Previous / next prompt | Cmd-Up / Cmd-Down | Ctrl-Shift-Up / Ctrl-Shift-Down |
| Settings | Cmd-, | Ctrl-, |
| Minimize | Cmd-M | — |
| Quit | Cmd-Q | Ctrl-Shift-Q |

## Build from source

### Windows

Install Rust 1.95.0, Visual Studio C++ Build Tools, and the Windows SDK. `rust-toolchain.toml` pins the Rust version; rustup selects the toolchain from that file.

Run the following in **Developer PowerShell for Visual Studio** with the C++ toolchain configured:

```powershell
git clone https://github.com/ErkkiErkko/ELYTerminal-Claude.git
cd ELYTerminal-Claude
cargo build --release --locked
.\target\release\elyterminal.exe
```

A local build produces `elyterminal.exe`; the release download is renamed to `ELYTerminal-Claude.exe`.

### macOS and Linux

Build and run from source:

```sh
cargo run --release --locked
```

On Debian / Ubuntu, install the build dependencies first:

```sh
sudo apt-get install pkg-config libwayland-dev libxkbcommon-dev libxkbcommon-x11-dev \
  libxcb1-dev libx11-xcb-dev libfontconfig-dev libfreetype-dev
```

The repository retains upstream packaging scripts, which write their output to `target/release`:

| Script | Purpose |
|---|---|
| `scripts/windows-zip.ps1` | Build the Windows executable and package a ZIP |
| `scripts/mac-app.sh` | Build a macOS application bundle and disk image; signing and notarization require your own configuration |
| `scripts/linux-tar.sh` | Build in Docker and package the Linux binary, desktop entry, and icon |

These scripts retain upstream output names. Customized macOS and Linux packages have not been verified.

### Logging

Logs go to standard error. `RUST_LOG=elyterminal=debug` enables additional logging; `trace` logs each paint. A Windows Release build does not open a console window, so redirect logs to a file:

```powershell
$env:RUST_LOG = "elyterminal=debug"
.\target\release\elyterminal.exe 2> log.txt
```

## Settings files

The settings window saves changes automatically to the platform's `settings.json`:

| Platform | Path |
|---|---|
| Windows | `%APPDATA%\ELYTerminal\settings.json` |
| macOS | `~/Library/Application Support/ELYTerminal/settings.json` |
| Linux | `$XDG_CONFIG_HOME/ELYTerminal/settings.json`, or `~/.config/ELYTerminal/settings.json` when unset |

If the configuration cannot be parsed or contains an out-of-range value, the application reports an error and stops rather than overwriting the file. This customization uses the same configuration location as ELYTerminal.

## Development and checks

- `scripts/check.sh` runs formatting checks, clippy, tests, and the 500-line limit check for handwritten files.
- [AGENTS.md](AGENTS.md) describes the project structure, development rules, and design decisions.
- [GitHub Actions](https://github.com/ErkkiErkko/ELYTerminal-Claude/actions) checks, tests, and builds Windows on pushes and pull requests. It also supports manual runs.
- Build artifacts are available from the corresponding Actions run; published downloads are under [Releases](https://github.com/ErkkiErkko/ELYTerminal-Claude/releases).

## Upstream and license

This customization is based on upstream `0.1.5`, commit `3759cf882553561d9dc4d10825f63b6b9c5d457e`. Upstream commit history and copyright notices are preserved.

**This customization and its added code continue to use the MIT License.** See [LICENSE](LICENSE). Third-party code and resources retain their own licenses:

- Box drawing and keyboard encoding follow Ghostty's code under MIT: [LICENSE-GHOSTTY](LICENSE-GHOSTTY).
- Themes come from iTerm2-Color-Schemes under MIT: [theme license](assets/themes/LICENSE).
- JetBrains Mono and its Nerd Font build use the SIL Open Font License: [JetBrains Mono license](assets/fonts/JetBrainsMono-LICENSE.txt) and [Nerd Font license](assets/fonts/JetBrainsMonoNerdFont-LICENSE.txt).
