# figma-skills

[简体中文](README.md) | [English](README.en.md)

面向 Codex 的 Figma 设计生产与设计还原工作流。两个 skill 都依赖 Codex 官方 Figma 插件提供的 Figma 读取、写入和设计上下文能力。

本仓库聚焦两条链路：

- **图片 → Figma**：把截图、视觉稿或参考图重建为可编辑、可维护的 Figma 设计。
- **Figma → WXA Skyline**：把 Figma 页面和组件实现为原生微信小程序 Skyline 页面。

## Skills

| Skill | 用途 | 主要产物 |
| --- | --- | --- |
| [`snapshot-to-figma`](skills/snapshot-to-figma/README.md) | 从截图或视觉参考重建 Figma 页面/组件 | 语义化图层、Auto Layout、变量、组件与视觉对比结果 |
| [`figma-to-wxa-skyline`](skills/figma-to-wxa-skyline/README.md) | 将 Figma 设计实现到 Skyline 小程序 | 原生 WXML/WXSS/JS/TS、glass-easel 组件、资源、状态与验证结果 |

## 安装

### 1. 安装 Codex 官方 Figma 插件

在 Codex 的插件目录中搜索并安装 OpenAI 发布的 **Figma** 插件，然后连接 Figma 账号。执行 skill 前，请确认插件可以访问目标 Figma 文件；`snapshot-to-figma` 还需要写入权限。

插件未安装、未连接或权限不足时，skill 必须停止 Figma 操作，且不能声称已经完成设计或设计还原。

### 2. 安装 Agent Skills

安装 `snapshot-to-figma`：

```bash
npx skills add tiyee/codex-figma-skills --path skills/snapshot-to-figma
```

安装 `figma-to-wxa-skyline` 时，必须先安装完整的微信官方 Skyline skills，再安装本仓库 skill：

```bash
npx skills add wechat-miniprogram/skyline-skills
npx skills add tiyee/codex-figma-skills --path skills/figma-to-wxa-skyline
```

不能只安装其中一部分；该包提供 Skyline 配置、组件、WXSS、Worklet、路由和滚动 API 的版本化规则。

安装本仓库 skill 时也可使用 pnpm（官方 Skyline 依赖仍按上面的命令先安装）：

```bash
pnpm dlx skills add tiyee/codex-figma-skills --path skills/snapshot-to-figma
pnpm dlx skills add tiyee/codex-figma-skills --path skills/figma-to-wxa-skyline
```

安装后，Codex 可以根据 `SKILL.md` 的 `name` 和 `description` 自动发现能力，也可以显式点名 skill。

## 使用示例

### 图片转 Figma

```text
用 snapshot-to-figma 把这些移动端截图还原到现有 Figma 文件，复用已有组件并做渲染对比。
把这张后台页面参考图重建成可编辑的 Figma 页面，不要把整张图当背景。
```

### Figma 转 WXA Skyline

```text
用 figma-to-wxa-skyline 实现这个 Figma 页面，接入当前 Skyline 小程序项目。
把这些 Figma 组件实现成可复用的 glass-easel 小程序组件，并补齐加载、空态和错误态。
```

## 设计原则

- 本仓库 skill 以 Codex 为目标运行环境，并把 Codex 官方 Figma 插件作为 Figma 工作流的硬依赖。
- skill 会在首次 Figma 操作前加载官方插件提供的对应 Figma 指令，并验证连接与目标文件权限。
- `figma-to-wxa-skyline` 以完整的 `wechat-miniprogram/skyline-skills` 为硬依赖，不在本仓库复制其易变化的平台规则。
- `figma-to-wxa-skyline` 会先读取目标仓库的项目指令和事实源，再遵循其页面注册、文档门禁、设计基准、复用体系、数据边界与验证约定。
- 先检查目标 Figma 文件或代码仓库，再决定复用、扩展或新建，避免覆盖已有设计系统和工程约定。
- `snapshot-to-figma` 会把项目要求的设计文档视为同次交付，并在修改共享资产时检查影响范围、保留可用现状并执行消费页面回归。
- 不以“看起来像”为唯一完成标准：交付前同时检查可维护结构、视觉还原、交互状态、平台约束与验证证据。
- 不伪造不可访问的 Figma 内容、后端接口、密钥、上传或发布结果。

## 仓库结构

```text
figma-skills/
├── AGENTS.md
├── README.md
├── README.en.md
└── skills/
    ├── snapshot-to-figma/
    │   ├── SKILL.md
    │   ├── README.md
    │   ├── README.en.md
    │   ├── references/
    │   └── evals/
    └── figma-to-wxa-skyline/
        ├── SKILL.md
        ├── README.md
        ├── README.en.md
        ├── references/
        └── evals/
```

## 贡献与验证

新增或修改 skill 时，请保持目录名与 `SKILL.md` 的 `name` 一致，并同步更新用户可见文档和行为评测。提交前至少执行：

```bash
git diff --check
git status --short
rg --files skills
```

本仓库目前没有统一的构建或测试 runner；详细约束见 [`AGENTS.md`](AGENTS.md)。

## 许可证

MIT
