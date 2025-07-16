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
- 1) checking remote
        ```
        git remote -v
        ```
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
            - Push my local branch named <branch> to the remote repo called <remote>, and update the **remote branch with the same name**.
            - After this git push and git pull will be valid ...
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
- Check for the All the branches (Current Branch) 
 - git branch (* -> represent current branch)
- Rename 
    - If you're on the branch:
        ```
        git branch -m new-branch-name
        ```
    - If you want to rename another branch (without checked out):
        ```
        git branch -m old-branch-name new-branch-name
        ```
-   Current Tracking Info
    ```
        git branch -vv
    ```
    - Which local branch you're on
    - What remote it's tracking
    - Whether it's ahead/behind

### Fetch
- 1) Fetch changes from a remote
    ```
    git fetch origin
    ```
    - Updates your local view of the remote but doesn't merge.
### Clone