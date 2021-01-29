# How to git

## Create a Repo
### init
`git init repo_name`

### clone
- local
    `git clone /path/to/repository <directory>`
- https
    `git clone https://github.com/aarentai/How-to.git <directory>`
- ssh
    `git clone git@github.com:aarentai/How-to.git <directory>`
- remote server
    `git clone username@host:/path/to/repository <directory>`

## Submit or Modify
### add
> add file from working directory to staging area(INDEX)
- files
    `git add [file1] [file2]`
- directory
    `git add <directory>`
- all files under current directory
    `git add .`

### diff
> compare files between working directory and staging area(INDEX)
    `git diff [file]`

### commit
> add file from staging area(INDEX) to local repo(HEAD)
- all files to local repo
    `git commit -m [remark]`
- designated files to local repo
    `git commit [file1] [file2] -m [remark]`

### config
- current repo
 `git config -e`
- all repo
 `git config -e --global`
- user info
```
git config --global user.name "test"
git config --global user.email test@outlook.com
```

### reset
`git reset`

## Push Your Modification
> push file from local repo(HEAD) to remote repo(MASTER)
    `git push origin master`
