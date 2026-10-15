# codex-reasoning

A standalone command-line tool for viewing active Codex agents and recent saved
reasoning summaries from local rollout logs. Requires Python 3.9 or later and
uses only the standard library.

## Install

```sh
git clone https://github.com/Midgaze/codex-reasoning.git
cd codex-reasoning
mkdir -p ~/.local/bin
install -m 755 codex-reasoning ~/.local/bin/codex-reasoning
```

Ensure `~/.local/bin` is on your `PATH`. You can also run the script directly:

```sh
python3 codex-reasoning --help
```

On Windows, use `py -3 codex-reasoning`.

## Usage

```sh
codex-reasoning                         # Active agents with recent log activity
codex-reasoning -a 5                    # Also show up to five recent finished sessions
codex-reasoning --max-age 15             # Limit activity and summaries to 15 minutes
codex-reasoning --details               # Include ancestry, turn events, and token usage
codex-reasoning --json                  # Emit a flat JSON array
codex-reasoning --codex-home ~/.codex-work --width 80
watch -n 2 codex-reasoning               # Refresh every two seconds; requires watch
```

Run `codex-reasoning --help` for all options and output details.

The tool reads `$CODEX_HOME/sessions`, defaulting to `~/.codex/sessions`.
`--codex-home` overrides that location. The default activity window is 60 minutes.
Active agents appear even when they have no saved reasoning summary. Text output
groups agents under their recorded parents and shows their model and reasoning
effort when available.

The command reads local files without making network requests or changing Codex
logs or configuration. Reasoning text comes from saved `summary_text` items;
availability depends on the model and Codex settings. The rollout JSONL format
is internal to Codex and may change. An agent marked active has a recorded started
turn and recent log activity; this is not a live process check.

Exit status is `0` on success, including no matching sessions, `1` for missing or
unreadable session directories, and `2` for invalid arguments.

## Local development

The repository contains the executable script directly, with no build step or
dependencies. To have edits take effect immediately, symlink it onto your `PATH`
instead of installing a copy:

```sh
ln -s "$PWD/codex-reasoning" ~/.local/bin/codex-reasoning
```

The destination must not already exist when creating the symlink.
