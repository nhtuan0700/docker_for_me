ARG PHP_VERSION

FROM php:${PHP_VERSION}-fpm
ARG APP_CODE_PATH_CONTAINER

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libonig-dev \
    libzip-dev \
    zip \
    unzip \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd mbstring zip pdo pdo_mysql

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR ${APP_CODE_PATH_CONTAINER}


# Set the entrypoint script (optional)
# COPY docker-entrypoint.sh /usr/local/bin/
# RUN chmod +x /usr/local/bin/docker-entrypoint.sh
# ENTRYPOINT ["docker-entrypoint.sh"]

# Expose port 9000 and start PHP-FPM server
EXPOSE 9000
CMD ["php-fpm"]
