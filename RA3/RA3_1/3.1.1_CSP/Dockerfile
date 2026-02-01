FROM pps11563090/pps:pr3.3.1
LABEL maintainer="aliiondra@alu.edu.gva.es"
LABEL description="RA3.1 Capa 1 - CSP & HSTS - Actividad 3.1.1"
COPY csp.conf /usr/local/apache2/conf/extra/csp.conf
RUN echo "Include conf/extra/csp.conf" >> /usr/local/apache2/conf/httpd.conf
EXPOSE 80
