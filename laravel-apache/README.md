# Docker Laravel Apache2

## Build & Run

```sh
# Build
docker build --no-cache -t demo/laravel:0.1 .

# Run laravel http://127.0.0.1:8000
docker run -p 8000:80 demo/laravel:0.1

# Check php extensions in php
docker run -it --rm php:8.2-fpm php -m
```
