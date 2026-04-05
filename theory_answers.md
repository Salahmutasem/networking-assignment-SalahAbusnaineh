# Theory Answers

## Part 1: Git & GitHub

### Q1. Define the following Git terms with examples

**Repository**  
A repository, or repo, is the place where a project’s files and their version history are stored. It contains the code, documents, and all tracked changes.  
Example: If you create a project called `student-system`, the folder with its Git tracking becomes a repository.

**Commit**  
A commit is a saved snapshot of the project at a specific point in time. It records the changes made to files with a message describing those changes.  
Example: After adding a login page, you may create a commit with the message:  
`Added login page`

**Branch**  
A branch is a separate line of development in a repository. It allows you to work on new features or fixes without affecting the main project.  
Example: You create a branch called `new-login-feature` to develop a login system without changing the main branch.

**Merge**  
Merge means combining changes from one branch into another. It is usually done after finishing work on a feature branch.  
Example: After completing the `new-login-feature` branch, you merge it into the main branch so the login feature becomes part of the main project.

**Clone**  
Clone means making a copy of an existing remote repository onto your local computer.  
Example: If a project is on GitHub, you can use `git clone` to download it to your device and start working on it.

---

### Q2. Explain the difference between

**git fetch vs git pull**  
`git fetch` downloads the latest changes from the remote repository but does not apply them to your current branch.  
`git pull` downloads the changes and automatically merges them into your current branch.

**git merge vs git rebase**  
`git merge` combines changes from one branch into another and keeps both histories, often creating a merge commit.  
`git rebase` moves your branch changes on top of another branch, creating a cleaner and linear history.

**Local repository vs Remote repository**  
A local repository is stored on your computer where you make changes and commits.  
A remote repository is stored on a server like GitHub and is used for sharing and collaboration.

---

### Q3. Purpose of .gitignore

The purpose of a `.gitignore` file is to tell Git which files and folders should not be tracked or uploaded to the repository. This helps avoid uploading unnecessary or sensitive files.

**Examples:**

- `node_modules/`
- `.env`
- `*.log`

---

## Task 3: Git Log & History Explanations

**1. git log --oneline**  
This command shows the commit history in a short one-line format. It helps quickly view commits such as adding files, creating branches, and resolving merge conflicts.

**2. git branch**  
This command shows all local branches and highlights the current branch with `*`. It confirms the created feature branches and the active branch.

**3. git status**  
This command shows the current state of the repository. It indicates whether there are changes to commit and confirms that the working directory is clean.

**4. git remote -v**  
This command displays the remote repository URLs used for fetching and pushing. It confirms that the local project is connected to GitHub.

**5. git log --graph --oneline --all**  
This command shows the commit history in a graphical format. It helps visualize how branches were created and merged into the main branch.

**6. git branch -a**  
This command lists all local and remote branches. It shows both local branches and the remote `origin/main` branch.
