# # Use official PHP image with Apache
# FROM php:8.2-apache

# # Set working directory
# WORKDIR /var/www/html

# # Install system dependencies
# RUN apt-get update && apt-get install -y \
#     git \
#     curl \
#     zip \
#     unzip \
#     libzip-dev \
#     libpng-dev \
#     libonig-dev \
#     libxml2-dev \
#     libmcrypt-dev \
#     libpq-dev \
#     && docker-php-ext-install pdo pdo_mysql zip mbstring exif pcntl bcmath gd

# # Enable Apache mod_rewrite
# RUN a2enmod rewrite

# # Install Composer globally
# COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

# # Copy existing application directory contents
# COPY . /var/www/html

# # Set permissions for Laravel
# RUN chown -R www-data:www-data /var/www/html \
#     && chmod -R 755 /var/www/html/storage

# # Expose port 80
# EXPOSE 80

# # Start Apache in foreground
# CMD ["apache2-foreground"]
# Use the official PHP image with Apache
FROM php:8.2-apache

# Set working directory
WORKDIR /var/www/html

# Install required system packages and PHP extensions
RUN apt-get update && apt-get install -y \
    zip unzip git curl libpng-dev libjpeg-dev libfreetype6-dev \
    libonig-dev libxml2-dev libzip-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql mbstring zip exif pcntl gd bcmath

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Copy custom Apache configuration (see below)
COPY apache.conf /etc/apache2/sites-available/000-default.conf

# Install Composer
COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

# Copy application code
COPY . /var/www/html

# Set file and folder permissions
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html \
    && chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache

# Expose port 80
EXPOSE 80

# Start Apache
CMD ["apache2-foreground"]

