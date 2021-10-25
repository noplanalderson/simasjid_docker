![Docker Automated build](https://badges.weareopensource.me:/docker/automated/noplanalderson/simasjid_docker?color=blue&label=SIMASJID%20DOCKER&style=for-the-badge)(https://hub.docker.com/r/noplanalderson/simasjid_docker) [![](https://badges.weareopensource.me:/docker/pulls/noplanalderson/simasjid_docker?style=for-the-badge)](https://hub.docker.com/r/noplanalderson/simasjid_docker) [![](https://badges.weareopensource.me:/docker/image-size/noplanalderson/simasjid_docker?style=for-the-badge)](https://hub.docker.com/r/noplanalderson/simasjid_docker) [![nginx 1.19.10](https://img.shields.io/badge/nginx-1.19.10-brightgreen.svg?&logo=nginx&logoColor=white&style=for-the-badge)](https://nginx.org/en/CHANGES) [![php 8.0.5](https://img.shields.io/badge/php--fpm-8.0.5-blue.svg?&logo=php&logoColor=white&style=for-the-badge)](https://secure.php.net/releases/8_0_5.php)

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
$ sudo docker run -d noplanalderson/simasjid_docker:latest
```

Default web root:
```
/usr/share/nginx/html/simasjid
```
