---
title: "Automate GitHub Dependency Updates with Dependabot"
datePublished: Tue Dec 31 2019 16:39:45 GMT+0000 (Coordinated Universal Time)
cuid: ck4u3kd2d00hktjs1llbiuf8d
slug: automate-github-dependency-updates-with-dependabot
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1577810225258/NZvNCt-SW.png
tags: bot, github, programming, automation

---

You should be familiar with this tiring email notification from GitHub.

![aaaaaa.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1577809729388/_vYYp_5n6.png)

If you have tons of repositories on GitHub like [me](https://github.com/BolajiAyodeji), you will receive tons of these emails virtually every day, and this can be annoying as most time, the vulnerabilities come from installed packages, which might get updated daily.

You can use automated or manual pull requests to update vulnerable dependencies. Before now, I only used the manual method, but this wasn't efficient as I sometimes have to send multiple pull requests to fix several vulnerabilities.

I figured that not everyone knows about this amazing service, and with this article, more developers will save the time used to fix vulnerabilities manually.

## Introducing Dependabot

[Dependabot](https://dependabot.com) is a GitHub App which is automatically installed on every repository where automated security updates are enabled and create pull requests to keep your dependencies secure and up-to-date.

> Every day, Dependabot checks your dependency files for outdated requirements and opens individual pull requests for any it finds. You review the PRs, merge them, and get to work on the latest, most secure releases.

Before now, Dependabot was a standalone paid service until it was [aquired by GitHub](https://dependabot.com/blog/hello-github/) and directly integrated into GitHub, thereby making it free of charge.

## How it works

When you receive a security alert about a vulnerable dependency in your repository, Dependabot resolves the vulnerability using an automated security update via a pull request.

GitHub automatically creates a pull request in your repository to upgrade the vulnerable dependency to the minimum possible secure version needed to avoid the vulnerability.

So it works in three steps:

- Dependabot checks for updates
- Dependabot opens a pull request
- You review and merge

## Getting Started

Before now, you would need to install the service, but since it is now integrated into GitHub, you would have to configure some settings to get started.

Dependabot currently supports [Ruby](https://dependabot.com/ruby), [JavaScript](https://dependabot.com/javascript), [Python](https://dependabot.com/python), [PHP](https://dependabot.com/php), [Elixir](https://dependabot.com/elixir), [Rust](https://dependabot.com/rust), [Java](https://dependabot.com/java), [NET](https://dependabot.com/dotnet), [Go](https://dependabot.com/go), [Elm](https://dependabot.com/elm), [Submodules](https://dependabot.com/submodules), [Docker](https://dependabot.com/docker), [Terraform](https://dependabot.com/terraform) and [GitHub Actions](https://dependabot.com/github-actions).

For repositories created before November 2019, GitHub has automatically enabled automated security updates if the repository meets some criteria and has received at least one push since May 23, 2019.

**Here's how to activate or deactivate Dependabot for your repository:**

- Navigate to the main page of the repository on GitHub

![main_page.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1577795272972/5PbXjVo94.png)

- Click on the Security tab, below the repository name

![security_tab.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1577796991228/lSRC1O7ON.png)

- Click on the **Automated security updates** drop-down menu and select or unselect Automated security updates to turn it on or off.

![toogle_updates.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1577805432662/qcZY_HPfh.png)

> In this page, you also get to see a list of open vulnerabilities alerts if turned on already

![alerts1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1577805478242/2piA35Eh-.png)

![alerts2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1577808211863/yW4JpeHOv.png)

- When there is any vulnerability update, Dependabot automatically creates a pull request to fix it, and all you have to do is merge.

![updatepng](https://cdn.hashnode.com/res/hashnode/image/upload/v1577808489179/QoFFpOCA_.png)

## Custom Configuration

You can also configure Dependabot via a commit config files to your repositories with more details of how Dependabot should behave.

The `config.yml` is used to configure how Dependabot behaves and is located in a folder named `.dependabot` at the root of your repository.

Here is an example of a starter configuration template that keeps tracks of updates in a Javascript project (Immediately there is an update) and Docker project (every week) and sets a custom user to review the updates and add label names.

```
version: 1
update_configs:
  # Keep package.json (& lockfiles) up to date as soon as
  # new versions are published to the npm registry
  - package_manager: "javascript"
    directory: "/"
    update_schedule: "live"
  # Keep Dockerfile up to date, batching pull requests weekly
  - package_manager: "docker"
    directory: "/"
    update_schedule: "weekly"

 # Apply default reviewer and label to created pull requests
    default_reviewers:
      - "bolajiayodeji"
      - "angiejones"

    default_labels:
      - "dependencies"
      -  "changelog"
```

[Read more about the configuration options](https://dependabot.com/docs/config-file/)

## Conclusion

Automated security updates help to easily and safely fix tiring dependency updates, and all you have to do is **merge a pull request** :).

I hope this helps you save more time and worry less about the numerous GitHub security alerts.

Dependabot is also open-sourced, feel free to contribute:

%[https://github.com/dependabot]