[toc]

# Git Note and Configurations

## TO-DO

- [ ] Learn Atlassian Git tutorial from the ref link

## Reference

- [Git Reference - Git](https://git-scm.com/doc)
- [GitHub Git Cheat Sheet - GitHub](https://training.github.com/downloads/github-git-cheat-sheet/)
- [Git Cheatsheet - NDP Software](https://ndpsoftware.com/git-cheatsheet.html)
- [Pro Git Online Book- Git](https://git-scm.com/book/en/v2)
- [How to Set Up Git for the First Time on macOS - freeCodeCamp](https://www.freecodecamp.org/news/setup-git-on-mac/)
- [How to upgrade Git on Mac (OSX) - Ajahne GitHub IO](https://ajahne.github.io/blog/tools/2018/06/11/how-to-upgrade-git-mac.html)
- [Create Useful .gitignroe Files for Your Project - gitignore.io](https://www.toptal.com/developers/gitignore)
- [Git Ignore and .gitignore - W3Schools](https://www.w3schools.com/git/git_ignore.asp?remote=github)
- [Git reset - Atlassian](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset)
- [Git Tutorials - Atlassian](https://www.atlassian.com/git/tutorials)

## Git in Homebrew

### Install

1. To replace the built-in Git on macOS, install the Git from Homebrew: 

   `brew install git`

2. Change the local path to the Homebrew version:

   `export PATH=/usr/local/bin:$PATH`

3. Check the current version:

   `git --version`

### Update

1. Fetch the newest version of Homebrew and all formulae:

   `brew update`

2. Upgrade Git:

   `brew upgrade git`

## Setups and Configurations

### Global

Path: `~/.gitconfig`

- Set up the global user name:

  `git config --global user.name "username"`

- Set up the global user email:

  `git config --global user.email "email_addr@example.com"`

- Check the global configuration:

  `git config --global --list`

  `git config --global --get <config_name>`
### Local

Path: `repo_path/.git/config`

- Set up the local user name:

  `git config --local user.name "username"`

- Set up the local user email:

  `git config --local user.email "email_addr@example.com"`

- Check the local configuration:

  `git config --local --list`

  `git config --local --get <config_name>`

### System

In Git, the system-level configuration refers to the configuration settings applied globally across all users on a system. These settings are stored in a system-wide configuration file and are typically shared among all users on a machine. The system configuration is the broadest level of Git configuration and affects all repositories on the system.

- Check the system configuration:

  `git config --system --list`
  
  `git config --system --get <config_name>`

## File Statement

### Untracked/Tracked

Files that are untracked or tracked by Git.

### Modified

Files that have been changed but not staged yet.

### Staged

Files that have been marked for the next commit.

### Committed

Files that have been committed to the repository.

### Stashed

Files that have been temporarily saved.

Usage:

- `git stash [save <message>]`: stash the current changes, and revert the current working directory to the state of the last commit.
- `git stash list`: show a list of stashes with their names and messages.
- `git stash apply [<stash>]`: apply the stash.
- `git stash pop [<stash>]`: apply and drop the stash.
- `git stash drop [<stash>]`: drop the stash.
- `git stash clear`: drop all stashes.

### Ignored

Files that are intentionally ignored by using `.gitignore`.

## Ignore Files

### Local Repo

#### Shared w/ Collaborators

1. Create a `.gitignore` inside the repo.
2. Add the names/patterns of files/directories to be ignored.
3. Save the file and commit to the repo.

Git will not track files and folders specified in the `.gitignore`, but the `.gitignore` itself will be tracked. It can also be created inside a subdirectory to ignore files/folders within the directory. 

#### Not Shared w/ Collaborators

1. Create a `.git/info/exclude` inside the repo.
2. Add the names/patterns of files/directories to be ignored.
3. Save the file and commit to the repo.

It works the same way as `.gitignore` but will not be shown to anyone else.

### Global Settings

1. Enable `core.excludesfile` option in the global Git configuration:

   ```git config --global core.excludesfile ~/<.global_ignore_cfg>```

2. Create the ```~/<.global_ignore_cfg>```.
3. Add the names/patterns of files/directories to be ignored.
4. Save the file.

The ~/<.global_ignore_cfg> rules will be applied to all Git repos.

## Git Undo

### Revert

`revert` will take a previous commit, recover the working directory based on the selected commit, and save the change in the commit log.

![before commit](https://www.w3schools.com/git/img_revert_part1.gif)![after commit](https://www.w3schools.com/git/img_revert_part2.gif)

- Commit by using the default `revert` message:

  `git revert --no-commit/-n <commit>`

- Revert a merged commit:

  `git revert --mainline/-m <parrent_num> <commit>`

### Reset

`reset` will take a previous commit, recover the working directory based on the selected commit, and drop all commits after the selected commit.

![before reset](https://www.w3schools.com/git/img_reset_part1.gif)

![after reset](https://www.w3schools.com/git/img_reset_part2.gif)

### Mixed (Default) Reset

`git reset [--mixed]` as the default reset operation, changes the `HEAD` and `index` at the same time.

Before `git reset b`:

![4 nodes with "main node" being the last one](https://wac-cdn.atlassian.com/dam/jcr:8d616ece-8cee-4fde-bdee-4b280a0a8334/01%20git-sequence-transparent%20kopiera.png?cdnVersion=1439)

After `git reset b`:

![2 sets of 2 nodes, with head,main pointing at the 2nd of the 1st set](https://wac-cdn.atlassian.com/dam/jcr:bdf5fda3-4aac-4170-ba35-58f7a66ea3c4/03%20git-reset-transparent%20kopiera.png?cdnVersion=1439)

To revert `HEAD` and `main`:

1. Use `git reflog`to search for the reference
2. Use `git reset [ref]` to move back

### Checkout as a Reset Method

  `git checkout` will only move the current `HEAD` to the specific position.

  Before `git checkout b`:

  ![4 nodes with "main node" being the last one](https://wac-cdn.atlassian.com/dam/jcr:8d616ece-8cee-4fde-bdee-4b280a0a8334/01%20git-sequence-transparent%20kopiera.png?cdnVersion=1439)

  After `git checkout b`:

  ![4 nodes with main pointing at last node and head pointing at 2nd node](https://wac-cdn.atlassian.com/dam/jcr:f45c4a34-8968-4c81-83cf-d55ebf01a447/02%20git-checkout-transparent%20kopiera.png?cdnVersion=1439) 

A **Normal `HEAD`** points to the lastest commit of a branch; A **Detached `HEAD`** is pointing to a specific commit other than a branch. 

To make changes on a detached `HEAD`: create a new branch `git checkout -b <branch_name>` before commit. 

To link the detached `HEAD` to a branch: `git switch <branch_name>`.

### Soft Reset vs Hard Reset vs Mixed Reset

![Diagram showcasing reset modes.](https://nulab.com/static/d3d319a98c48b1ce04570d547a6b0d84/5a190/03.png)

![diagram of scope of git resets](https://wac-cdn.atlassian.com/dam/jcr:7fb4b5f7-a2cd-4cb7-9a32-456202499922/03%20(8).svg?cdnVersion=1439)

## Git Amend

### Modify the last commit message

 `git commit --amend -m <new_message>` will modify the last commit message and keep anything else the same.

