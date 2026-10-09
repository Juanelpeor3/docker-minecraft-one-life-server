<div align="center">

# Minecraft One Life Server

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Shell Script](https://img.shields.io/badge/Shell_Script-121011?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Minecraft](https://img.shields.io/badge/Minecraft-62B47A?style=for-the-badge&logoColor=white)
<br />
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat)](LICENSE)

**Español** | [English](README.md)

</div>

Servidor de Minecraft **"One Life"** dockerizado. Si **cualquier jugador muere**, el mundo se resetea al instante con una nueva seed gracias a [WorldReset](https://modrinth.com/plugin/worldreset), sin necesidad de reiniciar el servidor.

## Como funciona

1. El servidor corre en modo **Hardcore** con regeneracion natural desactivada en los tres mundos (overworld, nether, end).
2. **WorldReset** detecta la muerte de un jugador y genera un mundo nuevo con una seed aleatoria al instante.
3. Un **entrypoint wrapper** re-aplica automaticamente los gamerules y el scoreboard cada vez que WorldReset genera un mundo nuevo.
4. En el **Tab** se muestran los corazones de cada jugador conectado.

> [!NOTE]
> Este repositorio ha sido probado y funciona en Minecraft **26.2** y **26.3**. Futuras actualizaciones de Minecraft pueden cambiar nombres de gamerules, compatibilidad de plugins o el comportamiento del servidor, lo que podria romper este setup. Si tienes problemas en una version mas nueva, establece `VERSION=26.3` en tu archivo `.env`.

> [!IMPORTANT]
> Al establecer `EULA=TRUE` en tu archivo `.env`, estas aceptando el [Acuerdo de Licencia de Usuario Final de Minecraft](https://www.minecraft.net/es-es/eula).

> [!NOTE]
> Este proyecto no esta afiliado, mantenido, autorizado ni respaldado por Mojang Studios, Microsoft, ni ninguna de sus filiales o subsidiarias.



## Requisitos

- [Docker](https://docs.docker.com/get-docker/) & Docker Compose

## Instalacion

```bash
git clone https://github.com/Juanelpeor3/mc-one-life-server.git
cd mc-one-life-server

# Copia el ejemplo y edita tus valores
cp .env.example .env
```

## Configuracion

Edita el archivo `.env` con tus valores:

| Variable              | Descripcion                              | Default  |
|-----------------------|------------------------------------------|----------|
| `VERSION`             | Version de Minecraft                     | `26.2`   |
| `RCON_PASSWORD`       | Contraseña RCON (requerida)              | -        |
| `WHITELIST`           | Jugadores permitidos, separados por coma | -        |
| `OPS`                 | Administradores del servidor             | -        |
| `VIEW_DISTANCE`       | Distancia de render en chunks            | `16`     |
| `SIMULATION_DISTANCE` | Distancia de simulacion en chunks        | `10`     |
| `INIT_MEMORY`         | Memoria inicial JVM                      | `4G`     |
| `MAX_MEMORY`          | Memoria maxima JVM                       | `6G`     |

## Uso

```bash
# Arrancar el servidor
docker compose up -d

# Ver logs en tiempo real
docker compose logs -f

# Detener el servidor
docker compose down
```

## Plugin WorldReset

Para comandos, configuracion y documentacion completa, visita la pagina del plugin:

https://modrinth.com/plugin/worldreset

## Estructura del proyecto

```
.
├── Dockerfile                 # Imagen basada en itzg/minecraft-server
├── docker-compose.yml         # Configuracion del servicio
├── entrypoint-wrapper.sh      # Gamerules, scoreboard y watcher de resets
├── plugins/
│   └── WorldReset-1.7.jar     # Plugin que resetea el mundo al morir
└── .env.example               # Plantilla de variables de entorno
```

## Licencia

[MIT](LICENSE)
