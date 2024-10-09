# Use the official PHP image with FPM and Alpine
FROM php:8.2-fpm-alpine AS builder

# Install necessary packages and PHP extensions
RUN apk add --no-cache \
    libjpeg-turbo-dev \
    libpng-dev \
    freetype-dev \
    libzip-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd bcmath pcntl zip

# Set the working directory
WORKDIR /app

# Copy composer files
COPY composer.json composer.lock ./

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy the application code
COPY . .

# Install dependencies
RUN composer install --no-dev --no-scripts --no-interaction --optimize-autoloader


# Expose the port your app runs on
EXPOSE 7001

# Start PHP-FPM
CMD ["php-fpm"]
