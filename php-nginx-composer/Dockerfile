# Custom Script -by Purwa Sabrang -c instagram.com/the.skinny.rat

ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

ARG APK_PACKAGES
ARG PHP_EXTENSIONS
RUN apk update && \
    apk add --no-cache nginx curl && \
    mkdir -p /run/nginx
RUN if [ -n "$APK_PACKAGES" ]; then apk add $APK_PACKAGES; fi
RUN if [ -n "$PHP_EXTENSIONS" ]; then docker-php-ext-install $PHP_EXTENSIONS; fi
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY ./nginx/default.conf /etc/nginx/http.d/default.conf
COPY ./php/php.ini /usr/local/etc/php/conf.d/php.ini
WORKDIR /var/www/html
COPY ./sites /var/www/html

CMD php-fpm -D && nginx -g 'daemon off;'