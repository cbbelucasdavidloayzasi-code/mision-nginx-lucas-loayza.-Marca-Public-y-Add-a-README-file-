# Bitácora de actividades

**Fecha:** 21/11/2026 · **Responsable:** Lucas David Loayza Silez
Las horas están en hora local (Bolivia, UTC-4) salvo que se indique. Las horas marcadas con [~] son aproximadas: completar con las reales.

| Hora | Actividad | Resultado / problema | Solución |
|---|---|---|---|
| [~] | Elección del proyecto | Se eligió Nginx por ser el de implementación más corta | — |
| [~] | `docker --version` | Error: `docker` no reconocido | Se instaló Docker Desktop con `winget` |
| [~] | `Test-Path ...docker.exe` | `True`: sí estaba instalado | Faltaba reiniciar y abrir Docker Desktop |
| [~] | `docker --version` tras reiniciar | Versión 29.9.3 | — |
| [~] | `docker run hello-world` | Error `docker_engine`: el motor no estaba corriendo | Se abrió Docker Desktop y se esperó "Engine running" |
| [~] | `docker run hello-world` | "Hello from Docker!" | — |
| [~] | `git --version` | Error: `git` no reconocido | Se instaló con `winget`; versión 2.56.1 |
| 12:25 | `git clone` de las plantillas | 186 MB, 10.341 archivos | — |
| [~] | Elección de la plantilla | `coffee-shop-free-html5-template`, con `index.html` en la raíz | — |
| 12:32 | `docker run` de `nginx:alpine` | Contenedor `web-nginx` creado (16:32 UTC en los logs) | — |
| 12:34 | `docker ps`, `os-release`, `curl -I` | Up en 8080; Alpine v3.24; 200 OK | — |
| [~] | `New-NetFirewallRule` | Error "Acceso denegado" | Se repitió en PowerShell como administrador; regla creada |
| [~] | `Get-NetConnectionProfile` | Red `TIGO-MANU` en perfil Público | Se cambió a Privado con `Set-NetConnectionProfile` |
| 12:42 | `curl -I http://192.168.0.12:8080` | 200 OK por la IP del Wi-Fi | — |
| 12:45 | Prueba desde celular Android | Página cargada completa; logs con User-Agent Android | — |
| [~] | Reinicio del contenedor | [COMPLETAR] | [COMPLETAR] |

## Observaciones
- El 404 de `/favicon.ico` en los logs es normal: la plantilla no incluye ese archivo.
- En los logs la IP de origen sale como `172.17.0.1` por el NAT de Docker Desktop, incluso para el celular.
- La primera captura del celular no mostraba la barra de direcciones; [COMPLETAR: se repitió / se dejó como evidencia complementaria].

## Colaboración
- Juan Manuel Chacón Villarroel (otra cuadrilla): [COMPLETAR: fecha, hora y qué hizo; por ejemplo, quién tomó la captura del celular].
