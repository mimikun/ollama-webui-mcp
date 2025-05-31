# Ollama + Open WebUI + MCPO 環境

ローカルでOllama、Open WebUI、MCPOを組み合わせたLLMチャット環境です。

## 必要条件

- Docker & Docker Compose
- Node.js (secretlint用)
- Windows側で動作するOllama

## セットアップ

1. 環境変数の設定
```bash
cp .env .env.local
# .env.localを編集してトークンを設定
```

2. 依存関係のインストール
```bash
npm install
```

3. シークレットチェック
```bash
npm run check-secrets
```

4. コンテナ起動
```bash
docker-compose up -d
```

## アクセス

- Open WebUI: http://localhost:8080
- MCPO: http://localhost:8000
- MCP各サービス: http://localhost:8000/{service-name}/docs

## MCP設定

`mcp-configs/config.json`でMCPサーバーを設定できます。

## セキュリティ

- `.env`ファイルは`.gitignore`に含まれています
- secretlintでシークレット漏洩を防止
- pre-commitフックでチェック実行