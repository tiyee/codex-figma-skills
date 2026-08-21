# Snapshot to Figma

[简体中文](README.md) | [English](README.en.md)

一个面向 Codex 的 Agent Skill，用于把截图、视觉稿和其他 UI 参考图重建为可编辑、可维护的 Figma 设计。

它兼顾视觉还原与生产级结构，包括语义化图层、Auto Layout、可复用组件、设计令牌、响应式行为、渲染对比和无障碍检查。把一张扁平截图直接放入 Figma 不视为完成设计。

## 安装

先在 Codex 的插件目录中安装 OpenAI 发布的官方 **Figma** 插件，连接 Figma 账号，并确认插件对目标文件具有写入权限。插件未安装、未连接或权限不足时，本 skill 不会执行 Figma 写入，也不能把规格说明当作已交付设计。

再安装本 skill。

使用 npm：

```bash
npx skills add tiyee/codex-figma-skills --path skills/snapshot-to-figma
```

使用 pnpm：

```bash
pnpm dlx skills add tiyee/codex-figma-skills --path skills/snapshot-to-figma
```

执行首次 Figma 操作前，skill 会按任务加载官方插件提供的 `figma-use`、`figma-generate-design`、`figma-generate-library` 或 `figma-create-new-file` 等指令。

## 使用示例

```text
把这些移动端截图转换为现有 Figma 文件中的可编辑页面。
在 Figma 中重建这个仪表盘视觉稿，并复用当前组件。
把这些浅色和深色状态图转换为可维护的组件集与页面流程。
在 Figma 中匹配这张截图，然后比较渲染结果并修复可见差异。
```

## 工作流

1. 将源图片映射到页面、状态、主题、断点和滚动位置。
2. 写入前检查项目设计规则和目标 Figma 文件。
3. 识别项目要求的设计伴生文档、索引和共享资产影响范围。
4. 将扁平像素转换为语义化布局树和还原策略。
5. 使用 Auto Layout、变量、样式、组件和可编辑资源进行重建。
6. 只添加源图或项目需求支持的状态与交互。
7. 在最终视觉验收前，通过分层、布局、尺寸/定位和变量绑定门禁，并重新比较渲染结果。
8. 对共享资产变更执行消费页面回归，并完成项目要求的交付文档。

## 边界

- 除非用户单独要求，否则不实现应用代码。
- 不把完整截图作为最终设计实现。
- 未检查范围和使用方前，不创建或修改共享 Figma 资产。
- 大范围修改存量设计时，在方案通过结构与视觉核验前保留现有可用版本。
- 不假定固定品牌、画板尺寸、文件、页面结构或文档目录。
- 未做渲染对比时，不声称达到像素级精度。

## 目录结构

```text
snapshot-to-figma/
├── SKILL.md
├── README.md
├── README.en.md
├── evals/
│   └── evals.json
└── references/
    ├── reconstruction-guide.md
    └── qa-checklist.md
```

## 许可证

MIT
