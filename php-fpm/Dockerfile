FROM php:7.3.6-fpm-alpine3.9

RUN apk add --no-cache openssl bash nodejs npm
RUN docker-php-ext-install pdo pdo_mysql bcmath 

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/html

ENTRYPOINT ["php-fpm"]
