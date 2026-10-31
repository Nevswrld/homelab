# Uptime Kuma

<img src="../src/images/uptime-kuma.png" width="400" alt="Uptime Kuma logo">

A self-hosted uptime monitoring tool. Ping your websites, APIs, and ports (HTTP/TCP/ping/DNS and more), get instant alerts when something goes down via 20+ notification channels (Telegram, Discord, email, ntfy, ...), and view response-time history on a clean dashboard.

## Links

- **GitHub:** https://github.com/louislam/uptime-kuma
- **Docs/Setup guides:** https://github.com/louislam/uptime-kuma#readme (README)

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    ports:
      - "3001:3001"
    volumes:
      - ./data:/app/data
    restart: unless-stopped
```

Notes:

- Create your admin account in the browser on first launch, then add monitors (URLs, hosts, ports) from the dashboard.
- Configure notification channels under **Settings** — useful ones for a homelab are Telegram/ntfy/Discord so you get alerts on your phone.
- All monitors, settings, and history live in `./data`.
