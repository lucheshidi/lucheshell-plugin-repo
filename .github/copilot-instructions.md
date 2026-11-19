# Duckshell Repo — Copilot 指南

目的：为 AI 编码代理提供快速上手要点、代码位置示例和可执行验证步骤，使其能立刻在此仓库内安全、可预测地工作。

快速要点
- 仓库为“插件分发镜像”：核心内容由 `static/`（站点说明）、`metadata/`（插件索引）和 `plugins/`（插件包和元数据）三部分构成。
- 不存在构建系统；部署即把仓库目录放到静态 HTTP 服务（Apache/Nginx）下并确保 `/static/` 与 `/metadata/` 可访问。

验证与本地调试（示例）
1. 在仓库根目录快速启动一个本地静态服务器：

```bash
python3 -m http.server 8000
# 然后在浏览器访问 http://localhost:8000/static/ 和 http://localhost:8000/metadata/
```

2. 验证关键 URL：`/static/`（站点说明），`/metadata/index.html`（插件索引），`/plugins/`（插件目录，建议启用 autoindex 列表以便调试）。

重要文件与说明（示例引用）
- 仓库入口跳转: [index.html](index.html) 会重定向到 `./static/`。
- 站点说明页面: [static/index.html](static/index.html) — 包含中英文切换（使用 `data-lang` 属性和 `body.en` 类切换），以及“如何构建/发布”的说明。
- 插件索引: [metadata/index.html](metadata/index.html) — 列出可用插件的链接。
- 单个插件元数据示例: [plugins/HelloWorldPlugin/plugin.json](plugins/HelloWorldPlugin/plugin.json#L1-L7) — 每个插件目录应包含 `plugin.json`（id/name/platforms/latest_version/author）和按版本组织的子目录（如 `v1.0/`）。

约定与模式（可被代理直接遵循）
- 插件组织：`plugins/<PluginName>/plugin.json`（描述） + `plugins/<PluginName>/<version>/`（二进制/可下载文件）。当需要添加插件，遵循此结构并在 `metadata/index.html` 中建立可访问链接。
- 可访问性要求：静态站点必须能返回 HTML 页面（`/static/` 和 `/metadata/`），而 `/plugins/` 在生产环境通常由 webserver 提供目录或 503 响应（参考 `static/index.html` 的“验证”段落）。
- 本地化：不要直接修改静态页面的 DOM 结构，切换语言时以 `body.en` 类为开关（示例在 `static/index.html` 中）。

开发/运维注意事项（可操作）
- 仓库无构建脚本：变更只需提交静态文件并重载 webserver。若需要临时查看效果，使用上面的 `python3 -m http.server`。
- 上线要求：README/站点中明确建议“必须配置 HTTPS 与公网可达”。代理对运行环境的假设是：静态 HTTP 服务、可启用 autoindex（用于调试插件列表）。

对 AI 代理的具体指令（执行策略）
- 仅做可见文件的更新：当需要添加插件，创建 `plugins/<Name>/plugin.json` 与版本目录，并在 `metadata/index.html` 增加索引项。
- 遇到结构或语义不明确时优先读取 `static/index.html`（站点说明）再修改元数据；不要假设额外的后端逻辑。
- 合并指导：如果仓库已有 `.github/copilot-instructions.md`，请保留任何“使用/部署”步骤和手动验证指令，合并新发现的插件约定与示例路径。

变更示例（添加插件）
1. 新建目录 `plugins/MyPlugin/`。
2. 添加 `plugins/MyPlugin/plugin.json`（参照 [plugins/HelloWorldPlugin/plugin.json](plugins/HelloWorldPlugin/plugin.json#L1-L7)）。
3. 在 `plugins/MyPlugin/v1.0/` 中放置二进制或可下载文件。
4. 在 `metadata/index.html` 中添加指向 `plugins/MyPlugin/` 的链接供镜像索引使用。

反馈请求：我已将基础指南写入本文件。请告诉我是否需要：添加更多命令示例、补充 nginx 配置片段，或合并其它团队的已有段落。
