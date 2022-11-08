## Install docker on OpenSUSE
1. `sudo zypper install docker`
2. Use Red Hat Package Manager to check if docker is installed
```
rpm -qi docker
```
3. Use `systemctl` to enable `docker` service
```
sudo systemctl enable docker
```
4. Start `docker` service
```
sudo systemctl start docker
```
5. Check if `docker` service is running
```
sudo systemctl status docker
```
6. Add yourself into the docker group
```
sudo usermod -aG docker $USERNAME
```
7. Check if you are in the docker group
```
id
```
8. Verify that Docker Engine is installed correctly by running the hello-world image.
```
sudo docker run hello-world
```