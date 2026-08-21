# figma-skills

[简体中文](README.md) | [English](README.en.md)

Figma production and design-implementation workflows for Codex. Both skills require the official Codex Figma plugin for Figma reads, writes, and design context.

This repository focuses on two workflows:

- **Image → Figma**: reconstruct screenshots, visual mockups, or reference images as editable, maintainable Figma designs.
- **Figma → WXA Skyline**: implement Figma screens and components as native WeChat Mini Program pages using Skyline.

## Skills

| Skill | Purpose | Main deliverables |
| --- | --- | --- |
| [`snapshot-to-figma`](skills/snapshot-to-figma/README.en.md) | Reconstruct Figma screens/components from screenshots or visual references | Semantic layers, Auto Layout, variables, components, and rendered comparison |
| [`figma-to-wxa-skyline`](skills/figma-to-wxa-skyline/README.en.md) | Implement Figma designs in a Skyline Mini Program | Native WXML/WXSS/JS/TS, glass-easel components, assets, states, and validation evidence |

## Installation

### 1. Install the official Codex Figma plugin

In the Codex plugin directory, find and install the **Figma** plugin published by OpenAI, then connect your Figma account. Before running either skill, confirm that the plugin can access the target Figma file; `snapshot-to-figma` also requires write access.

If the plugin is missing, disconnected, or lacks the required permission, the skill must stop Figma operations and must not claim that the design or implementation was delivered.

### 2. Install the Agent Skills

Install `snapshot-to-figma`:

```bash
npx skills add tiyee/figma-skills --path skills/snapshot-to-figma
```

For `figma-to-wxa-skyline`, first install the complete official WeChat Skyline skills package, then install this repository skill:

```bash
npx skills add wechat-miniprogram/skyline-skills
npx skills add tiyee/figma-skills --path skills/figma-to-wxa-skyline
```

Do not install only part of the official package. It provides versioned guidance for Skyline configuration, components, WXSS, Worklet, routing, and scroll APIs.

You may use pnpm to install this repository's skills after installing the official Skyline dependency with the command above:

```bash
pnpm dlx skills add tiyee/figma-skills --path skills/snapshot-to-figma
pnpm dlx skills add tiyee/figma-skills --path skills/figma-to-wxa-skyline
```

Codex can discover an installed skill from the `name` and `description` in `SKILL.md`, or invoke it explicitly.

## Example requests

### Image to Figma

```text
Use snapshot-to-figma to reconstruct these mobile screenshots in our existing Figma file, reuse current components, and compare the rendered output.
Rebuild this admin dashboard reference as an editable Figma screen; do not use the full image as a background implementation.
```

### Figma to WXA Skyline

```text
Use figma-to-wxa-skyline to implement this Figma screen in our existing Skyline Mini Program.
Turn these Figma components into reusable glass-easel components and add loading, empty, and error states.
```

## Design principles

- These skills target Codex and require the official Codex Figma plugin for every Figma workflow.
- Before the first Figma operation, each skill loads the applicable instructions provided by the official plugin and verifies the connection and target-file permissions.
- `figma-to-wxa-skyline` requires the complete `wechat-miniprogram/skyline-skills` package instead of copying its version-sensitive platform rules into this repository.
- `figma-to-wxa-skyline` reads the target repository's instructions and facts first, then follows its page registry, documentation gates, design baseline, reuse system, data boundaries, and validation conventions.
- Inspect the target Figma file or codebase before deciding whether to reuse, extend, or create assets and components.
- `snapshot-to-figma` treats project-required design documentation as part of the same delivery and checks impact, preserves usable current work, and regression-tests consumers when shared assets change.
- Visual similarity alone is not completion: verify maintainable structure, fidelity, interaction states, platform constraints, and validation evidence.
- Never fabricate inaccessible Figma content, backend contracts, credentials, uploads, submissions, or release results.

## Repository structure

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

## Contributing and validation

Keep each skill directory name aligned with the `name` in its `SKILL.md`. When user-visible behavior changes, update both language versions of the relevant README and the behavioral evaluations.

Run at least:

```bash
git diff --check
git status --short
rg --files skills
```

This repository currently has no unified build or test runner. See [`AGENTS.md`](AGENTS.md) for the complete maintenance rules.

## License

MIT
