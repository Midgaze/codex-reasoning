# codex-reasoning

See what your Codex agents are working on, including their latest saved reasoning
summaries. Requires Python 3.9+; no dependencies.

## Install

```sh
mkdir -p ~/.local/bin
curl -fL https://raw.githubusercontent.com/Midgaze/codex-reasoning/main/codex-reasoning -o ~/.local/bin/reasoning
chmod +x ~/.local/bin/reasoning
```

Make sure `~/.local/bin` is on your `PATH`. Run these commands again to update.

## Usage

```sh
reasoning                 # Active agents
reasoning -a              # Include recent finished sessions
reasoning --details       # Model, ancestry, turn events, and token usage
reasoning --json          # JSON output
watch -n 2 reasoning      # Refresh every two seconds
```

See `reasoning --help` for all options.

Reads local logs in `~/.codex/sessions` (or `$CODEX_HOME/sessions`) without
modifying them or making network requests. Saved summaries depend on the model
and Codex settings. Codex's internal log format may change.
