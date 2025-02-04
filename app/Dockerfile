FROM php:7.4-fpm

# Set working directory
WORKDIR /var/www/html

# Install dependencies
RUN apt-get update && apt-get install -y \
    apt-utils \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales mlocate \
    zip libzip-dev unzip libonig-dev \
    jpegoptim optipng pngquant gifsicle \
    vim git curl sqlite3 \
    zlib1g-dev libicu-dev g++

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-freetype=/usr/include/
RUN docker-php-ext-install gd mbstring zip exif pcntl mysqli pdo pdo_mysql intl

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
# RUN groupadd -g 1000 www-data
# RUN useradd -u 1000 -ms /bin/bash -g www-data www-data

# Copy existing application directory contents
# COPY . /var/www/html

# Copy existing application directory permissions
# COPY --chown=www-data:www-data . /var/www/html

# Change current user to www
# USER www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]