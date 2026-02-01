# RA3.1.2 - Web Application Firewall (WAF)

## Descripción
Implementación del motor de Firewall de Aplicación Web **ModSecurity** sobre la infraestructura previa.

## Medidas de seguridad
1.  **Instalación**
    * Instalación de `libapache2-mod-security2` y sus dependencias (`mod_unique_id`).
2.  **Configuración activa:**
    * Renombrado de `modsecurity.conf-recommended`.
    * Cambio de directiva a `SecRuleEngine On` para pasar de modo "detección" a modo "prevención" (bloqueo activo).
3.  **Gestión de logs:**
    * Creación y asignación de permisos correctos para los logs de auditoría en `/var/log/apache2/`.

## Despliegue
**Imagen base:** `pps11563090/pps:pr3.1.1` (cascada)

```bash
docker build -t pps11563090/pps:pr3.1.2 .
docker run -d -p 8082:80 pps11563090/pps:pr3.1.2