FROM php:8-apache

# Repositories
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -

# Packages
RUN apt-get update && apt-get install -y nodejs git libzip-dev zip

# PHP extensions
# List from https://laravel.com/docs/8.x/deployment#server-requirements
RUN docker-php-ext-install bcmath ctype fileinfo json mbstring openssl pdo pdo_mysql tokenizer xml
# Extra extensions
RUN docker-php-ext-install zip

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Apache webhost config
COPY conf/000-default.conf /etc/apache2/sites-available/000-default.conf

# Apache extensions
RUN a2enmod rewrite
RUN a2enmod remoteip

WORKDIR /var/www

CMD ["apache2-foreground"]
