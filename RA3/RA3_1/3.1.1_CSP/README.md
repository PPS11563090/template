# RA3.1.1 - Apache Hardening: CSP & HSTS

## Descripción
Implementación de cabeceras de seguridad HTTP sobre la imagen base endurecida.

## Medidas de seguridad
1.  **Content Security Policy (CSP):**
    * Configurado `default-src 'self'`.
    * Restringe la carga de recursos únicamente al propio origen, mitigando XSS y ataques de inyección de datos.
2.  **HTTP Strict Transport Security (HSTS):**
    * Configurado con `max-age=63072000; includeSubDomains`.
    * Fuerza a los navegadores a conectarse únicamente vía HTTPS en el futuro.

## Despliegue
**Imagen base:** `pps11563090/pps:pr3.3.1`

```bash
docker build -t pps11563090/pps:pr3.1.1 .
docker run -d -p 8081:80 pps11563090/pps:pr3.1.1