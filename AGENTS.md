# AGENTS.md

本文件适用于仓库根目录及其所有子目录。当前仓库没有更深层的 `AGENTS.md`。

## 仓库定位

这是一个用于沉淀和发布 Figma 工作流 Agent Skills 的文档型仓库，面向 Codex，并以 Codex 官方 Figma 插件作为 Figma 读写能力的硬依赖。仓库当前没有应用代码、依赖清单、构建系统或自动化测试 runner。

当前发布的 skill：

- `skills/snapshot-to-figma/`：把截图、视觉稿或参考图重建为可编辑、可维护的 Figma 设计。
- `skills/figma-to-wxa-skyline/`：把 Figma 页面和组件实现为原生微信小程序 Skyline/glass-easel 代码。

运行任一 skill 前，必须在 Codex 中安装 OpenAI 发布的官方 Figma 插件、连接 Figma 账号，并授予目标文件所需的读写权限。

安装单个 skill：

```bash
npx skills add tiyee/codex-figma-skills --path skills/<skill-name>
```

## 目录约定

每个 skill 位于 `skills/<skill-name>/`，目录名使用小写 kebab-case。

```text
skills/<skill-name>/
├── SKILL.md              # 必需：发现信息与核心工作流
├── README.md             # 可选：英文安装、用法与边界，顶部链接中文版
├── README.zh-CN.md       # 有 README.md 时必需：中文版本，顶部链接英文版
├── agents/               # 可选：客户端元数据；不能作为核心行为依赖
├── references/           # 可选：按需加载的详细指南或检查清单
├── scripts/              # 可选：确定性的辅助脚本
└── evals/                # 可选：声明式行为评测
```

## 修改和新增 skill

1. 先完整阅读目标 skill 的 `SKILL.md`、`README.md` 和 `README.zh-CN.md`，再按正文路由读取相关 `references/` 和 `evals/`。
2. `SKILL.md` 必须以 YAML frontmatter 开始，至少包含 `name` 和 `description`；`name` 与目录名一致，`description` 应准确说明能力、触发场景和必要边界。
3. 把共同目的、关键决策、核心工作流和安全边界留在 `SKILL.md`；把平台细节、长检查清单和低频步骤放入 `references/`，并明确加载时机。
4. 所有路径引用相对于 skill 目录。skill 不得依赖本仓库绝对路径或未声明的其他 skill。
5. 所有依赖 Figma 读写的工作流必须先验证 Codex 官方 Figma 插件已安装、已连接且具有目标文件所需权限，并按场景加载插件提供的 Figma skill；缺少插件或权限时必须停止 Figma 操作，不得声称已交付 Figma 结果。
6. 用户可见能力、安装方式、目录结构或边界变化时，同步更新对应 README 和根 README。
7. 可示例化的行为变化应新增或更新 `evals/evals.json`。评测应检查决策与可观察结果，不要只匹配标题或固定措辞。
8. 不提交真实 AppID、API key、token、账号信息、私有 Figma 链接、本机绝对路径、`.DS_Store` 或生成的临时文件。
9. `figma-to-wxa-skyline` 必须同时保留 Codex 官方 Figma 插件，以及完整 `wechat-miniprogram/skyline-skills` 包的硬依赖和七个官方 skill 的场景路由；不要复制其完整兼容性表或用本仓库内容替代官方包。
10. 所有 `README.md` 使用英文，配套 `README.zh-CN.md` 使用中文；两者顶部必须提供语言切换链接，英文版使用 `[English](README.md) | [简体中文](README.zh-CN.md)`，中文版使用 `[简体中文](README.zh-CN.md) | [English](README.md)`，用户可见内容变化时同步维护。`SKILL.md` 保持英文，作为 Codex 的运行时 skill 指令。

## 内容质量要求

- 指令应具体、可执行，避免重复 Codex 已经具备的通用编程常识。
- 明确默认行为是读取、写入 Figma、修改代码还是仅输出规格；外部发布、上传、共享资产修改和危险操作必须保留用户授权边界。
- 先检查现有设计系统或工程约定，再决定复用、扩展或新建，不得为了视觉捷径破坏共享组件或重写项目技术栈。
- Figma 还原类 skill 必须同时覆盖设计上下文读取、结构/资源映射、视觉对比和交付定位。
- Skyline 实现类 skill 必须同时覆盖原生小程序结构、Skyline/glass-easel 配置、WXML/WXSS 兼容性、滚动与安全区、数据与状态边界、开发者工具/真机验证和残余风险。
- 引用文件名、命令、参数和输出模板前，确认它们确实存在。
- 优先链接官方资料并只固化稳定规则，不复制会频繁过时的整段平台文档。

## 验证方式

本仓库没有统一的 build、lint 或 test 命令。提交前至少执行：

```bash
git diff --check
git status --short
rg --files skills
```

并人工检查：

- 每个 skill 都有可解析的 YAML frontmatter，且 `name`、目录名和 README 描述一致。
- `SKILL.md` 中引用的 `references/`、`scripts/`、`evals/` 文件都存在。
- README 列出的 skill、能力、目录和安装命令与仓库实际内容一致。
- 每个 README 中英文版本都存在切换链接，章节、安装命令、能力和边界保持语义一致。
- JSON/YAML 语法有效，Markdown 链接、代码块和相对路径没有明显错误。
- 变更只包含必要源文件，没有缓存、构建产物、密钥或复制来源遗留信息。

对 `snapshot-to-figma` 的修改，还应检查 Codex 官方 Figma 插件前置、“不可用整张截图冒充完成结果”、设计系统复用、Auto Layout、渲染对比和精确交付位置。

对 `figma-to-wxa-skyline` 的修改，还应检查 Codex 官方 Figma 插件前置、完整 `wechat-miniprogram/skyline-skills` 安装前置、七个官方 skill 路由、能力边界只覆盖原生 Skyline/glass-easel、Figma 证据映射、Skyline 配置与兼容性、资源复用、状态实现、开发者工具/真机验证和“不伪造后端或发布结果”。

如本机可访问系统 `skill-creator` 的验证脚本，可额外对每个 skill 运行 `quick_validate.py`；该检查只验证结构和 frontmatter，不能替代行为审查。

## 交付与发布

提交前查看完整差异：

```bash
git diff --stat
git diff -- README.md AGENTS.md skills/<skill-name>
```

仓库当前未定义 CI、发布脚本或版本号更新流程，不要凭空引入发布步骤或修改版本元数据。对外发布前，优先按 `npx skills add tiyee/codex-figma-skills --path skills/<skill-name>` 验证目标 skill 能否独立安装和使用。
