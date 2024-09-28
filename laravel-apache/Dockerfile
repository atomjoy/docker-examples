# docker build --no-cache -t demo/laravel:0.1 .
# docker run -p 8000:80 demo/laravel:0.1
# docker run -it --rm php:8.2-fpm php -m

# Stage 1
FROM php:8.2-apache-bookworm AS apache_stage

# Install
RUN apt-get update -y
RUN apt-get install -y curl libpng-dev libzip-dev zip
RUN rm -rf /var/lib/apt/lists/*

# Install php ext
RUN docker-php-ext-install pdo pdo_mysql zip

# Enable mod_rewrite
RUN a2enmod rewrite

# Envs
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public

# Configure vhost
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/conf-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf

# Copy from context to container
COPY --chown=www-data --chmod=2775 ./webapp /var/www/html

# Set working directory
WORKDIR /var/www/html

# Install composer
COPY --from=composer:2.7 /usr/bin/composer /usr/bin/composer

# Install
RUN composer install

# Laravel Update
RUN php artisan config:clear
RUN php artisan cache:clear
RUN php artisan migrate
RUN php artisan storage:link

# Set permissions
RUN chown -R www-data:www-data /var/www/html/bootstrap
RUN chown -R www-data:www-data /var/www/html/storage
RUN chown -R www-data:www-data /var/www/html/public
RUN chmod -R 2775 /var/www/html/bootstrap
RUN chmod -R 2775 /var/www/html/storage
RUN chmod -R 2775 /var/www/html/public