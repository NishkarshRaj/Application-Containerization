## Introduction to Docker Swarm

For real applications IT users and app teams need more sophisticated tools. Docker supplies two such tools: Docker Compose and Docker Swarm Mode. The two tools have some similarities but some important differences:

**Compose** is used to control multiple containers on a single system. Much like the Dockerfile we looked at to build an image, there is a text file that describes the application: which images to use, how many instances, the network connections, etc. But Compose only runs on a single system so while it is useful, we are going to skip Compose1 and go straight to Docker Swarm Mode.

**Swarm Mode** tells Docker that you will be running many Docker engines and you want to coordinate operations across all of them. Swarm mode combines the ability to not only define the application architecture, like Compose, but to define and maintain high availability levels, scaling, load balancing, and more. With all this functionality, Swarm mode is used more often in production environments than it’s more simplistic cousin, Compose.

### The application

The voting app is a multi-container application often used for demo purposes during Docker meetups and conferences. It basically allow users to vote between two choices, the default being “cat” and “dog”, but could be “space” or “tab”, too, if you feel like it. This application is available on Github and updated very frequently when new features are developed.

### Initialize Master Node

```
$ docker swarm init --advertise-addr $(hostname -i)
```

### Initialize Worker Node

```
$ docker swarm join --token [token] [host IP]
```

### Show member nodes from master

```
$ docker node ls
```

### Docker Swarm Architecture

### Clone the Voting Application on Master Node

```
$ git clone https://github.com/docker/example-voting-app
$ cd example-voting-app
```

### Create Docker Compose file

```yml
version: "3"services:

  redis:    
    image: redis:alpine
    networks:
      - frontend
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure
  db:
    image: postgres:9.4
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "postgres"
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - backend
    deploy:
      placement:
        constraints: [node.role == manager]
  vote:
    image: dockersamples/examplevotingapp_vote:before
    ports:
      - 5000:80
    networks:
      - frontend
    depends_on:
      - redis
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
      restart_policy:
        condition: on-failure
  result:
    image: dockersamples/examplevotingapp_result:before
    ports:
      - 5001:80
    networks:
      - backend
    depends_on:
      - db
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure

  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - frontend
      - backend
    depends_on:
      - db
      - redis
    deploy:
      mode: replicated
      replicas: 1
      labels: [APP=VOTING]
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
      placement:
        constraints: [node.role == manager]

  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    stop_grace_period: 1m30s
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]

networks:
  frontend:
  backend:

volumes:
  db-data:
```

### Deploy Application Stack

```
$ docker stack deploy --compose-file=docker-stack.yml voting_stack
$ docker stack ls
$ docker stack services voting_stack
```

### Stack vs Service vs Tasks in Docker Swarms

### Scaling Swarm Application

```
$ docker service scale voting_stack_vote=5
```

## References

[Play With Docker ClassRoom](https://training.play-with-docker.com/ops-s1-swarm-intro/)
