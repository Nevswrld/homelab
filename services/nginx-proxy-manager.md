# Nginx Proxy Manager

<img src="../src/images/nginx.svg" width="400" alt="Nginx logo">

A Docker-based reverse proxy with a web UI. It manages hostnames, forwards traffic to your services, and issues/renews Let's Encrypt TLS certificates automatically — no manual nginx config editing required.

## Links

- **Website:** https://nginxproxymanager.com
- **GitHub:** https://github.com/jc21/nginx-proxy-manager
- **Guides:** https://nginxproxymanager.com/guides/

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  nginx-proxy-manager:
    image: jc21/nginx-proxy-manager:latest
    container_name: npm
    ports:
      - "80:80"     # HTTP
      - "443:443"   # HTTPS
      - "81:81"     # web UI
    volumes:
      - ./data:/data                  # proxy config + database
      - ./letsencrypt:/etc/letsencrypt  # TLS certificates
    restart: unless-stopped
```

Notes:

- The web UI runs on port `81`; create "proxy hosts" there pointing at your services (e.g. `http://nextcloud:80`).
- Certificates are stored in the `./letsencrypt` volume, so they survive container rebuilds and renew automatically.
- For public domains, point DNS A records at your server first; HTTP-01 challenges require ports 80/443 to be reachable from the internet.
