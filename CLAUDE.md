# Project Context for Claude Code

This project creates a local LLM chat environment combining Ollama (running on Windows host), Open WebUI, and MCPO (Model Context Protocol) in WSL.

## Key Technical Details

### Architecture
- Ollama runs on Windows host (accessible at `host.docker.internal:11434` from WSL containers)
- Open WebUI and MCPO run as Docker containers in WSL
- MCPO provides MCP server integration for Open WebUI

### Important Configuration
- Use `host.docker.internal` to connect from WSL containers to Windows host services
- MCPO uses Claude Desktop-compatible config format with additional features (SSE, streamable HTTP)
- Docker volumes are mounted as local directories (not named volumes) for easier access

### Security Considerations
- Always run `npm run check-secrets` before committing
- Never commit actual tokens - use `.env.local` for real values
- secretlint is configured with pre-commit hooks

### Common Commands
- Start services: `docker-compose up -d`
- Check logs: `docker-compose logs -f`
- Scan for secrets: `npm run check-secrets`

### File Locations
- MCP config: `mcp-configs/config.json`
- Environment variables: `.env` (template), `.env.local` (actual values)
- Data directories: `mcpo-data/`, `open-webui-data/`

## Development Notes
- When modifying docker-compose.yml, remember Windows Ollama is external
- MCP servers defined in config.json are automatically exposed as HTTP endpoints
- Each MCP server gets OpenAPI docs at `http://localhost:8000/{server-name}/docs`