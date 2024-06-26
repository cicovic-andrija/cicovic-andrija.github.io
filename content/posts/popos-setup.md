---
title: "Setup of a Pop!_OS System"
date: "2024-05-03T17:10:16Z"
categories: ["software"]
tags: ["operating-systems", "linux"]
draft: false
---

_Formerly known as "Setup of an Ubuntu System"._

This is a reference for a skeleton configuration of my Pop!_OS system. Last time tried out on
Pop!_OS 22.04 LTS.

## Core Packages

```bash
sudo apt update
sudo apt install build-essential git cmake tmux python3 libfuse2 jq mpv ffmpeg unzip wget curl tree gnome-tweaks
```

## Home Directory Cleanup

```bash
rmdir $HOME/Music/ $HOME/Pictures/ $HOME/Public/ $HOME/Templates/ $HOME/Videos/
```

## Set the PATH Environment Variable

Needed for programs that have yet to be installed.

```bash
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin:$HOME/neovim/bin' >> $HOME/.bashrc
```

## GitHub

Generate a new [SSH key for GitHub and add it to the `ssh-agent`](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

This is still a manual (non-CLI) step because GitHub's CLI client is not easily installable.

Example:

```bash
ssh-keygen -t ed25519 -C "cicovic.andrija@gmail.com"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
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

# Get the codebase, build and install for the current user.
mkdir -p $HOME/neovim
cd $HOME/src
git clone https://github.com/neovim/neovim
cd neovim
git checkout stable
make CMAKE_BUILD_TYPE=Release CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=$HOME/neovim"
make install

# Install the vim-plug plugin manager (https://github.com/junegunn/vim-plug).
# e.g.
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'

# Configure.
mkdir $HOME/.config/nvim
cp $HOME/src/dotfiles/linux/init.vim $HOME/.config/nvim/init.vim

# Update .bashrc (or alternative) with aliases.
echo 'alias vim="nvim"' >> $HOME/.bashrc
echo 'alias vimdiff="nvim -d"' >> $HOME/.bashrc
echo 'export EDITOR=nvim' >> $HOME/.bashrc

# Version info.
vim -V1 -v

# vim-plug: install all plugins.
vim +PlugInstall +qall

# Uninstall (if needed later).
#cd $HOME/src/neovim
#cmake --build build/ --target uninstall
```

## Go

Install the Go programming language toolchain:

```bash
wget "https://go.dev/dl/$(curl 'https://go.dev/VERSION?m=text' | head -n 1).linux-amd64.tar.gz" -P $HOME/Downloads/
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf $HOME/Downloads/go1.22.2.linux-amd64.tar.gz
go version
```

## Fonts

```bash
mkdir -p $HOME/.fonts
unzip $HOME/Downloads/JetBrainsMono-2.304.zip "*.ttf" "*.otf" -d $HOME/.fonts
fc-cache -f -v
```

## GNOME Configuration

```bash
gsettings set org.gnome.desktop.interface text-scaling-factor 1.25
gsettings set org.gnome.desktop.interface cursor-size 32
gsettings set org.gnome.desktop.interface clock-format 24h
gsettings set org.gnome.desktop.interface clock-show-date true
gsettings set org.gnome.desktop.interface clock-show-weekday true
gsettings set org.gnome.desktop.wm.preferences button-layout appmenu:minimize,maximize,close
gsettings set org.gnome.desktop.peripherals.touchpad natural-scroll true
gsettings set org.gnome.desktop.peripherals.touchpad two-finger-scrolling-enabled true
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
```

## Other Software

### Hugo

```bash
CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@latest
hugo version
```

### Subsurface

```bash
sudo add-apt-repository ppa:subsurface/subsurface-daily
sudo apt update && sudo apt install subsurface
subsurface --version
```
