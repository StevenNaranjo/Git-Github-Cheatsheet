# Git and GitHub Guide

## Git Basics
### Initial Setup
- `git config --global user.name "Your Name"` -> Set your Git username.
- `git config --global user.email "youremail@example.com"` -> Set your Git email.
- `git config --list` -> Verify your Git configuration.

### Creating and Cloning Repositories
- `git init` -> Initialize a new Git repository.
- `git clone <RepositoryURL>` -> Clone an existing repository.

### Staging and Committing
- `git status` -> Show the status of changes.
- `git add <file>` -> Stage a specific file.
- `git add .` -> Stage all changes in the current directory.
- `git commit -m "Your message"` -> Commit staged changes with a message.

### Branching
- `git branch` -> List all branches.
- `git branch <branch-name>` -> Create a new branch.
- `git checkout <branch-name>` -> Switch to a branch.
- `git checkout -b <branch-name>` -> Create and switch to a new branch.
- `git merge <branch-name>` -> Merge a branch into the current branch.
- `git branch -d <branch-name>` -> Delete a branch locally (only if merged).
- `git branch -D <branch-name>` -> Force delete a branch locally (even if not merged).
- `git push origin --delete <branch-name>` -> Delete a branch in the remote repository.

### Pushing and Pulling
- `git remote add origin <RepositoryURL>` -> Add a remote repository.
- `git push -u origin <branch-name>` -> Push the branch to the remote repository.
- `git pull` -> Pull the latest changes from the remote repository.

## Tips: Returning to a Previous Commit
### Checkout a Commit (Detached HEAD State)
- `git checkout <commit-hash>` -> Move to a previous commit temporarily.

### Create a New Branch from a Commit
- `git checkout -b <new-branch-name> <commit-hash>` -> Create a new branch from a specific commit.

### Revert Changes Without Affecting History
- `git revert <commit-hash>` -> Create a new commit that undoes the changes of a specific commit.

### Reset to a Previous Commit (Destructive)
- `git reset --soft <commit-hash>` -> Reset to a commit but keep changes staged.
- `git reset --mixed <commit-hash>` -> Reset to a commit and unstage changes.
- `git reset --hard <commit-hash>` -> Reset to a commit and discard all changes.

**Note:** After making changes to a previous commit, push with `git push --force` to overwrite the remote history (if necessary).

### Deleting Commits
- `git reset --hard HEAD~1` -> Delete the last commit and discard changes.
- `git reset --soft HEAD~1` -> Delete the last commit but keep changes staged.
- `git revert <commit-hash>` -> Undo a specific commit by creating a new commit that reverses its changes.

## Handling Changes After Returning to a Previous Commit
If you return to a previous commit (e.g., `commit 2`) and make changes, here are your options:

### **Option 1: Create a New Branch**
1. Create a new branch to isolate the changes:
   ```bash
   git checkout -b new-branch
   ```
2. Commit your changes:
   ```bash
   git add .
   git commit -m "Changes made from commit 2"
   ```
3. Push the branch to the remote repository (if needed):
   ```bash
   git push origin new-branch
   ```

### **Option 2: Continue in the Same Branch**
1. If you want to overwrite the existing history in the same branch:
   - Perform a soft reset to `commit 2`:
     ```bash
     git reset --soft <commit-2-hash>
     ```
   - Stage and commit the new changes:
     ```bash
     git add .
     git commit -m "Updated changes from commit 2"
     ```
2. Push the updated branch, forcing the overwrite:
   ```bash
   git push --force
   ```

### **Option 3: Merge the Changes Back**
1. Create a new branch from `commit 2`:
   ```bash
   git checkout -b feature-branch <commit-2-hash>
   ```
2. Commit your changes in the new branch:
   ```bash
   git add .
   git commit -m "New changes from commit 2"
   ```
3. Switch back to the original branch:
   ```bash
   git checkout Rama1
   ```
4. Merge the new branch:
   ```bash
   git merge feature-branch
   ```

### **Option 4: Rebase to Rewrite History**
1. Start an interactive rebase:
   ```bash
   git rebase -i HEAD~3
   ```
2. In the rebase editor, mark the second commit (`commit 2`) as `edit`.
3. Make your changes, stage them, and commit:
   ```bash
   git add .
   git commit --amend --no-edit
   ```
4. Continue the rebase:
   ```bash
   git rebase --continue
   ```
5. Push the rewritten history (force required if already pushed):
   ```bash
   git push --force
   ```

---

## Visualize branches

### Using a git command
   ```sh
   git log --oneline --graph --all --decorate
   ```
## Using a VS Code Extention
   - Git Graph






---
## Where to learn git
- [Git Documentation](https://git-scm.com/docs)
- [Learn Git Branching](https://learngitbranching.js.org/)




---

## Working with GitHub
### Forking and Pull Requests
1. Fork a repository.
2. Clone your fork with `git clone <your-fork-url>`.
3. Create a new branch, make changes, and push to your fork.
4. Open a pull request from your fork to the original repository.

### GitHub CLI
- `gh auth login` -> Authenticate GitHub CLI.
- `gh repo clone <repository>` -> Clone a GitHub repository.
- `gh issue list` -> List issues in a repository.
- `gh pr create` -> Create a pull request.

## Using Git with VS Code
### Setup
1. Open VS Code.
2. Install the **GitHub** and **GitLens** extensions.
3. Sign in to your GitHub account in VS Code.

### Basic Workflow in VS Code
1. Open the integrated terminal (Ctrl+`).
2. Use the source control view (Ctrl+Shift+G) to stage, commit, and push changes.
3. View diffs, blame, and commit history with GitLens.

### Resolving Merge Conflicts
1. Use the merge conflict editor provided by VS Code.
2. Select changes (e.g., `Accept Current`, `Accept Incoming`, or `Accept Both`).
3. Test your resolution and commit.

## Additional Tips
- **Undo Last Commit:**
  - `git reset --soft HEAD~1` -> Undo the last commit but keep changes staged.
  - `git reset --mixed HEAD~1` -> Undo the last commit and unstage changes.
  - `git reset --hard HEAD~1` -> Undo the last commit and discard changes.

- **Stash Changes:**
  - `git stash` -> Temporarily save changes.
  - `git stash apply` -> Apply stashed changes.

- **Tagging Commits:**
  - `git tag <tag-name>` -> Create a tag.s
  - `git push origin <tag-name>` -> Push a tag to the remote repository.

- **Show Commit History:**
  - `git log` -> Show detailed commit history.
  - `git log --oneline` -> Show a concise commit history.

---

This guide provides an overview of Git and GitHub commands, along with tips for common workflows and integration with VS Code. Expand or modify as needed!
