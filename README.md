# claude-code-launcher (lite)

A single-file Python/GTK4 port of
[claude-code-launcher](https://github.com/jamesdedon/claude-code-launcher),
without the animations. A small popup where you type a prompt; Enter opens a
terminal running Claude Code with that prompt.

It reads the same config and history files as the Rust original, so you can
switch between them freely.

## Requirements

Python 3.11+, GTK 4 (≥ 4.10) and PyGObject. On Debian/Ubuntu:

```sh
sudo apt install python3-gi gir1.2-gtk-4.0
```

## Install

```sh
ln -s "$PWD/claude-code-launcher" ~/.local/bin/claude-code-launcher
claude-code-launcher
```

The first run writes a starter config to
`~/.config/claude-code-launcher/config.toml`. Set `working_directory` and
`terminal_command` there, then run it again.

In sway, show it as a floating popup on a hotkey:

```
for_window [app_id="dev.dedon.ClaudeCodeLauncher"] floating enable, border none
bindsym Ctrl+Mod1+space exec claude-code-launcher
```

## Keys

| Key | Action |
|---|---|
| `Enter` | launch Claude Code with the prompt |
| `Ctrl+Enter` | launch with `--resume` (works with an empty prompt) |
| `Shift+Enter` | new line |
| `Ctrl+Tab` / `Ctrl+Shift+Tab` | cycle the target project directory |
| `Up` / `Down` | prompt history |
| `/` | complete slash commands from `~/.claude/commands` (`Tab` accepts) |
| `Esc` | close |

## Config

```toml
working_directory = "/home/you/Projects"
terminal_command = ["foot", "--working-directory={cwd}", "claude", "{prompt}"]

# Optional: subdirectories become Ctrl+Tab targets
projects_directory = "/home/you/Projects"

# Optional: extra targets
[[projects]]
name = "notes"
path = "/home/you/Documents/notes"

# history_size = 100
# resume_args = ["--resume"]
# title = "Ask Claude..."
```

`{cwd}` and `{prompt}` are substituted into `terminal_command`. The prompt is
always passed as one argument and never goes through a shell. Theme colours and
font sizes can be set under `[theme]`; the starter config lists them.

History is kept in `~/.local/state/claude-code-launcher/history.toml`.

## License

GPL-3.0-or-later. See [LICENSE](LICENSE).
