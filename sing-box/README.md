# sing-box 规则集

此目录只保存可被客户端配置引用的规则集，不包含完整配置、节点或订阅凭据。已有 direct.json、proxy.json、reject.json 保持原样。

## SiriAI

| 配置入口 | 可编辑源规则 | 编译规则 |
| --- | --- | --- |
| sing-box 1.14 | [1.14/SiriAI.json](1.14/SiriAI.json) | [1.14/SiriAI.srs](1.14/SiriAI.srs) |
| sing-box 1.15 | [1.15/SiriAI.json](1.15/SiriAI.json) | [1.15/SiriAI.srs](1.15/SiriAI.srs) |

两版目前保留相同的 18 个匹配项：5 个完整域名、12 个域名后缀、1 个关键词。分目录是为了后续按配置版本分别维护，并非表示内容需要不同格式。JSON 中的 version: 3 是规则集格式版本，不是客户端版本；两者均可使用该格式。

从用户提供的 Clash / Surge 规则转换，已修正多余空格、换行及两处抄写错误：

- gspe1-ss1.1s.apple.com → gspe1-ssl.ls.apple.com
- 1s.apple.com → ls.apple.com

原文的 ChatGPT 为策略组名称，不写进 headless 规则集；主配置应将 rule_set: SiriAI 路由到实际存在的策略组或出站。应优先于通用 Apple 规则，否则可能先被 Apple 规则命中。

注意：关键词 siri 匹配任何包含此字符串的域名，并不限于 Apple；ls.apple.com 覆盖其全部子域名。本规则按原文保留这些匹配范围，不保证所有命中都仅属于 Siri / ChatGPT，也不保证启用 Apple Intelligence。规则内的 Cloudflare 域名是匹配对象，不是 Cloudflare DoH 配置。

## 原始文件地址

- https://raw.githubusercontent.com/SadNoo/proxy-rules/main/sing-box/1.14/SiriAI.json
- https://raw.githubusercontent.com/SadNoo/proxy-rules/main/sing-box/1.14/SiriAI.srs
- https://raw.githubusercontent.com/SadNoo/proxy-rules/main/sing-box/1.15/SiriAI.json
- https://raw.githubusercontent.com/SadNoo/proxy-rules/main/sing-box/1.15/SiriAI.srs

## 手动维护

保持人工维护，不添加自动化工作流。在本目录内修改对应 JSON 后编译并一并提交源文件与二进制：

```sh
sing-box rule-set compile --output 1.14/SiriAI.srs 1.14/SiriAI.json
sing-box rule-set compile --output 1.15/SiriAI.srs 1.15/SiriAI.json
```

本次使用 sing-box 1.14.0 编译并验证规则匹配；1.15 目录使用相同的兼容格式与规则内容，没有宣称已完成 1.15 客户端或真机联网验收。

规则格式以 [sing-box 官方文档](https://sing-box.sagernet.org/configuration/rule-set/source-format/) 为准。模块仅定义匹配条件，不指定 DNS、不创建策略组。
