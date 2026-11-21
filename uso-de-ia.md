# Uso de IA

Se usó **una sola conversación** con Claude (Anthropic) como apoyo de consulta. La IA no ejecutó nada: todos los comandos fueron ejecutados por Lucas en su equipo, y los resultados se pegaron en la conversación para que la IA los interpretara. **[Adjuntar aquí el enlace o exportación de la conversación.]**

## Consultas relevantes, recomendaciones y validación

| Consulta | Recomendación de la IA | Validación del equipo |
|---|---|---|
| Qué proyecto se termina en menos de 1 hora | Nginx o File Browser; recomendó Nginx | El equipo eligió Nginx; falta confirmación del docente |
| `docker` no reconocido | Reiniciar, abrir Docker Desktop y verificar con `Test-Path` | `Test-Path` devolvió `True` y `docker --version` respondió 29.9.3 |
| Error `docker_engine` | Abrir Docker Desktop y esperar "Engine running" | `docker run hello-world` funcionó |
| Obtener una plantilla | Clonar `learning-zone/website-templates` (la IA no pudo verificar que siguiera disponible) | El clon funcionó (10.341 archivos); se comprobó `index.html` en la carpeta elegida |
| Plantilla concreta | La IA sugirió `coffee-shop-free-html5-template` | Lucas la aceptó tras ver la lista y comprobar que contiene `index.html` |
| Levantar Nginx | `docker run` con puerto 8080, volumen `:ro` y `nginx:alpine` | `docker ps`, `os-release` (Alpine) y `curl -I` (200 OK) |
| Acceso desde otro equipo | Abrir regla de firewall, pasar la red a Privada, probar desde celular | Regla creada como administrador; se probó desde un Android; los logs lo confirmaron |

## Errores o imprecisiones de la IA detectados

1. **IP en los logs:** la IA dijo que los logs mostrarían una IP `192.168.0.x` para el celular. Era incorrecto: Docker Desktop hace NAT y todo aparece como `172.17.0.1`. Se detectó al revisar los logs reales y se corrigió usando el User-Agent (Android) como evidencia.
2. **Marcador sin reemplazar:** los comandos de la IA incluían `NOMBRE-DE-LA-PLANTILLA`, que daba error hasta reemplazarlo por la carpeta real.
3. **Permisos:** la IA no advirtió que `New-NetFirewallRule` requiere PowerShell como administrador; el primer intento falló con "Acceso denegado".

## Decisiones propias del equipo
- Probar con un celular real en vez de aceptar solo `curl` local.
- Cambiar el perfil de red a Privado.
- [COMPLETAR: otras decisiones que Lucas haya tomado].

## Reflexión
[COMPLETAR con palabras propias: qué se aprendió y qué se contrastó con la documentación oficial de Docker/Nginx.]
