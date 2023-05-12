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
<!-- use ssh rather than https -->
git remote add origin git@github.com:aarentai/Metric-Nn-3D.git
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
   -  `git commit --amend`

- **BRANCH**


- **PUSH** 
your modification to remote
   - `git push origin main`
overwrite the remote repo with local
   - `git push -f origin main`
If you've correctly added your SSH key to your GitHub account, it should allow you to authenticate without a password when you push changes to a repository. However, there are a few reasons why you might still be prompted for a password:

   - Check that you're using the correct URL for the repository. If you're using the HTTPS URL instead of the SSH URL, you'll still be prompted for a password. To check the URL, go to your repository on GitHub, click on the green "Code" button, and make sure that "SSH" is selected.

   - Make sure that your local repository is using the SSH URL. If you've previously cloned the repository using the HTTPS URL, you'll need to update the remote URL to use SSH. You can do this using the `git remote set-url` command, like this:

   ```
   git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
   ```

   Replace "USERNAME" and "REPOSITORY" with your GitHub username and the name of the repository you're working with.

   - Check that your SSH key is being used. When you run the `ssh` command, you should see a message like "Welcome to GitHub, USERNAME!" If you don't see this message, it means that your SSH key is not being used and you're being prompted for a password.

   - If you're still having issues, try restarting your SSH agent. Run the following commands in your terminal:

   ```
   eval "$(ssh-agent -s)"
   ssh-add
   ```

   This will start the SSH agent and add your SSH key. Then try pushing your changes again.

   If you're still having issues, you can check the GitHub documentation on troubleshooting SSH connectivity issues: https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/troubleshooting-ssh.

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