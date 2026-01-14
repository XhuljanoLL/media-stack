# Media Management Stack (Docker Compose)

A complete **self-hosted media automation setup** using Docker Compose for **Windows**.  
This stack combines request management, indexers, media managers, and a download client to fully automate movies, TV shows, music, books, and more.

The compose file has some extra stuff at the moment, including Plex (Plex and Docker on Windows are a mess, better install it for Windows), and Monitoring options. They are optional, feel free to configure them on your own.

## Services Included

| Service | Purpose |
| ------- | -------- |
| **Overseerr** | Media request management and user-friendly frontend |
| **Prowlarr** | Indexer manager for all *Arr services |
| **Sonarr** | TV show management |
| **Radarr** | Movie management |
| **Readarr** | Book and audiobook management |
| **Lidarr** | Music management |
| **qBittorrent** | Torrent download client |

All services are orchestrated using **Docker Compose** for easy deployment and maintenance.

## Architecture Overview

```bash
Users → Overseerr
            ↓
     Sonarr / Radarr 
            ↓
    Prowlarr (Indexers)
            ↓
   qBittorrent (Downloads)
            ↓
       Media Library
```

## Requirements

- Docker Desktop
- Windows 10/11 (WSL recommended on Windows)
- At least 4 GB RAM
- Sufficient disk space for media storage


## Setup Instructions

1. Clone the repository

    ```bash
    git clone https://github.com/yourusername/your-repo-name.git
    cd your-repo-name
    ```

2. Configurations

    What needs to be done before using the compose file is to set up the right paths for all containers. On each service, there is a volume mount (bind mount):

    ```bash
    volumes:
      - P:\Overseerr\Config:/config
    ```

    ```bash
    HOST_PATH : CONTAINER_PATH
    ```

    This contains two parts:
    - **P:\Overseerr\Config** - Windows path on your machine. The folder must exist (or Docker will try to create it)
    - **/config** - Path inside the Linux container.
    So, when a service writes to */config/settings.json*, it actually writes to *P:\Overseerr\Config\settings.json* on Windows. **You will need to change these paths depending on where you want to store all the configs**.

3. (Optional) Change environment variables and ports

    - By default, the Timezone is set to Europe/Tirana, you can change it to your own timezone.
    - Ports are set to default ones for each container, if you have any busy ports, you can change them on the compose file by your needs.

4. Start the stack

    ```bash
    docker compose up -d
    ```

## Web Interfaces

| Service | URL |
| ------- | -------- |
| Overseerr | <http://localhost:5055> |
| Prowlarr | <http://localhost:9696> |
| Sonarr | <http://localhost:8989> |
| Radarr | <http://localhost:7878> |
| Readarr | <http://localhost:8787> |
| Lidarr | <http://localhost:8686> |
| qBittorrent | <http://localhost:8080> |

*(Default credentials for qBittorrent are usually **admin/adminadmin** — change immediately.)*

## Recommended Initial Configuration

1. [Prowlarr](https://github.com/XhuljanoLL/media-stack/blob/main/docs/prowlarr.md)
2. [Radarr](https://github.com/XhuljanoLL/media-stack/blob/main/docs/radarr.md)
3. [Sonarr](https://github.com/XhuljanoLL/media-stack/blob/main/docs/sonarr.md)
4. [Lidarr](https://github.com/XhuljanoLL/media-stack/blob/main/docs/lidarr.md)
5. [Readarr](https://github.com/XhuljanoLL/media-stack/blob/main/docs/readarr.md)
6. [qBittorrent](https://github.com/XhuljanoLL/media-stack/blob/main/docs/qbittorrent.md)
7. [Overseerr](https://github.com/XhuljanoLL/media-stack/blob/main/docs/overseerr.md)
8. [Flaresolverr](https://github.com/XhuljanoLL/media-stack/blob/main/docs/flaresolverr.md)

## Notes

- Designed for personal media management
- No media files are included
- You are responsible for complying with your local laws

## Credits

- LinuxServer.io images
- Overseerr, Sonarr, Radarr, Prowlarr, Lidarr, Readarr teams
- Docker community

Built for power users who believe in **self-hosting, data ownership, and control over their media libraries**.
