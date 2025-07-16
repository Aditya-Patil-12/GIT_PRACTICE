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
- 2) Rename Branch 
    - If you're on the branch:
        ```
        git branch -m new-branch-name
        ```
    - If you want to rename another branch (without checked out):
        ```
        git branch -m old-branch-name new-branch-name
        ```

### Fetch
- 1) Fetch changes from a remote
    ```
    git fetch origin
    ```
    - Updates your local view of the remote but doesn't merge.
### Clone

### Status
- 1) Checking whethere the changes are Stagged or not OR If the local repo and remote repo are ahead or behind of their commits
    ```
        git status
    ```