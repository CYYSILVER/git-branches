# git-branches

[简体中文](./README.zh-CN.md) | English

An interactive terminal UI for managing git branches — browse, search, create, delete, and switch branches, all with inline descriptions.

![zsh](https://img.shields.io/badge/shell-zsh-blue)
![i18n](https://img.shields.io/badge/i18n-zh%20%7C%20en-green)

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

```bash
git clone https://github.com/<your-username>/git-branches.git ~/Project/tools/git-branches
```

Add to your shell config (`~/.zshrc` or `~/.bash_profile`):

```bash
function branches() {
    ~/Project/tools/git-branches/git-branches "$@"
}
```

Then reload your shell or run `source ~/.zshrc`.

## Usage

Navigate to any git repository and run:

```bash
branches
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

| Key | Action |
|-----|--------|
| `j` / `↓` | Move down |
| `k` / `↑` | Move up |
| `Enter` | Checkout selected branch |
| `Space` | Toggle mark on branch (for multi-select) |
| `/` | Search / filter branches |
| `c` | Create new branch (with description prompt) |
| `d` | Delete selected branch, or all marked branches |
| `r` | Edit description of selected branch (`$EDITOR`) |
| `Esc` | Cancel current action / clear marks / quit |
| `q` | Quit |

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
