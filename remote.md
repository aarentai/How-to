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
5. Open terminal 1 enter instructions below
```
ssh hdai@cibcgpu1.sci.utah.edu
jupyter notebook
```
6. Open terminal 2 enter instruction below
```
ssh hdai@cibcgpu1.sci.utah.edu -L 127.0.0.1:1234:0.0.0.0:9999
```


## Run local Python project in remote server by PyCharm
1. Make sure your PyCharm is professional version
2. `File`->`Setting`->`Project`->`Python Interpreter`->`Add python interpreter`->`SSH interpreter`->`New server configuration`

