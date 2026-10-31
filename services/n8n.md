# n8n

<img src="../src/images/n8n.svg" width="400" alt="n8n logo">

A workflow automation tool for connecting apps and APIs. Build visual workflows ("nodes") to move data between services, send notifications, run scheduled jobs, or orchestrate AI agents — with 400+ integrations plus HTTP/webhook nodes for anything else.

## Links

- **Website:** https://n8n.io
- **GitHub:** https://github.com/n8n-io/n8n
- **Docs:** https://docs.n8n.io

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    container_name: n8n
    ports:
      - "5678:5678"
    environment:
      - GENERIC_TIMEZONE=America/New_York   # set to your timezone
      # Only needed if you expose public webhooks through a reverse proxy:
      # - WEBHOOK_URL=https://n8n.example.com/
    volumes:
      - ./n8n-data:/home/node/.n8n
    restart: unless-stopped
```

Notes:

- Create your owner account in the browser on first launch.
- All workflows, credentials, and execution history are stored in `./n8n-data` — back it up regularly.
- If a workflow needs to reach services on the Docker host (e.g. a local LLM server), use `host.docker.internal` as the hostname inside HTTP nodes.

## Workflows in Use

The workflows below all run on a schedule and use locally hosted LLMs (served by [llama.cpp](./llamacpp)) — no cloud AI APIs involved. Results are posted to my homelab Discord server via Webhook URLs.

- **Local AI daily digest** — fetches the top 10 trending models from Hugging Face and recent posts from r/LocalLLaMA, then a local LLM writes up a short daily summary of what's happening in the locally hosted AI world, posted to my homelab Discord server.
- **Daily briefing** — gathers home server status from [Uptime Kuma](./uptime-kuma), latest news headlines/trends, the day's weather, the last 24 hours of email, and a daily joke; a small local LLM follows a template to compose one curated message, sent to my homelab Discord channel.
