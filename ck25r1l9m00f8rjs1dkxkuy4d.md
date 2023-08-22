---
title: "How to Fix Git Always Asking for User Credentials"
datePublished: Sat Jul 20 2019 23:00:00 GMT+0000 (Coordinated Universal Time)
cuid: ck25r1l9m00f8rjs1dkxkuy4d
slug: how-to-fix-git-always-asking-for-user-credentials
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1588425226427/K8wN4rRTS.png
tags: github, programming, git, cli

---

Have you ever encountered Git asking you for your username and password every time you try to interact with GitHub even after configuring it? Well, this is a very common problem among users who use the HTTPS clone URL for their repository. In this article, I'll show you how to fix this.

---

The `https://` clone URLs are available on all public and private repositories. These URLs work everywhere, even if you are behind a firewall or proxy.

![](https://res.cloudinary.com/bolaji/image/upload/v1570636713/null/blog/0003/01.png)

When you interact with a remote repository using HTTPS URLs on the command line, you'll be asked for your GitHub username and password, this sucks right?

Well using an HTTPS remote URL has some advantages: it's easier to set up than SSH :), and usually works through strict firewalls and proxies. However, it also prompts you to enter your GitHub user credentials every time you pull or push a repository :(.

## You can fix this by configuring Git to store your password for you.
---
Here's how:

- Update the URL of origin remote using SSH instead of HTTPS;

```bash
git remote set-url origin git@github.com:username/repo.git
```
or

- Make Git store the username and password and it will never ask for them. 

```bash
git config --global credential.helper store
```


- Save the username and password for a session (cache it);

```bash
git config --global credential.helper cache
```

- You can also set a timeout for the above setting

```bash
git config --global credential.helper 'cache --timeout=600'
```

Bingo, you just fixed it, Git will never ask for your credentials again.

---

## Conclusion
However, due to security reasons, it is advisable that you use SSH to interact with GitHub, especially if you work for a company or you're using a computer that isn't yours.

Using the SSH protocol, you can connect to GitHub without supplying your username or password every time. Learn how to connect to GitHub with SSH [here](https://help.github.com/en/articles/connecting-to-github-with-ssh).
