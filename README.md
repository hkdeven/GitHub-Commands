# GITHUB: Setups and Command Prompts

<img src="./octocat-detective.jpg" align="right"/>

* [Setting up SSH access to multiple GitHub accounts with just one command][1]
* [View and kill servers running in the background][2]
* [Identify remote url your local directory is tied to on github.com (if any)][3]
* [How to ignore those pesky 'DS_Store' files once and for all][4]
* [Branching off of existing branches and commting][5]
* [Markdown Tricks with GitHub][6]
* [Quickly recall what was committed via your terminal][7]
* [Merging need-to-know][8]

## Configurations

<a name="adding-command-aliases"></a>
### I want to add aliases for some git commands

On OS X and Linux, your git configuration file is stored in ```~/.gitconfig```.  I've added some example aliases I use as shortcuts (and some of my common typos) in the ```[aliases]``` section as shown below:

```vim
[aliases]
    a = add
    amend = commit --amend
    c = commit
    ca = commit --amend
    ci = commit -a
    co = checkout
    d = diff
    dc = diff --changed
    ds = diff --staged
    f = fetch
    loll = log --graph --decorate --pretty=oneline --abbrev-commit
    m = merge
    one = log --pretty=oneline
    outstanding = rebase -i @{u}
    s = status
    unpushed = log @{u}
    wc = whatchanged
    wip = rebase -i @{u}
    zap = fetch -p
```

<a name="credential-helper"></a>
### I want to cache a username and password for a repository

You might have a repository that requires authentication.  In which case you can cache a username and password so you don't have to enter it on every push / pull. Credential helper can do this for you.

```sh
$ git config --global credential.helper cache
# Set git to use the credential memory cache
```

```sh
$ git config --global credential.helper 'cache --timeout=3600'
# Set the cache to timeout after 1 hour (setting is in seconds)
```

<a href="#ive-no-idea-what-i-did-wrong"></a>
## I've no idea what I did wrong

So, you're screwed - you `reset` something, or you merged the wrong branch, or you force pushed and now you can't find your commits. You know, at some point, you were doing alright, and you want to go back to some state you were at.

This is what `git reflog` is for. `reflog` keeps track of any changes to the tip of a branch, even if that tip isn't referenced by a branch or a tag. Basically, every time HEAD changes, a new entry is added to the reflog. This only works for local repositories, sadly, and it only tracks movements (not changes to a file that weren't recorded anywhere, for instance).

```sh
(master)$ git reflog
0a2e358 HEAD@{0}: reset: moving to HEAD~2
0254ea7 HEAD@{1}: checkout: moving from 2.2 to master
c10f740 HEAD@{2}: checkout: moving from master to 2.2
```

The reflog above shows a checkout from master to the 2.2 branch and back. From there, there's a hard reset to an older commit. The latest activity is represented at the top labeled `HEAD@{0}`.

If it turns out that you accidentally moved back, the reflog will contain the commit master pointed to (0254ea7) before you accidentally dropped 2 commits.

```sh
$ git reset --hard 0254ea7
```

Using git reset it is then possible to change master back to the commit it was before. This provides a safety net in case history was accidentally changed.

(copied and edited from [Source](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog)).


# Other Resources

## Books

* [Pro Git](https://git-scm.com/book/en/v2) - Scott Chacon's excellent git book

## Tutorials

* [Getting solid at Git rebase vs. merge](https://medium.com/@porteneuve/getting-solid-at-git-rebase-vs-merge-4fa1a48c53aa)
* [git-workflow](https://github.com/asmeurer/git-workflow) - [Aaron Meurer](https://github.com/asmeurer)'s howto on using git to contribute to open source repositories
* [GitHub as a workflow](http://hugogiraudel.com/2015/08/13/github-as-a-workflow/) - An interesting take on using GitHub as a workflow, particularly with empty PRs

## Scripts and Tools

* [firstaidgit.io](http://firstaidgit.io/) A searchable selection of the most frequently asked Git questions
* [git-extra-commands](https://github.com/unixorn/git-extra-commands) - a collection of useful extra git scripts
* [git-extras](https://github.com/tj/git-extras) - GIT utilities -- repo summary, repl, changelog population, author commit percentages and more
* [git-fire](https://github.com/qw3rtman/git-fire) - git-fire is a Git plugin that helps in the event of an emergency by adding all current files, committing, and pushing to a new branch (to prevent merge conflicts).
* [git-tips](https://github.com/git-tips/tips) - Small git tips
* [git-town](https://github.com/Originate/git-town) - Generic, high-level Git workflow support! http://www.git-town.com

## GUI Clients
* [GitKraken](https://www.gitkraken.com/) - The downright luxurious Git client,for Windows, Mac & Linux
* [git-cola](https://git-cola.github.io/) - another git client for Windows and OS X
* [GitUp](https://github.com/git-up/GitUp) - A newish GUI that has some very opinionated ways of dealing with git's complications
* [gitx-dev](https://rowanj.github.io/gitx/) - another graphical git client for OS X
* [Source Tree](https://www.sourcetreeapp.com/) - a free graphical git client for Windows and OS X
* [Tower](http://www.git-tower.com/) - graphical git client for OS X (paid)



[1]: ./multi-github-account-ssh-setup.md
[2]: ./view-and-kill-active-servers.md
[3]: ./list-remote-url.md
[4]: ./gitignore-ds-store-files.md
[5]: ./branching-off-of-existing-branches.md
[6]: ./github-markdown-tricks.md
[7]: https://github.com/kamranahmedse/git-standup
[8]: ./merging.md
