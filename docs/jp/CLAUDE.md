# Claude Code用プロジェクトコンテキスト

このプロジェクトは、Ollama（Windowsホストで実行）、Open WebUI、MCPO（Model Context Protocol）をWSL環境で組み合わせたローカルLLMチャット環境を構築します。

## 主要な技術的詳細

### アーキテクチャ
- OllamaはWindowsホスト上で実行（WSLコンテナから`host.docker.internal:11434`でアクセス可能）
- Open WebUIとMCPOはWSL内のDockerコンテナとして実行
- MCPOはOpen WebUI用のMCPサーバー統合を提供

### 重要な設定
- WSLコンテナからWindowsホストサービスへの接続には`host.docker.internal`を使用
- MCPOはClaude Desktop互換の設定フォーマットに追加機能（SSE、streamable HTTP）を搭載
- Dockerボリュームは名前付きボリュームではなくローカルディレクトリとしてマウント（アクセスしやすくするため）

### セキュリティに関する考慮事項
- コミット前に必ず`npm run check-secrets`を実行
- 実際のトークンは絶対にコミットしない - 実際の値は`.env.local`を使用
- secretlintがpre-commitフックで設定済み

### よく使うコマンド
- サービス起動: `docker-compose up -d`
- ログ確認: `docker-compose logs -f`
- シークレットスキャン: `npm run check-secrets`

### ファイルの場所
- MCP設定: `mcp-configs/config.json`
- 環境変数: `.env`（テンプレート）、`.env.local`（実際の値）
- データディレクトリ: `mcpo-data/`、`open-webui-data/`

## 開発メモ
- docker-compose.ymlを修正する際は、Windows上のOllamaが外部にあることを忘れずに
- config.jsonで定義されたMCPサーバーは自動的にHTTPエンドポイントとして公開される
- 各MCPサーバーのOpenAPIドキュメントは`http://localhost:8000/{server-name}/docs`で確認可能