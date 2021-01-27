# Custom VS Code Title Bar/Theme for Front-End and Back-End Projects (macOS Guide)

This guide will give you some basic exposure to Bash scripting. If you want to have more of a deep dive then you can check out a cheat sheet or tutorial which is beyond the scope of this guide [Bash Cheatsheet](https://devhints.io/bash) Two great VS Code extensions for changing your workspace are [Peacock](https://marketplace.visualstudio.com/items?itemName=johnpapa.vscode-peacock) (my preference) and [ColorTabs](https://marketplace.visualstudio.com/items?itemName=orepor.color-tabs-vscode-ext)

![The Visual Studio Code Editor, with a color scheme title bar for Back-End Projects](https://dev-to-uploads.s3.amazonaws.com/i/56jv935lf67o0obz41iv.png)
![The Visual Studio Code Editor, with a color scheme title bar for Front-End Projects](https://dev-to-uploads.s3.amazonaws.com/i/xvwd19yjmb50akj4d6ln.png)

Creating Bash scripts gives you a manual way to do this and you will also learn how to create Bash scripts. This guide is for macOS however you should be able to adapt it for any operating system. Just do your research (google) and use the appropriate commands and files for your operating system.

The VS Code theme I have installed as of writing is [Night Owl — Sarah Drasner](https://marketplace.visualstudio.com/items?itemName=sdras.night-owl) You can probably use any theme you want just be aware that you will be changing the title bar color. This is completely optional however i believe its both visually appealing and it makes it easier for anyone to distinguish between a front-end and back-end project. So for example you can have two VS Code windows open one for front-end and the other for back-end. Great for when you are working on full-stack applications or even just one of the two. And you will know which one is which just by looking at the title bar.

This is inspired by Wes Bos who i saw first saw using it in his course [Advanced React & GraphQL — Build Full Stack Applications with React and GraphQL](https://advancedreact.com/) You can get his theme [Cobalt2 Theme Official for VS Code](https://marketplace.visualstudio.com/items?itemName=wesbos.theme-cobalt2) 

## Prerequisites
First make sure that your Visual Studio Code editor is set up for custom title bars.

Code > Preferences > Settings

In the search box type “title”

1. Uncheck the box for Window: Native Tabs
2. Set Window Titlebar Style to: Custom (You might need to restart the code editor to get it working)
3. Click on the hamburger menu and select Open settings.json. Go to the Workspace Settings tab.

A file and folder tree will automatically be created in the folder you opened in your code editor. It will use the workspace settings in VS Code. Examples can be seen below. This is the manual way to have a custom workspace but i think it’s much faster and feels more natural to do it using the terminal once you have it set up. Anyone who is used to using their terminal for setting up projects in Javascript, React, Vue or other frameworks will understand this. The same is true of anyone who uses npm or yarn for installing project dependencies its just a natural part of the developer workflow.

*Folder Tree*

```bash
└── .vscode/
└── settings.json/
```

*settings.json*

```json
{
	"workbench.colorCustomizations": {
		"titleBar.activeForeground": "#000",
		"titleBar.inactiveForeground": "#000000CC",
		"titleBar.activeBackground": "#F3DB04",
		"titleBar.inactiveBackground": "#f3db04bd"
	}
}

```

# Setup
1. Create a bin directory

The first thing that you need to do is create a bin directory. Because bin is the normal naming convention for executable programs which are held in a subdirectory. Also make sure that you are in the main directory for users. It is always the default directory that the Terminal App will open in. Using the command `pwd`  in your terminal window will give you the current location too. Replace YOURNAME with your actual username for your computer home directory.

/Users/YOURNAME

Create a bin folder in that directory.

```bash
cd ~      # this takes us to /Users/YOURNAME
mkdir bin # this creates /Users/YOURNAME/bin
```

2. Export your bin directory to the PATH

If you don’t see hidden files and directories or those that begin with a full stop/dot. Press `Command + SHIFT + .`  on your keyboard [Quickly Show/Hide Hidden Files on macOS](https://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/)

Make sure that you are in /Users/YOURNAME/ and open the .bash_profile file in your code editor. Create .bash_profile if it does not exist. Add the code below and save the file.

```bash
export PATH=$PATH:/Users/YOURNAME/bin
```

If you have Oh My Zsh installed open .zshrc which will be located at /Users/YOURNAME/.zshrc and add this line to the file.

```bash
export PATH=$HOME/bin:/usr/local/bin:$PATH
```

3. Create a script file and make it an executable

Navigate to the bin folder located in /Users/YOURNAME

```bash
cd bin
```

Create a file called dev-back-end (with no extension) in this folder.

```bash
touch dev-back-end
```

Open the file in your text editor of choice and add the following.

```bash
#!/bin/bash
```

Bash scripts need to start with *#!/bin/bash* so that the OS knows that it must use bash and not a different shell. It is a term referred to as “shebang”. Using the command *which bash* will show you where it’s located. The file needs to be an executable to work so change its file permissions using the code below in the terminal.

```bash
chmod u+x dev-back-end
```

Add the code below to the file dev-back-end

```bash
#!/bin/bash
mkdir .vscode
cd .vscode
cat <<END >settings.json
{
    "workbench.colorCustomizations": {
        "titleBar.activeForeground": "#000",
        "titleBar.inactiveForeground": "#000000CC",
        "titleBar.activeBackground": "#FF2C70",
    "titleBar.inactiveBackground": "#FF2C70CC"
    }
}
END
```

Duplicate dev-back-end and rename the copied file to dev-front-end. Add the code below.

```bash
#!/bin/bash
mkdir .vscode
cd .vscode
cat <<END >settings.json
{
    "workbench.colorCustomizations": {
        "titleBar.activeForeground": "#000",
        "titleBar.inactiveForeground": "#000000CC",
        "titleBar.activeBackground": "#FFC600",
        "titleBar.inactiveBackground": "#FFC600CC"
    }
}
END
```

Your folder tree should look like below.

```bash
└── bin/
|── dev-back-end/
└── dev-front-end/
```

4. Working on Visual Studio Code Projects

Now when you are starting a project the first thing that you should do is cd into that folder and run the front end or back end command from your terminal app. This should create a *.vscode/settings.json* folder and file structure that will have your custom workspace settings. You can easily customise the colour scheme to match your theme or brand by changing the json settings in the bash files. You can get these from workspace settings in VS Code. Obviously add your own custom settings to the file as well. The name that you give the file will be the name that you must run in your terminal app it can be anything you want.

*Back-end Developer Project*

```bash
dev-back-end
```

*Front-end Developer Project*

```bash
dev-front-end
```

*VS Code Workspace Settings*

```bash
└── .vscode/
└── settings.json/
```