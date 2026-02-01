FROM owasp/modsecurity-crs:nginx
LABEL maintainer="aliiondra@alu.edu.gva.es"
LABEL description="RA3.1 Capa 5 - Nginx - Actividad 3.1.5"
USER root
RUN apt-get update && apt-get install -y php-fpm openssl apache2-utils && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
RUN mkdir -p /etc/nginx/ssl /var/www/html/privado && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt \
    -subj "/C=ES/ST=Castellon/L=Castellon/O=IES/OU=Informatica/CN=localhost" && \
    htpasswd -bc /etc/nginx/.htpasswd admin admin
RUN sed -i 's|listen = /run/php/php.*-fpm.sock|listen = 127.0.0.1:9000|' /etc/php/*/fpm/pool.d/www.conf
COPY default.conf /etc/nginx/conf.d/default.conf
RUN rm -f /etc/nginx/templates/conf.d/default.conf.template
RUN echo "<?php phpinfo(); ?>" > /var/www/html/index.php
RUN echo '#!/bin/bash\nservice $(ls /etc/init.d/ | grep php) start\n/docker-entrypoint.sh nginx -g "daemon off;"' > /start.sh && \
    chmod +x /start.sh
EXPOSE 80 443
ENTRYPOINT ["/start.sh"]