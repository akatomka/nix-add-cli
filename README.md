# nix-add

A small CLI utility for NixOS that lets you **look up and add packages to `configuration.nix`** using simple commands like `add kitty`.

The tool verifies that packages exist in Nix, handles typos interactively, updates your system configuration, and rebuilds automatically.

---

## Features

- Add packages to `environment.systemPackages`
- Look up packages in Nix without modifying your system
- Lookup + add in a single command
- Interactive typo correction with suggestions
- Optional non-interactive mode with `--yes`
- Multiple packages in one command
- Colorized terminal output
- Summary table showing what happened
- Automatic backup of `configuration.nix`

---

## Installation

1. Create a bin directory if you don’t already have one:

```bash
mkdir -p ~/bin
Save the script as add:

bash
Copy code
nano ~/bin/add
Paste the script and save.

Make it executable:

bash
Copy code
chmod +x ~/bin/add
Ensure ~/bin is in your PATH:

bash
Copy code
export PATH="$HOME/bin:$PATH"
(Optional, recommended) Persist it:

bash
Copy code
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
Commands
Add packages
bash
Copy code
add kitty
+ kitty
Adds the package to configuration.nix and runs:

bash
Copy code
sudo nixos-rebuild switch
Lookup packages (no changes)
bash
Copy code
lkp neovim
Checks whether the package exists in Nix channels.

Lookup + add
bash
Copy code
add lkp neovim
Verifies the package exists

Adds it to configuration.nix

Rebuilds the system

Handle typos interactively
bash
Copy code
add lkp neovimm
If the package doesn’t exist, you’ll be prompted with suggestions:

sql
Copy code
Did you mean:
  1) neovim
  2) neovim-qt
  0) Skip
Auto-select suggestions (non-interactive)
bash
Copy code
add lkp neovimm --yes
Automatically selects the closest match. Useful for scripts.

Multiple packages
bash
Copy code
add neovim kitty htop
add lkp neovimm kitty htop
All packages are processed in one run.

Output Summary
At the end of each run, a summary table is shown:

pgsql
Copy code
Package              Status       Action Taken
--------------------------------------------------
neovimm              NOT FOUND    [SELECTED] neovim
kitty                FOUND        Added
htop                 FOUND        Added
Safety
Your configuration.nix is backed up automatically as:

pgsql
Copy code
configuration.nix.bak
Existing packages are not duplicated

Missing packages can be skipped safely

Requirements
NixOS

nix command available

Standard environment.systemPackages = [ ... ]; layout
