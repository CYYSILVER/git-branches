# git-branches

[简体中文](./README.zh-CN.md) | English

An interactive terminal UI for managing git branches — browse, search, create, delete, and switch branches, all with inline descriptions.

![zsh](https://img.shields.io/badge/shell-zsh-blue)
![i18n](https://img.shields.io/badge/i18n-zh%20%7C%20en-green)

## Why

You run `git branch` and get a wall of names — `fix-login`, `temp`, `feature-xx-v2` — with zero context about what they do or when you last touched them. You vaguely remember working on something yesterday but can't pick it out of thirty branches. Switching means typing (or tab-completing) the full name; cleaning up means running `git branch -d` one by one.

**git-branches** replaces that workflow with a single interactive screen:

- Branches are **sorted by last checkout time**, so what you were working on is always at the top.
- Each branch shows its **description** right next to the name — no more guessing what `feature-auth-refactor` was about.
- One keypress to **switch**, **search**, **create**, or **batch-delete**.

It's a single shell script, zero dependencies beyond zsh + git, and installs in one `curl` command. If you spend any amount of your day juggling branches, this will save you real time.

## Features

- **Sorted by recently used** — branches you checked out most recently appear first (parsed from `git reflog`)
- **Inline descriptions** — displays `git branch --edit-description` text alongside each branch
- **Real-time search** — press `/` to filter branches by name or description
- **Create branches** — press `c` to create a new branch and set its description inline
- **Delete branches** — press `d` to delete a single branch, or use `Space` to mark multiple branches for batch deletion
- **Edit descriptions** — press `r` to open `$EDITOR` for the selected branch's description
- **Keyboard-driven** — fully navigable with `j`/`k`, arrow keys, and single-key actions
- **i18n** — Chinese (default) and English, auto-detected from system locale

## Installation

One-line install (also works for updates):

```bash
curl -fsSL https://raw.githubusercontent.com/cyysilver/git-branches/main/git-branches -o /usr/local/bin/git-branches && chmod +x /usr/local/bin/git-branches
```

> If `/usr/local/bin` requires sudo, prepend `sudo` to the command, or install to a user-local directory:
>
> ```bash
> curl -fsSL https://raw.githubusercontent.com/cyysilver/git-branches/main/git-branches -o ~/.local/bin/git-branches && chmod +x ~/.local/bin/git-branches
> ```

Since the script follows the `git-xxx` naming convention, it is automatically available as a **git subcommand** once in `PATH`:

```bash
git branches
```

### Aliases (optional)

Add short aliases to your `~/.zshrc` or `~/.bash_profile`:

```bash
alias br='git-branches'
alias branches='git-branches'
```

Three ways to invoke:


| Command        | Description                            |
| -------------- | -------------------------------------- |
| `br`           | Shortest, 2 chars — best for daily use |
| `branches`     | Full semantic name                     |
| `git branches` | Git subcommand style (no alias needed) |


### Alternative: clone the repo

```bash
git clone https://github.com/cyysilver/git-branches.git ~/tools/git-branches
export PATH="$PATH:$HOME/tools/git-branches"  # add to your shell config
```

## Usage

Navigate to any git repository and run:

```bash
git branches    # or: br / branches
```

### Language

The UI language is auto-detected from your system locale. To override:

```bash
# Force English
export GIT_BRANCHES_LANG=en

# Force Chinese (default)
export GIT_BRANCHES_LANG=zh
```

## Keybindings


| Key       | Action                                          |
| --------- | ----------------------------------------------- |
| `j` / `↓` | Move down                                       |
| `k` / `↑` | Move up                                         |
| `Enter`   | Checkout selected branch                        |
| `Space`   | Toggle mark on branch (for multi-select)        |
| `/`       | Search / filter branches                        |
| `c`       | Create new branch (with description prompt)     |
| `d`       | Delete selected branch, or all marked branches  |
| `r`       | Edit description of selected branch (`$EDITOR`) |
| `Esc`     | Cancel current action / clear marks / quit      |
| `q`       | Quit                                            |


## How descriptions work

Git natively supports branch descriptions via:

```bash
git branch --edit-description <branch-name>
```

These are stored in `.git/config` as `branch.<name>.description`. This tool reads and displays them inline, making it easy to remember what each branch is for.

## Requirements

- **zsh** (macOS default shell, or install via package manager)
- **git** ≥ 2.0

## License

MIT