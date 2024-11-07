# GIT and GitHub  
## A Beginner Guide to Source Control Management


### What is Git and GitHub?

**Git** is a tool that helps to track changes in the code. **GitHub** is a website where developers can upload their code and collaborate with other developers. GitHub is also called **Source Control Management (SCM)**.

### Basic Workflows of GitHub

- **Creating a repository**: A repository is where you store your project files, such as HTML documents, CSS stylesheets, JavaScript source code, images, videos, etc.
- **Cloning a repository**: When you create a repository on GitHub but want to access and modify it locally, you clone the repo to your local machine.
- **Making changes**: You write, edit, stage, commit, and pull changes.
- **Pushing**: After making changes locally, you push those changes to the remote repository to reflect them online.

---

### Basic Git Commands

- **git clone**: Clone the repository to your local PC.
- **git status**: Check the status of your git repository.
- **git add <filename/source>**: Add the new or modified file to the staging area so that it is ready to commit.
- **git commit -m "message"**: Add a commit message to describe the changes made.

### File Types in Git

- **Untracked file**: A new file that Git doesn't yet track.
- **Modified**: A file that has been changed.
- **Staged**: A file that is ready to be committed.
- **Unmodified**: A file that has not been changed.

---

### Important Git Commands

- **PUSH COMMAND**: Uploads the local repository to the remote repository.

  ```bash
  git push origin main

-  The -u flag allows you to always push changes to the main branch without specifying origin main each time.
Where `origin` is the name we have made for the remote repo and `main` is the branch where we want to change. 


### INIT Command: 
Used to create a new repository in the folder:

- `git remote add origin <url>`
- `git remote -v`: To verify the remote.
- `git branch`: To check the branches of the repo.
- `git branch -M main`: To rename branches.

## Branch Commands

- To check the current branch with: `git branch`
- To create a new branch: `git checkout -b`
- To switch between branches: `git checkout`
- To delete a branch: `git branch -d`
- `git branch -D`: This can be used if you are sure about deleting the branch.

### Merging Branches
To merge two branches (main/master) with other branches:
- Go to the branch from which you want to merge using: `git checkout`
- Use the command: `git merge <main>` (where `main` is the branch name).

Alternatively, create a pull request in GitHub, then accept it.

### Pull Command
After making changes in the remote repo of GitHub, they will not show until you write a pull command in the local repo:

`git pull origin <branch_name>`
This is used to fetch and download all the changes from the remote repo to your local machine.

## Resolving Merge Conflicts
Occurs when git is unable to automatically resolve differences in code between two commits. You will see:
<<<<<<< HEAD ======= >>>>>>>

You need to manually edit the file to resolve the conflicts. Once done, save the file and use:
`git add `to stage the file.

## Undoing Changes

### Case 1: Staged Changes (added but not committed yet)
` git reset `
This will unstage the file, but the change will still remain in the working directory.

### Case 2: Committed Change (for 1 committed file only)
`git reset HEAD ~ 1`
It will undo your last commit.

### Case 3: Committed Change (for many committed files)
- Use `git log` to see the list of commits.
- `git reset <commit_code>` to reset to a specific commit.
- `git reset --hard <commit_id>`: Command is used to reset your current branch to a specific commit.

### Case 4: Revert a Commit
In case of a mistake in your latest commit, use:
`git revert <commit_id>`
to undo that commit.

## Git Logs
Shows the history of commits made on a specific branch. Lists each commit’s SHA, author, date, and commit message. It is used to view the history of the project.

## Fork
A new repository that shares code and visibility settings with the original repository. A fork is like a rough copy of someone's work that you save in your own account for creating changes or contributing.

To fork the repo, go to the repo you want to fork. There will be a fork option in the top right corner. Click on create new fork, and then create the repo.



