# Run LLMs locally with Ollama

## Local Install

```bash
curl -fsSL https://ollama.com/install.sh | sh # Install ollama
ollama pull <model> # e.g. deepseek-r1:1.5b
ollama run <model>
```

## Run Inside Docker Container

Run container:

```bash
# Via Docker CLI
docker run \
  -d \
  --device=nvidia.com/gpu=all \
  -v ollama:/root/.ollama \
  -p 11434:11434 \
  --name ollama \
  ollama/ollama

# Via Docker Compose
# Prepare docker-compose.yml
docker compose up -d # Start ollama container with gpu in detached mode
```

Interact with LLM:
```bash
# Via Docker CLI
docker exec -it ollama ollama run <model>

# Via CURL
curl -X POST http://localhost:11434/api/generate -d '{
  "model": <model>,
  "prompt": <prompt>
}'
```

## Run with Open-WebUI

1. Start container with image `ghcr.io/open-webui/open-webui:main`.
2. Expose the desired ports
3. Start both container
4. Access Open-WebUI from designated port on localhost

Best done with `Docker Compose`.
