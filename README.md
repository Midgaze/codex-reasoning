# codex-reasoning

A standalone command-line tool for viewing active Codex agents and recent saved
reasoning summaries from local rollout logs. Requires Python 3.9 or later and
uses only the standard library.

## Install

On Linux or macOS, download the script and install it as `reasoning`:

```sh
curl -fL https://raw.githubusercontent.com/Midgaze/codex-reasoning/main/codex-reasoning -o codex-reasoning
mkdir -p ~/.local/bin
install -m 755 codex-reasoning ~/.local/bin/reasoning
```

Ensure `~/.local/bin` is on your `PATH`, then run `reasoning --help`. If needed,
add this line to your shell's startup file (for example, `~/.bashrc` or `~/.zshrc`):

```sh
export PATH="$HOME/.local/bin:$PATH"
```

You can delete the downloaded file after installation. Repeat the download and
install commands to update to the latest version.

Alternatively, run the downloaded script directly:

```sh
python3 codex-reasoning --help
```

On Windows, use `py -3 codex-reasoning`.

## Usage

```sh
reasoning                         # Active agents with recent log activity
reasoning -a 5                    # Also show up to five recent finished sessions
reasoning --max-age 15             # Limit activity and summaries to 15 minutes
reasoning --details               # Include ancestry, turn events, and token usage
reasoning --json                  # Emit a flat JSON array
reasoning --codex-home ~/.codex-work --width 80
watch -n 2 reasoning               # Refresh every two seconds; requires watch
```

Run `reasoning --help` for all options and output details.

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

Clone the repository wherever you keep source code. There is no build step or
dependency installation:

```sh
git clone https://github.com/Midgaze/codex-reasoning.git
cd codex-reasoning
```

To have edits take effect immediately, symlink the script into a directory on
your `PATH`. For example, if you use `~/bin`:

```sh
mkdir -p ~/bin
ln -s "$PWD/codex-reasoning" ~/bin/reasoning
```

The destination must not already exist when creating the symlink. If you
previously installed a copy elsewhere on your `PATH`, remove it or ensure the
symlink's directory comes first. Use `git pull` in the checkout to update.
