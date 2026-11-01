# Homelab

## Services

Some of the services running on the homelab, with a brief description of what each is used for.

| Icon | Service | Description | Link |
| --- | --- | --- | --- |
| <img src="src/images/homepage.png" height="32" style="padding-right:12px" align="absmiddle"> | **Homepage** | Self-hosted start page that links to every homelab service with live status widgets (Docker, Jellyfin, etc.). The default landing page for the lab. | [Docs](./services/homepage.md) |
| <img src="src/images/nginx.svg" height="32" style="padding-right:12px" align="absmiddle"> | **Nginx Proxy Manager** | Reverse proxy and single entry point for all HTTP(S) traffic; manages hostnames and issues/renews Let's Encrypt certificates automatically. | [Docs](./services/nginx-proxy-manager.md) |
| <img src="src/images/cloudflare-ddns.svg" height="32" style="padding-right:12px" align="absmiddle"> | **Cloudflare DDNS** | Background daemon that keeps the Cloudflare A records pointing at the home connection's current public IP, so public subdomains keep working when the ISP changes it. | [Docs](./services/cloudflare-ddns.md) |
| <img src="src/images/nextcloud.svg" height="32" style="padding-right:12px" align="absmiddle"> | **Nextcloud** | Private cloud for file storage and sharing, calendar, and contacts (app + MariaDB). | [Docs](./services/nextcloud.md) |
| <img src="src/images/seerr.png" height="32" style="padding-right:12px" align="absmiddle"> | **Seerr** | Movie & series request manager: browse catalogs, request titles, with Discord notifications when the media lands in the library. | [Docs](./services/seerr.md) |
| <img src="src/images/n8n.svg" height="32" style="padding-right:12px" align="absmiddle"> | **n8n** | Workflow automation for connecting apps and APIs. Runs scheduled jobs powered by locally hosted LLMs — a daily local-AI digest and a curated morning briefing, both posted to Discord via webhook. | [Docs](./services/n8n.md) |
| <img src="src/images/openwebui.png" height="32" style="padding-right:12px" align="absmiddle"> | **Open WebUI** | Chat interface for local LLMs; pointed at llama.cpp running natively on the host so all inference stays on the network. | [Docs](./services/openwebui.md) |
| <img src="src/images/home-assistant.svg" height="32" style="padding-right:12px" align="absmiddle"> | **Home Assistant** | Home automation hub: smart device integrations, automations, scenes, and dashboards (runs privileged for hardware access). | [Docs](./services/home-assistant.md) |
| <img src="src/images/uptime-kuma.png" height="32" style="padding-right:12px" align="absmiddle"> | **Uptime Kuma** | Uptime monitoring: checks that homelab services and external sites stay up, tracks response times, and sends alerts on outages. | [Docs](./services/uptime-kuma.md) |
| <img src="src/images/megans-library.png" height="32" style="padding-right:12px" align="absmiddle"> | **Megan's Library** | My wife's online book tracker for her personal library — she has cataloged **600+ books** so far and is working toward a goal of **1,000**. Built with React, Express & PostgreSQL. | [Docs](./services/megans-library.md) |
| <img src="src/images/internal-links.svg" height="32" style="padding-right:12px" align="absmiddle"> | **tools.nevswrld** | My internal tool utility kit: media downloader (yt-dlp → MP4/MP3) and file converter (ffmpeg), built on Vue 3 + FastAPI. | [Docs](./services/tools-nevswrld.md) |
| <img src="src/images/jellyfin.svg" height="32" style="padding-right:12px" align="absmiddle"> | **Jellyfin** | The media server — streams movies and TV from the local library (2× 8 TB WD Red Pro) to any device, wired into Seerr for requests. | [Docs](./services/jellyfin.md) |
| <img src="src/images/llamacpp-light.svg" height="32" style="padding-right:12px" align="absmiddle"> | **llama.cpp** | Local LLM inference running natively on the host — serves an OpenAI-compatible API used by Open WebUI, n8n and OpenCode. Runs Qwen3.8 27B and Ornith 1.5 35b A3B across two RTX 3060s. | [Docs](./services/llamacpp.md) |

## Hardware

<table>
  <tr>
    <td style="vertical-align: top;">
      <img src="src/images/homelab.jpg" width="250" alt="The homelab server">
    </td>
    <td style="vertical-align: top; padding-left: 16px;">
      <table>
        <tr><th>Component</th><th>Spec</th></tr>
        <tr><td>CPU</td><td>AMD Ryzen 7 5700 (8C/16T desktop)</td></tr>
        <tr><td>RAM</td><td>64 GB DDR4 (Corsair Vengeance)</td></tr>
        <tr><td>GPU</td><td>2× NVIDIA GeForce RTX 3060 12 GB GDDR6 (24 GB VRAM total)</td></tr>
        <tr><td>Storage</td><td>3× 1 TB SSD + 2× 8 TB WD Red Pro HDD (media library)</td></tr>
        <tr><td>Motherboard</td><td>ASRock X470 Master SLI</td></tr>
        <tr><td>PSU</td><td>MSI MAG A1000GL PCIe5 — fully modular 1000 W, 80+ Gold</td></tr>
        <tr><td>UPS</td><td>Goldenmate 1000 VA / 800 W lithium battery backup & surge protector</td></tr>
        <tr><td>Network</td><td>Ubiquiti Cloud Gateway Ultra (UCG-Ultra)</td></tr>
      </table>
      The dual GPUs run local LLM inference, everything else runs in Docker. The UPS rides out short power blips, and the UCG-Ultra routes the whole home network.
    </td>
  </tr>
</table>
