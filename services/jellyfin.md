# Jellyfin

<img src="../src/images/jellyfin.svg" width="400" alt="Jellyfin logo">

The media server at the heart of the homelab — streams movies and TV from the local library (a pair of 8 TB WD Red Pro drives) to any device on the local network.

## Links

- **Website:** https://jellyfin.org
- **GitHub:** https://github.com/jellyfin/jellyfin
- **Docs:** https://docs.jellyfin.org

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    ports:
      - "8096:8096"
    volumes:
      - ./config:/config
      - /path/to/media:/media:ro   # the media library
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    restart: unless-stopped
```

Notes:

- Create your admin account in the browser on first launch.
- Libraries are scanned from `/media`; keep the media volume read-only so Jellyfin can never modify files.
- [Seerr](./seerr) connects to Jellyfin so requests can see what's already in the library, and a [Homepage](./homepage) widget surfaces now-playing info.
