FROM wordpress:latest

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN { \
    echo 'ServerTokens Prod'; \
    echo 'ServerSignature Off'; \
} >> /etc/apache2/conf-available/security.conf && \
    a2enconf security

RUN chown -R www-data:www-data /var/www/html && \
    chmod -R 755 /var/www/html