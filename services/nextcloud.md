# Nextcloud

<img src="../src/images/nextcloud.svg" width="400" alt="Nextcloud logo">

A self-hosted private cloud for file storage and sharing, with built-in calendar, contacts, office docs, and a large app ecosystem. Think "your own Dropbox + Google Drive + Calendar" that you fully control.

## Links

- **Website:** https://nextcloud.com
- **GitHub:** https://github.com/nextcloud/server
- **Docs:** https://docs.nextcloud.com

## Hosting It Yourself

Nextcloud needs a database (MariaDB or PostgreSQL) plus the app container:

```yaml
services:
  db:
    image: mariadb
    container_name: nextcloud-db
    environment:
      MARIADB_DATABASE: nextcloud
      MARIADB_USER: nextcloud
      MARIADB_PASSWORD: change-me
      MARIADB_ROOT_PASSWORD: change-me-root
    volumes:
      - ./db-data:/var/lib/mysql

  app:
    image: nextcloud
    container_name: nextcloud
    ports:
      - "8080:80"
    environment:
      MYSQL_HOST: db
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: change-me
    volumes:
      - ./html:/var/www/html   # user files + config live here
    depends_on:
      - db
    restart: unless-stopped
```

Notes:

- Open the app in a browser to run the initial setup (create admin account, pick database settings).
- Back up **both** `./html` and `./db-data` — files alone are not enough.
- If exposing it publicly, put it behind HTTPS (e.g. [Nginx Proxy Manager](nginx-proxy-manager.md)) and enable 2FA for all accounts.
