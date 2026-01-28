# Retro Arcade Machine 🕹️

A Docker Compose setup for running classic retro games in your browser. This project creates a retro arcade machine with a game selector interface and multiple classic games.

## What Does This Docker Compose File Do?

This Docker Compose configuration sets up a complete retro gaming arcade system with:

1. **Game Selector Interface** - A stylish retro-themed landing page to choose games
2. **Three Classic Games** - Super Mario, Tetris, and Pac-Man
3. **Isolated Containers** - Each game runs in its own Docker container
4. **Easy Access** - All games accessible via web browser

## Services and Ports

The compose file defines 4 services with the following port mappings:

| Service | Container Name | Port | Description |
|---------|----------------|------|-------------|
| **nginx** | game-selector | 8080 | Game selection landing page |
| **supermario** | supermario | 8081 | Super Mario browser game |
| **tetris** | tetris | 8082 | Tetris browser game |
| **pacman** | pacman | 8083 | Pac-Man browser game |

All ports can be customized via the `.env` file.

## Service Details

### 1. Nginx (Game Selector)
- **Container Name:** `game-selector`
- **Image:** `nginx`
- **Port:** `8080` (configurable via `nginxPort`)
- **Purpose:** Serves the game selection interface
- **Features:** 
  - Retro-styled landing page with scanline effects
  - Visual game thumbnails
  - Direct links to each game
  - Hosted from the `./Website/` directory

### 2. Super Mario
- **Container Name:** `supermario`
- **Image:** `vijaygiduthuri/mario:latest`
- **Port:** `8081` (configurable via `marioPort`)
- **Purpose:** Browser-based Super Mario game
- **Features:** 
  - Classic Super Mario gameplay
  - Runs entirely in the browser
  - Auto-restart on failure

### 3. Tetris
- **Container Name:** `tetris`
- **Image:** `bsord/tetris`
- **Port:** `8082` (configurable via `tetrisPort`)
- **Purpose:** Browser-based Tetris game
- **Features:** 
  - Classic Tetris gameplay
  - Web-based interface
  - Auto-restart on failure

### 4. Pac-Man
- **Container Name:** `pacman`
- **Image:** `yuravorobei/pacman-web:latest`
- **Port:** `8083` (configurable via `pacmanPort`)
- **Purpose:** Browser-based Pac-Man game
- **Features:** 
  - Classic Pac-Man gameplay
  - Web-based interface
  - Auto-restart on failure

## Prerequisites

- Docker Engine installed
- Docker Compose installed

## Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd retro
   ```

2. **Configure ports (optional):**
   Edit the `.env` file to customize the ports:
   ```
   nginxPort=8080
   marioPort=8081
   tetrisPort=8082
   pacmanPort=8083
   website=./Website/
   ```

3. **Start the arcade:**
   ```bash
   docker-compose up -d
   ```

4. **Access the games:**
   - Open your browser and navigate to `http://localhost:8080`
   - Select your game from the retro-styled interface
   - Or access games directly:
     - Super Mario: `http://localhost:8081`
     - Tetris: `http://localhost:8082`
     - Pac-Man: `http://localhost:8083`

## Usage

### Starting the Arcade
```bash
docker-compose up -d
```

### Stopping the Arcade
```bash
docker-compose down
```

### Viewing Logs
```bash
# All services
docker-compose logs

# Specific service
docker-compose logs supermario
docker-compose logs tetris
docker-compose logs pacman
docker-compose logs nginx
```

### Restarting Services
```bash
# Restart all
docker-compose restart

# Restart specific service
docker-compose restart supermario
```

## Environment Variables

The following environment variables can be configured in the `.env` file:

- `nginxPort` - Port for the game selector (default: 8080)
- `marioPort` - Port for Super Mario (default: 8081)
- `tetrisPort` - Port for Tetris (default: 8082)
- `pacmanPort` - Port for Pac-Man (default: 8083)
- `website` - Path to the website directory (default: ./Website/)

## Features

✨ **Retro Design** - CRT-style scanline effects and pixel-perfect rendering
🎮 **Multiple Games** - Three classic arcade games
🐳 **Containerized** - Easy deployment with Docker
🔄 **Auto-Restart** - Services automatically restart on failure
⚙️ **Configurable** - Easily customize ports via environment variables
🌐 **Browser-Based** - No installation required, play directly in your browser

## Troubleshooting

### Port Already in Use
If you get a "port already in use" error, modify the ports in the `.env` file.

### Container Won't Start
Check logs for the specific container:
```bash
docker-compose logs <service-name>
```

### Game Not Loading
1. Ensure all containers are running: `docker-compose ps`
2. Check if ports are accessible: `curl http://localhost:<port>`
3. Restart the specific service: `docker-compose restart <service-name>`

## Architecture

```
┌─────────────────────────────────────────┐
│   Browser (http://localhost:8080)      │
│   ┌─────────────────────────────┐      │
│   │  Game Selector Interface    │      │
│   │  (Nginx Container)          │      │
│   └─────────────────────────────┘      │
│          │       │         │            │
│          │       │         │            │
│    ┌─────┘  ┌────┘    └────┐          │
│    │        │              │           │
│    ▼        ▼              ▼           │
│ ┌──────┐ ┌──────┐      ┌──────┐      │
│ │Mario │ │Tetris│      │PacMan│      │
│ │:8081 │ │:8082 │      │:8083 │      │
│ └──────┘ └──────┘      └──────┘      │
└─────────────────────────────────────────┘
```

## License

This project uses the following Docker images:
- `vijaygiduthuri/mario:latest`
- `bsord/tetris`
- `yuravorobei/pacman-web:latest`
- `nginx`

Please refer to the individual image repositories for their respective licenses.
