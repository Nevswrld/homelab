# Home Assistant

<img src="../src/images/home-assistant.svg" width="400" alt="Home Assistant logo">

The leading open-source home automation hub. Connect smart devices (lights, plugs, sensors, cameras), build automations and scenes ("when motion is detected at night, turn on the hallway light"), and control everything from dashboards or voice assistants. Supports hundreds of device integrations plus Zigbee/Z-Wave/Thread radios.

## Links

- **Website:** https://www.home-assistant.io
- **GitHub:** https://github.com/home-assistant/core
- **Docs:** https://www.home-assistant.io/docs/

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  home-assistant:
    image: ghcr.io/home-assistant/home-assistant:stable
    container_name: homeassistant
    privileged: true   # only needed for USB/Bluetooth/Zigbee hardware access
    ports:
      - "8123:8123"
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
```

Notes:

- On first launch, the onboarding wizard walks you through creating an admin account and adding your first integrations.
- `privileged: true` is only required if you pass hardware through (USB dongles for Zigbee/Z-Wave, Bluetooth). Drop it if you don't need that.
- Everything (automations, dashboards, integrations) lives in `./config` — back up this folder regularly; the built-in "Configuration → Backups" feature can export it.
