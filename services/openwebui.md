# Open WebUI

<img src="../src/images/openwebui.png" width="400" alt="Open WebUI logo">

A self-hosted chat interface for large language models. Point it at any OpenAI-compatible backend (Ollama, LM Studio, or a hosted API) and get a polished ChatGPT-style UI with model management, web search, file uploads, and multi-user support — all on your own hardware.

## Links

- **Website:** https://open-webui.com
- **GitHub:** https://github.com/open-webui/open-webui
- **Docs:** https://docs.openwebui.com

## Hosting It Yourself

Minimal `docker-compose.yml`:

```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    ports:
      - "3050:8080"
    volumes:
      - ./data:/app/backend/data
    # Point it at your LLM backend (any OpenAI-compatible /v1 endpoint):
    environment:
      - OPENAI_API_BASE_URL=http://host.docker.internal:1234/v1
    restart: unless-stopped
```

Notes:

- The container itself is just the UI — you still need an LLM server running somewhere (Ollama, llama.cpp, a hosted API). Set `OPENAI_API_BASE_URL` to its endpoint. In this homelab it points at [llama.cpp](./llamacpp) on the host.
- If the backend runs on the Docker host, use `host.docker.internal` as the hostname from inside the container.
- All chats, users, and settings are stored in `./data`.
