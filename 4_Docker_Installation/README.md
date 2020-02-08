# Install Docker on Ubuntu Linux

## Way 1: Unofficial docker.io package

1. Go to root folder with root priviliges

2. Update and upgrade
```
$ sudo apt-get update && sudo apt-get upgrade
```
3. Uninstall Old Docker version
```
$ sudo apt-get remove docker docker-engine docker.io
```
4. Install Docker
```
$ sudo apt install docker.io
```
5. Start and configure docker
```
$ sudo systemctl start docker
$ sudo systemctl enable docker
```
6. Check docker version to verify installation
```
$ docker --version
```
7. Run Hello World container to verify successfull installation of client, daemon etc.
```
$ docker run hello-world
```

**Note:** Run Ubuntu bash using:
```
$ docker run -it ubuntu bash
```

## Way 2: Official Docker registry installation

1. Ensure the downloads are valid, add the GPG key for the official Docker repository to your system:
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

2.	Add the Docker repository to APT sources:
```
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

3. Update the package database with the Docker packages from the newly added repo:
```
$ sudo apt-get update
```
4. Make sure you are about to install from the Docker repo instead of the default Ubuntu 18.04 repo:
```
$ apt-cache policy docker-ce
```
5. Install Docker engine:
```
$ sudo apt-get install -y docker-ce
```
6. Verify Docker Installtion
```
$ sudosystemctl status docker
```
