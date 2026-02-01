FROM httpd:2.4
LABEL maintainer="aliiondra@alu.edu.gva.es"
LABEL description="RA3.1 Base Hardened Apache - Actividad 3.3.1"
RUN apt-get update && apt-get upgrade -y && rm -rf /var/lib/apt/lists/*
COPY hardening.conf /usr/local/apache2/conf/extra/hardening.conf
RUN echo "Include conf/extra/hardening.conf" >> /usr/local/apache2/conf/httpd.conf
RUN sed -i 's/^#LoadModule rewrite_module/LoadModule rewrite_module/' /usr/local/apache2/conf/httpd.conf
RUN sed -i \
    -e 's/^LoadModule autoindex_module/#LoadModule autoindex_module/' \
    -e 's/^LoadModule status_module/#LoadModule status_module/' \
    -e 's/^LoadModule info_module/#LoadModule info_module/' \
    -e 's/^LoadModule dav_module/#LoadModule dav_module/' \
    -e 's/^LoadModule dav_fs_module/#LoadModule dav_fs_module/' \
    /usr/local/apache2/conf/httpd.conf
EXPOSE 80