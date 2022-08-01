# Git Notes

Quick Git reference with most used commands. It is mainly based on notes taken from [The Git & Github Bootcamp](https://www.udemy.com/course/git-and-github-bootcamp/) Colt's Udemy course.

## Configure Git

```
git config --global user.name <username>
```
Set up your Git username. The name `<username>` will be associated to all your work. The `--global` parameter means that this configuration will be used across every Git instance.

```
git config --global user.email <email>
```
Set up your Git email. The email `<email>` will be associated to all your work. If you have Github, you can use the same email used in your Github account.

```
git config user.name
```
Check up if there is any name configured in Git.

## Create a Git Repository

```
git init
```
Create a new Git repository inside your current working directory. You can use `git status` to make sure there isn't a Git repository configured yet. If you create a Git repository inside a working directory, this will apply in all child directories as well.

```
git status
```
Show if the current working directory has been configured as a Git repository. In that case, it will show if there are changes in the working directory pending to be added or committed.

## Adding and Commiting

```
git add <filename.txt>
```
Add `<filename.txt>` to the staging area, so that it could be committed later. You can check all filenames in your working directory that has been changed from your last commit using `git status`.

```
git add .
```
Add all filenames in your working directory that have been changed from your last commit to the staging area, so that they could be committed later.

```
git commit
```
Publish all changes in the staging area to the current branch you are on. It will open a window of your default text editor, in order to specify a messaged to identify with the main commit changes.

```
git commit -m "<Commit message name>"
```
Publish all changes in the staging area to the current branch you are on. You can set up a message for that commit using `-m` parameter, and then the message you decide in quotation marks.

```
git log
```
View all commit history of the current branch from your local Git repository.

```
git log --oneline
```
View all commit history of the current branch from your local Git repository. This is an option to see all results in a more condensed way, in which every commit will be displayed in one line.

## Branches

```
git branch
```
View all branches used in your current Git repository. The branch you are currently on is highlighted with *.

```
git branch <branch>
```
Create a new branch called `<branch>` taking the current commit on the branch you are on as the initial reference. The HEAD will continue pointing to the current branch, as we are not switching to the new one, just creating it.

```
git switch <branch>
```
Switch to an existing branch on your local repo. The HEAD will now point to the last commit published to `<branch>`, and you will be able to commit new work to this branch from that point.

```
git switch -c <branch>
```
Create a new branch taking the current commit on the branch you are on as the initial reference, and switch to it at the same time. The HEAD will now point to that same commit but from the newly created branch.

```
git branch -d <branch>
```
Detele one specific branch on your local repo. Deleting a branch can only be made from outside of that branch. This command will display an error if that branch is not fully-merged. If you are sure to delete the branch anyway, you can change the `-d` parameter for `-D`.

```
git branch -m <branch>
```
Change the name of the current local branch you are on.

```
git branch -m master main
```
Rename your local repo default branch name from `master` to `main`. This change will not apply to other local repositories, just the current one.

```
git config --global init.defaultBranch main
```
Change the local Git default branch name to `main`, in order to follow the Github criteria. The `--global` parameter means that this configuration will be used across every Git instance, so all new local repositories will use now `main` as the default branch name.

## Merging

```
git merge <branch>
```
Merge all commits from `<branch>` into the current local branch you are on. 
- If there are not additional commits to the current branch since you split off and created `<branch>`, the merge is a fast-forward. All commits from `<branch>` will be added to the current branch, and the current branch will end up referring to the same last commit of `<branch>`.
- If there are additional commits to the current branch since the split off, in case there are no conflicts, Git will create a merge commit for us, adding all changes from `<branch>` to the current branch. This commit will have two parent branches, both `<branch>` and the current branch.
- If there are additional commits to the current branch since the split off, but there are conflicting changes, Git will alert that to us. In that case, you will have to manually open the files with conflicting changes (Git will add specific markers in those files) and fix them. Finally you will need to add those changes to the staging area, and commit them.

## Rebasing

```
git rebase <branch>
```
Move the entire branch you are on into `<branch>`, starting at the tip of `<branch>`. The original commits on `<branch>` are unchanged, but Git will create new commits at the tip of `<branch>`, for each of the original commits from the branch you are on. This ends up in a linear structure and avoids merge commits, but also rewrites the history. Rebasing is used as an alternative to merging, but also as a cleanup tool. The main workflow use of rebase is this: 
- If you are working on a feature branch, but the main branch is very active, you may need to constantly merge all new work of the main branch to your feature branch, so the feature branch will end up with a bunch of merge commits and the history will become muddied. You can instead rebase the feature branch onto the main branch, moving the entire feature branch at the tip of the main branch, rewritting the history.
- When working in collaborative projects, and you have pushed commits up to GitHub, do not rebase them unless you are positive no one on the team is using those commits.

```
git rebase --continue
```
Continue with the rebasing, in case of conflicting changes during the first attempt. Just like with merging, rebasing may end up with conflicts. In this case, the rebase may have been started but not completely finished, so you will need to resolve the conflicts on files, adding them to the staging area with `git add`, and finally, instead of make a commit with that, continue the rebasing.

```
git rebase -i HEAD~<n>
```
Enter the interactive mode, which allows you to edit commits, add files, drop commits, etc. In this case, you are not rebasing onto another branch. Instead, you are rebasing a series of commits onto the HEAD they currently are based on.

## Stashing

```
git stash
```
Stash all uncommitted changes (staged and unstaged) in your working directory, in order to return to them later. If you have changes in your working directory, and want to switch to another branch without commiting them, Git will alert you to commit those changes before. If you don't want to commit them, and also don't want to take them with you in other branches, you can use `git stash` to save them for a future use and clean your working directory.

```
git stash pop
```
Remove the most recently stashed changes in your stash and re-apply them to your working copy, in order to be able to commit them, or continue working with them.

## Changing HEAD Reference

```
git checkout <commit-hash>
```
Jump back in time to a particular commit, specified by its hash. You are now in a "detached HEAD" state, meaning that HEAD does not point to a branch reference (the branch reference is a pointer to the last commit made on this particular branch), but to a particular commit. If you type `git log`, we will see all commits published up until this one. In this state, you cannot make changes, but you can:
- Examine contents of that old commit and finally get out of the "detached HEAD" state by switching back to a particular branch.
- Create a new branch from this state, which will be created taking this commit reference. If you switch to that new branch, you will no longer be on a "detached HEAD" state (HEAD will point to that new branch reference), so you will be able to publish new commits to this branch.

## Restore, Reset and Revert

```
git restore <filename.txt>
```
Discard changes made on `<filename.txt>` and restore it back to where it looked like at HEAD (which by default ponts to the last commit of the current branch). This is useful if you have made changes to a file, saved it, but then you decide you don't want these changes to be applied.

```
git restore --staged <filename.txt>
```
Remove `<filename.txt>` to the staging area, so that it will not be included in the next commit, when you execute `git commit`. This is useful if you accidentally added a file to the staging area with `git add`.

```
git reset <commit-hash>
```
Reset the current repo back to a previous commit, specified by its hash, discarding any changes made after that commit. It removes all commits that came after that, but all changes on files still remain on your working directory, so you don't lose the changes, only the commits. This is useful if you made some commits on the wrong branch, and you want to keep that work, but move it to a separate branch.

```
git reset --hard <commit-hash>
```
Reset the current repo back to a previous commit, specified by its hash, discarding any changes made after that. It removes both the commits and the actual changes on files.

```
git revert <commit-hash>
```
It's similar to `git reset` in that they both undo changes, but `git revert` does that by creating a brand new commit which reverses all changes made from a particular commit. As it results in a new commit, you will be prompted to enter a commit message. If you collaborate with other people, and you want to reverse some commits that other people already have on their machines, you should use `git revert` instead of `git reset`. 

## Remote Repositories

```
git remote
```
Display all remotes you have in the current local repo. Before you can push anything up to GitHub (or any other hosted Git platform), you need to tell Git about your remote repository on GitHub, a destination to push up to. These destinations are called remotes, and each remote is simply a label for a URL where a hosted repository live.
- When you create a new remote for a local repo pointing to hosted repo, you must specify the name for it. A convention to name it is `origin`.
- When you clone a GitHub repo to your local machine, the default remote name setup for you is called `origin`.

```
git remote -v
```
Display all remotes you have in the current local repo, alongisde with the corresponding URL of the GitHub repo.

```
git remote add <remote> <url>
```
Adding a new remote indicating its name and the URL of the particular GitHub repo. You can specified the name you want, but `origin` is the standard name used for a remote.

```
git clone <url>
```
Clone a remote repo, providing its URL, to your local machine. Git will retrieve all the files associated with the repository and will copy them to your local machine. In addition, Git initializes a new local repo on your machine, giving you access to the full Git history of the cloned project. When you clone a GitHub repo to your local machine, the default remote name setup for you is called `origin`. Even though you have access to all Git history of the cloned project, only the default branch is imported as a local branch and is connected to the corresponding remote-tracking branch. Other branches in the remote repo are accessible only as remote-tracking branches, and will not be listed if you type `git branch`.

## Remote Branches

```
git branch -r
```
View all remote-tracking branches your local repo knows about. When you work with remote repos, your local repo have two references, which will start to the same spot but will diverge as you make new commits on the branch locally.
- The standard local branch reference, which will be moving around as you publish new commits.
- A remote-tracking branch, which is a reference to the state of the branch on the specific remote. It cannot be moved by yourself, as it indicates where this branch was pointing at the time you last communicated with the remote repo. It follows this pattern: `<remote>/<branch>`.

```
git checkout <remote>/<branch>
```
Switch to a remote-tracking branch. When cloning a remote repo to yout local machine, only the default branch is imported as a local branch and is connected to the corresponding remote-tracking branch. Other remote branches are accessible locally but as remote-tracking branches. You can switch to one of them, but you will be in a "detached HEAD" state, so you will not be able to publish new commits from there. 

```
git switch <remote-branch>
```
If you use `git switch` with the name of a specific remote tracking branch that does not exist as a local branch on your repo, if Git detects it exists, it will create a new local branch from the remote-tracking branch of the same name, and will connect both. Now we will be able to publish new commits from there.

## Pushing

```
git push <remote> <branch>
```
Push the work on your local repo up to GitHub, once you have a remote set up, either by using `git clone` or `git remote add`. You need to specify the name of the remote, which usually is `origin` and the specific local branch you want to push up to that remote. It will also create that branch on Github, in case it does not exist yet.

```
git push -u <remote> <branch>
```
In this case, the `-u` option allows you to set the upstream of the branch you are pushing. It's as a link connecting your local branch to a branch on GitHub. This sets the upstream of the local branch specified, so that it tracks that same branch on the remote repo. This allow you to use `git push` next time, without having to specify the remote name nor the branch name, everytime you want to push the last changes of that local branch up to GitHub.

## Fetching and Pulling

```
git fetch <remote>
```
Retrieve changes from a remote repo you have configured under `<remote>` (if not specified, it defaults to `origin`) to your local repo. It updates the remote-tracking branches with the latest changes from the remote repository, but does not merge changes onto your current HEAD branch. It lets you see what others have been working on, without having to merge those changes into your local repo. You will be able to see them using `git checkout <remote>/<branch>`.

```
git fetch <remote> <branch>
```
You can also fetch one single branch, specifying the branch name after the remote name. This means only changes from one specific remote branch will be imported to your local repo.

```
git pull <remote> <branch>
```
Retrieve changes from a remote repo to your local repo. Unlike `git fetch`, it actually updates your local HEAD branch with whatever changes are retrieved from the remote, merging them in. It's like a combination of `git fetch` and `git merge`. Just like `git merge`, whatever branch you run it from is where the changes will be merged into. If there are merge conflicts, the pull will not be automatic, and you will need to fix the conflicts on the affected files, publish a commmit containing that fix, and make a push back to the remote repo.

## Pull Requests

When collaborating in projects with other people, it's a common pattern that every user is working in some specific feature on a separated branch. In that scenario, Pull requests provide a mechanism to alert team-members to new work that needs to be reviewed and approved on a given branch, in order to be merged to another branch (usually the main branch). 

Pull requests are not a native Git feature, but a functionallity built into platforms like GitHub or Bitbucket. They typically follow this workflow:

1. Do some work locally on a feature branch.
2. Push up the feature branch on GitHub.
3. Open a pull request using the feature branch just pushed up to GitHub.
4. Wait for the pull request to be approved and merged.

Just like any other merge, sometimes there are conflicts that need to be resolved when merging a pull request. In this case, you can perform the merge and fix the conflicts using the GitHub's interactive editor, or on your local machine.

If you want to resolve the conflics locally, you need to follow these steps:

```
git fetch <remote>
git switch <feature-branch>
git merge main
```
First, you need to switch to the feature branch, merging in the main branch, and then resolve the conflicts in the affected files.

```
git switch main
git merge <feature-branch>
git push <remote> main
```
Finally, you need to swith to the main branch, merge in the feature branch (with the fix applied), and push changes up to GitHub again.

## Forks

When collaborating in big projects with other people, it's a common pattern that every user creates a personal copy of the original project. This copy is known as a form of the original project.

Forks are not a native Git feature, but a functionallity built into platforms like GitHub or Bitbucket. If you clone the original project to your local machine, usually you don't have permissions to push your own work, but if you clone your fork, these restrictions will not apply anymore. Working with forks in big projects usually follows this workflow:

1. Make your own fork of the original project (each collaborator will work with its own fork).
2. Clone your forked repo to your local machine. Git automatically adds a remote called `origin` that points to yout forked repo on GitHub.
3. Set up a second remote, usually named `upstream`, pointing to the original project repo on GitHub.
4. Regularly, before doing new work, make a pull from the upstream remote repo to your local repo, in order to get the latest changes in your local repo.
5. To share your changes, push your local repo to the origin remote repo.
6. From your forked repo on GitHub, make a pull request to the original project GitHub repo.
7. Once your pull request is accepted, the original project repo will contain your changes.

This workflow allows a project maintainer to accept contributions from developers all around the world without having to add them as actual owners of the main project repo or worry about giving them permissions to push to the repo.
