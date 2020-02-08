1. Start Vagrant
$ vagrant up
2. Up a vagran box on vagrant
$ vagrant ssh
3. install docker
$ sudo apt install docker.io
4. pull alpine image
$ docker pull alpine
5. run container
$ docker run alpine
6. go inside container terminal
$ docker run -it alpine 
7. stop the container
ctrl + p + s -> goes in detached mode : up but in daemon
-> destroy container: $ docker stop <container name>
8. start the exited container
$ docker ps
$ docker ps -a
$ docker start container-id : Launches an exited container in up and running state
9. execute linux command in container using alpine shell
$ docker run -it alpine /bin/sh
10. delete container -> remove exited containers from memory -> cannot see them after docker ps -a
$ docker rm container id
11. delete images
$ docker images -> to see all the images locally present
$ docker rmi <image name>

-> docker run -it -d alpine \bin\sh (run in background)
-> docker run -it alpine \bin\sh (get terminal)
(to execute detached image that is up -> Either by CTRL + P + Q or by opening it in detached mode -d)
-> docker exec -it containter-name \bin\sh
-> docker exec -it cont-name ls

ctrl+p+q -> move back to parent os terminal without exiting and stopping container

*** start vs exec vs attach
