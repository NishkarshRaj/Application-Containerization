## Docker Compose

**1. Installation**

❖ Install docker-compose on your machine, if not already installed.

```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
```

* **Add executable permissions to Docker-compose program**

```
$ sudo chmod +x /usr/local/bin/docker-compose
```

❖ Check docker-compose version.

```
$ docker-compose --version
```

**2. Creating compose files**

❖ Create a directory named nginx in your root.
```
$ sudo mkdir nginx
```
❖ Switch to that directory and create a file named docker-compose.yml

```
$ cd nginx
$ sudo vi docker-compose.yml
```

```
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
```

**Depends on: priortizes task -> If this container is not up, wont up rest containers.**

**82:80** -> Input to Output

❖ Create the environment file for passing as parameter to **docker-compose.yml** file
```
$ gedit evs.env
```
```
MYSQL_ROOT_PASSWORD=redhat08
MYSQL_DATABASE=nginxdb
MYSQL_USER=root
```

**3. Running images using docker-compose**

❖	Save docker-compose.yaml file and do docker-compose up.
```
$ docker-compose up –d
```

Launches all specified container in the .yml file

```
$ docker ps
```

❖	Verify nginx service is up and is accessible on machine.

```
$ curl localhost:80
```

❖	Stop and remove your dockercontainer usingdocker-compose.

$ docker-compose down

Stops and removes all containers
