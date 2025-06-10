# TODO

- [ ] README.md 作成および充実
- [ ] compose.home.yaml
- [x] compose.work.yaml
- [ ] compose.portable.yaml
- [ ] MCPOの登録および有効化の制約について検討
  - 現在、MCPOのserviceはOpen WebUIのserviceと同時に起動するようになっている。
    - 自動検出???
  - 自動検出
    - ユーザーによる登録の手間は不要
    - 不必要なツールまで自動で導入され、強制的に有効になる
  - 手動検出
    - Claudeのデスクトップアプリと同様の設定方法
    - ユーザーが手で設定ファイルいじって反映させる
- [ ] Excel MCP用サンプルデータ生成手順のドキュメント化
  - `paru -S gnumeric` して、 `ssconvert sample.csv sample.xlsx` するだけ
- [ ] Makefile作成
  - [ ] 各環境の切り替え方法

---

<https://docs.docker.com/engine/storage/volumes/#when-to-use-volumes>

> Volumes are not a good choice if you need to access the files from the host, as the volume is completely managed by Docker. Use bind mounts if you need to access files or directories from both containers and the host.

ホストからデータを見に行くケースについて考える.
生成されたデータはウェブサイトからダウンロードする一般的な経路だから、bind mountではなくてもよい？
volume mountに変えた。

ファイルをOpenWebUI上からアップロードしたらmcpoの方でも`uploads-data`以下に表示されるようになった

```shell
❯ docker compose -f compose.work.yaml exec mcpo /bin/sh
# ls uploads-data/98c314bb-a938-4172-8e6b-4da90f26b7a3_hoge.txt
uploads-data/98c314bb-a938-4172-8e6b-4da90f26b7a3_hoge.txt
# ls
CHANGELOG.md  Dockerfile  LICENSE  README.md  config.json  pyproject.toml  src  uploads-data  uv.lock
```

後は各種ローカルシステムを見に行くものは`/app/uploads-data/`を見に行くように設定すればExcelでもなんでも読み込めるはず

