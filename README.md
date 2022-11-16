# media-stack
Simple docker-compose file combining sonarr radarr and jacket into a single stack with mounted volumes
Adjust as needed, and share updates if you want, I'm new at this so always looking to improve :) 
```
---
version: "2.1"
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Denver
    volumes:
      - /mnt/server/config:/config
      - /path/to/data:/tv
      - /path/to/data:/anime #optional
      - /path/to/data:/downloads #optional
    ports:
      - 8989:8989
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Denver
    volumes:
      - /path/to/data/config/radarr:/config
      - /path/to/data/Movies:/movies #optional
      - /path/to/data/Downloads:/downloads #optional
    ports:
      - 7878:7878
    restart: unless-stopped
    
  jackett:
    image: lscr.io/linuxserver/jackett:latest
    container_name: jackett
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Denver
      - AUTO_UPDATE=true #optional
    volumes:
      - /path/to/data/config:/config
      - /path/to/data/downloads:/downloads
    ports:
      - 9117:9117
    restart: unless-stopped
```
