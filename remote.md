## Run remote C project in remote server by VS Code
1. `ctrl`+`shift`+`p`
2. Select `Remote SSH: Connect to Host`
3. Enter password
4. Open folder
5. Edit
6. Run by `gcc` or `make`

## Run remote Python project in remote server by VS Code
1. `ctrl`+`shift`+`p`
2. Select `Remote SSH: Connect to Host`
3. Enter password
4. Install `Python` extension in remote server
5. Select interpreter `/home/sci/hdai/anaconda2/envs/python37/bin/python`
6. Open folder
7. Edit
8. Run

## Run remote Python project in remote server by Jupyter Notebook
1. Find and open `/home/sci/hdai/.jupyter/jupyter_notebook_config.py`
2. Generate hash password to avoid enter it every time by
```
$ from notebook.auth import passwd
$ passwd()
Enter password:
Verify password:
'sha1:........................'
```
3. Uncomment the line and modify it as
```
c.NotebookApp.allow_remote_access   = True
c.NotebookApp.ip                    = '0.0.0.0'
c.NotebookApp.open_browser          = False
c.NotebookApp.password              = u'sha1:........................' # paste the hash password above
c.NotebookApp.port                  = 9999
c.ConnectionFileMixin.ip            = '0.0.0.0'
```
4. Save it and type `jupyter notebook` in terminal to make the configure file updated.
5. Open terminal 1 and enter instructions below
```
ssh hdai@cibcgpu1.sci.utah.edu
jupyter notebook
```
6. Open terminal 2 and enter instruction below
```
ssh hdai@cibcgpu1.sci.utah.edu -L 127.0.0.1:1234:0.0.0.0:9999
```
If the following warning pop up,
```
bind [127.0.0.1]:1234: Permission denied
channel_setup_fwd_listener_tcpip: cannot listen to port: 1234
Could not request local forwarding.
```
then change it to whatever ip which has not been occupied, say `127.0.0.1:4321`.
7. Open browser and go to
```
http://localhost:1234/
```


## Run local Python project in remote server by PyCharm
1. Make sure your PyCharm is professional version
2. `File`->`Setting`->`Project`->`Python Interpreter`->`Add python interpreter`->`SSH interpreter`->`New server configuration`


## Add new kernel for jupyter notebook after create new conda environment
```
python -m ipykernel install --user --name [name of new environment] --display-name ['name you want to display in notebook']
```

## SSH without password
```
ssh-keygen -t ed25519
```
paste the .pub into /home/sci/hdai/.ssh/authorized_keys

## VScode remote from browser

mkdir -p tunnel && cd tunnel
curl -Lk 'https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64' --output vscode_cli.tar.gz
tar -xf vscode_cli.tar.gz
./code tunnel