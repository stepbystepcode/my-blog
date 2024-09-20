---
layout: posts
title: Mac-starter
date: 2024-09-20 21:17:55
tags:
---

浅浅记录一下装机日志
```bash
# network
curl -I https://www.google.com
# homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/stepbystep/.zprofile\n    eval "$(/opt/homebrew/bin/brew shellenv)"
brew install --cask font-jetbrains-mono-nerd-font
brew install htop ffmpeg fastfetch neovim fzf ranger miniforge lazygit lux duf cmake jenv lsd
# oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# bun
curl -fsSL https://bun.sh/install | bash
# dracula-theme
git clone https://github.com/dracula/iterm.git
# Finder settings
chflags nohidden ~/Library
defaults write com.apple.finder AppleShowAllFiles YES
defaults write com.apple.finder ShowPathbar -bool true
defaults write com.apple.finder ShowStatusBar -bool false
killall Finder;
# nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
nvm install --lts
# lazyvim
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git
nvim
# mamba
bash Miniforge3-MacOSX-arm64.sh
# xcode
sudo xcodebuild -license
# java
echo 'eval "$(jenv init -)"' >> /Users/stepbystep/.zshrc
jenv doctor
jenv add /Users/stepbystep/Library/Java/JavaVirtualMachines/corretto-21.0.4/Content/Home
jenv add /Users/stepbystep/Library/Java/JavaVirtualMachines/corretto-17.0.12/Contents/Home
jenv add /Users/stepbystep/Library/Java/JavaVirtualMachines/corretto-1.8.0_422/Contents/Home
jenv global 17
java --version
```
![final](final.jpeg)