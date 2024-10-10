FROM debian:bullseye

RUN apt update && apt upgrade -y && \
    apt install -y \
    inetutils-ping \
    nginx \
    openssl \
    curl

RUN mkdir -p var/www/html && \
    chown -R www-data:www-data /var/www/html && \
    chmod -R 755 /var/www/html

COPY conf/nginx.conf /etc/nginx/nginx.conf

# Generate SSL certificate
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/cert.key -out /etc/ssl/certs/cert.crt -subj "/C=FR/ST=LeHavre/L=LeHavre/O=42/OU=42/CN=ale-boud.42.fr"

# Redirect Nginx logs to stdout and stderr for Docker logs
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

CMD [ "nginx", "-g", "daemon off;" ]
