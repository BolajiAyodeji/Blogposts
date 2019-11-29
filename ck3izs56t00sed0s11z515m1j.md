## Writing Good Commit Messages: A Practical Guide

To create a useful revision history, teams should first agree on a commit message convention to use, and this also applies to personal projects.

Recently I asked a question on [Hashnode](https://hashnode.com) asking users **"Which commit message convention they use at work?"** and I got quite some amazing responses with users explaining the conventions they use at work and for their personal projects.

%[https://hashnode.com/post/which-commit-message-convention-do-you-use-at-work-ck3e4jbdd00zyo4s1h7mc7e0g]

In this article, I'll go over why you should write good commit messages and how you can write good commit messages.

---

## Introduction to version control with Git

Version control software is an essential part of the every-day modern-day software developer practices.

By far, [Git](https://git-scm.com/) is the most widely used modern version control system in the world today is. It is a distributed and actively maintained open source project originally developed in 2005 by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), the famous creator of the Linux operating system kernel.

New to Git? Check out the official [getting started guide](https://git-scm.com/book/en/v1/Getting-Started) or [this slide](https://slides.com/bolajiayodeji/introduction-to-version-control-with-git-and-github) from my past talk.

## What is a commit message?

The **commit** command is used to save changes to a local repository after staging in Git. However, before you can save a change in Git, you have to tell Git which changes you want to save as you might have made tons of changes. A great way to do that is by adding a **commit message** to identify your changes.

### Commit Options

- **-m <message>**

This option sets the commit's message.

```bash
git add static/admin/config.yml
git commit -m "Setup multiple roles for netlify-cms git gateway"
```

- **-a**

This option rewrites the last commit with any staged changes or a new commit message and should only be performed on commits that have not been pushed to a remote repository, yet.

```bash
git commit -a "Setup multiple roles for netlify-cms git gateway"
```

- **--amend**

This option rewrites the very last commit with any currently staged changes or a new commit message and should only be performed on commits that have not been pushed to a remote repository, yet.

```bash
git add .
git commit --ammend -m "Update roles for netlify-cms git gateway"
```

## Why should you write good commit messages?

You might say, "It's just a personal project," but yes, you work alone now, but what happens when you work with a team or contribute to open source?

A well-crafted Git commit message is the best way to communicate context about a change to other developers working on that project and indeed to your future self. Have you tried running `git log` one of your old projects to see the "weird" commit messages you have used since inception? It becomes hard for you to explain why you made some changes in the past, and you wish you have read this article before now :).

Commit messages can adequately tell you why a change was made, and understanding why a change was made makes development and collaboration more efficient.

## How to write commit messages with Git

Before now, I only used `git commit -m "Fix X to allow Y to use Z"` on my personal projects with just a subject and no extra description. This is great for small and clear fixes like `git commit -m "Fix typo in README.md` but in cases of more extensive changes, you would need to add some extra details.

### Editor method

Run `git commit` without a message or option and it'll open up your default text editor to write a commit message.

> To configure your "default" editor:

```
git config --global core.editor nano
```
This would configure git to use nano as your default editor. Replace "nano" with "emacs," "vim," or whichever your preference is. 

In the opened editor, the first line is the subject (short description), leave a blank line after it, and everything else is the extended description (body).

```bash
<Summarize change(s) in around 50 characters or less>

<More detailed explanatory description of the change wrapped into about 72
characters>
```

### Command Line method 

```
git commit -m "Subject" -m "Description..."
```

The first `-m` option is the subject (short description), and the next is the extended description (body).

## How to write good commit messages

There are several conventions used by several teams and developers to write good commit messages. I'll only outline some general rules and tips for writing commit messages, you would have to decide what convention you want to follow and if you work for a company or contribute to open source, you would have to adapt to their convention :).

For consistency, you can use one convention for work and another for personal projects as you might change your job sometime, and the convention might change.

> Ensure to check [this thread](https://hashnode.com/post/which-commit-message-convention-do-you-use-at-work-ck3e4jbdd00zyo4s1h7mc7e0g) for some amazing commit message conventions or add yours to help someone make a decision.

Here's a great template of a good commit message originally written by [Tim pope](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)

```bash
Capitalized, short (50 chars or less) summary

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the
two together.

Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
or "Fixes bug."  This convention matches up with commit messages generated
by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too

- Typically a hyphen or asterisk is used for the bullet, followed by a
  single space, with blank lines in between, but conventions vary here

- Use a hanging indent

If you use an issue tracker, add a reference(s) to them at the bottom,
like so:

Resolves: #123
```

Looks great, right? Here's how you can make yours great too:

1. Specify the type of commit:
 - **feat**:  The new feature you're adding to a particular application
 - **fix**: A bug fix
 - **style**: Feature and updates related to styling
 - **refactor**: Refactoring a specific section of the codebase
 - **test**: Everything related to testing
 - **docs**: Everything related to documentation
 - **chore**: Regular code maintenance.  
[ You can also use emojis to represent commit types]
2. Separate the subject from the body with a blank line
3. Your commit message should not contain any whitespace errors
4. Remove unnecessary punctuation marks
5. Do not end the subject line with a period
6. Capitalize the subject line and each paragraph
7. Use the imperative mood in the subject line
8. Use the body to explain what changes you have made and why you made them.
9. Do not assume the reviewer understands what the original problem was, ensure you add it.
10. Do not think your code is self-explanatory
11. Follow the commit convention defined by your team

## Conclusion

The most important part of a commit message is that it should be clear and meaningful. In the long run, writing good commit messages shows how much of a collaborator you are, and the benefits of writing good commit messages are not only limited to your team but indeed to yourself and future contributors.

Want to learn more about Git and become a professional "version controller," check out these excellent resources:

- https://try.github.io/
- https://git-scm.com/book/en/v2
- https://www.git-tower.com/learn/
- https://learngitbranching.js.org/