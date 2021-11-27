# How I setup my Development Environment on macOS 2021 Edition

**Current Full-Stack Developer Technical Stack 2021**

Front-End: HTML, CSS,  JavaScript, Typescript, React, React Native, Redux, Flutter/Dart

Back-End: Python, NodeJS, SQL, NoSQL, Kotlin

## Transfer Files

Either use a cloud backup solution to restore your data or use an external storage device to transfer your files to your new computer.

## Install Web Browsers

Google Chrome

Google Chrome Canary

Firefox

Firefox Developer Edition

Firefox Nightly

Safari Technology Preview

Tor Browser

### Install Web Browser Extensions (chrome)

Adblock Plus

Apollo Client Developer Tools

Bitwarden

ColorZilla

Honey

JSON Viewer

Lighthouse

Momentum

React Developer Tools

Redux DevTools 

Pocket

Video DownlodHelper

Wappalyzer

Web Developer

daily.dev

## Install Software

I would install all of the apps that I use this includes personal and developer related. So tools like Adobe CC, Microsoft Office, Discord, Slack etc.... I will just include the developer apps as they are more relevant in this guide.

### Developer Apps

Android Studio

Docker

Hyper

Insomnia

IntelliJ IDEA CE

iTerm 2

MongoDB Compass

Postman

Valentina Studio

Visual Studio Code

Xcode

## Install Package Managers

- Hombrew
- npm
- Pip

### Hombrew

[https://brew.sh/](https://brew.sh/)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### Install Packages

- Hombrew automatically installs Pip pointing to the Homebrew’d Python 3 for you

You can install [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) through the Homebrew package manager. This will also install Node.js if it is not already installed. If you use nvm or similar you should exclude installing Node.js so that nvm’s version of Node.js is used. 

Use brew to install the below packages

```bash
brew install tree (It allows you to view all files in a tree view)
brew install ruby
brew install git
brew install node
brew install python
brew install kotlin
brew install postgresql
brew install yarn or brew install yarn --without-node
brew tap heroku/brew && brew install heroku
brew install graphql-playground
brew install deno
```

**Install oh-my-zsh**

ZSH is already preinstalled in the latest versions of macOS. Catalina onwards I believe. I also install [https://ohmyz.sh/](https://ohmyz.sh/) as it allows for more configuration and is required in some cases.

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Use the command line to show all hidden files as the files you are searching for are going to be hidden by default.

```bash
defaults write com.apple.Finder AppleShowAllFiles true
killall Finder
```
Install the Oh My Zsh plugins below

```bash
brew install zsh-autosuggestions
brew install zsh-syntax-highlighting
```

To activate the plugins, add the following at the end of your .zshrc:

  ```bash
source /usr/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
  ```

You will also need to force reload of your .zshrc: 

```bash
source ~/.zshrc
```

If you receive "highlighters directory not found" error message, you may need to add the following to your .zshenv:

```bash
export ZSH_HIGHLIGHT_HIGHLIGHTERS_DIR=/usr/local/share/zsh-syntax-highlighting/highlighters
```

**MongoDB Install and Setup**

[https://stackoverflow.com/questions/57856809/installing-mongodb-with-homebrew](https://stackoverflow.com/questions/57856809/installing-mongodb-with-homebrew)

1. Install the Xcode command-line tools and the Homebrew from https://brew.sh/#install

```bash
xcode-select --install
```

2. Tap the MongoDB Homebrew Tap:

```bash
brew tap mongodb/brew
```

3. Verify installation prerequisites in the macOS Terminal:

```bash
brew tap | grep mongodb
```

4. install MongoDB

```bash
brew install mongodb-community@4.4
```

5. Finally to run MongoDB (i.e. the mongod process) as a macOS service, issue the following

```bash
brew services start mongodb-community@4.4
```

6. Download and install MongoDB Compass [https://www.mongodb.com/try/download/compass](https://www.mongodb.com/try/download/compass)

Use the command `brew list` to see all installed packages

### npm

#### Install Packages Globally

```bash
npm i -g babel-cli
npm i -g eslint
npm i -g expo-cli
npm i -g firebase-tools
npm i -g gatsby-cli
npm i -g jest
npm i -g lighthouse
npm i -g netlify-cli
npm i -g newman
npm i -g node-sass
npm i -g parcel-bundler
npm i -g pm2
npm i -g prettier
npm i -g serve
npm i -g spaceship-prompt
npm i -g surge
npm i -g typescript
npm i -g update
npm i -g vercel
npm i -g yarn
```

Use the command `npm list -g --depth 0` to see all installed packages

### Pip

#### Install Packages

Use the command `pip` or `pip3` to install depending on your system.

```bash
pip3 install astroid
pip3 install autopep8
pip3 install certifi
pip3 install chardet2
pip3 install click
pip3 install Flask
pip3 install Flask-Cors
pip3 install harperdb
pip3 install idna
pip3 install isort
pip3 install itsdangerous
pip3 install Jinja
pip3 install lazy-object-proxy
pip3 install MarkupSafe
pip3 install mccabe
pip3 install psycopg2
pip3 install psycopg2-binary
pip3 install pycodestyle
pip3 install pylint
pip3 install python-dotenv
pip3 install requests
pip3 install setuptools
pip3 install six
pip3 install toml
pip3 install urllib3
pip3 install Werkzeug
pip3 install wrapt
```

Use the command `pip3 list` or `pip list` to see all installed packages

## Flutter Setup

[https://flutter.dev/docs/get-started/install/macos](https://flutter.dev/docs/get-started/install/macos)

Also install the Flutter/Dart and Kotlin plugins and extensions for Visual Studio Code, IntelliJ IDEA CE, and Android Studio.

## React Native Setup

https://expo.io/

## Setup Terminal App and Code Editors

I am currently using the [dracula](https://draculatheme.com/) theme in Visual Studio Code, IntelliJ IDEA CE, Android Studio and the Hyper Terminal.

### Typeface

For typefaces I am using Jebrains Mono and FiraCode is currently my second choice.

[https://www.jetbrains.com/lp/mono/](https://www.jetbrains.com/lp/mono/)

[https://github.com/tonsky/FiraCode](https://github.com/tonsky/FiraCode)

### Hyper Terminal

**Install Plugins and customize** 

```bash
hyper i hypercwd
hyper i hyper-snazzy
hyper i hyper-dracula
```

```javascript
// default font size in pixels for all tabs
    fontSize: 16,

// font family with optional fallbacks
    fontFamily: 'JetBrains Mono, Menlo, "DejaVu Sans Mono", Consolas, "Lucida Console", monospace',
```

### Visual Studio Code

If it is your first time using Visual Studio Code then do a clean install and configure it whicever way you want. Otherwise install the Settings Sync extension by Shan Khan and then do a download to sync your settings. 

```bash
# Upload
SHIFT + OPTION + U

# Download
SHIFT + OPTION + D 
```

**As of January 2021 Visual Studio Code has a Settings Sync Feature which probably works the same but is in Early Release**.

Set Visual Studio Code as the default editor for programming files by right clicking on that file, and going to "Open with" then change all.

Configure Visual Studio Code so that you can [Launch from the command line](https://code.visualstudio.com/docs/setup/mac)

#### Extensions I have installed with Visual Studio Code

  better-comments

  bracket-pair-colorizer

  code-beautifier

  code-settings-sync

  dart-code

  debugger-for-chrome

  dotenv

  es7-react-js-snippets

  flutter

  gc-excelviewer

  gitlens

  graphql-for-vscode

  HTMLHint

  javascript-ejs-support

  jupyter

  Kotlin

  LiveServer

  material-icon-theme

  mdx

  mongodb-vscode

  mssql

  night-owl

  npm-intellisense

  open-in-browser

  prettier-vscode

  project-manager

  python

  quokka-vscode

  rainbow-csv

  remote-containers

  shades-of-purple

  theme-dracula

  vsc-community-material-theme

  vsc-material-theme

  vsc-material-theme-icons

  vscode-color

  vscode-colorize

  vscode-docker

  vscode-eslint

  vscode-graphql

  vscode-import-cost

  vscode-jest

  vscode-markdownlint

  vscode-npm-script

  vscode-peacock

  vscode-pull-request-github

  vscode-styled-components

  vscode-typescript-tslint-plugin