# **init**
- `git init repo_name`

# **clone**
- `git clone /path/to/repository <directory>`  
- `git clone https://github.com/aarentai/How-to.git <directory>`
- `git clone git@github.com:aarentai/How-to.git <directory>`
- `git clone username@host:/path/to/repository <directory>`

# **add** *file from working directory to staging area(INDEX)*
- `git add [file1] [file2]`
- `git add <directory>`
- `git add .`

# **diff** *files between working directory and staging area(INDEX)*
- `git diff [file]`

# **commit** *file from staging area(INDEX) to local repo(HEAD)*
-  `git commit -m [remark]`
-  `git commit [file1] [file2] -m [remark]`

# **config**
- `git config -e`
- `git config -e --global`
- 
```
git config --global user.name "test"
git config --global user.email test@outlook.com
```

# **reset** *the modification*
- `git reset`

# **push** *your modification to remote*
- `git push origin master`