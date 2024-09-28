FROM php:fpm-alpine

COPY --chown=www-data:www-data ./data/ /var/www/html/

# Clear cache
RUN rm -rf /var/cache/apk/*

# # Install system dependencies
# RUN apk --no-cache add \
#     build-base \
#     libpng-dev \
#     libjpeg-turbo-dev \
#     libwebp-dev \
#     libxpm-dev \
#     freetype-dev \
#     libzip-dev \
#     zip \
#     unzip \
#     bash \
#     fcgi \
#     oniguruma-dev \
#     postgresql-dev
#     # git \
#     # libmcrypt-dev \

# # Install PHP extensions
# RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp
# RUN docker-php-ext-install gd pdo pdo_mysql pdo_pgsql mbstring zip exif pcntl bcmath opcache

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

# Change current user to www
USER www-data

RUN php artisan cache:clear
RUN php artisan config:clear
RUN php artisan migrate
RUN php artisan storage:link

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]

# BUILD 1

# # Install dependencies
# RUN apk --no-cache --update add \
#     git \
#     libxml2-dev \
#     sqlite-dev \
#     curl-dev \
#     libzip-dev \
#     libpng-dev \
#     libjpeg-turbo-dev \
# 	libwebp-dev \
#     freetype-dev && \
#     rm -rf /tmp/* && \
#     rm -rf /var/cache/apk/*

# # Installing PHP
# RUN apk add --no-cache php-fpm \
#     php-pdo \
#     php-opcache \
#     php-gd \
#     php-zip \
#     php-phar \
#     php-iconv \
#     php-cli \
#     php-curl \
#     php-openssl \
#     php-mbstring \
#     php-tokenizer \
#     php-fileinfo \
#     php-json \
#     php-xml \
#     php-xmlwriter \
#     php-simplexml \
#     php-dom \
#     php-pdo_mysql \
#     php-pdo_sqlite \
#     php-tokenizer \
#     php-pecl-redis

# RUN docker-php-ext-install bcmath pdo_mysql pcntl zip
# RUN docker-php-ext-configure gd --with-jpeg --with-freetype --with-webp
# RUN docker-php-ext-install gd

# Php apache
# RUN apk add --no-cache php php-common

# BUILD 2

# # Install gd, iconv, mbstring, mysql, soap, sockets, zip, and zlib extensions
# # see example at https://hub.docker.com/_/php/
# RUN apk add --update \
# 		$PHPIZE_DEPS \
# 		freetype-dev \
# 		git \
# 		libjpeg-turbo-dev \
# 		libpng-dev \
# 		libwebp-dev \
# 		libxml2-dev \
# 		libzip-dev \
# 		openssh-client \        
#         php-fpm \
#         php-session \
#         php-xml \
#         php-xmlwriter \
#         php-simplexml \
# 		php-json \
# 		php-openssl \
# 		php-pdo \
# 		php-pdo_mysql \
# 		php-pgsql \
# 		php-pdo_pgsql \
#         php-xdebug \
#         php-session \
#         php-zlib \
#         php-phar \
#         php-fileinfo \
#         php-tokenizer \		
# 		imagemagick \
# 		imagemagick-libs \
# 		imagemagick-dev \
# 		php-imagick \
# 		php-pcntl \		
# 		php-zip \
# 		php-opcache \
# 		sqlite \        
#         php-redis \        
#     && docker-php-ext-install xml bcmath pdo_mysql pcntl \
# 	&& docker-php-ext-configure gd --with-jpeg --with-freetype --with-webp \
# 	&& docker-php-ext-install gd \
# 	&& docker-php-ext-install zip

# # Install intl extension
# RUN apk add --no-cache \
#     icu-dev \
#     && docker-php-ext-install -j$(nproc) intl \
#     && docker-php-ext-enable intl \
#     && rm -rf /tmp/*

# # Install mbstring extension
# RUN apk add --no-cache \
# oniguruma-dev \
# && docker-php-ext-install mbstring \
# && docker-php-ext-enable mbstring \
# && rm -rf /tmp/*

# # Setup bzip2 extension
# RUN apk add --no-cache \
#     bzip2-dev \
#     && docker-php-ext-install -j$(nproc) bz2 \
#     && docker-php-ext-enable bz2 \
#     && rm -rf /tmp/*

# # Install opcache, xdebug, redis, mongodb
# RUN docker-php-source extract \
#     && pecl install opcache redis mongodb apcu \    
#     && docker-php-ext-enable opcache redis mongodb apcu \
#     && docker-php-source delete \
#     && rm -rf /tmp/*

# RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
# 	&& php composer-setup.php \
# 	&& php -r "unlink('composer-setup.php');" \
# 	&& mv composer.phar /usr/bin/composer

# # Composer
# COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# WORKDIR /var/www/html

# RUN php artisan cache:clear
# RUN php artisan config:clear
# RUN php artisan migrate
# RUN php artisan storage:link

# Errors
# RUN printf "\n" | pecl install \
#     imagick && \
#     docker-php-ext-enable --ini-name 20-imagick.ini imagick

# RUN printf "\n" | pecl install \
#     pcov && \
#     docker-php-ext-enable pcov