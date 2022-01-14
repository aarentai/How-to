## Clone an existing repo from github and edit locally
```
git clone git@github.com:aarentai/How-to.git
# add or edit the files
git add [file]/<directory>/.
git commit [file]/<directory>/ -m "comment"
git push origin main
```
----
## or initialize a repo locally then push to github
```
git init [repo]
# add or edit the files
git add [file]/<directory>/.
git commit [file]/<directory>/ -m "comment"
git push origin main
```
----
## or push an local repo to github
```
# enter the directory
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/aarentai/Atlas2D.git
git branch -M main
git push -u origin main
```
## or delete a file from repo and push
```
git rm [file]
git commit -m ""
git push
```
## or rename a file from repo and push
```
git mv [oldfile] [newfile]
git commit -m ""
git push origin main
```
## pull the edited version from remote and merge with local versions
```
git stash
git pull
// if failed due to conflict
git mergetool
:diffg LO
git pull origin main
```
----
- **INIT**
   - `git init repo_name`

- **CLONE**
   - `git clone /path/to/repository <directory>`  
   - `git clone https://github.com/aarentai/How-to.git <directory>`
   - `git clone git@github.com:aarentai/How-to.git <directory>`
   - `git clone username@host:/path/to/repository <directory>`

- **ADD** 
file from working directory to staging area(INDEX)
   - `git add [file1] [file2]`
   - `git add <directory>`
   - `git add .`
> REMARK: SAVE FILE BEFORE ADD

- **COMMIT** 
file from staging area(INDEX) to local repo(HEAD)
   -  `git commit -m [remark]`
   -  `git commit [file1] [file2] -m [remark]`

- **BRANCH**


- **PUSH** 
your modification to remote
   - `git push origin main`

- **PULL** 
your modification from remote
   - `git pull origin main`

- **CONFIG**
   - `git config -e`
   - `git config -e --global`
   - 
```
git config --global user.name "test"
git config --global user.email test@outlook.com
```

- **RESET** 
the modification
   - `git reset`
   - `git reset --soft HEAD~3`, go back 3 versions
ungit a folder
   - `rm -rf .git`

- **DIFF** 
files between working directory and staging area(INDEX)
   - `git diff [file]`

- **GREP**
   - `git grep [keyword]`