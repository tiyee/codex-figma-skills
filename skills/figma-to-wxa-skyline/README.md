# Figma to WXA Skyline

[简体中文](README.md) | [English](README.en.md)

一个 Agent Skill，用于把指定的 Figma 页面和组件实现为使用 Skyline 渲染引擎及 glass-easel 的原生微信小程序页面。

该 skill 负责协调 Figma 证据、原生 WXML/WXSS/JS/TS 实现、Skyline 配置、组件与滚动模型选择、Worklet/路由行为、视觉对比和小程序验证。

## 必需依赖

### Codex 官方 Figma 插件

先在 Codex 的插件目录中安装 OpenAI 发布的官方 **Figma** 插件，连接 Figma 账号，并确认插件能够读取所有目标节点。插件未安装、未连接或权限不足时，本 skill 会在修改小程序代码前停止，不能用浏览器自动化、通用 MCP 服务或其他宿主的 Figma 集成替代。

### 微信官方 Skyline skills

必须先安装完整的微信官方 Skyline skills。仅安装其中一部分不能满足该工作流。

```bash
npx skills add wechat-miniprogram/skyline-skills
```

该包提供：

- `skyline-overview`
- `skyline-config`
- `skyline-components`
- `skyline-wxss`
- `skyline-worklet`
- `skyline-route`
- `skyline-scroll-api`

然后安装本 skill：

```bash
npx skills add tiyee/codex-figma-skills --path skills/figma-to-wxa-skyline
```

也可以使用 pnpm 安装本仓库 skill：

```bash
pnpm dlx skills add tiyee/codex-figma-skills --path skills/figma-to-wxa-skyline
```

Codex 还需要具有目标原生小程序仓库的写入权限。完整运行时验证需要微信开发者工具和真机。

## 使用示例

```text
用 figma-to-wxa-skyline 把这个 Figma 首页实现到现有 Skyline 小程序中。
把这些 Figma 卡片转换为可复用的 glass-easel 组件，并集成到当前 Skyline 页面。
使用 Skyline scroll-view 实现这个 Figma 列表，并补齐加载、空态、错误态和渲染对比。
使用 Worklet 还原这个 Figma 交互，并在真机上验证。
```

## 工作流

1. 确认 Codex 官方 Figma 插件已安装、已连接且能够读取准确目标节点，同时确认已经安装完整的微信官方 Skyline skills。
2. 读取适用的 `AGENTS.md` 等仓库指令，确认页面注册、前置文档、设计基准、复用约定、数据边界和真实可用的验证方式。
3. 确认准确的 Figma 节点、原生小程序目标、Skyline 配置、任务范围和验证环境。
4. 加载 `skyline-config`、`skyline-components` 和 `skyline-wxss`；迁移、Worklet、路由或程序化滚动按需加载对应 skill。
5. 把 Figma 布局、WXML、组件、导航、样式、资源、状态和原型行为映射为原生 Skyline 职责；仓库要求 UI Wiki 或页面规格先行时，先完成并在实现中同步维护。
6. 实现已注册的 WXML/WXSS/JSON/JS/TS 页面和 glass-easel 组件。
7. 运行当前环境真实存在的静态检查、官方 Skyline 检查、仓库检查和微信开发者工具编译。
8. 将 Skyline 渲染结果与准确的 Figma 节点比较，并验证设备相关行为。
9. 报告验证证据、假设、差异和未验证项。

实施指南和 QA 清单进一步覆盖 WXML 结构与文本节点、组件契约和注册、导航与失败分支、WXSS 单位/令牌/Flex/文本/隔离/兼容性，以及静态检查、Skyline 工具、开发者工具、视觉对比和真机证据分层。

## 边界

- 只生成原生 Skyline/glass-easel 小程序源码。
- 不生成 WebView、Taro、uni-app、Remax、React、Vue 或 Web 实现。
- 一个页面需要 Skyline 时，不擅自迁移整个应用。
- 不把扁平 Figma 截图作为页面实现。
- 不编造 API、凭据、支付/授权成功结果、包管理脚本、测试、真机结果或发布状态。
- 不把某个项目的 UI Wiki、750 稿换算、导航组件或数据分层约定擅自推广为所有 Skyline 项目的默认规则。
- 未经单独授权，不编辑 Figma、不上传代码，也不发布小程序。

## 目录结构

```text
figma-to-wxa-skyline/
├── SKILL.md
├── README.md
├── README.en.md
├── evals/
│   └── evals.json
└── references/
    ├── implementation-guide.md
    └── qa-checklist.md
```

## 许可证

MIT
