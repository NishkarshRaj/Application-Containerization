# Install Docker on Ubuntu Linux

1. Go to root folder with root priviliges
2. Update and upgrade
$ sudo apt-get update && sudo apt-get upgrade
3. Uninstall Old Docker version
$ sudo apt-get remove docker docker-engine docker.io
4. Install Docker
$ sudo apt install docker.io
5. Start and configure docker
$ sudo systemctl start docker
$ sudo systemctl enable docker
6. Check docker version to verify installation
$ docker --version
7. Run Hello World container to verify successfull installation of client, daemon etc.
$ docker run hello-world

Note: Run Ubuntu bash using:
$ docker run -it ubuntu bash
