FROM pps11563090/pps:pr3.1.3
LABEL maintainer="aliiondra@alu.edu.gva.es"
LABEL description="RA3.1 Capa 4 - mod_evasive Apache 2.4 Fix"
RUN apt-get update && apt-get install -y wget gcc make apache2-dev --no-install-recommends && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
RUN wget https://github.com/shivaas/mod_evasive/archive/master.tar.gz && \
    tar -zxvf master.tar.gz && \
    cd mod_evasive-master && \
    sed -i 's/remote_ip/client_ip/g' mod_evasive24.c && \
    apxs -i -a -c mod_evasive24.c
RUN mkdir -p /var/log/mod_evasive && \
    chown -R www-data:www-data /var/log/mod_evasive && \
    chmod 777 /var/log/mod_evasive
RUN echo '<IfModule mod_evasive24.c>\n\
    DOSHashTableSize    3097\n\
    DOSPageCount        2\n\
    DOSSiteCount        50\n\
    DOSPageInterval     1\n\
    DOSSiteInterval     1\n\
    DOSBlockingPeriod   10\n\
    DOSLogDir           "/var/log/mod_evasive"\n\
</IfModule>' >> /usr/local/apache2/conf/httpd.conf
EXPOSE 80