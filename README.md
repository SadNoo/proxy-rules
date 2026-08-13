# proxy-rules

Loon 与 sing-box 的远程分流规则。规则由人工维护，不使用 GitHub Actions。

- `loon/*.list`：Loon Remote Rule 格式。
- `sing-box/*.json`：sing-box source rule-set，兼容 sing-box 1.13 及以上版本。

修改并推送文件后，客户端会按配置中的更新周期自动拉取。
