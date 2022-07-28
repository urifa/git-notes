# Git Notes

Quick Git reference with most used commands. It is mainly based on notes taken from [The Git & Github Bootcamp](https://www.udemy.com/course/git-and-github-bootcamp/) Colt's Udemy course.

## Configure Git

```
git config --global user.name
```
Set up your Git username. This name will be associated to all your work. The `--global` parameter means that this configuration will be used across every Git instance.

```
git config --global user.email
```
Set up your Git email. This email will be associated to all your work. If you have Github, you can use the same email used in your Github account.

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
git add filename.txt
```
Add filename.txt to the staging area, so that it could be committed later. You can check all filenames.txt in your working directory that has been changed from your last commit using `git status`.

```
git add .
```
Add all filenames in your working directory that have been changed from your last commit to the staging area, so that they could be committed later.

```
git commit
```
Publish all changes in the staging area to the current branch you are on. It will open a window of your default text editor, in order to specify a messaged to identify with the main commit changes.

```
git commit -m "This is the commit name"
```
Publish all changes in the staging area to the current branch you are on. You can set up the commit name using `-m` parameter, and then the message you decide in quotation marks.

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
git branch branch-name
```
Create a new branch called `branch-name` taking the current commit on the branch you are on as the initial reference. The HEAD will continue pointing to the current branch, as we are not switching to the new one, just creating it.

```
git switch branch-name
```
Switch to the branch called `branch-name`. The HEAD will now point to the last commit published to `branch-name`, and you will be able to commit new work to this branch from that point.

```
git switch -c branch-name
```
Create a new branch called `branch-name` taking the current commit on the branch you are on as the initial reference, and switch to it at the same time. The HEAD will now point to that same commit but from the newly created branch.

```
git branch -d branch-name
```
Detele the branch called `branch-name`. Deleting a branch can only be made from outside of that branch. This command will display an error if that branch is not fully-merged. If you are sure to delete the branch anyway, you can change the `-d` parameter for `-D`.

```
git branch -m new-branch-name
```
Change the name of the current branch you are on for `new-branch-name`.

```
git branch -m master main
```
Rename your local repository default branch name from `master` to `main`. This change will not apply to other local repositories, just the current one.

```
git config --global init.defaultBranch main
```
Change the local Git default branch name to `main`, in order to follow the Github criteria. The `--global` parameter means that this configuration will be used across every Git instance, so all new local repositories will use now `main` as the default branch name.

```
git merge branch-name
```
Merge all commits from `branch-name` into the current branch you are on. 
- If there are not additional commits to the current branch since you split off and created `branch-name`, the merge is a fast-forward. All commits from `branch-name` will be added to the current branch, and the current branch will end up referring to the same last commit of `branch-name`.
- If there are additional commits to the current branch since the split off, in case there are no conflicts, Git will create a merge commit for us, adding all changes from `branch-name` to the current branch. This commit will have two parent branches, both `branch-name` and the current branch.
- If there are additional commits to the current branch since the split off, but there are conflicting changes, Git will alert that to us. In that case, you will have to manually open the files with conflicting changes (Git will add specific markers in those files) and fix them. Finally you will need to add those changes to the staging area, and commit them.

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
git checkout commit-hash
```
Jump back in time to a particular commit specified by its commit hash. You are now in a "detached HEAD" state, meaning that HEAD does not point to a branch reference (the branch reference is a pointer to the last commit made on this particular branch), but to a particular commit. If you type `git log`, we will see all commits published up until this one. In this state, you cannot make changes, but you can:
- Examine contents of that old commit and finally get out of the "detached HEAD" state by switching back to a particular branch.
- Create a new branch from this state, which will be created taking this commit reference. If you switch to that new branch, you will no longer be on a "detached HEAD" state (HEAD will point to that new branch reference), so you will be able to publish new commits to this branch.

## Restore, Reset and Revert

```
git restore filename.txt
```
Discard changes made on filename.txt and restore it back to where it looked like at HEAD (which by default ponts to the last commit of the current branch). This is useful if you have made changes to a file, saved it, but then you decide you don't want these changes to be applied.

```
git restore --staged filename.txt
```
Remove filename.txt to the staging area, so that it will not be included in the next commit, when you execute `git commit`. This is useful if you accidentally added a file to the staging area with `git add`.

```
git reset commit-hash
```
Reset the current repo back to a previous commit, discarding any changes made after that commit. It removes all commits that came after that, but all changes on files still remain on your working directory, so you don't lose the changes, only the commits. This is useful if you made some commits on the wrong branch, and you want to keep that work, but move it to a separate branch.

```
git reset --hard commit-hash
```
Reset the current repo back to a previous commit, discarding any changes made after that commit. It removes both the commits and the actual changes on files.

```
git revert commit-hash
```
It's similar to `git reset` in that they both undo changes, but `git revert` does that by creating a brand new commit which reverses all changes made from a particular commit. As it results in a new commit, you will be prompted to enter a commit message. If you collaborate with other people, and you want to reverse some commits that other people already have on their machines, you should use `git revert` instead of `git reset`. 

## Remote Repositories

```
git remote
```
Display all remotes you have in the current local repo. Before you can push anything up to Github, you need to tell Git about your remote repository on Github, a destination to push up to. These destinations are called remotes, and each remote is simply a label for a URL where a hosted repository live.
- When you create a new remote for a local repo pointing to hosted repo, you must specify the name for it. A convention to name it is `origin`.
- When you clone a Github repo to your local machine, the default remote name setup for you is called `origin`.

```
git remote -v
```
Display all remotes you have in the current local repo, alongisde with the corresponding URL where the hosted repository live.

```
git remote add origin url
```
Adding a new remote called `origin`, which is the standard name for a remote, associated to a particular Github repo URL. Origin is a conventional Git remote name, but you can use any other name.

```
git clone url
```
Clone a repo hosted on Github or some other cloud platform, providing its url. Git will retrieve all the files associated with the repository and will copy them to your local machine. In addition, Git initializes a new repository on your machine, giving you access to the full Git history of the cloned project. Just like with `git init`, make sure you are not in a Git repository when you clone. When you clone a Github repo to your local machine, the default remote name setup for you is called `origin`.

```
git push origin branch-name
```
Once you have a remote set up, either by using `got clone` or `git remote add`, you can push the work on your local repo up to Github using this command. You need to specify the name of the remote, which in this case is `origin` and the specific local branch you want to push up to that remote. It will also create that branch on Github, in case it does not exist yet.

```
git push -u origin branch-name
```
In this case, the `-u` option allows you to set the upstream of the branch you are pushing. It's as a link connecting your local branch to a branch on Github. This sets the upstream of the local branch specified, so that it tracks that same branch on the origin repo. This allow you to use `git push` next time, without having to specify the remote name nor the branch name, everytime you want to push the last changes of that local branch up to Github.
