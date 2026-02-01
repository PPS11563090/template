# RA3.1.3 - OWASP ModSecurity

## Descripción
Incorporación de OWASP al motor ModSecurity para dotar al WAF de inteligencia contra las vulnerabilidades web más críticas.

## Medidas de seguridad
1.  **Reglas CRS:**
    * Clonado del repositorio oficial `owasp-modsecurity-crs`.
    * Inclusión de todas las reglas base (`rules/*.conf`) para protección proactiva.
2.  **Configuración:**
    * Habilitación de `crs-setup.conf`.
3.  **Protección:**
    * Mitigación de ataques como SQL Injection, (XSS), Command Injection y Path Traversal.

## Despliegue
**Imagen base:** `pps11563090/pps:pr3.1.2` (cascada)

```bash
docker build -t pps11563090/pps:pr3.1.3 .
docker run -d -p 8083:80 pps11563090/pps:pr3.1.3