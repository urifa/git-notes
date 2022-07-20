# Git Notes

Quick Git reference with most used commands. It is mainly based on notes taken from [The Git & Github Bootcamp](https://www.udemy.com/course/git-and-github-bootcamp/) Colt's Udemy course

## Configuring Git

```
git config --global user.name
```
Configure the name Git will associate with your work. The `--global` parameter means that this configuration will be used across every Git instance

```
git config --global user.email
```
Configure the email Git will associate with your work. If you have Github, you can use the same email used in your Github account

```
git config user.name
```
Check up if there is any name configured in Git

## Setting up Git

```
git init
```
Create a new Git repository inside your current working directory. You can use `git status` to make sure there isn't a Git repository configured yet. If you create a Git repository inside a working directory, this will apply in all child directories as well

```
git status
```
Show if the current working directory has been configured as a Git repository. In that case, it will show if there are changes in the working directory pending to be added or committed

## Adding and Commiting

```
git add filename.txt
```
blablabla

```
git add .
```
blablabla

```
git commit -m "This is the commit name"
```
blablabla

## Branches

```
git branch
```
View all branches used in the current Git repository. The branch you are currently on is highlighted with *

```
git branch branch-name
```
Create a new branch called `branch-name` taking the current branch you are on as the initial reference

## Stashing

## Restore, Reset and Revert
