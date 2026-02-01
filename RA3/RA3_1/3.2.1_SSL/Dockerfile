FROM pps11563090/pps:pr3.1.4
LABEL maintainer="aliiondra@alu.edu.gva.es"
LABEL description="RA3.1 Capa 2 - SSL - Actividad 3.2.1"
RUN apt-get update && apt-get install -y openssl && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /usr/local/apache2/conf/server.key \
    -out /usr/local/apache2/conf/server.crt \
    -subj "/C=ES/ST=Castellon/L=Castellon/O=Caminas Web Projects/CN=www.midominioseguro.com"
RUN sed -i \
    -e 's/^#LoadModule ssl_module/LoadModule ssl_module/' \
    -e 's/^#LoadModule socache_shmcb_module/LoadModule socache_shmcb_module/' \
    -e 's/^#Include conf\/extra\/httpd-ssl.conf/Include conf\/extra\/httpd-ssl.conf/' \
    /usr/local/apache2/conf/httpd.conf
COPY default-ssl.conf /usr/local/apache2/conf/extra/httpd-ssl.conf
EXPOSE 80 443