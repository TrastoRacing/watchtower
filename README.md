# Watchtower - Fork Actualizado con Configuración Avanzada

[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/nicholas-fedor/watchtower)

Una configuración Docker Compose optimizada para Watchtower usando el **fork activo** de [nicholas-fedor/watchtower](https://github.com/nicholas-fedor/watchtower), que mantiene desarrollo activo y correcciones de bugs del proyecto original abandonado.

## Características

- **Fork Actualizado**: Usa el fork de nicholas-fedor con desarrollo activo (v1.12.1+)
- **Programación Cron**: Actualizaciones automatizadas a las 00:05 diarias
- **Reinicio Escalonado**: Rolling restarts para minimizar downtime
- **Limpieza Automática**: Elimina imágenes antiguas tras actualizar
- **Logs Estructurados**: Formato JSON para mejor análisis
- **Seguridad Mejorada**: Configuraciones de seguridad optimizadas

## 📋 Prerrequisitos

- Docker Engine 20.10+
- Docker Compose v2.0+
- Acceso al socket de Docker

## 🛠️ Instalación Rápida

1. **Clona este repositorio**:
```
git clone https://github.com/tu-usuario/watchtower-compose.git
cd watchtower-compose
```


## Configuración

### Variables de Entorno Principales

| Variable | Valor | Descripción |
|----------|-------|-------------|
| `WATCHTOWER_SCHEDULE` | `0 5 0 * * *` | Cron para actualizaciones (00:05 diarios) |
| `WATCHTOWER_CLEANUP` | `true` | Limpia imágenes antiguas automáticamente |
| `WATCHTOWER_ROLLING_RESTART` | `true` | Reinicia contenedores de forma escalonada |
| `WATCHTOWER_LOG_FORMAT` | `json` | Formato de logs estructurados |

### Personalización del Schedule

Para cambiar la programación, modifica `WATCHTOWER_SCHEDULE`:
Cada 8 horas
WATCHTOWER_SCHEDULE=0 */8 * * *

Solo los domingos a las 02:00
WATCHTOWER_SCHEDULE=0 2 * * 0

Diario a las 03:30
WATCHTOWER_SCHEDULE=30 3 * * *


## Control Granular (Opcional)

### Usando Scope para Contenedores Específicos

1. **Activa el scope** en watchtower:
environment:

WATCHTOWER_SCOPE=mystack


2. **Etiqueta contenedores** a incluir:
services:
mi-app:
image: mi-imagen:latest
labels:
- "com.centurylinklabs.watchtower.scope=mystack"


3. **Excluye contenedores** críticos:
services:
database:
image: postgres:15
labels:
- "com.centurylinklabs.watchtower.enable=false"

## 🐛 Resolución de Problemas

### Error: "Cannot define both interval and schedule"
- **Causa**: Usar `WATCHTOWER_POLL_INTERVAL` y `WATCHTOWER_SCHEDULE` juntos
- **Solución**: Eliminar uno de los dos

### Error: "API token is empty or unset"
- **Causa**: Puerto expuesto sin token API
- **Solución**: Eliminar sección `ports:` o añadir `WATCHTOWER_HTTP_API_TOKEN`

## 🔗 Enlaces Útiles

- [Fork Watchtower (nicholas-fedor)](https://github.com/nicholas-fedor/watchtower)
- [Documentación Original](https://containrrr.dev/watchtower/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

## ⭐ ¿Te resulta útil?

Si este repositorio te ayuda, ¡dale una estrella! ⭐

---

**Nota**: Este fork mantiene compatibilidad completa con el Watchtower original pero añade características y correcciones importantes para entornos de producción.



