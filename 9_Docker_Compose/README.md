## Docker Compose

**Installation**

❖ Install docker-compose on your machine, if not already installed.

```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
```

* **Add executable permissions to Docker-compose program**

```
$ sudo chmod +x /usr/local/bin/docker-compose
```

❖	Check docker-compose version.

$ docker-compose --version


●	Creating compose files

❖	Create a directory named nginx in your root.

$ sudo mkdir nginx

❖	Switch to that directory and create a file named docker-compose.yaml

$ cd nginx
$ sudo vi docker-compose.yml

❖	Use docker-compose version 2 to create docker-compose.yaml file.
Create a service named "databases". Use image named "mysql"
Map container 3306 port to host machine 3306 port.
Add environment variables named "MYSQL_ROOT_PASSWORD", "MYSQL_DATABASE", "MYSQL_USER" and "MYSQL_PASSWORD" along with corresponding values for all.

		$ evs.env
MYSQL_ROOT_PASSWORD=redhat08
MYSQL_DATABASE=nginxdb
MYSQL_USER=root

	Add another service named "web"
Use image "nginx"

$ cat docker-compose.yml
version: '3'
services:
databases:
image: mysql
ports:
      - "3307:3306"
env_file:
      - evs.env
web:
image: nginx
ports:
      - "82:80" 
depends_on:
      - databases

Priority decided by databases
●	Running images using docker-compose

❖	Save docker-compose.yaml file and do docker-compose up.
$ docker-compose up –d

Ups two containers – docker ps

❖	Verify nginx service is up and is accessible on machine.

$ curl localhost:80

❖	Stop and remove your dockercontainer usingdocker-compose.

$ docker-compose down

Stops and removes all containers
