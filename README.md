# 9Router — 纯净版（Pure Build）

> 本仓库是 **[decolua/9router](https://github.com/decolua/9router)** 的**去广告 / 去推广 / 去遥测 / 去自动更新**纯净分支。
> **仅供学习与代码参考**，与上游作者无关。

---

## 这是什么

9Router 是一个 AI 路由网关：把 Claude Code、Codex、Cursor、Cline、OpenCode、OpenClaw 等各种 AI 编程工具，统一接入 40+ 家 AI 供应商、100+ 模型，用一个本地端点（`http://127.0.0.1:20128`）对外服务。

核心能力：

- **RTK Token 节省器** — 压缩工具输出（`git diff`、`grep`、`ls`…）后再发给 LLM，每次请求省 20-40% 输入 token
- **Headroom Token 节省器** — 进一步的上下文裁剪
- **自动降级回退** — 订阅 → 便宜 → 免费，零中断
- **多账号轮询** — 同一供应商多个账号负载均衡
- **实时配额追踪 / Usage 统计 / 组合模型（Combos）**
- **格式翻译** — OpenAI / Anthropic / Gemini 等协议互转
- **MITM 流量录制代理、代理池、CLI 工具集成（OAuth 自动导入）**

---

## 相对上游移除了什么（净化清单）

### 遥测 / 上报
- **Google Analytics**（`G-LC959F603F`）及其 `@next/third-parties` 依赖
- **Donate 上报端点** `9router.com/api/donate` 及其按钮/弹窗组件

### 自动更新（应本仓库需求一并移除）
- `/api/version`（向 `registry.npmjs.org` 拉取最新版本号）
- `/api/version/update`（自安装）
- `cli.js` 内 npm registry 版本检查与"Update"菜单分支
- SideBar 更新提示 UI 与 `ManualUpdatePanel` 组件
- `src/lib/updater/updater.js` 独立 detached 更新进程
- `UPDATER_CONFIG` 中更新专用字段（保留 `appPort` 本地端口常量）

### 推广 / 广告
- 9Remote / 9English 交叉推广（侧栏外链、`NineRemoteButton`/`NineRemotePromoModal` 组件）
- 营销落地页 `src/app/landing/` 整目录
- `DonateModal` 组件
- README / i18n / 文档中的徽章（shields/trendshift/starchart/contrib.rocks）、YouTube 推广画廊、捐赠/赞助区块、第三方 fork 推广（OmniRoute）、求 star 文案

## 保留（属正常功能，非广告/遥测）

- `models.dev` 模型能力目录同步、`raw.githubusercontent.com` changelog 拉取、`api.anthropic.com/mcp-registry` MCP 市场 —— 均为功能必需的数据源
- `/api/version/shutdown`（关机接口）、本地鉴权 `machineId` / `x-9r-cli-token`
- `disableEssentialTelemetry` —— 该配置是**关闭**下游 CLI 工具遥测用的，保留
- 全部代理 / 路由 / 仪表盘功能

---

## 构建 / 运行

```bash
npm install
npm run build      # next build --webpack + 拷贝 standalone 资源
npm start          # node custom-server.js → http://localhost:20128
# 开发
npm run dev        # next dev --port 20127
```

部署方式（本地 / Docker / VPS）与上游一致，见原 README 备份或 `gitbook/`。

---

## 免责声明

- 本仓库**仅供学习与代码参考**，不用于任何商业或生产用途。
- 代码版权归上游作者 **decolua/9router**（MIT License）及其致谢项目（CLIProxyAPI / RTK / Caveman / Ponytail 等）所有，LICENSE 文件随源码保留。
- 使用者须自行遵守所在国家/地区法律法规及各 AI 供应商的服务条款，**本仓库作者不承担任何责任**。
- 若上游作者或任何权利人认为本仓库构成侵权，**请随时联系删除**：通过本仓库 GitHub Issues 或邮箱 `cyb2831173936@163.com` 联系，我会尽快处理。

---

## License

MIT License — 见 [LICENSE](LICENSE)。上游项目为 MIT，本仓库沿用同一协议。
