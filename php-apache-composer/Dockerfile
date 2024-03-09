# Custom Script -by Purwa Sabrang -c instagram.com/the.skinny.rat

ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

# Install Apache and required packages
RUN apk update && \
    apk add --no-cache apache2 apache2-proxy curl

# Configure Apache to use PHP-FPM
RUN echo "LoadModule proxy_module modules/mod_proxy.so" >> /etc/apache2/httpd.conf && \
    echo "LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so" >> /etc/apache2/httpd.conf && \
    echo "<FilesMatch \.php$>" >> /etc/apache2/httpd.conf && \
    echo "    SetHandler \"proxy:fcgi://127.0.0.1:9000\"" >> /etc/apache2/httpd.conf && \
    echo "</FilesMatch>" >> /etc/apache2/httpd.conf

ARG APK_PACKAGES
ARG PHP_EXTENSIONS
RUN if [ -n "$APK_PACKAGES" ]; then apk add $APK_PACKAGES; fi
RUN if [ -n "$PHP_EXTENSIONS" ]; then docker-php-ext-install $PHP_EXTENSIONS; fi
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy Apache configuration file
COPY ./apache/default.conf /etc/apache2/conf.d/default.conf

# Copy PHP configuration file
COPY ./php/php.ini /usr/local/etc/php/conf.d/php.ini

WORKDIR /var/www/html
COPY ./sites /var/www/html

# Start PHP-FPM and Apache
CMD php-fpm -D && httpd -D FOREGROUND