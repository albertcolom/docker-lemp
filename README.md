Docker LEMP + Redis
===========================
[![Build Status](https://travis-ci.org/albertcolom/docker-lemp.svg?branch=master)](https://travis-ci.org/albertcolom/docker-lemp)
### Docker multicontainer: Nginx, php7-fpm, MySQL, Redis

### Requirements
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Installation
Clone this repository
```sh
$ git clone git@github.com:albertcolom/docker-lemp.git
```

Start docker compose
```sh
$ docker-compose up -d

Creating docker_mysql_1
Creating docker_php_1
Creating docker_web_1
Creating docker_redis_1
```

List the contents
```sh
├── README.md
├── config
│   ├── nginx
│   │   └── default.conf
│   └── php-fpm
│       └── php-fpm.conf
├── docker-compose.yml
├── logs
│   └── nginx
│       ├── access.log
│       └── error.log
└── www
    └── index.php
```
Web Server
- [http://localhost:8080](http://localhost:8080)

List the containers
```sh
$ docker-compose ps

     Name                  Command             State                     Ports
-------------------------------------------------------------------------------------------------
docker_mysql_1   docker-entrypoint.sh mysqld   Up      0.0.0.0:3306->3306/tcp
docker_php_1     php-fpm                       Up      0.0.0.0:9080->9000/tcp
docker_redis_1   docker-entrypoint.sh redis    Up      0.0.0.0:6379->6379/tcp
docker_web_1     nginx -g daemon off;          Up      0.0.0.0:443->443/tcp, 0.0.0.0:8080->80/tcp
```

Stop containers docker compose
```sh
$ docker-compose stop

Stopping docker_web_1 ... done
Stopping docker_php_1 ... done
Stopping docker_redis_1 ... done
Stopping docker_mysql_1 ... done
```

Remove containers docker compose
```sh
$ docker-compose rm -f

Going to remove docker_web_1, docker_php_1, docker_redis_1, docker_mysql_1
Removing docker_web_1 ... done
Removing docker_php_1 ... done
Removing docker_redis_1 ... done
Removing docker_mysql_1 ... done
```

### Tips
Connect to Docker container
```sh
$ docker exec -i -t 665b4a1e17b6 /bin/bash #by ID
or
$ docker exec -i -t docker_redis_1 /bin/bash #by Name
```

Stop all Docker containers
```sh
$ docker stop $(docker ps -a -q)
```

Remove all Docker containers
```sh
$ docker rm $(docker ps -a -q)
```

Remove all Docker images
```sh
$ docker rmi $(docker images -q)
```