## GIT CheatSheet


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
4.  Sync remote branch with fork to get latest changes made to remote branch
  ```
  git fetch upstream
  git merge upstream/master
  git push origin master
  ```
5.	Create and switch to a branch for a new check (optional):
  ```
  git branch [new-branch-name]
  git checkout [new-branch-name]
  ```
  OR
  ```
  git checkout -b [new-branch]
  ```
6.	Commit changes to [new-branch]:
  ```
  git status
  git add .
  git commit -m "[commit message]"
  ```
7.	To push branch/changes ([new-branch] to remote):
  ```
  git push origin [new-branch]
  ```
8. Raise a PR:
  ```
  git request-pull [-p] <start> <url> [<end>]
  ```
