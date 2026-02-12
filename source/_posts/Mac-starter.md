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
# zimfw
curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
# homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# 字体
brew install --cask font-jetbrains-mono-nerd-font
# ai coding
brew tap farion1231/ccswitch
brew install --cask cc-switch
# 自动切换输入法
brew install --cask keyboardholder
# alt tab
brew install --cask alt-tab
# 终端
brew install --cask ghostty
# 命令行工具集合
brew install htop fastfetch neovim lazygit lux git duf cmake eza curl wget
brew install yazi ffmpeg sevenzip jq poppler fd ripgrep fzf zoxide resvg imagemagick font-symbols-only-nerd-font yt-dlp
# 截图
brew install --cask pixpin
# 自建服务器远程控制
brew install --cask rustdesk
# 播放器
brew install --cask iina
# 虚拟机、容器（除了Windows）
brew install --cask orbstack
# 虚拟机（桌面包括Windows）
brew install --cask virtualbox
# 局域网传文件
brew install --cask localsend
# 全能的神器
brew install --cask raycast
# jetbrains
brew install jetbrains-toolbox
# 笔记软件
brew install --cask obsidian
# 录屏软件(轻度使用pixpin即可)
brew install --cask obs
# postman
brew install --cask postman
# IDE
open https://antigravity.google/
open https://qoder.com/download
# browser
brew install --cask google-chrome@beta
open https://www.diabrowser.com/
# office (只下载三件套即可)
open https://apps.apple.com/us/app-bundle/microsoft-365/id1450038993
# bun
curl -fsSL https://bun.sh/install | bash
# uv
curl -LsSf https://astral.sh/uv/install.sh | sh
# dracula-theme
mkdir -p ~/.config/ghostty/themes/ && curl -o ~/.config/ghostty/themes/dracula https://raw.githubusercontent.com/dracula/ghostty/refs/heads/main/dracula && echo "theme = dracula" >> ~/Library/Application\ Support/com.mitchellh.ghostty/config
# Finder settings
chflags nohidden ~/Library
defaults write com.apple.finder AppleShowAllFiles YES
defaults write com.apple.finder ShowPathbar -bool true
defaults write com.apple.finder ShowStatusBar -bool false
killall Finder;
# nodejs
curl -o- https://fnm.vercel.app/install | bash
fnm install 24
corepack enable pnpm
# lazyvim
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git
nvim
# xcode
sudo xcodebuild -license
# java
curl -s "https://get.sdkman.io" | bash
sdk install java 21.0.9-amzn
```
![final](final.jpeg)