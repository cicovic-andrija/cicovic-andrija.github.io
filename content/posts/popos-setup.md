---
title: "Setup of a Pop!_OS System"
date: "2024-05-03T17:10:16Z"
categories: ["software"]
tags: ["operating-systems", "linux"]
draft: false
---

> Formerly known as "Setup of an Ubuntu System".

This is a reference for a skeleton configuration of my Pop!_OS system. Last time tried out on
Pop!_OS 22.04 LTS.

## Core Packages

```bash
sudo apt update
sudo apt install build-essential git cmake tmux python3 libfuse2 jq mpv ffmpeg unzip curl tree
```

## GitHub

Generate a new [SSH key for GitHub and add it to the `ssh-agent`](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

Example:

```bash
ssh-keygen -t ed25519 -C "cicovic.andrija@gmail.com"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

## Home Directory Cleanup

```bash
rmdir Music/ Pictures/ Public/ Templates/ Videos/
```

## Configuration Files

```bash
mkdir -p $HOME/src
git clone git@github.com:cicovic-andrija/dotfiles.git $HOME/src/dotfiles
```

## Git

Configure git:

```bash
cp $HOME/src/dotfiles/linux/.gitconfig $HOME/.gitconfig
```

## Neovim

Build, install, and configure Neovim:

```bash
# Install missing dependencies.
sudo apt install ninja-build gettext

# Get the codebase, build and install Neovim for the current user.
mkdir -p $HOME/neovim
cd $HOME/src
git clone https://github.com/neovim/neovim
cd neovim
git checkout stable
make CMAKE_BUILD_TYPE=Release CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=$HOME/neovim"
make install

# Install vim-plug by following official instructions: https://github.com/junegunn/vim-plug
# e.g.
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'

# Configure Neovim.
mkdir $HOME/.config/nvim
cp $HOME/src/dotfiles/linux/init.vim $HOME/.config/nvim/init.vim

# Update .bashrc (or alternative) with aliases.
# alias vim="nvim"
# alias vimdiff="nvim -d"
# export EDITOR=nvim

# Update PATH (see below).

# Install plugins.
vim +PlugInstall +qall

# How to uninstall:
#cd $HOME/src/neovim
#cmake --build build/ --target uninstall
```

## Go

Install the Go programming language toolchain:

```bash
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf $HOME/Downloads/go1.22.2.linux-amd64.tar.gz

# Update PATH (see below).
```

## Set the PATH Environment Variable

```bash
# Update .bashrc (or alternative).
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin:$HOME/neovim/bin
```

## Fonts

```bash
mkdir -p $HOME/.fonts
unzip $HOME/Downloads/JetBrainsMono-2.304.zip "*.ttf" "*.otf" -d $HOME/.fonts
fc-cache -f -v
```
