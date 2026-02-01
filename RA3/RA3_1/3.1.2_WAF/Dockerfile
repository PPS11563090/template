FROM pps11563090/pps:pr3.1.1
LABEL maintainer="aliiondra@alu.edu.gva.es"
LABEL description="RA3.1 Capa 2 - WAF ModSecurity - Fix Permisos"
RUN apt-get update && apt-get install -y libapache2-mod-security2 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
RUN cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf && \
    sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf
RUN mkdir -p /var/log/apache2 && \
    touch /var/log/apache2/modsec_audit.log && \
    chown -R www-data:www-data /var/log/apache2
RUN sed -i 's/^#LoadModule unique_id_module/LoadModule unique_id_module/' /usr/local/apache2/conf/httpd.conf && \
    echo "LoadModule security2_module /usr/lib/apache2/modules/mod_security2.so" >> /usr/local/apache2/conf/httpd.conf && \
    echo "Include /etc/modsecurity/modsecurity.conf" >> /usr/local/apache2/conf/httpd.conf
EXPOSE 80