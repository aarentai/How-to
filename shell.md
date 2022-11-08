### Quit
Press `q`
### Show files
```
ls
ls -a  # will show the hidden files
ls -al # will list the files and directories with detailed information like the permissions, size, owner, etc.
ls -R  # will list all the files in the sub-directories as well
```
### Load directory
```
cd <directory>
cd .. # move one directory up
cd    # to go straight to the home folder
cd-   # move to your previous directory
```
### Edit file
```
vim [file]
```
### Copy
```
cp [file] <directory>
```
### Move
```
mv [file] <directory>
mv [file] [file] # rename a file
```
### Print working directory
```
pwd
```
### Edit directory
```
mkdir <directory>
rmdir <directory> # only empty directory
```
### Delete files and directories
```
rm [file]/<directory>
rm -r # only want to delete the directory
```
### Super user do 
```
sudo
```
### Download files from the internet 
```
wget <link>
```
### Uncompress files
```
tar     -xvf    *.tar
tar     -xzvf   *.tar.gz/*tgz
gzip    -d      *.gz
unrar   e       *.rar
unzip           *.zip
```
### Manual about command
```
man cd # which ways the cd can be used
```
### Change permissions
```
chmod [option] [file]
chmod u=rwx,g=rx,o=r myfile
chmod 754 myfile
chmod 700 -R <directory>
```
>u: "user", g: "group", and o: "other"
>
>r: "read", w: "write", and x: "execute"
>
> Here the digits 7, 5, and 4 each individually represent the permissions for the user, group, and others, in that order. Each digit is a combination of the numbers 4, 2, 1, and 0:
>
>4: "read", 2: "write", 1: "execute", 0: "no permission"
### Connect remote server
```
ssh hdai@cibcgpu1.sci.utah.edu
ssh -Y u1265496@lab1-35.eng.utah.edu
```
### Run a python .py file
```
python3 cky.py [arg]
```
### Run a single .c file
```
gcc assignment1.c -o assignment1
./assignment1
```
### Run a makefile
```
make
./tester
```
### Run python background
```
nohup python BrainAtlasBuilding3D.py &> output_brain3.log
kill -9 pid
```
### Check running processes
```
top (-u hdai)
```
### Check folder size
```
du -h --max-depth=1
```
### 
```
ping/source/echo
```
### Check login history
```
last -f /var/log/wtmp
```