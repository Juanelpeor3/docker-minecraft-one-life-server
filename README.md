

# mc-one-life-server

[Español](README.es.md) | **English**

Dockerized Minecraft **"One Life"** server. If **any player dies**, the world resets instantly with a new seed thanks to [WorldReset](https://modrinth.com/plugin/worldreset), without restarting the server.

## How it works

1. The server runs in **Hardcore** mode with natural regeneration disabled across all three worlds (overworld, nether, end).
2. **WorldReset** detects a player death and instantly generates a new world with a random seed.
3. An **entrypoint wrapper** automatically re-applies gamerules and the scoreboard every time WorldReset generates a new world.
4. The **Tab** list shows each online player's hearts.

> **Warning:**
> This repository has been tested and works on Minecraft **26.2** and **26.3**. Future Minecraft updates may change gamerule names, plugin compatibility, or server behavior, which could break this setup. If you run into issues on a newer version, set `VERSION=26.3` in your `.env` file.

## Requirements

- [Docker](https://docs.docker.com/get-docker/) & Docker Compose

## Installation

```bash
git clone https://github.com/Juanelpeor3/mc-one-life-server.git
cd mc-one-life-server

# Copy the example and edit your values
cp .env.example .env
```

## Configuration

Edit the `.env` file with your values:

| Variable              | Description                        | Default  |
|-----------------------|------------------------------------|----------|
| `VERSION`             | Minecraft version                  | `26.2`   |
| `RCON_PASSWORD`       | RCON password (required)           | -        |
| `WHITELIST`           | Allowed players, comma-separated   | -        |
| `OPS`                 | Server admins                      | -        |
| `VIEW_DISTANCE`       | Render distance in chunks          | `16`     |
| `SIMULATION_DISTANCE` | Simulation distance in chunks      | `10`     |
| `INIT_MEMORY`         | Initial JVM memory                 | `4G`     |
| `MAX_MEMORY`          | Max JVM memory                     | `6G`     |

## Usage

```bash
# Start the server
docker compose up -d

# Watch logs
docker compose logs -f

# Stop the server
docker compose down
```

## WorldReset plugin

For commands, configuration and full documentation, see the plugin page:

https://modrinth.com/plugin/worldreset

## Project structure

```
.
├── Dockerfile                 # Image based on itzg/minecraft-server
├── docker-compose.yml         # Service configuration
├── entrypoint-wrapper.sh      # Gamerules, scoreboard & reset watcher
├── plugins/
│   └── WorldReset-1.7.jar     # Plugin that resets the world on death
└── .env.example               # Environment variables template
```

## License

[MIT](LICENSE)
