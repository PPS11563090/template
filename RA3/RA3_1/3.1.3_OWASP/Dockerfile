FROM pps11563090/pps:pr3.1.2
LABEL maintainer="aliiondra@alu.edu.gva.es"
LABEL description="RA3.1 Capa 3 - OWASP CRS - Actividad 3.1.3"
RUN apt-get update && apt-get install -y git && \
    git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git /usr/local/apache2/conf/owasp-crs && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
RUN cp /usr/local/apache2/conf/owasp-crs/crs-setup.conf.example /usr/local/apache2/conf/owasp-crs/crs-setup.conf
RUN echo "Include /usr/local/apache2/conf/owasp-crs/crs-setup.conf" >> /usr/local/apache2/conf/httpd.conf && \
    echo "Include /usr/local/apache2/conf/owasp-crs/rules/*.conf" >> /usr/local/apache2/conf/httpd.conf
EXPOSE 80