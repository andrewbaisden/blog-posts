**Current Software Developer Technical Stack 2022**

Front-End: HTML, CSS, JavaScript, TypeScript, React, React Native, Redux  
Back-End: Python, NodeJS, C#, SQL, NoSQL, Docker

## Transfer Files

I always prefer to do a clean install when setting up a new computer. Either use a cloud backup solution to restore your data or use an external storage device to transfer your files to your new computer.

## Install Web Browsers

- [Brave](https://brave.com/)
- [Google Chrome](https://www.google.com/intl/en_uk/chrome/)
- [Google Chrome Canary](https://www.google.com/intl/en_uk/chrome/canary/)
- [Firefox](https://www.mozilla.org/en-GB/firefox/new/)
- [Firefox Developer Edition](https://www.mozilla.org/en-GB/firefox/developer/)
- [Firefox Nightly](https://www.mozilla.org/en-GB/firefox/channel/desktop/)
- [Microsoft Edge](https://www.microsoft.com/en-us/edge)
- [Safari Technology Preview](https://developer.apple.com/safari/technology-preview/)
- [Tor Browser](https://www.torproject.org/download/)

### Install Web Browser Extensions (chromium)

- [Bitwarden](https://chrome.google.com/webstore/detail/bitwarden-free-password-m/nngceckbapebfimnlniiiahkandclblb)
- [ColorZilla](https://chrome.google.com/webstore/detail/colorzilla/bhlhnicpbhignbdhedgjhgdocnmhomnp)
- [daily.dev](https://chrome.google.com/webstore/detail/dailydev-the-homepage-dev/jlmpjdjjbgclbocgajdjefcidcncaied)
- [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh)
- [Lighthouse](https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk)
- [Momentum](https://chrome.google.com/webstore/detail/momentum/laookkfknpbbblfpciffpaejjkokdgca)
- [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)
- [Pocket](https://chrome.google.com/webstore/detail/save-to-pocket/niloccemoadcdkdjlinkgdfekeahmflj)
- [uBlock Origin](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)
- [Video DownlodHelper](https://chrome.google.com/webstore/detail/video-downloadhelper/lmjnegcaeklhafolokijcfjliaokphfk)
- [Wappalyzer](https://chrome.google.com/webstore/detail/wappalyzer-technology-pro/gppongmhjkpfnbhagpmjfkannfbllamg)
- [Web Developer](https://chrome.google.com/webstore/detail/web-developer/bfbameneiokkgbdmiekhjnmfkcnldhhm)

## Install Software

I would install all of the apps that I use this includes personal and developer related. I will just include the developer apps as they are more relevant in this guide.

- [Adobe CC](https://www.adobe.com/uk/)
- [Android Studio](https://developer.android.com/studio?gclid=CjwKCAiA6Y2QBhAtEiwAGHybPTTF6mpurPpUq-hlu7vquMnAkoaWuUX4w51Anb19wMDuxkItdThqlBoCQr8QAvD_BwE&gclsrc=aw.ds)
- [Bitwarden](https://bitwarden.com/)
- [Centered](https://www.centered.app)
- [Cypress](https://www.cypress.io/)
- [Discord](https://discord.com/)
- [Docker](https://www.docker.com/)
- [Figma](https://www.figma.com/)
- [Hyper](https://hyper.is/)
- [iTerm 2](https://iterm2.com/)
- [Microsoft Office](https://www.microsoft.com/en-gb/microsoft-365/microsoft-office)
- [Microsoft Teams](https://www.microsoft.com/en-gb/microsoft-teams/group-chat-software)
- [MongoDB Compass](https://www.mongodb.com/products/compass)
- [Notion](https://www.notion.so/)
- [Obsidian](https://obsidian.md/)
- [PyCharm](https://www.jetbrains.com/pycharm/)
- [Slack](https://slack.com/intl/en-gb/)
- [Todoist](https://todoist.com/home)
- [Trello](https://trello.com/en-GB)
- [Valentina Studio](https://www.valentina-db.com/en/)
- [Visual Studio](https://visualstudio.microsoft.com/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Xcode](https://apps.apple.com/gb/app/xcode/id497799835?mt=12)
- [Zoom](https://zoom.us/)

## Install Package Managers

- Hombrew
- npm
- Pip

### Hombrew

[https://brew.sh/](https://brew.sh/)

**M1 Macs**
Before installing Homebrew you will need to install the Rosetta2 emulator for the new ARM silicon (M1 chip). Install Rosetta2 using the terminal:

```bash
/usr/sbin/softwareupdate --install-rosetta --agree-to-license
```

After installing Rosetta2 using the code above you can then use the Homebrew cmd and install Homebrew for ARM M1 chip.

```bash
arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Once Homebrew for M1 ARM is installed use this Homebrew command to install packages:

```bash
arch -x86_64 brew install <package>
```

#### Install Packages

- Hombrew automatically installs Pip pointing to the Homebrew’d Python 3 for you.

Use brew to install the below packages

```bash
brew install tree (It allows you to view all files in a tree view)
brew install ruby
brew install git
brew install python
brew install kotlin
brew install postgresql
brew install yarn --without-node
brew tap heroku/brew && brew install heroku
brew install deno
brew install watchman
```

**Install oh-my-zsh**

ZSH is already preinstalled in the latest versions of macOS. I also install [https://ohmyz.sh/](https://ohmyz.sh/) as it allows for more configuration and is required in some cases.

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

1. Install the Xcode command-line tools and the Homebrew one from https://brew.sh/#install

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

Use the command `brew list` to see all installed packages.

### npm

Install node via nvm because `nvm` lets you quickly install and use different versions of node via the command line.

[https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)

#### Install Packages Globally

```bash
npm i -g @aws-amplify/cli
npm i -g @sanity/cli
npm i -g babel-cli
npm i -g expo-cli
npm i -g firebase-tools
npm i -g gatsby-cli
npm i -g lighthouse
npm i -g netlify-cli
npm i -g newman
npm i -g node-sass
npm i -g parcel-bundler
npm i -g pm2
npm i -g serve
npm i -g spaceship-prompt
npm i -g surge
npm i -g typescript
npm i -g update
npm i -g vercel
npm i -g yarn
```

Use the command `npm list -g --depth 0` to see all installed packages.

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

#### Updating Python Packages

Pip can be used to upgrade all packages:

1. Output a list of installed packages into a requirements file (requirements.txt):

```shell
pip freeze > requirements.txt
```

2. Edit requirements.txt, and replace all `==` with `>=` Use the ‘Replace All’ command in the editor.
3. Upgrade all outdated packages:

```shell
pip install -r requirements.txt --upgrade
```

## React Native Setup

https://expo.io/

## Setup BASH Application, Code Editors and IDE

I am currently using the [dracula](https://draculatheme.com/) theme in Visual Studio Code, Visual Studio, Android Studio, PyCharm and both Hyper and iTerm 2.

### Typeface

For typefaces I am using Jebrains Mono.

[https://www.jetbrains.com/lp/mono/](https://www.jetbrains.com/lp/mono/)

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

### Visual Studio

Download and install the latest version of [NET, including ASP.NET Core](https://dotnet.microsoft.com/en-us/download).

### Visual Studio Code

If it is your first time using Visual Studio Code then do a clean install and configure it however you want. Otherwise use the built in [Settings Sync](https://code.visualstudio.com/docs/editor/settings-sync) feature to sync the settings from your previous setup.

#### Visual Studio Code Extensions I use

I currently have 41 extensions installed.

[Beautify css/sass/scss/less](https://marketplace.visualstudio.com/items?itemName=michelemelluso.code-beautifier)
[Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments)
[C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
[colorize](https://marketplace.visualstudio.com/items?itemName=kamikillerto.vscode-colorize)
[Data Workspace](https://marketplace.visualstudio.com/items?itemName=ms-mssql.data-workspace-vscode)
[Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
[DotENV](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv)
[Dracula Official](https://marketplace.visualstudio.com/items?itemName=dracula-theme.theme-dracula)
[EJS language support](https://marketplace.visualstudio.com/items?itemName=DigitalBrainstem.javascript-ejs-support)
[ES7+ React/Redux/React-Native snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
[Excel Viewer](https://marketplace.visualstudio.com/items?itemName=GrapeCity.gc-excelviewer)
[GitHub Pull Requests and Issues](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
[GitLens — Git supercharged](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
[HTMLHint](https://marketplace.visualstudio.com/items?itemName=mkaufman.HTMLHint)
[Import Cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)
[Jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest)
[Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)
[Jupyter Keymap](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter-keymap)
[Jupyter Notebook Renderers](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter-renderers)
[Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
[markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
[MDX](https://marketplace.visualstudio.com/items?itemName=silvenon.mdx)
[MongoDB for VS Code](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode)
[npm](https://marketplace.visualstudio.com/items?itemName=eg2.vscode-npm-script)
[npm Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)
[open in browser](https://marketplace.visualstudio.com/items?itemName=techer.open-in-browser)
[Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
[Project Manager](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager)
[Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
[Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
[Rainbow CSV](https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv)
[Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
[Shades of Purple](https://marketplace.visualstudio.com/items?itemName=ahmadawais.shades-of-purple)
[SQL Database Projects](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sql-database-projects-vscode)
[SQL Server (mssql)](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)
[SVG](https://marketplace.visualstudio.com/items?itemName=jock.svg)
[Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)
[TSLint](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-tslint-plugin)
[vscode-styled-components](https://marketplace.visualstudio.com/items?itemName=styled-components.vscode-styled-components)
