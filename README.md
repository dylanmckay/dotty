# polk

Dotfile manager.

# Installation

## With Cargo

```bash
cargo install polk
```

# Examples

```bash
# Grab and symlink dotfiles from my GitHub account.
# (assumes repository named 'dotfiles')
polk setup github:dylanmckay

# Grab and symlink dotfiles from another repository.
polk setup github:dylanmckay/otherdotfiles

# Download dotfiles to a local cache folder but don't create symlinks
polk grab github:dylanmckay

# Create symlinks to the currently grabbed dotfiles
polk link

# Update the dotfiles (via git)
polk update

# Remove all symlinks created by polk.
polk unlink

# Remove all symlinks and cached dotfiles/repositories (~/.polk)
polk forget

# Print a bunch of information
polk info
```

# Your dotfiles repository

A repository would generally look something like this

```
.
..
.bashrc
.rspec
.tmux.conf
.tmux.linux.conf
.vim
.config/awesome/config.lua
README.md
```

# How symlinking works works

Here is a table of how dotfiles within a repository map to symlinks in `$HOME`.

| File                          | Symlink                                                    |
| ----------------------------- | ---------------------------------------------------------- |
|  `.bashrc`                    |  `~/.bashrc -> ~/<dotfiles repository path>/.bashrc`       |
| `.tmux.conf`                  |  `~/.tmux.conf -> ~/<dotfiles repository path>/.tmux.conf` |
| `.config/awesome/config.lua`  |  `~/.config/awesome/config.lua -> ~/<dotfiles repository path>/.config/awesome/config.lua` |

#### Handling of config files in subdirectories

As you can see in the above table, if a dotfile resides in a subdirectory(s), those directories
will get created in `$HOME` and then a symlink to the dotfile will be created within the subdirectories.

It is not possible with this tool to symlink an entire directory within a dotfiles repository to `$HOME`.
If this were possible, applications would/could write new files into the repository, which isn't good.

