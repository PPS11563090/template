# RA3.1.5 - Práctica 5: Nginx y ModSecurity

## Descripción
Práctica adicional independiente donde se replica la arquitectura de seguridad en un servidor **Nginx**, sustituyendo a Apache.

## Medidas de seguridad
1.  **WAF con reglas OWASP:**
    * Uso de imagen base `owasp/modsecurity-crs:nginx`.
    * ModSecurity activo en modo bloqueo.
2.  **Cabeceras de seguridad:**
    * `Strict-Transport-Security` (HSTS).
    * `Content-Security-Policy` (CSP): `default-src 'self'`.
3.  **Servidor seguro (HTTPS):**
    * Certificado autofirmado generado con `openssl`.
    * Servidor escuchando en puerto 443 SSL.
4.  **Control de acceso:**
    * Protección del directorio `/privado` mediante autenticación básica.
    * Soporte PHP-FPM configurado y securizado.

## Despliegue
```bash
docker build -t pps11563090/pps:pr3.1.5_extra .
docker run -d -p 8086:80 -p 8443:443 pps11563090/pps:pr3.1.5_extra