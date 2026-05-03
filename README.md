# superclaude

Claude Code with tmux session management. Two scripts:

- **`superclaude`** — full CLI: create / list / attach / kill named tmux sessions running `claude`. Session names are derived from `$PWD` so each project gets its own sticky session. `superclaude list all` opens an `fzf` picker over every session.
- **`sc`** — short, mobile-friendly wrapper around the same session pool. `sc` opens an `fzf` picker filling the screen, with "+ new session" pinned at the top. `sc n` creates new, `sc <N>` attaches by row index.

## Install

```sh
git clone git@github.com:scharc/superclaude.git
ln -s "$PWD/superclaude/bin/superclaude" ~/.local/bin/superclaude
ln -s "$PWD/superclaude/bin/sc"          ~/.local/bin/sc
```

Requires `tmux`, `fzf`, and `claude` (Claude Code CLI) on `$PATH`.

## Usage

```
superclaude              attach existing session for $PWD, or create one
superclaude new          new session in $PWD (auto-numbered if one exists)
superclaude list         list sessions for $PWD
superclaude list all     fzf picker over ALL sc sessions
superclaude attach NAME  attach to a specific session
superclaude kill NAME    kill a specific session

sc                       fzf picker over ALL sc sessions, "+ new" at top
sc n                     new session in $PWD
sc <N>                   attach to row N (most-recent first)
```

The picker shows `idx ●/· age  title  ·  dir` per row — `●` = attached, `·` = idle.

## Notes

- Sessions are launched with `claude --dangerously-skip-permissions`. Edit `CLAUDE_CMD` in `bin/superclaude` if you want different defaults.
- Session-name slug: `sc|<absolute-path>`. Multiple sessions for the same path get suffixed `-2`, `-3`, ...
