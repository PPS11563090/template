# RA3.2.1 - Certificados SSL/TLS

## Descripción
Capa final de la arquitectura Apache. Implementación de cifrado SSL/TLS y forzado de HTTPS, cerrando el ciclo de securización.

## Medidas de seguridad
1.  **Cifrado:**
    * Generación automatizada de certificado digital autofirmado (RSA 2048 bits).
    * Configuración de `mod_ssl` en el puerto 443.
2.  **Redirección forzosa:**
    * Configuración de VirtualHost en puerto 80 para redirigir todo el tráfico a HTTPS.
3.  **Herencia completa:**
    * Esta imagen incluye todas las protecciones anteriores: Hardening Base, CSP, HSTS, WAF OWASP y Anti-DoS.

## Despliegue
**Imagen case:** `pps11563090/pps:pr3.1.4` (cascada)

```bash
docker build -t pps11563090/pps:pr3.2.1 .
docker run -d -p 80:80 -p 443:443 pps11563090/pps:pr3.2.1