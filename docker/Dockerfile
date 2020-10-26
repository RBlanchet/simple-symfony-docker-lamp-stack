FROM library/php:7.3.20-apache

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN apt-get update \
    && apt-get install -y \
        git \
    \
    && install-php-extensions \
        intl \
        zip \
        xml \
        pdo_mysql \
        pdo_sqlite \
        mysqli \
        tokenizer \
        json \
        mbstring \
    \
    && curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && apt-get update \
    && apt-get install -y nodejs \
    && npm install -g yarn \
    \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-source delete

RUN curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer && /usr/bin/composer self-update

RUN a2enmod rewrite headers

WORKDIR /var/www/html