FROM --platform=linux/amd64 php:8.0.22-fpm-alpine

ARG APCU_VERSION=5.1.21

RUN apk add unzip zlib-dev libzip-dev autoconf g++ make

RUN printf "\n" | pecl install apcu-${APCU_VERSION} \
    && docker-php-ext-enable apcu

RUN docker-php-ext-install zip

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1

WORKDIR /var/www

ENTRYPOINT ["sh", "tests/docker/php/entrypoint.sh"]
CMD ["sleep", "infinity"]