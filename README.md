# nix-add

A small CLI helper for NixOS that lets you add packages to
`configuration.nix` without opening an editor every time.

Instead of manually editing your config and rebuilding, you can just run:
```bash
add kitty
```
The tool checks if the package exists, handles typos, updates your config,
and runs nixos-rebuild switch for you.

Features

- Add packages to environment.systemPackages

- Look up packages in Nix without changing anything

- Lookup + add in a single command

- Interactive typo correction with suggestions

- Optional non-interactive mode with --yes

- Multiple packages in one command

- Colorized terminal output

- Summary table showing what happened

- Automatic backup of configuration.nix

Installation
```bash
git clone https://github.com/akatomka/nix-add-cli.git
cd nix-add-cli
python3 nixaddlkp.py
```
Usage
Add a package
```bash
add kitty
```
Shortcut version:

```bash
+ kitty
```
This adds kitty to environment.systemPackages and runs:

```bash
sudo nixos-rebuild switch
```
Look up a package (no changes)
```bash
lkp neovim
```
Checks whether the package exists in Nix channels, but does not modify
your configuration.

Look up and add
```bash
add lkp neovim
```
Confirms the package exists

Adds it to configuration.nix

Rebuilds the system

Typo handling
```bash
add lkp neovimm
```
If a package doesn’t exist, you’ll be prompted with suggestions:

```bash
Did you mean:
  1) neovim
  2) neovim-qt
  0) Skip
```
Non-interactive mode
```bash
add lkp neovimm --yes
```
Automatically selects the closest match. Useful for scripts or batch installs.

Multiple packages
```bash
add neovim kitty htop
add lkp neovimm kitty htop
```
All packages are processed in one run.

Summary Output
After running, you’ll see a summary like this:

```bash
Package              Status       Action Taken
--------------------------------------------------
neovimm              NOT FOUND    [SELECTED] neovim
kitty                FOUND        Added
htop                 FOUND        Added
```
This makes it easy to see what was added, skipped, or corrected.

Safety Notes
Your configuration.nix is backed up automatically as:

```bash
configuration.nix.bak
```
Existing packages are not duplicated

Missing packages can be skipped safely
