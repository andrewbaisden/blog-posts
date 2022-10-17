This guide is for macOS however it should be easy enough to get it working on Windows and Linux assuming the same software and tools are available as well otherwise use alternatives. Just use the commands appropriate for that operating system when doing the installation.

This is a clean install so you might need to restart the Terminal/Mac a few times before everything works properly.

## Install Software

**Web Browsers (Normal, Developer, and Nightly Builds)**

Chrome

Firefox

Safari

**Code Editor and Terminal Apps**

Visual Studio Code (Install shell commands too)

Hyper and iTerm 2 plus Oh My Zsh

**Design Tools**

Adobe CC

Figma/Adobe XD/Sketch

**API Test Tools**

Postman/Insomnia

**Documentation Browser**

devdocs.io (Chrome installation)

**File Transfer Tools**

Cyberduck/Transmit

## Install Developer and Web Browser Tools

Adblock Plus

Apollo Client Developer Tools (Chrome)

ColorZilla

Honey

JSON Viewer (Chrome)

LastPass

Lighthouse

Momentum

Notion Web Clipper (Only when and if you have Notion Installed)

React Developer Tools

Redux DevTools

Video DownlodHelper

Vue.js Devtools

Wappalyzer

Web Developer (Chrome)

### Install Programming Font for Code Editors and Terminal Applications

[GitHub - tonsky/FiraCode: Monospaced font with programming ligatures](https://github.com/tonsky/FiraCode)

- Visual Studio Code
- Hyper
- iTerm 2

### Install Python, pip, and the AWS CLI on macOS

#### Install and setup AWS Accounts

[Configuring the AWS CLI - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-quick-configuration)

[Install the AWS Command Line Interface on macOS - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-install-macos.html)

[macos - AWS CLI $PATH Settings - Stack Overflow](https://stackoverflow.com/questions/26574232/aws-cli-path-settings)

1. Download and install Python
2. Download pip https://bootstrap.pypa.io/get-pip.py
3. `cd` into the folder with the downloaded pip file and in your terminal use the command below

```bash
python3 get-pip.py
```

4. Use pip to install the AWS CLI.

```bash
pip3 install awscli --upgrade --user
```

5. Verify that the AWS CLI is installed correctly.

```bash
aws --version
```

If the executable cant be found then add it to your command line path depending on where python installed it.

Find your shell's profile script in your user folder. If you are not sure which shell you have, run `echo $SHELL`

```bash
Bash – .bash_profile, .profile, or .bash_login.
Zsh – .zshrc (zsh is the one in use right now)
Tcsh – .tcshrc, .cshrc or .login.
```

```bash
yourName/.zshrc
```

Add the export command to the profile script

```bash
export PATH=/Users/yourName/Library/Python/3.6/bin/:$PATH
```

### Install Hombrew

[Brew Install](https://brew.sh/)

[FAQ — Homebrew Documentation](https://docs.brew.sh/FAQ)

Install Hombrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

**How do I update my local packages?**

First update the formulae and Homebrew itself:

```bash
brew update
```

You can now find out what is outdated with:

```bash
brew outdated
```

Upgrade everything with:

```bash
brew upgrade
```

Or upgrade a specific formula with:

```bash
brew upgrade <formula>
```

You can install [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) through the Homebrew package manager. This will also install Node.js if it is not already installed. If you use nvm or similar you should exclude installing Node.js so that nvm’s version of Node.js is used.

Use brew to install the below packages

```bash
brew install tree (It allows you to view all files in a tree view)
brew install ruby
brew install git
brew install mongodb
brew install yarn or brew install yarn --without-node
brew install heroku
brew install graphql-playground
brew install deno
```

**Full brew list installed packages**

```bash
deno            heroku-node     openssl         python@2        sqlite
gdbm            icu4c           openssl@1.1     python@3.8      tree
gettext         libyaml         pcre2           readline        xz
git             mongodb         pkg-config      ruby            yarn
heroku          node            python          sphinx-doc
```

### Install MongoDB Compass

[Install MongoDB Community Edition on macOS — MongoDB Manual 3.6](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

[Install Compass — MongoDB Compass stable](https://docs.mongodb.com/compass/master/install/)

[Connection String URI Format — MongoDB Manual 3.6](https://docs.mongodb.com/manual/reference/connection-string/)

### Install Node Version Manager

Use it to install Nodejs and NPM

[Node Version Manager](https://nodejs.org/en/download/package-manager/)

[node.js - How to update node with nvm - Stack Overflow](https://stackoverflow.com/questions/34810526/how-to-update-node-with-nvm)

### Use NPM to install packages

```bash
npm i --global @gridsome/cli @vue/cli babel-cli eslint firebase-tools gatsby-cli jest lighthouse netlify-cli newman node-sass nodemon now npm parcel-bundler pm2 prettier serve spaceship-prompt surge update
```

**Globally Installed Packages**

```bash
├── @gridsome/cli@0.0.9
├── @vue/cli@3.12.1
├── babel-cli@6.26.0
├── eslint@5.16.0
├── firebase-tools@6.12.0
├── gatsby-cli@2.12.65
├── jest@25.5.4
├── lighthouse@4.3.1
├── netlify-cli@2.58.0
├── newman@4.6.1
├── node-sass@4.14.1
├── nodemon@1.19.4
├── now@17.1.1
├── npm@6.14.7
├── parcel-bundler@1.12.4
├── pm2@4.4.0
├── prettier@1.19.1
├── serve@11.3.2
├── spaceship-prompt@3.11.2
├── surge@0.20.5
└── update@0.7.4
```

**Locally Installed Packages**

webpack and webpack Dev Server (Locally). Note that a global webpack installation is not a recommended practice. This locks you down to a specific version of webpack and might fail in projects that use a different version.

**NPM Versioning Files Example**

5.17.1

The first number is the major version number also known as a significant new release with major changes like a new design or big feature set. Or when there is a break so the functionality requires a new build.

The second number is the minor version number also known as new feature updates.

The third number is the patch version number also known as bug fixes and performance increases to the build.
