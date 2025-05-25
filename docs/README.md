# .dotfiles
Personal system and application configuration files. Includes customizations for terminals, shells, editors, development tools, system utilities, and more.

## Approach
Instead of using a dedicated tool like Stow or chezmoi, contents of this dotfiles repo are managed with plain Git plus some convenience shell aliases.

* **Zero extra dependencies.** Uses only vanilla Git; no dedicated/helper tools.
* **"In-place" tracking.** Files live on disk where programs expect them; a separate, out of the way bare repo tracks them.
* **Fast syncs**. A single `config-sync` command ensures the remote repo (i.e., GitHub) reflects the current state of all tracked config files.

An effect of using this approach is that the contents of the `dotfiles` repository are organized in the same hierarchical structure that the files live in situ, with the root of the repository corresponding to the path `$HOME/`.

## Usage
Use either the handful of `config*` shell aliases described below *or* interact with the repository directly with Git.

### Day-to-day usage

| Task | Command |
|------|---------|
| **See what changed** | `config status -vv` |
| **Stage *tracked* changes + commit + push** | `config-sync` |
| **Track a new file** | `config add ~/.new-untracked.rc && config commit -m "chore: add new file" && config push` |

### Quick start on a new machine
```bash
# Clone the repository *as a bare repo*
git clone --bare git@github.com:ryancwallace/dotfiles.git $HOME/home/code/dotfiles

# Define convenience shell aliases (assumes zsh)
echo "alias config='git --git-dir=$HOME/home/code/dotfiles/ --work-tree=$HOME'" >> ~/.zshrc
echo "alias config-sync='config add -u && config commit -m \"chore: update config files as of \$(date +\"%Y-%m-%dT%H:%M:%S\")\" && config push origin main'" >> ~/.zshrc
source ~/.zshrc

# Check out the actual dotfiles into $HOME
config checkout

# Hide untracked noise
config config --local status.showUntrackedFiles no
```

## Reminders
* On `Ryans-Macbook-Pro`, the bare repository lives at `~/home/code/dotfiles/`.
