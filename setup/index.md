---
layout: guide
title: Set Up Your Dev Setup
subject: setup
---

# Set Up Your Dev Setup

Programming is hard! Your brain already has a lot to do as it tries to solve complex problems and write clean and modular code and there's no time to struggle with the intricacies of package installation and annoyances of your code editor. It's a good idea to invest some time up front to set up your dev setup to help you save a few keystrokes for common programming workflows and have a nicer time while writing code, overall.

There is a whole world of dotfiles and package management to set up, but we'll focus our time today talking about 4 things:
1. Package Managment
1. Writing and Executing Code
1. Common Frameworks (especially for the rest of the talks)

Before we move on, a word of caution. At the end of the day, all of this boils down to personal preferences and style. Your mileage may vary with a lot of things here, but what's most important is to start thinking about the dev setup that works for you.

You can find the slides [here](slides.pdf)!

## Terminal

Download iTerm
```
https://www.iterm2.com/
```

Download Hyper
```
https://hyper.is/
```

## Windows Subsystem for Linux

Install a New Linux Distro:
```
https://docs.microsoft.com/en-us/windows/wsl/install-win10
```

Initialize Your New Distro:
```
https://docs.microsoft.com/en-us/windows/wsl/initialize-distro
```

## Homebrew

Install Homebrew
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Install `tree`
```
brew install tree
```

## Zsh

Install Oh My Zsh
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Install Pure Prompt
```
npm install --global pure-prompt
```

```
autoload -U promptinit; promptinit
prompt pure
```

Install `z`
```
git clone https://github.com/agkozak/zsh-z $ZSH_CUSTOM/plugins/zsh-z
```

Install `zsh-autosuggestions`
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Install `zsh-syntax-highlighting`
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Source Your Packages
```
plugins=(
    z
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```

```
vi ~/.zshrc
source ~/.zshrc
```

## Visual Studio Code

Install Visual Studio Code
```
https://code.visualstudio.com/
```

Download Fira Sans
```
https://www.fontsquirrel.com/fonts/fira-sans
```

Install Fira Sans in Visual Studio Code
```
{
    "editor.fontFamily": "'FiraCode-Retina'",
    "editor.fontLigatures": true,
}
```

Install `pdflatex`
```
brew cask install mactex
```

## Python

Install `python`
```
brew install python
```

Install `virtualenv`
```
pip install virtualenv
```

## Node.js

Install Node.js and Yarn on macOS

```
brew install node yarn
```

Install Node.js on Windows/Linux
```
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install node
```

Install Yarn on Windows/Linux
```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update & sudo apt-get install yarn
```
