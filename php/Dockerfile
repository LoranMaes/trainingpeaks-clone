FROM php:8.3.15-fpm

# Install PHP extensions and dependencies
RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && echo "assert.warning=0" >> /usr/local/etc/php/php.ini

# Install Node.js and npm
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt install -y nodejs

WORKDIR /var/www/trainingpeaks

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Symfony CLI and move binary
RUN curl -sS https://get.symfony.com/cli/installer | bash \
    && mv $HOME/.symfony*/bin/symfony /usr/local/bin/symfony

RUN git config --global user.email "loran.maes@gmail.com" \
    && git config --global user.name "Loran Maes"