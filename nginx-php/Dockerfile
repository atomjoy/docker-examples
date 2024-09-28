FROM nginx:1.27-bookworm AS web_server

# Apt https
RUN apt-get install apt-transport-https -y
RUN apt-get update -y

# Laravel 11 php 8.2
RUN apt-get install -y php-fpm php-pdo php-mysql php-sqlite3 php-sockets
# RUN apt-get install -y openssl php-cli php-common php-curl php-json php-bcmath php-xml php-mbstring php-intl php-tokenizer php-zip php-gd 

COPY --chown=www-data:www-data --chmod=2775 ./webapp /var/www/html

COPY ./nginx/sock/default.conf /etc/nginx/conf.d/default.conf

COPY ./php/sock/www.conf /etc/php/8.2/fpm/pool.d/www.conf

RUN usermod -aG www-data nginx

RUN touch /run/php/php8.2-fpm.sock
RUN chown -R www-data:www-data /run/php
RUN chmod 660 /run/php/php8.2-fpm.sock

RUN nginx -t

RUN service php8.2-fpm restart

RUN service nginx restart

# WORKDIR /var/www/html/public

# USER www-data
# EXPOSE 8000
