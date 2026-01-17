# nix-add-cli

A polished, interactive CLI tool for **managing Nix packages** in your `configuration.nix`.  
It allows you to quickly **look up packages**, **add them interactively**, **auto-correct typos**, and **batch install multiple packages** — all with colorful terminal output and a summary table.

---

## Features

- ✅ **Add packages** to `configuration.nix` (`add` or `+`)  
- ✅ **Lookup packages** in Nix channels (`lkp`)  
- ✅ **Lookup + add** in one command (`add lkp`)  
- ✅ **Interactive typo correction** with suggestions  
- ✅ **Auto-select first suggestion** with `--yes` for scripting  
- ✅ **Multi-package support** (`add neovim kitty htop`)  
- ✅ **Colorized terminal output** for clarity  
- ✅ **Summary table** showing package status and actions  
- ✅ **Automatic backup** of `configuration.nix` before changes  

---

## Installation

1. Save the script to a file in your home directory, for example:

```bash
mkdir -p ~/bin
nano ~/bin/add
Paste the Python script and save.

Make it executable:

bash
Copy code
chmod +x ~/bin/add
Make sure ~/bin is in your PATH:

bash
Copy code
export PATH="$HOME/bin:$PATH"
Optionally, add it to your shell config (~/.bashrc or ~/.zshrc):

bash
Copy code
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
Usage
Basic add
bash
Copy code
add neovim
# or shortcut:
+ neovim
Adds neovim to environment.systemPackages and runs nixos-rebuild switch.

Lookup only
bash
Copy code
lkp neovim kitty
Checks if packages exist in Nix channels without modifying your config.

Output example:

pgsql
Copy code
[FOUND] neovim exists in Nix channels.
[FOUND] kitty exists in Nix channels.
Lookup + Add (interactive)
bash
Copy code
add lkp neovimm kitty htop
neovimm is a typo → prompts user to choose a suggestion

kitty and htop exist → added automatically

Summary table displayed at the end

Example summary table:

pgsql
Copy code
Package              Status       Action Taken
--------------------------------------------------
neovimm              NOT FOUND    [SELECTED] neovim
kitty                FOUND        Added
htop                 FOUND        Added
Auto-select suggestions (--yes)
bash
Copy code
add lkp neovimm kitty htop --yes
Automatically selects the first suggestion for typos without prompting. Great for scripts or batch installs.

Multiple packages at once
bash
Copy code
add neovim kitty htop
+ neovim kitty htop
Adds all specified packages in one command, skipping already installed ones.

Notes
A backup of configuration.nix is automatically created as configuration.nix.bak before changes.

Works best with standard NixOS configuration.nix formatting: environment.systemPackages = [ ... ];

The summary table helps track exactly what was added, skipped, or auto-corrected.

Typos are handled interactively unless --yes is specified.
