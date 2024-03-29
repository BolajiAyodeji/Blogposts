---
title: "Git First Time Setup"
datePublished: Sun Jul 21 2019 16:17:37 GMT+0000 (Coordinated Universal Time)
cuid: cjyd6027g0012sbs1afuje609
slug: git-first-time-setup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1588425047471/gUa6sLzQ9.png
tags: terminal, version-control, bash, git, hashnode

---

Git is a Free and Open Source Distributed Version Control System.

By far, Git is the most widely used modern version control system in the world today. Git is a distributed and actively maintained open source project originally developed in 2005 by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), the famous creator of the Linux operating system kernel.

Unlike older centralized version control systems such as SVN and CVS, Git is distributed: every developer has the full history of their code repository locally. Git also works well on a wide range of operating systems and IDEs (Integrated Development Environments).

In this article, I'll show you how to install Git, set it up for the first time, and useful tips and resources to learn more/ learn advanced git concepts. Let's roll!

- - -

I assume you already know what Version control is, if you don't, kindly check out this [slide](http://slides.com/bolajiayodeji/introduction-to-version-control-with-git-and-github) to learn more. 

Here's a quick recap of what Version control means:

> Version control is the process of managing changes to source code or set of files over time.

Version control software keeps track of every modification to the code in a special kind of database.
If a mistake is made, developers can restore and compare earlier versions of the code to help fix the mistake while minimizing disruption to all team members or contributors.

- - -

Now that you know what Version Control and Git mean, let's install it.

## For Mac OS:

[Download Git for macOS](http://git-scm.com/download/mac)
or install using [Homebrew](https://brew.sh)

```
brew install git
```

## For Linux OS:

[Download Git for Linux](https://git-scm.com/download/linux) or 
Install for Debian-based Linux systems 

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git
```

or Install for Red Hat-based Linux systems

```
sudo yum upgrade
sudo yum install git
```

## For Windows OS:

[Download Git for Windows](https://git-scm.com/download/win)

> #### Here's a more detailed installation guide for different systems on [Git official docs](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

---

Now that you have Git on your system, let's set up the Git environment. <br> 
Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates.

- First set your identity, your name and email address like so:

```
git config --global user.name "bolajiayodeji"
git config --global user.email mailtobolaji@gmail.com
```
the `--global` option makes sure these values are used throughout your system

- Next set up the default text editor you'll use whenever you need to enter a message in Git. This is not compulsory, if you don't configure this, Git will use your default editor. If you want to use something else, configure like so:

```
git config --global core.editor emacs
```

- Next, set up colors for your Git console.

> For Linux OS users, you can use third pary Zsh configurators like [oh my zsh](https://ohmyz.sh/) to customize your terminal look with themes :).
To configure this, do this:

```
git config --global color.ui true
```
The color.ui is a meta configuration that includes all the various color.* configurations available with git commands. 

Now Git is ready for use. 

## Check your settings

```
git config --list
```

```
user.name=bolajiayodeji
user.email=mailtobolaji@gmail.com
color.ui=true
```

---

Want to learn some super Git commands? I wrote an article: [Git Cheat Sheet](https://blog.bolajiayodeji.com/git-cheat-sheet) that covers some important Git commands you'll need. 

You can also find more resources to learn Git [here](https://try.github.io).


## Conclusion

Version control software is an essential part of every day of modern-day software developers' practice. Once accustomed to the powerful benefits of version control systems, many developers wouldn’t consider working without it even for non-software projects.
