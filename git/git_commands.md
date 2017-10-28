## GIT Commands


1. Create a new repo: 
  ```
  git init “new_project_name”
  ```
2. Clone the remote repository to your local machine. (copy "SSH clone URL" from github page)
  ```
  git clone <ssh/https_link>
  ```
3.	Configuring a remote for a fork:
  ```
  git remote -v
  git remote add upstream <ORIGINAL_REPOSITORY.git>
  ```
4.	Create and switch to a branch for a new check (optional):
  ```
  git branch [new-branch-name]
  git checkout [new-banch-name]
  ```
  OR
  ```
  git checkout -b [new-branch]
  ```
5.	Commit changes to [new-branch]:
  ```
  git status
  git add . 
  git commit -m "[commit message]"
  ```
6.	To push branch/changes ([new-branch] to remote):
  ```
  git push origin [new-branch]
  ```
7. Raise a PR:
  ```
  git request-pull [-p] <start> <url> [<end>]
  ```
  
