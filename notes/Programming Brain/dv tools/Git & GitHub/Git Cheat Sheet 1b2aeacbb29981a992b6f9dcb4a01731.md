# Git Cheat Sheet

Git cheat sheet that serves as a quick reference for basic Git commands to help you learn Git. Git branches, remote repositories, undoing changes, and more.

---

➤ Git initialize a local repository.

```bash
git init
```

➤ Git configuration including user Name and Email.

```bash
git config --global user.name "Your Name"
git config --global user.email "Your Email"
```

➤ Git clone a repository from a remote server to your local machine.

```bash
git clone <remote-url>
```

➤ Git add files to staging area.

```bash
git add <file-name> # Add a single file
git add . # Add all files
git add -A # Add all files
```

➤ Git Commit changes without a message.

```bash
git commit
```

➤ Git Commit changes with a message.

```bash
git commit -m "Commit message here"
```

➤ Git Commit changes and skip the staging area.

```bash
git commit -a -m "Commit message here"
```

➤ Git Commit changes with a message and add all files.

```bash
git commit -am "Commit message here"
```

➤ Git status of the current repository including staged, unstaged, and untracked files.

```bash
git status
```

➤ Git commit history of the current repository.

```bash
git log
```

➤ Git commit history including changes of the current repository.

```bash
git log -p
```

➤ Git commit history of a specific file in the current repository.

```bash
git log -p <file-name>
```

➤ Git changes made before committing.

```bash
git diff
```

➤ Git changes made after committing.

```bash
git diff --staged
```

➤ Git remove tracked files from the current working tree.

```bash
git rm <file-name>
```

➤ Git remove tracked files from the current working tree and staging area and also remove the file from the local repository.

```bash
git rm -f <file-name>
```

➤ Git rename file in the current working tree.

```bash
git mv <old-file-name> <new-file-name>
```

➤ Git revert unstaged changes in the current working tree.

```bash
git checkout <file-name>
```

➤ Git revert staged changes in the current working tree.

```bash
git reset HEAD <file-name>
git reset HEAD -p
```

➤ Git revert committed changes in the current working tree.

```bash
git revert <commit-id>
```

➤ Git revert committed changes and delete the commit history.

```bash
git reset --hard <commit-id>
```

➤ Git create a new branch in the current repository.

```bash
git branch <branch-name>
```

➤ Git create a new branch and switch to it in the current repository.

```bash
git checkout -b <branch-name>
```

➤ Git switch to a branch in the current repository.

```bash
git checkout <branch-name>
```

➤ Git merge a branch into the current branch in the current repository.

```bash
git merge <branch-name>
```

➤ Git delete a branch from the current repository.

```bash
git branch -d <branch-name>
```

➤ Git branch rename in the current repository.

```bash
git branch -m <new-branch-name> #Rename the current branch
git branch -m <old-branch-name> <new-branch-name> #Rename any branch
```

➤ Git list branches in the current repository.

```bash
git branch
```

➤ Git list all branches in the current repository including remote branches.

```bash
git branch -a
```

➤ Git list all remote branches.

```bash
git branch -r
```

➤ Git add a remote repository to the current repository.

```bash
git remote add <remote-name> <remote-repo-url>
```

➤ Git rename a remote repository to the current repository.

```bash
git remote rename <old-remote-name> <new-remote-name>
```

➤ Git remove a remote repository from the current repository.

```bash
git remote remove <remote-name>
```

➤ Git remote url of the current repository.

```bash
git remote -v
```

➤ Git push changes to the remote repository.

```bash
git push
```

➤ Git push changes to the remote repository with a new branch branch.

```bash
git push -u <remote-name> <branch-name>
```

➤ Git remove a branch from the remote repository.

```bash
git push <remote-name> --delete <branch-name>
```

➤ Use the **-force** flag along with the Git Push command to **force** a push.

```bash
git push -u <remote-name> <branch-name> --force
git push -f -u <remote-name> <branch-name>
```

➤ Git push all the branches to the remote repository.

```bash
git push --all <remote-name>
```

➤ Git pull changes from the remote repository.

```bash
git pull
```

➤ Remove Git from Your Project Directory

To remove Git from a folder, you need to delete the .git directory, which contains all the repository's metadata and history. Here are the steps to remove Git from a folder:

1. **Navigate to the folder:** Open a terminal or command prompt and navigate to the directory where your Git repository is located.
2. **Delete the .git directory:** Use the appropriate command to delete the .git directory. The command varies depending on your operating system.

Windows (Command Prompt):

```bash
rmdir /s /q .git
```

Windows (PowerShell):

```bash
Remove-Item -Recurse -Force .git
```

or

```bash
rm .git
```

Unix/Linux/macOS:

```bash
rm -rf .git
```