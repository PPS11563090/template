# RA3.3.1 - Apache Hardening Base

## Descripción
Imagen base que establece los cimientos de seguridad del servidor Apache, aplicando las **Best Practices de Geekflare**. Esta imagen sirve como punto de partida para las siguientes capas.

## Medidas de seguridad
1.  **Minimización de información:**
    * `ServerTokens Prod`: oculta la versión detallada del servidor.
    * `ServerSignature Off`: elimina la firma de pie de página.
2.  **Reducción de superficie de ataque:**
    * Desactivación de módulos innecesarios: `autoindex`, `status`, `dav`, `info`.
    * `TraceEnable Off`: bloqueo del método TRACE para evitar ataques XST.
    * Restricción de métodos HTTP: solo se permiten `GET`, `POST` y `HEAD`.
3.  **Protección de directorios:**
    * `Options -Indexes`: bloqueo del listado de ficheros.
    * `Options -Includes`: desactivación de Server Side Includes.
4.  **Protocolos y rendimiento:**
    * Bloqueo estricto de **HTTP 1.0**.
    * Eliminación de la cabecera `ETag`.
    * Ajuste de `Timeout` a 60 segundos.

## Despliegue
```bash
docker build -t pps11563090/pps:pr3.3.1 .