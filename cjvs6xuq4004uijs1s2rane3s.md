---
title: "Git Cheat Sheet for Beginners and Intermediates"
datePublished: Sun Feb 17 2019 23:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cjvs6xuq4004uijs1s2rane3s
slug: git-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1648108038820/6n-Po2XK6.png
tags: github, git, command-line, cli, cheatsheet

---


Git cheat sheet saves you time when you just can't remember a specific command. It is hard to memorize all the important Git commands as a newbie, most times Senior Developers forget too. This is why you need a reference you can come back to when you get stuck.

In this article, I'd show you the basic Git commands to help you learn Git, and more advanced concepts around Git branches, remote repositories, reverting changes, and more. At the end of this article, I'd also show you some Version Control Best Practices.

Let's get started :)

**Cheat Sheet Contents**
- Git Basics
- Reverting Changes
- Rewriting Git History
- Git Branches
- Remote Repositories
- git config
- git log
- git dif
- git reset
- Version Control best practises

I believe you already know git and you probably should be using it, but in case you don't know:

> 
Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. Git manages your source code history and versions. More details  [here](https://git-scm.com/) 

**Cheat Sheet**

| command                                               |  usage                                                                                                                                                                     |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| git init                                              |  Creates an empty Git repository in the specified directory.                                                                                                               |
| git clone <repository name>                           |  Clones a repository located at <repository name> onto your local machine.                                                                                                 |
| git add <directory>                                   |  Stages only the specified changes for the next commit. Replace <directory> with a <file> to change a specific file.                                                       |
| git add .                                             |  Stages new files and modifications without deletions                                                                                                                      |
| git add -A                                            |  Stages all changes                                                                                                                                                        |
| git add -all                                          |  Equivalent to git add -A                                                                                                                                                  |
| git add -u                                            |  Stages modifications and deletions without adding new files                                                                                                               |
| git add --update                                      |  Equivalent to git add -u                                                                                                                                                  |
| git commit -m ”<message>”                             |  Commits the staged snapshot. replace <message> with the commit message.                                                                                                   |
| git status                                            |  List which files are staged unstaged and untracked.                                                                                                                       |
| git log                                               |  Displays the entire commit history using the default format.                                                                                                              |
| git diff                                              |  Shows unstaged changes between your index and working directory.                                                                                                          |
| git pull                                              |  Fetchs the remote copy of the current branch.                                                                                                                             |
| git pull --rebase <remote>                            |  Fetchs the remote copy of current branch and rebases it into the local copy. Use git rebase instead of merge to integrate the branches.                                   |
| git push origin master                                |  Push all of your commits to master branch.                                                                                                                                |
| git push <remote> --all                               |  Push all of your local branches to the specified remote.                                                                                                                  |
| git push <remote> --tags                              |  Tags aren’t automatically pushed when you push a branch or use the --all flag. The --tags flag sends all of your local tags to the remote repo.                           |
| git push <remote> --force                             |  Forces the git push even if it results in a non-fast-forward merge. Do not use the --force flag unless you’re absolutely sure you know what you’re doing.                 |
|                                                       |                                                                                                                                                                            |
| git revert <commit>                                   |  Creates new commit that undoes all of the changes made in <commit> and then applys it to the current branch.                                                              |
| git reset <file>                                      |  Removes <file> from the staging area but leaves the working directory unchanged - This unstages a file without overwriting any changes.                                   |
| git clean -n                                          |  Shows which files would be removed from working directory. Use the -f flag in place of the -n flag to execute the clean.                                                  |
|                                                       |                                                                                                                                                                            |
| git commit --amend                                    |  Replaces the last commit with the staged changes and last commit combined. Use with nothing staged to edit the last commit’s message.                                     |
| git rebase <base>                                     |  Rebase the current branch onto <base>. <base> can be a commit ID a branch name a tag or a relative reference to HEAD.                                                     |
| git reflog                                            |  Show a log of changes to the local repository’s HEAD. Add --relative-date flag to show date info or --all to show all refs.                                               |
|                                                       |                                                                                                                                                                            |
| git branch                                            |  Lists all of the branches in your repo.                                                                                                                                   |
| git branch <branch name>                              |  Creates a new branch with the name <branch name>.                                                                                                                         |
| git checkout -b <branch name>                         |  Creates and check out a new branch named <branch name>.                                                                                                                   |
| git checkout <branch name>                            |  Checkout an existing branch.                                                                                                                                              |
| git merge <branch>                                    |  Merge <branch> into the current branch.                                                                                                                                   |
|                                                       |                                                                                                                                                                            |
| git remote add <name> <url>                           |  Creates a new connecti                                                                                                                                                    |
| git log --stat                                        |  Include which files were altered and the relative number of lineson to a remote repo. After adding a remote you can use <name> as a shortcut for <url> in other commands. |
| git fetch <remote> <branch>                           |  Fetches a specific <branch> from the repo. Leave off <branch> to fetch all remote refs.                                                                                   |
| git pull <remote>                                     |  Fetches the specified remote’s copy of current branch and immediately merge it into the local copy.                                                                       |
| git push <remote> <branch>                            |  Pushes the branch to <remote> along with necessary commits and objects. Creates named branch in the remote repo if it doesn’t exist.                                      |
|                                                       |                                                                                                                                                                            |
| git config --global user.name <name>                  |  Defines the author name to be used for all commits by the current user.                                                                                                   |
| git config --global user.email <email>                |  Defines the author email to be used for all commits by the current user.                                                                                                  |
| git config --global alias. <alias-name> <git-command> |  Creates shortcut for a Git command. E.g. alias.p push will set git p equivalent to git push.                                                                              |
| git config --system core.editor <editor>              |  Set text editor used by commands for all users on the machine. <editor> arg should be the command that launches the desired editor (e.g; vi).                             |
| git config --global --edit                            |  Opens the global configuration file in a text editor for manual editing.                                                                                                  |
|                                                       |                                                                                                                                                                            |
| git log -<limit>                                      | Limits the number of git rebase -i E.g. git log -5 will limit to 5 commits.                                                                                                |
| git log --oneline                                     |  Condenses each commit to a single line.                                                                                                                                   |
| git log -p                                            |  Displays the full diff of each commit.                                                                                                                                    |
| git log --stat                                        |  Include which files were altered and the relative number of lines that were added or deleted from each of them.                                                           |
| git log --author= ”<pattern>”                         |  Searchs for commits by a particular author.                                                                                                                               |
| git log --grep=”<pattern>”                            |  Searchs for commits with a commit message that matches <pattern>.                                                                                                         |
| git log <since>..<until>                              |  Shows commits that occur between <since> and <until>. Args can be a any kind of revision reference.                                                                       |
| git log -- <file>                                     |  Only display commits that have the specified file.                                                                                                                        |
| git log --graph --decorate                            |  --graph flag draws a text based graph of commits on left side of commit msgs. --decorate adds names of branches or tags of commits shown.                                 |
|                                                       |                                                                                                                                                                            |
| git diff HEAD                                         |  Shows difference between working directory and last commit.                                                                                                               |
| git diff --cached                                     |  Shows difference between staged changes and last commit                                                                                                                   |
|                                                       |                                                                                                                                                                            |
| git reset                                             |  Resets the staging area to match most recent commit but leaves the working directory unchanged.                                                                           |
| git reset --hard                                      |  Resets the staging area and working directory to match most recent commit and overwrites all changes in the working directory.                                            |
| git reset <commit>                                    |  Moves the current branch tip backward to <commit> resets the staging area to match but leaves the working directory unchanged.                                            |
| git reset --hard <commit>                             |  Same as previous but resets both the staging area & working directory to match. Deletes uncommitted changes and all commits after <commit>.                               |
|                                                       |                                                                                                                                                                            |
| git rebase -i <base>                                  |  Interactively rebase current branch onto <base>. Launches editor to enter commands for how each commit will be transferred to the new base.                               |


**Version Control Best Practises**

- Commit Related Changes
- Don't commit an unfinished work
- Your commit message should be clear enough and describes changes you made
- Add screenshots were possible to describe your changes better
- Ensure you open an issue first before you work on a new feature
- When pushing a new feature that was not discussed before, add a reason why you made that commit
- Test your commits before you push
- Use branches to work on new features
- Always pull before you push
- Fix merge conflicts as soon as possible

**Conclusion**

Git is a tricky tool to get your head around. Knowing the commands is one thing, but knowing how and when to use them is another. This cheat-sheet would come in handy whenever you forget any command.
Do share with your friends also, :)

**Reference**
- https://git-scm.com/
- https://www.atlassian.com/git/