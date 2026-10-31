# Seerr

<img src="../src/images/seerr.png" width="400" alt="Seerr logo">

A request manager for my [Jellyfin](./jellyfin) library. I browse the movie and TV catalogs from the web UI and request titles; Seerr posts a message to my homelab Discord server through a Webhook URL whenever a new media request comes in, so I always know what's been asked for.

## Links

- **Website:** https://seerr.org
- **GitHub:** https://github.com/seerr-team/seerr
- **Docs/Setup guides:** https://github.com/seerr-team/seerr#readme (README)

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  seerr:
    image: ghcr.io/seerr-team/seerr:latest
    container_name: seerr
    ports:
      - "5055:5055"
    volumes:
      - ./config:/app/config
    environment:
      - LOG_LEVEL=info
    init: true
    restart: unless-stopped
```

Notes:

- On first launch, open the web UI to create your admin account.
- In **Settings → Media Servers**, connect [Jellyfin](./jellyfin) so it can show what's already in the library.
- Under **Settings → Notifications**, I point Seerr at a Discord Webhook URL for my homelab server — every new media request (and the follow-up when it's ready to watch) shows up as a message in the channel.
- All settings, users, and request history live in `./config`.
