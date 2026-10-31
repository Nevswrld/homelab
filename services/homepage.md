# Homepage

<img src="../src/images/homepage.png" width="400" alt="Homepage logo">

A self-hosted start page / dashboard that aggregates links to all your services, with live status widgets (Docker containers, media servers, disks, and more). Highly customizable via YAML config files.

## Links

- **Website:** https://gethomepage.dev
- **GitHub:** https://github.com/gethomepage/homepage
- **Docs:** https://gethomepage.dev/installation/

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    ports:
      - "3000:3000"
    volumes:
      - ./config:/app/config
      # Optional: lets the Docker widget show live container status
      - /var/run/docker.sock:/var/run/docker.sock:ro
    restart: unless-stopped
```

Notes:

- All UI content (services, widgets, bookmarks) is defined in YAML files inside `./config` (`services.yaml`, `widgets.yaml`, `bookmarks.yaml`) — edit them and the page updates automatically.
- Mounting the Docker socket read-only is optional but recommended for container-status widgets.
- Set `HOMEPAGE_ALLOWED_HOSTS` if you access it through a reverse proxy with a custom hostname.
