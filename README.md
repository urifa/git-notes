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
Create a new branch called `branch-name` taking the current branch you are on as the initial reference.

```
git branch -m master main
```
Rename your local repository default branch name from `master` to `main`. 

```
git config --global init.defaultBranch main
```
Change the default branch name to `main`, in order to follow the Github criteria. The `--global` parameter means that this configuration will be used across every Git instance, so all new local repositories will use `main` as the default branch name.

## Stashing

## Change HEAD Reference

## Restore, Reset and Revert

```
git restore filename.txt
```
Restore filename.txt content to the contents in the HEAD. This is useful if you have made changes to a file, saved it, but then you decide you don't want these changes to be applied.

```
git restore --staged filename.txt
```
Remove filename.txt to the staging area, so that it will not be included in the next commit, when you execute `git commit`. This is useful if you accidentally added a file to the staging area with `git add`.

## Remote Repositories

```
git clone 
```
kjlkj

```
git remote
```
khkjh

