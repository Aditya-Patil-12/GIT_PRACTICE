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
    - If some merge conflict comes resolve it manully by selecting the line out of the confilct area to be kept
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