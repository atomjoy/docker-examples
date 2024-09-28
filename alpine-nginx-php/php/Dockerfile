FROM php:fpm-alpine
RUN docker-php-ext-install opcache
COPY php/production/opcache.ini /usr/local/etc/php/conf.d/opcache.ini
COPY ./data/ /var/www/html/

FROM php:fpm-alpine
COPY ./data/ /var/www/html/

# Install gd, iconv, mbstring, mysql, soap, sockets, zip, and zlib extensions
# see example at https://hub.docker.com/_/php/
RUN apk add --update \
		$PHPIZE_DEPS \
		freetype-dev \
		git \
		libjpeg-turbo-dev \
		libpng-dev \
		libwebp-dev \
		libxml2-dev \
		libzip-dev \
		openssh-client \
		php-json \
		php-openssl \
		php-pdo \
		php-pdo_mysql \
		php-session \
		php-simplexml \
		php-tokenizer \
		php-xml \
		imagemagick \
		imagemagick-libs \
		imagemagick-dev \
		php-imagick \
		php-pcntl \
		php-zip \
		sqlite \
	&& docker-php-ext-install bcmath pdo_mysql pcntl \
	&& docker-php-ext-configure gd --with-jpeg --with-freetype --with-webp \
	&& docker-php-ext-install gd \
	&& docker-php-ext-install zip

RUN printf "\n" | pecl install \
		imagick && \
		docker-php-ext-enable --ini-name 20-imagick.ini imagick

RUN printf "\n" | pecl install \
		pcov && \
		docker-php-ext-enable pcov

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	&& php composer-setup.php \
	&& php -r "unlink('composer-setup.php');" \
	&& mv composer.phar /usr/bin/composer

WORKDIR /var/www/html

RUN php artisan cache:clear
RUN php artisan config:clear
RUN php artisan migrate
RUN php artisan storage:link