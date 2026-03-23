# claude-kitty-hypr

## What This Is
A Claude Code hook script providing visual feedback via Kitty terminal (tab colors, background tinting) and Hyprland window borders. Distributed as a single bash script with an optional AUR package.

## Architecture
- **`claude-kitty-hypr`** — Main script (~180 lines bash). Three responsibilities:
  1. `--setup` / `--uninstall` — Manages hook entries in `~/.claude/settings.json` via `jq`
  2. Hook event dispatch — Reads JSON from stdin, updates Kitty + Hyprland
  3. Config loading — Sources `~/.config/claude-kitty-hypr/config` for user overrides
- **`claude-kitty-hypr.install`** — Pacman `.install` file, delegates to `--setup`/`--uninstall`
- **`PKGBUILD`** — AUR package definition (may never be submitted to AUR — undecided)
- **`config.example`** — All configurable variables with defaults

## Key Design Decisions
- No `set -euo pipefail` — hook scripts must always exit 0 to avoid blocking Claude Code
- `HOOK_CMD` resolved via `readlink -f "$0"` — works from any install location
- jq cleanup uses `endswith("claude-kitty-hypr")` fallback for cross-version compatibility
- `set-colors` uses `id:` matching, `set-tab-color`/`set-tab-title` use `window_id:` matching (Kitty quirk)
- Background tinting only on state transitions (not on every PreToolUse/PostToolUse)

## Testing
```bash
# Full test suite (setup, idempotency, merge preservation, uninstall)
TMPDIR=$(mktemp -d)
mkdir -p "$TMPDIR/.claude"
echo '{"hooks":{"PostCompact":[{"matcher":"","hooks":[{"type":"command","command":"echo hi","timeout":5}]}]},"env":{"FOO":"bar"}}' > "$TMPDIR/.claude/settings.json"
HOME="$TMPDIR" ./claude-kitty-hypr --setup
HOME="$TMPDIR" ./claude-kitty-hypr --setup  # idempotency — should still be 1 entry per event
HOME="$TMPDIR" ./claude-kitty-hypr --uninstall  # should preserve PostCompact and env
rm -rf "$TMPDIR"
```

## Dependencies
- Runtime: `jq`, `kitty` (kitten remote control), `hyprland` (hyprctl)
- Lint: `shellcheck`
