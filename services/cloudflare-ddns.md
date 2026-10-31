# Cloudflare DDNS

<img src="../src/images/cloudflare-ddns.svg" width="400" alt="Cloudflare logo">

A small background daemon that keeps your Cloudflare DNS records pointing at your current public IP address. If you have a dynamic home connection, this means your public subdomains (e.g. `cloud.example.com`) keep working even when the ISP changes your IP — no manual DNS updates needed.

## Links

- **GitHub:** https://github.com/timothyjmiller/cloudflare-ddns
- **Docs/Config reference:** https://github.com/timothyjmiller/cloudflare-ddns#configuration (README)

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  cloudflare-ddns:
    image: timothyjmiller/cloudflare-ddns:latest
    container_name: cloudflare-ddns
    network_mode: host   # needed so it can detect the real public IP
    volumes:
      - ./config.json:/etc/cloudflare-ddns/config.json
    restart: unless-stopped
```

Notes:

- Create an API token in Cloudflare with **Zone → DNS (Edit)** permission for your zone.
- Get your Zone ID from the Cloudflare dashboard (Overview page of the zone).
- `config.json` maps each domain to its zone, e.g.:

  ```json
  {
    "email": "",
    "key": "<api-token>",
    "proxied": false,
    "domains": [
      { "domain": "cloud.example.com", "zone_id": "<zone-id>" }
    ]
  }
  ```

- It checks and updates the A record on an interval (default every few minutes); no web UI — it's purely a background service.
