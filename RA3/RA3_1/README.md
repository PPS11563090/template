# 3.1.1 - Apache Hardening: CSP & HSTS

## Descripción
Implementación de cabeceras de seguridad siguiendo estrictamente el material docente de `psegarrac.github.io`.

## Justificación del Código
1. **CSP**: Se ha configurado `Content-Security-Policy: default-src 'self'` siguiendo el primer ejemplo del apartado "CSP" del material. Esto restringe la carga de recursos al propio origen.
2. **HSTS**: Se ha configurado `Strict-Transport-Security` con `max-age=63072000; includeSubDomains` tal como indica el apartado "HSTS" del material.

## Validación
Comando para verificar las cabeceras:
`curl -I http://localhost:8081`

Salida esperada:
- `Strict-Transport-Security: max-age=63072000...`
- `Content-Security-Policy: default-src 'self'`

# 3.1.2 - Web Application Firewall (WAF)

## Descripción
Implementación de un Firewall de Aplicación Web utilizando **ModSecurity** sobre la infraestructura previa.

## Justificación (Fuente: psegarrac.github.io)
1. **Instalación**: Se ha instalado `libapache2-mod-security2` siguiendo el manual.
2. **Activación**: Se ha modificado `modsecurity.conf` para establecer `SecRuleEngine On`, permitiendo que el firewall no solo detecte, sino que bloquee ataques.
3. **Dependencias**: Se ha habilitado `mod_unique_id` en Apache, requisito indispensable para el funcionamiento de ModSecurity.

## Validación
Para verificar que el módulo está activo, ejecutar:
`docker exec <nombre_contenedor> httpd -M | grep security`

## Despliegue
**Imagen Base (Cascada):** `pps11563090/pps:pr3.1.1`
**Pull:** `docker pull pps11563090/pps:pr3.1.2`

# 3.1.3 - Reglas OWASP ModSecurity

## Descripción
Esta capa a?ade el **Core Rule Set (CRS) de OWASP** a ModSecurity para proporcionar una protecci?n proactiva contra las vulnerabilidades web m?s cr?ticas.

## Justificación (Fuente: psegarrac.github.io)
1. **Reglas**: Se ha clonado el repositorio oficial de OWASP CRS tal como indica la pr?ctica.
2. **Configuración**: Se ha habilitado `crs-setup.conf` y se han incluido todas las reglas del directorio `rules/*.conf`.
3. **Protecci?n**: Esto permite al servidor detener ataques de Command Injection, SQLi y Path Traversal.

## Validación
Intentar un acceso de Path Traversal:
`curl "http://localhost:8083/index.html?exec=/../../"`
Debe devolver un **403 Forbidden**.

## Despliegue
**Imagen Base (Cascada):** `pps11563090/pps:pr3.1.2`
**Pull:** `docker pull pps11563090/pps:pr3.1.3`

# 3.1.4 - Protecci?n DoS (mod_evasive)

## Descripci?n
Implementaci?n de protecci?n contra ataques de Denegaci?n de Servicio (DoS) mediante el m?dulo **mod_evasive**.

## Justificaci?n (Fuente: psegarrac.github.io)
Se ha configurado el m?dulo para bloquear IPs que superen los umbrales de peticiones definidos:
1. `DOSPageCount 2`: Bloquea si se pide la misma p?gina m?s de 2 veces por segundo.
2. `DOSLogDir`: Se ha creado y configurado el directorio de logs con permisos para Apache.

## Validaci?n
Realizar m?ltiples peticiones r?pidas con `curl`. El servidor debe responder con **403 Forbidden** tras superar el umbral.

## Despliegue
**Imagen Base:** `pps11563090/pps:pr3.1.3`
**Pull:** `docker pull pps11563090/pps:pr3.1.4`

# RA3.1.5 - Práctica 5: Nginx y ModSecurity

## 📋 Descripción
En esta práctica extra hemos instalado **Nginx** replicando las configuraciones de seguridad realizadas previamente en Apache, incluyendo PHP, certificados SSL, protección de directorios y reglas WAF.

## 🛡️ Medidas de Seguridad Implementadas (Según enunciado)
1.  **WAF con Reglas OWASP:** Se utiliza la imagen base `owasp/modsecurity-crs:nginx` que ya incluye ModSecurity y el Core Rule Set (CRS) activados para bloquear ataques.
2.  **Cabeceras de Seguridad:**
    * `Strict-Transport-Security` (HSTS): Forzado por 1 año (`max-age=63072000`).
    * `Content-Security-Policy` (CSP): Configurado a `default-src 'self'`.
3.  **Servidor Seguro (HTTPS):**
    * Generación de certificado autofirmado con `openssl`.
    * Configuración del puerto 443 SSL.
4.  **Protección de Directorios:**
    * Ruta `/privado` protegida mediante autenticación básica (`auth_basic`).
5.  **PHP:**
    * Instalación de PHP-FPM y creación de `index.php` con `phpinfo()`.

## 🚀 Despliegue
```bash
docker build -t pps11563090/pps:pr3.1.5_extra .
docker run -d --name test-nginx -p 8086:80 -p 8443:443 pps11563090/pps:pr3.1.5_extra
```

# RA3.2 - Implementación de Certificados SSL/TLS en Apache

## 📋 Descripción
Esta práctica (3.2.1) consiste en la securización de un servidor web Apache mediante la implementación de un **Certificado Digital Auto-firmado**. 
El objetivo es cifrar la comunicación entre el cliente y el servidor utilizando el protocolo HTTPS (puerto 443) y forzar la redirección desde el protocolo inseguro HTTP (puerto 80).

Esta imagen Docker automatiza los pasos de la guía de la asignatura, generando las claves y configurando el Virtual Host automáticamente al construir la imagen.

---

## 🛠️ Archivos del Proyecto
* **Dockerfile**: Automatiza la activación de `mod_ssl`, la generación del certificado con `openssl` y la configuración del sitio.
* **default-ssl.conf**: Configuración del Virtual Host para el puerto 443 y redirección 301 (Permanent) del puerto 80.

## 🚀 Despliegue

### 1. Construcción de la Imagen
```bash
docker build -t pps11563090/pps:pr3.2.1 .

# 3.3.1 Apache Hardening Base

## Descripción
Imagen base con hardening aplicado siguiendo las Best Practices de Geekflare.

## Justificación Técnica
- **ServerTokens Prod**: Oculta la versión del servidor en las cabeceras.
- **ServerSignature Off**: Oculta la firma en páginas de error.
- **Options -Indexes**: Desactiva el listado de directorios si no hay index.html.
- **Timeout 60**: Mitigación básica contra ataques DoS lentos.

## Validación
Comando: `curl -I http://localhost:80`
Resultado: La cabecera `Server` debe mostrar solo `Apache` (sin números de versión).

## Uso
**Pull:** `docker pull pps11563090/pps:pr3.3.1`
