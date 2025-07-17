### Git config 
- 1) Check all the configurations of the git repo 
        ```
            git config --list
        ```
- 2) Setting and Getting Git Username 
        ```
            git config --global user.name 'you-github-name' // set
            git config --local user.name 'you-github-name' // set,need to do for every project
            git config user.name // get
        ```
- 3) Setting and Getting Email 
        ```
            git config --global user.email 'you-github-emai' // set
            git config --local user.email 'you-github-emai' // set , need to do for every project
            git config user.email // get
        ```
- 4) Password Save
        ```
            git config --global credential.helper store
        ```
### Create git repo
- Intializing Git Repo
    ```
        git init 
    ```
    - default branch main( prior to v2.28 it was master )
    - -b <branch-name> --initial-branch=<branch-name>
    - Use <branch-name> for the initial branch in the newly created repository. otherwise origin
- Adding Files to be tracked
    ```
        git add . 
    ```
- Commit Changes to Changes to Git repo
    ```
        git commit -m "Your Commit Message" 
    ```

### Remote(github, origin) and Local (device, main)
- 1) Checking all the Remotes(alias) for git repo.
        ```
            git remote 
        ```
        - with -v we get all the url for alias also 
- 2) Adding the remote  
        ``` 
        git remote add <alias> <remote-repo-url>
        ```
        - alias , **optional** shortform to for remote url
        - default origin
- 3) Change/Intialize a remote:
    ```
        git remote set-url <alias> <new-url>
    ```
    - alias **compulsory**
- 4) Rename remote 
    ```
        git remote rename <old-alias> <new-alias>
    ```
- 5) Remove remote  
    ```
        git remote remove <alias>
    ```

### Push 
- 1) To Push we need to set the upstream 
    - Option 1 
        - #### Common Way
            ```
                git push -u <remote-alias> <local-branch>
            ```
            -  u flag set upstream 
            - Push my local branch named **branch** to the remote repo called <remote>, and update the **remote branch with the same name**.
            - After this git push and git pull will be valid ...
            - if no -u is used then again do 
            - git push remote-alias local-branch
        - #### Explict Way
            ```
                git push <remote-name> <local-branch>:<remote-branch>
            ```
    - Option 2 
        - 1) First Fetch the remote 
            ``` 
            git fetch remote-url
            ```
        - 2) Set upstream (only if remote is fetched)
        ```
            git branch --set-upstream-to=<remote-alias>/branch <local-branch>
        ```
        - local-branch ->optional or else current branch is considered ...

### Branch 
- 1) Check for the All the branches (* -> Represent Current Branch in o/p) 
    ```
        git branch 
    ```
    - options -v
        - o/p -> local_branch_name Latest_Commit_hash Latest_Commit_Message
    - options -vv
        - o/p -> local_branch_name Latest_Commit_hash[alias/remote_branch] Latest_Commit_Message
- 2) Create a branch
    - Only creates
    ```
        git branch <new_branch_name>
    ```
    - Creates and move (checkout is use to move) 
    ```
        git checkout -b  <new_branch_name>
    ```
- 3) Move to other branch 
    ```
        git checkout <branch_name_to_move>
    ```
- 4) Rename Branch 
    - If you're on the branch:
        ```
        git branch -m new-branch-name
        ```
    - If you want to rename another branch (without checked out):
        ```
        git branch -m old-branch-name new-branch-name
        ```
- 5) Delete Branch 
    ```
        git branch -d <branch_name_to_be_deleted>
    ```
- 6) Checking difference between Branch 
    - difference between current branch and comparing branch
    ```
        git diff <comparing_branch>
    ```
    - difference between branch1 and branch2 (to go from branch1 -> branch2)
    ```
        git diff branch1 branch2
    ```
- 7) Merging Branch
    - current branch with other branch 
    ```
        git merge <other-branch>
    ```
    - If some merge conflict comes resolve it manully by selecting the line out of the conflict area to be kept
    - Afer merge
        - **Before merge**  Files are different, but changes don’t conflict. Checkout allowed.                                                   
        - **After merge** File (`README.md`) differs across branches and you have local changes. Checkout would overwrite **Git blocks it**. 

    - use git stash to save and switch 

### Fetch 
- Downloads all new commits, branches, and tags from the remote
- but it will never add it in our Local Repo 
- 1) Fetch changes from a remote
    ```
        git fetch origin
    ```
    - Updates your local view of the remote but doesn't merge.
- 2) Merge the changes from remote repo
    ```
        git merge <remote-url>/<branch-main>
    ```

### Pull
-   Fetch + Merge  
-   ```
        git fetch <remote-url> <branch-name>
    ```
-  options rebase( Scenario : Two developers one pushed the changes to remote repo
other is behind the remote and has not pushed his commits to remote so now need to fetch them and add his commits on top of new commits  )
    ```
        git pull --rebase
    ```
    - same as
-   ```
        git fetch
        git rebase <remote-alias>/<branch>
    ```
### Clone
- Clone own or public repo
    ```
        git clone <url>
    ```
- Scenario 1: Cloning Your Own Repo
    - Full commit history is cloned
    - origin is set to your remote repo & Local main tracks origin/main
    - You can push directly if you have write access
-  Scenario 2: Cloning Someone Else’s Repo (e.g., a public project)
    - Full commit history is cloned
    - origin is set to your remote repo & Local main tracks origin/main
    - You cannot push directly as you don't have write access
- Public Repo Contribution 
    - For Scenario 2 we other way  
    - To contribute:
    - Fork the repo on GitHub
    - Add your fork as origin
    - Add original repo as upstream:
    - git remote add upstream 

### Status
- 1) Checking whethere the changes are Stagged or not OR If the local repo and remote repo are ahead or behind of their commits
    ```
        git status
    ```



### Rebase 
-  It helps you place your changes on top of another commit, resulting in a cleaner, linear history, especially useful when working with feature branches.
-  git rebase rewrites history by applying your changes directly to the target branch (typically main or master).
    ```
        git checkout <feature-branch>
       git rebase <base-branch>
    ```
- Happens after you run command
    - Git temporarily removes your commits from the feature branch.
    - Git updates the branch to the latest commit from master 
    - Git reapplies your commits on top of the latest commit from master, one by one.
    -  any conflicts, Git will stop and ask you to fix them.
    - Once the rebase is complete, your feature-branch will appear as if all your changes were made directly on top of the latest master branch, resulting in a cleaner history(in oneline).

- Interactive Rebase
    - To edit, squash, reorder or delete commits in your branch
    - full control over the commit history, cleaning up commit messages or **combining multiple commits into one**.
    - git rebase -i

### git reset 
- To delete the latest commit **but keep changes** (unstaged):
    ```
        git reset --soft HEAD~1
    ```
- To **delete** the latest commit and **discard changes**:
    ```
        git reset --hard HEAD~1 // delete latest hash
    ```
- After hard delete recover the code (Possible under 30 days)
    ```
        git reflog // find commit-hash
    ```
    ```
        git reset --hard HEAD@{n} // reset uptil to n th previous hash
    ```
### git stash
- Scenario
    - developer is working on a feature in a branch if he has to work urgently on some other feature, but the feature he is currently working on is incomplete. In this case, you cannot commit the partial code of the currently working feature. To add this new feature, you have to remove your current changes and store them somewhere else.

- git stash temporarily saves (stashes) your uncommitted changes (both staged and unstaged), cleans your working directory, and lets you switch branches or pull updates without losing your work.
- 1) first push by 
    ```
        git stash
    ```
- 2) come back want the saved changes 
    ```
        git statsh pop
    ```
- 3) Extra stash command 
    ```
         `git stash -u` or `--include-untracked` // Also stash **untracked files**                
         `git stash list`                        // Show all stashed entries                      
         `git stash apply`                       // Apply stash but **keep** it in stash list     
         `git stash drop`                        // Delete latest stash entry                     
         `git stash clear`                       // Delete **all** stash entries                  
         `git stash show`                        // Show what was stashed                         
         `git stash show -p`                     // Show stash changes in **patch (diff)** format 
    ```
### Common Questions
| Repo                          | Branch                               |
| ----------------------------- | ------------------------------------ |
| Entire project (with history) | A version of the code inside a repo  |
| Acts like a container         | Tracks parallel lines of development |

| Git                              | GitHub                               |
| -------------------------------- | ------------------------------------ |
| Local version control tool       | Remote hosting service for Git repos |
| Manages source code locally      | Collaborates, stores repos online    |
| Created by Linus Torvalds (2005) | Owned by Microsoft                   |

| Clone                                 | Remote                               |
| ------------------------------------- | ------------------------------------ |
| Copies the entire repo to your system | URL or name of the **online origin** |
| `git clone <url>`                     | `git remote -v` shows remote info    |

| `git diff`                              | `git status`                                    |
| --------------------------------------- | ----------------------------------------------- |
| Shows **what has changed** line-by-line | Shows **what is staged / unstaged / untracked** |
| More detailed(line by line change)      | More high-level summary                         |


- Version Control System (VCS)
    A VCS helps track changes in code over time, enabling collaboration, rollbacks, and branching.

    Types:

    🔸 Local VCS: Tracks files on your machine (old, limited).

    🔸 Centralized VCS: One server (e.g., SVN).

    🔸 Distributed VCS: Full repo on every machine (e.g., Git).


| Git                                 | SVN (Subversion)                    |
| ----------------------------------- | ----------------------------------- |
| Distributed VCS(present on everyone's machine)| Centralized VCS(after commit files uploaded to server)                     |
| Works offline                       | Needs network for most operations   |
| Faster, flexible branching          | Slower branching                    |


| Merge                                     | Rebase                                 |
| ----------------------------------------- | -------------------------------------- |
| Combines branches **with a merge commit** | Moves commits on top of another branch (all the respective branch commits are moved to top from top to bottom) |
| Keeps full branch history                 | Makes history linear                   |
| Good for preserving context               | Good for clean, linear history         |
|git merge branch-name -m "branches mergered"|     g            | 
