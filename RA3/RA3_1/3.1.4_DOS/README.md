# RA3.1.4 - Protección DoS

## Descripción
Implementación de protección contra ataques de Denegación de Servicio (DoS) y fuerza bruta mediante el módulo **mod_evasive**.

## Medidas de seguridad
1.  **Instalación personalizada:**
    * Compilación manual del módulo para Apache 2.4 con parche para `client_ip`.
2.  **Umbrales de bloqueo:**
    * `DOSPageCount 2`: bloquea si se solicita la misma página más de 2 veces/segundo.
    * `DOSBlockingPeriod 10`: baneo temporal de 10 segundos a la IP atacante.
3.  **Logging:**
    * Directorio de logs configurado en `/var/log/mod_evasive` con permisos adecuados.

## Despliegue
**Imagen base:** `pps11563090/pps:pr3.1.3` (cascada)

```bash
docker build -t pps11563090/pps:pr3.1.4 .
docker run -d -p 8084:80 pps11563090/pps:pr3.1.4