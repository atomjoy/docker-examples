# Docker

Docker examples

## Docker compose build

```sh
docker compose build --no-cache && docker compose up --force-recreate -d

docker compose -f docker-compose-prod.yml up -d --build
```

## Docker laravel-apache build

```sh
# Build dockerfile
docker build --no-cache -t demo/laravel:0.1 .

# Run docker service
docker run -p 8000:80 demo/laravel:0.1

# Run php cmd
docker run -it --rm php:8.2-fpm php -m
```

## Cmd

```sh
# Clear docker images C:\<username>\AppData\Local\Docker\wsl
docker system prune
docker container prune
rm ~/.docker/config.json
sudo rm -rf ~/.docker/buildx

# Up
docker compose up
docker compose up -d

# Up force
docker compose up --force-recreate
docker compose up --force-recreate -d
docker compose up --build -d

# Build & Run
docker compose build --no-cache && docker compose up --force-recreate -d

# Show
docker ps
docker compose ps

# Down refresh
docker compose down -v
docker compose up --build -d

# Run terminal in container
docker compose ps
docker exec -it web_host bash
docker exec -it {service_name_here} sh
tail -f /var/log/nginx/*

# Run in container
docker exec php php artisan migrate:fresh

# Storage volume
docker volume create logs

# Network
docker network create -d bridge my-net

# If a service can run without privileges, use USER to change to a non-root user. 
# USER Start by creating the user and group in the Dockerfile with something like the following example:
RUN groupadd -r postgres && useradd --no-log-init -r -g postgres postgres

# Create user
RUN usermod -u 1000 postgres

# Change user
USER postgres

# The host has a changing IP address, or none if you have no network access. 
# We recommend that you connect to the special DNS name host.docker.internal, 
# which resolves to the internal IP address used by the host.
host.docker.internal
```

## Php fpm

```sh
# /etc/php/8.2/fpm/pool.d/www.conf
# /run/php/php8.2-fpm.sock
```

## Php cli

```sh
FROM php:8.3-cli
COPY . /usr/src/myapp
WORKDIR /usr/src/myapp
CMD [ "php", "./your-script.php" ]
```
