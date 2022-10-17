## Useful Links

[Git Command Explorer - Find the right commands you need without digging through the web.](https://gitexplorer.com/)

[Git Branch | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/using-branches)

[Gitflow Workflow | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

[Deploy Websites In Seconds With Netlify - YouTube](https://www.youtube.com/watch?v=bjVUqvcCnxM&t=0s)

## Prerequisites

Setup a local folder for your GIT repo
Go to github and create the repo
Once the repo is created, transfer your files into the folder and git push them

## Setup using HTTPS

_…or create a new repository on the command line_

```bash
echo "# github-test" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/yourname/github-test.git
git push -u origin master
```

_…or push an existing repository from the command line_

```bash
git remote add origin https://github.com/yourname/github-test.git
git push -u origin master
```

_…or clone an existing repository from the command line_

```bash
git clone https://github.com/yourname/test-db.git
git push
```

## Useful CLI Commands

[Visual Studio Code on macOS](https://code.visualstudio.com/docs/setup/mac)
[Visual Studio Code on Windows](https://code.visualstudio.com/docs/setup/windows)
[Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux)

Use the command `code` to open Visual Studio Code from the Terminal Window

`code .` to open Visual Studio Code

`code index.html` to open index.html

`mkdir backend` for creating folders

`touch README.md` for creating files like `README.md`

### Basic GIT Commands

`cd` into the folder with your files

**To see the files needed for staging**

`git status`

**To see a running record of commits and to check commit messages (Press Q to quit out from this mode)**

`git log`

**To add a change in the working directory to the staging area**

`git add --all`

`git add .`

**To add commit descriptions**

`git commit –m “Put commit message here”`

**To push to the master branch**

`git push`

**To pull from the master branch**

`git pull`

**List all of the branches in your repository. This is synonymous with git branch --list. Press Q to quit out**

`git branch`

**Creating branches**

`git branch test1`

Adds the remote repo to local repo config and pushes the test1 branch to new-remote-repo

```bash
git remote add new-remote-repo https://github.com/yourname/github-test.git
git push new-remote-repo test1
```

Switching between branches and the master

```bash
git checkout master
git checkout test1
git checkout test2
```

To push the current branch and set the remote as upstream, use

```bash
git push --set-upstream origin test1
git push origin test1
```

To delete a branch (local or remote)

[Git says remote ref does not exist when I delete remote branch - Stack Overflow](https://stackoverflow.com/questions/35941566/git-says-remote-ref-does-not-exist-when-i-delete-remote-branch/35941658)

```bash
git branch -d the_local_branch
git push origin --delete the_remote_branch
```

Git clone a repo. Make sure that you delete the hidden `.git` folder inside so that you can start from scratch and upload to a new repo.

```bash
git clone https://github.com/yourname/github-test.git
cd github-test
```

### Basic GIT Merge and Merge Conflict Workflow Commands

[Git & GitHub Tutorial for Beginners #9 - Merging Branches (& conflicts) - YouTube](https://www.youtube.com/watch?v=XX-Kct0PfFc)

**GIT Merge**

If the merge commit screen comes up do the following

Press the `O` key on your keyboard to insert your text
Press the `esc` key on your keyboard to stop inserting text
Press `SHIFT : wq` to save changes and exit the screen

1. Create a branch and start making changes to the files in that branch

```bash
git branch example1
git checkout example1
```

3. Stage, then commit the changes. Return to your master branch

```bash
git add .
git commit -m "Your commit message"
git checkout master
```

4. Merge the branch changes into your master branch

```bash
git merge example1
```

5. Push the changes to your Git Repo

```bash
git push
```

**GIT Merge Conflict**

1. Resolve and fix the merge conflicts in the files associated
2. Add the files to the staging area

```bash
git add .
```

3. Commit the changes you don’t need a message as its just a merge commit

```bash
git commit
```

4. On the merge commit screen save and exit - On the keyboard press `SHIFT : wq`

```bash
:wq
```

5. See the commit messages including the merge conflict commit

```bash
git log --oneline
```

### Basic GIT Rebase Commands

[Rewriting Commit Messages in Git](https://youtu.be/4YjKY0u9Z6I)

### For rewriting previous commit messages

**To redo the last commit's message**

`git commit --amend`

**To push the last amend to the master branch**

`git push --force`

**To look over & reword the last N commits**

N = The commit in the list eg 1,2,3,4,5
a14338f9ffc302cf26bc36095e77887c32af6d66 = The name of the commit

`git rebase -i HEAD~N`

`git rebase -i HEAD~1`

`git rebase -i a14338f9ffc302cf26bc36095e77887c32af6d66`

### Retrieve specific commit from a remote Git repository

[git fetch - Retrieve specific commit from a remote Git repository - Stack Overflow](https://stackoverflow.com/questions/14872486/retrieve-specific-commit-from-a-remote-git-repository)

1. Create a folder on your local machine and initialise with GIT

```bash
git init
```

2. Pull the codebase down from the GIT repo

For the master branch

```bash
git pull --rebase <repo>
git pull --rebase https://github.com/yourname/test.git
```

For the subtree branch

```bash
git pull --rebase <repo> <branch>
git pull --rebase https://github.com/yourname/test.git tree1
```

3. Select the commit that you want to download and work from

```bash
git reset --hard <commit-hash>
git reset --hard 83d515fd4149dd8608f38ab02314897276c0307b
```

### Git Stash

[Git Tutorial: Using the Stash Command - YouTube](https://www.youtube.com/watch?v=KLEDKgMmbBI)

## Deploying a subfolder to GitHub Pages

Sometimes you want to have a subdirectory on the `master` branch be the root directory of a repository’s `gh-pages` branch. This is useful for things like sites developed with Yeoman, or if you have a Jekyll site contained in the `master` branch alongside the rest of your code.

For the sake of this example, let’s pretend the subfolder containing your site is named `dist`.

### Step 1

Remove the `dist` directory from the project’s `.gitignore` file (it’s ignored by default by Yeoman).

### Step 2

Make sure git knows about your subtree (the subfolder with your site).

```sh
git add dist && git commit -m "Initial dist subtree commit"
```

### Step 3

Use subtree push to send it to the `gh-pages` branch on GitHub.

```sh
git subtree push --prefix dist origin gh-pages
```

Boom. If your folder isn’t called `dist`, then you’ll need to change that in each of the commands above.

---

If you do this on a regular basis, you could also create a script containing the following somewhere in your path:

```sh
#!/bin/sh
if [ -z "$1" ]
then
  echo "Which folder do you want to deploy to GitHub Pages?"
  exit 1
fi
git subtree push --prefix $1 origin gh-pages
```

Which lets you type commands like:

```sh
git gh-deploy path/to/your/site
```

### VIM Mode Commands

[Basic Vim commands - For getting started (Example)](https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started)

Vim has two modes.

1. Insert mode (Where you can just type like normal text editor. Press i for insert mode)
2. Command mode (Where you give commands to the editor to get things done. Press ESC for command mode)

Most of them below are in command mode

- x - to delete the unwanted character
- u - to undo the last the command and U to undo the whole line
- CTRL-R to redo
- A - to append text at the end
- :wq - to save and exit
- :q! - to trash all changes
- dw - move the cursor to the beginning of the word to delete that word
- 2w - to move the cursor two words forward.
- 3e - to move the cursor to the end of the third word forward.
- 0 (zero) to move to the start of the line.
- d2w - which deletes 2 words .. number can be changed for deleting the number of consecutive words like d3w
- dd to delete the line and 2dd to delete to line .number can be changed for deleting the number of consecutive words

## How to remove node_modules

1. Create a `.gitignore` file in the git repository if it does not contain one

`touch .gitignore` 2. Open up the `.gitignore` and add the following line to the file

node_modules 3. Remove the `node_modules` folder from the git repository

`git rm -r --cached node_modules` 4. Commit the git repository without the node modules folder

`git commit -m "Removed node_module folder"` 5. Push the repository to github

`git push origin master`

After all of that, you should also add the `.gitignore` and commit it to the repository

`git add .gitignore`

`git commit -m "Updated the .gitignore file`

`git push origin master`
