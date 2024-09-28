FROM php:fpm-alpine

RUN docker-php-ext-install opcache

COPY ./php/production/opcache.ini /usr/local/etc/php/conf.d/opcache.ini

COPY --chown=www-data:www-data ./data/ /var/www/html/

# Install system dependencies
RUN apk --no-cache add \
    build-base \
    libpng-dev \
    libjpeg-turbo-dev \
    libwebp-dev \
    libxpm-dev \
    freetype-dev \
    libzip-dev \
    zip \
    unzip \
    git \
    bash \
    fcgi \
    libmcrypt-dev \
    oniguruma-dev \
    postgresql-dev

# Clear cache
RUN rm -rf /var/cache/apk/*

# Install PHP extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp
RUN docker-php-ext-install gd pdo pdo_mysql pdo_pgsql mbstring zip exif pcntl bcmath opcache

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

RUN php artisan cache:clear
RUN php artisan config:clear
RUN php artisan migrate
RUN php artisan storage:link

# Change current user to www
USER www-data

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]