[![Docker Hub; noplanalderson/simasjid_docker](https://badges.weareopensource.me:/docker/automated/noplanalderson/simasjid_docker?color=blue&label=SIMASJID%20DOCKER&style=for-the-badge)](https://hub.docker.com/r/noplanalderson/simasjid_docker) [![](https://badges.weareopensource.me:/docker/pulls/noplanalderson/simasjid_docker?style=for-the-badge)](https://hub.docker.com/r/noplanalderson/simasjid_docker) [![](https://badges.weareopensource.me:/docker/image-size/noplanalderson/simasjid_docker?style=for-the-badge)](https://hub.docker.com/r/noplanalderson/simasjid_docker) [![nginx 1.19.10](https://img.shields.io/badge/nginx-1.19.10-brightgreen.svg?&logo=nginx&logoColor=white&style=for-the-badge)](https://nginx.org/en/CHANGES) [![php 8.0.5](https://img.shields.io/badge/php--fpm-8.0.5-blue.svg?&logo=php&logoColor=white&style=for-the-badge)](https://secure.php.net/releases/8_0_5.php)

## Introduction
This is a Dockerfile to build a debian based container image running nginx and php-fpm 8.0.x & Composer.

### Versioning
| Docker Tag | GitHub Release | Nginx Version | PHP Version | Debian Version | Composer
|-----|-------|-----|--------|--------|------|
| latest | master Branch |1.19.10 | 8.0.5 | buster | 2.0.13 |

## Building from source
To build from source you need to clone the git repo and run docker build:
```
$ git clone https://github.com/noplanalderson/simasjid_docker.git
$ cd simasjid_docker
```

followed by
```
$ docker build -t simasjid_docker:latest . # PHP 8.0.x
```


## Pulling from Docker Hub
```
$ docker pull noplanalderson/simasjid_docker:latest
```

## Running
To run the container:
```
$ docker run -d noplanalderson/simasjid_docker:latest
```

Default web root:
```
/usr/share/nginx/html/simasjid
```

## Using Docker Compose or Stack

```
$ mkdir db-data simasjid_logs
```
```
$ touch simasjid_logs/access.log simasjid_logs/error.log
```
```
$ nano docker-compose.yml
```
And copy this script to docker-compose.yml file.
```
version: "3"

services:
  nginx:
    image: 'noplanalderson/simasjid_docker:latest'
    ports:
        - '80:8080'
        - '443:8443'
    volumes:
        - ./simasjid_logs/access.log:/var/log/nginx/simasjid-access.log
        - ./simasjid_logs/error.log:/var/log/nginx/simasjid-error.log
        - ./simasjid:/usr/share/nginx/html/simasjid
        - ./default.conf:/etc/nginx/conf.d/default.conf
    networks:
      app_net:
        ipv4_address: 172.20.0.2

  mysql:
    image: 'mariadb'
    ports:
        - '3306:3306'
    volumes:
        - ./db-data:/var/lib/mysql
    environment:
        - MARIADB_ROOT_PASSWORD=K4s1hp4ssw0rdY4n9kUat!
        - MARIADB_DATABASE=db_simasjid
        - MARIADB_USER=userdb_simasjid
        - MARIADB_PASSWORD=K4s1hp4ssw0rdY4n9kUat!
    networks:
      app_net:
        ipv4_address: 172.20.0.3

networks:
  app_net:
    ipam:
      driver: default
      config:
        - subnet: "172.20.0.0/29"
```
```
$ docker-compose up -d
```

## Warning
1. This image not include MySQL Server
2. Dont forget to change server_name value in default.conf

    ```
    server_name _; # Replace _ with your domain or Host's IP Address
    ```
