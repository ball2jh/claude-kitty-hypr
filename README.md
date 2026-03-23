# claude-kitty-hypr

Visual feedback for Claude Code sessions via Kitty tab colors and Hyprland window borders.

## What it does

A hook script that watches Claude Code events and updates your terminal in real time:

| State | Color | When |
|-------|-------|------|
| Blue | `#2563eb` | Claude is working (processing, running tools) |
| Orange | `#ea580c` | Claude needs your input |
| Green | `#16a34a` | Task complete |

Both the Kitty tab background and the Hyprland window border change color. On session end, everything resets to your defaults.

<!-- TODO: add demo GIF -->

## Install (Arch / AUR)

```bash
yay -S claude-kitty-hypr
```

The install automatically adds hook entries to `~/.claude/settings.json` (backs up the existing file first). If that doesn't work (e.g., installed from a root shell), run `claude-kitty-hypr --setup` manually.

## Configuration

Copy the example config and edit as needed:

```bash
mkdir -p ~/.config/claude-kitty-hypr
cp /usr/share/claude-kitty-hypr/config.example ~/.config/claude-kitty-hypr/config
```

Key variables (all optional — defaults are shown in the file):

- `COLOR_ACTIVE` / `COLOR_ACTIVE_HEX` — blue, working
- `COLOR_NOTIFY` / `COLOR_NOTIFY_HEX` — orange, needs input
- `COLOR_DONE` / `COLOR_DONE_HEX` — green, done
- `TITLE_WORKING`, `TITLE_NOTIFY`, `TITLE_DONE` — tab title strings
- `BORDER_SIZE` — Hyprland border width in pixels

## Manual install (non-Arch)

```bash
git clone https://github.com/ball2jh/claude-kitty-hypr.git
cd claude-kitty-hypr
sudo cp claude-kitty-hypr /usr/local/bin/claude-kitty-hypr
claude-kitty-hypr --setup
```

## Uninstall

AUR:
```bash
yay -R claude-kitty-hypr
```

Manual:
```bash
claude-kitty-hypr --uninstall
sudo rm /usr/local/bin/claude-kitty-hypr
```

## Requirements

- **Kitty** — with remote control enabled in `kitty.conf`:
  ```
  allow_remote_control yes
  listen_on unix:/tmp/kitty-{kitty_pid}
  ```
- **Hyprland**
- **jq**

## License

MIT
