# Ollama(Local LLM) + WebUI(Open WebUI) + MCP(MCPO) システム

## 制約

### Home

- セキュリティ: 無
- PCスペック: 高
    - OS: Windows
    - CPU: Ryzen 7 9800X3D
    - RAM: 96GB
        - WSL割当: 8GB
    - VRAM: 32GB
        - GPU: RTX 5090

### Work

- セキュリティ: 有
- PCスペック: 中
    - OS: Windows
    - CPU: Intel Core i5 14400
    - RAM: 16GB
        - WSL割当: 8GB
    - VRAM: null
        - GPU: オンボード

### Portable

- セキュリティ: 無
- PCスペック: 中
    - OS: Linux(Arch Linux)
    - CPU: Intel Core i5 14400
    - RAM: 16GB
    - VRAM: null
        - GPU: オンボード

## 構成

### Home

- Docker
    - Docker CEをWSLのLinuxに入れている
        - 将来的にDocker Desktop for Windowsを使うかもしれない
- Ollama
    - Windowsに入れている
        - 将来的にOllamaをやめてLM Studioを使うかもしれない

### Work

上記の制約により少し厳しい

- Docker
    - Docker CEをWSLのLinuxに入れている
- Ollama
    - OllamaをWSLのLinuxに入れている

### Portable

Linuxなので性能をフルに使える

- Docker
    - Docker CEをWSLのLinuxに入れている
- Ollama
    - OllamaをWSLのLinuxに入れている


## 実行

各環境での必要なものをすべて立ち上げた後に

```fish
set -x COMPOSE_FILE_NAME compose.home.yaml # homeの場合
docker compose -f compose.yaml -f COMPOSE_FILE_NAME pull
docker compose -f compose.yaml -f COMPOSE_FILE_NAME build
docker compose -f compose.yaml -f COMPOSE_FILE_NAME up -d
```
