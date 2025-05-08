FROM php:8.2-fpm

# Install sistem dependencies dan ekstensi PHP
RUN apt-get update && apt-get install -y \
    git curl unzip libzip-dev libicu-dev libonig-dev libpq-dev libxml2-dev tzdata \
    && docker-php-ext-install intl zip pdo_pgsql mbstring xml bcmath pcntl \
    && docker-php-ext-enable pdo_pgsql \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Composer
COPY --from=composer:2.7 /usr/bin/composer /usr/bin/composer

# Set working directory ke Laravel project
WORKDIR /var/www

# Set permissions untuk Laravel
RUN mkdir -p /var/www/storage /var/www/bootstrap/cache \
    && chown -R www-data:www-data /var/www \
    && chmod -R 775 /var/www/storage /var/www/bootstrap/cache

# Gunakan user www-data (opsional, lebih aman untuk prod)
USER www-data

EXPOSE 9000
CMD ["php-fpm"]
