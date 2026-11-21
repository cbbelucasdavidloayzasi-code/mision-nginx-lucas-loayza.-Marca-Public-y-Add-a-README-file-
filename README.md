# Misión: Servidor web con Nginx (Alpine + Docker)

**Materia:** Sistemas Operativos · **Docente:** Ing. Diego Cárdenas · **Universidad Franz Tamayo**
**Fecha de la práctica:** 21/11/2026

## 1. Integrantes y colaboración

| Nombre completo | Rol |
|---|---|
| Lucas David Loayza Silez | Responsable de la cuadrilla (cumple todos los roles; cuadrilla individual, pendiente de validación del docente) |

**Colaboración externa:** Juan Manuel Chacón Villarroel apoyó con: [COMPLETAR: describir con precisión qué hizo]. Él pertenece a otra cuadrilla y no figura como integrante de esta.

**Herramienta de IA:** se usó una sola conversación con Claude (Anthropic) como apoyo de consulta. Detalle y validación en [uso-de-ia.md](uso-de-ia.md).

## 2. Proyecto y objetivo

Proyecto n.º 2: servidor web con Nginx sobre Alpine Linux en Docker, publicando una plantilla ya construida (sin desarrollar un sitio desde cero).

**Objetivo:** publicar la plantilla en un contenedor `nginx:alpine` y comprobar su funcionamiento desde otro equipo de la red.

**Breve investigación**
- **Nginx:** servidor web y proxy inverso, ligero, que sirve archivos estáticos.
- **nginx:alpine:** imagen oficial basada en Alpine Linux, de tamaño reducido.
- **Volumen (bind mount):** la carpeta del anfitrión `C:\sitio\coffee-shop-free-html5-template` se monta en `/usr/share/nginx/html` como solo lectura (`:ro`), de modo que el contenedor no puede modificar el sitio.
- **Docker Desktop en Windows** ejecuta los contenedores sobre WSL 2 (el log de Nginx lo muestra: `Linux ...microsoft-standard-WSL2`).
- **Plantilla:** `coffee-shop-free-html5-template`, del repositorio `learning-zone/website-templates` (HTML/CSS estático, no requiere compilar).
- **Por qué este proyecto:** se eligió por ser el de implementación más corta (un solo contenedor, sin usuarios ni configuración compleja).

## 3. Estado inicial y requerimientos

- Equipo: PC con Windows (PowerShell 5.1), red Wi-Fi doméstica `TIGO-MANU`, IP `192.168.0.12`.
- Al inicio **no estaban instalados** Docker ni Git (`docker` y `git` no eran reconocidos en PowerShell).
- Requerimientos: Docker Desktop (WSL 2), Git, una plantilla web, un dispositivo externo en la misma red (celular Android) y una regla de firewall para el puerto 8080.

## 4. Instalación, configuración y puesta en marcha

1. Instalar Docker Desktop con `winget`; reiniciar y abrir Docker Desktop hasta ver "Engine running".
2. Verificar: `docker --version` (29.9.3) y `docker run hello-world`.
3. Instalar Git con `winget` y verificar con `git --version` (2.56.1).
4. Clonar las plantillas y confirmar que la elegida tiene `index.html` en su raíz.
5. Levantar Nginx (ver sección 5).
6. Abrir el puerto 8080 en el firewall de Windows (PowerShell como administrador) y pasar la red Wi-Fi a perfil Privado.
7. Probar localmente y desde un celular.

## 5. Comandos usados

```powershell
winget install -e --id Docker.DockerDesktop
winget install -e --id Git.Git --source winget
docker --version
docker run hello-world
git clone https://github.com/learning-zone/website-templates.git C:\sitio
dir C:\sitio\coffee-shop-free-html5-template

docker run -d --name web-nginx `
  -p 8080:80 `
  -v C:\sitio\coffee-shop-free-html5-template:/usr/share/nginx/html:ro `
  --restart unless-stopped `
  nginx:alpine

docker ps
docker exec web-nginx cat /etc/os-release
curl.exe -I http://localhost:8080
docker logs web-nginx

# PowerShell como administrador
New-NetFirewallRule -DisplayName "Nginx 8080" -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow
Set-NetConnectionProfile -InterfaceAlias "Wi-Fi" -NetworkCategory Private

# Verificación desde otro equipo
docker logs web-nginx --since 10m | findstr /i "android"
```

No se usaron contraseñas, tokens ni credenciales.

## 6. Pruebas y verificación

| Prueba | Resultado | Evidencia |
|---|---|---|
| `docker run hello-world` | Mensaje "Hello from Docker!" | `evidencias/04-hello-world.png` |
| `docker ps` | `web-nginx` Up, `nginx:alpine`, `0.0.0.0:8080->80/tcp` | `evidencias/08-docker-ps.png` |
| `/etc/os-release` | Alpine Linux v3.24 | `evidencias/09-os-alpine.png` |
| `curl.exe -I http://localhost:8080` | HTTP/1.1 200 OK (nginx/1.31.9) | `evidencias/10-curl-localhost.png` |
| `curl.exe -I http://192.168.0.12:8080` | 200 OK por la IP del Wi-Fi | `evidencias/10b-curl-ip-wifi.png` |
| Celular Android (Firefox), `http://192.168.0.12:8080` | Página cargada completa | `evidencias/15-sitio-desde-celular.png` |
| Logs de Nginx | Peticiones con User-Agent `Android 10; Mobile ... Firefox/160.0`, hora 16:45 UTC (12:45 local), todas con 200 | `evidencias/12b-logs-celular.png` |
| Reinicio del contenedor | [COMPLETAR tras ejecutar `docker restart web-nginx`] | `evidencias/16-restart.png` |

**Nota técnica:** en los logs la IP de origen aparece como `172.17.0.1` (gateway interno de Docker Desktop, que hace NAT), también para el celular. Por eso la evidencia de acceso externo es la captura del celular más el User-Agent Android en los logs, no la IP de origen.

## 7. Seguridad

- Volumen montado como **solo lectura** (`:ro`).
- Solo se expone el puerto 8080/TCP.
- La regla de firewall se creó con perfil `Any`. [COMPLETAR: si se restringe a Privado con `Set-NetFirewallRule -DisplayName "Nginx 8080" -Profile Private`, indicarlo aquí]. La red Wi-Fi se cambió de Pública a Privada.
- No se abrieron puertos del router a internet.
- No se subió información sensible al repositorio.

## 8. Bitácora, problemas y soluciones

Ver [bitacora.md](bitacora.md).

## 9. Uso de IA

Ver [uso-de-ia.md](uso-de-ia.md).

## 10. ActivityWatch, conclusiones y pendientes

- **ActivityWatch:** [COMPLETAR: adjuntar reporte en `activitywatch/` o indicar que no estuvo disponible].
- **Conclusiones:** [COMPLETAR con palabras propias; ejemplo: qué se aprendió sobre contenedores, volúmenes, puertos, firewall y perfiles de red].
- **Pendientes:** captura de la barra de direcciones del celular, prueba de reinicio, confirmación del docente sobre la cuadrilla individual.
