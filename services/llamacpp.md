# llama.cpp

<img src="../src/images/llamacpp.svg" width="400" alt="llama.cpp logo">

Local LLM inference in C/C++. Runs the homelab's language models natively on the host and serves an OpenAI-compatible API that [Open WebUI](./openwebui), [n8n](./n8n) and OpenCode talk to.

## Links

- **GitHub:** https://github.com/ggml-org/llama.cpp
- **Docs:** https://github.com/ggml-org/llama.cpp/tree/master/docs

## Models

| Model | Notes |
| --- | --- |
| Qwen3.8 27B | Primary chat model |
| Ornith 1.5 35b A3B | MoE (3B active) — fast on the dual GPUs |

## Hardware

Runs on the two RTX 3060 12 GB cards (24 GB VRAM total), with layers split across both via tensor splitting.

## Usage

- Serves an OpenAI-compatible `/v1` endpoint; other services reach it at `http://host.docker.internal:8080/v1`.
- The same models power [OpenCode](https://opencode.ai) sessions run from the host.
