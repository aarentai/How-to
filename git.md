## Clone an existing repo from github and edit locally
```
git clone git@github.com:aarentai/How-to.git
# add or edit the files
git add [file]/<directory>/.
git commit [file]/<directory>/ -m "comment"
git push origin main
```
----
## ...or initialize a repo locally then push to github
```
git init [repo]
# add or edit the files
git add [file]/<directory>/.
git commit [file]/<directory>/ -m "comment"
git push origin main
```
----
## or push an existing repo from the command line
```
# enter the directory
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/aarentai/Atlas2D.git
git branch -M main
git push -u origin main
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

- **PUSH** 
your modification to remote
   - `git push origin main`

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

- **DIFF** 
files between working directory and staging area(INDEX)
   - `git diff [file]`