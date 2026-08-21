# Snapshot to Figma

[简体中文](README.md) | [English](README.en.md)

A Codex Agent Skill for reconstructing screenshots, mockups, and other UI reference images as editable, maintainable Figma designs.

It balances visual fidelity with production-quality structure: semantic layers, Auto Layout, reusable components, design tokens, responsive behavior, rendered comparison, and accessibility checks. It does not treat a flattened screenshot placed in Figma as a completed design.

## Installation

First install the official **Figma** plugin published by OpenAI from the Codex plugin directory, connect your Figma account, and confirm that the plugin has write access to the target file. If the plugin is missing, disconnected, or lacks permission, this skill will not write to Figma and will not treat a specification as a delivered design.

Then install this skill.

Using npm:

```bash
npx skills add tiyee/figma-skills --path skills/snapshot-to-figma
```

Using pnpm:

```bash
pnpm dlx skills add tiyee/figma-skills --path skills/snapshot-to-figma
```

Before the first Figma operation, the skill loads the applicable instructions supplied by the official plugin, such as `figma-use`, `figma-generate-design`, `figma-generate-library`, or `figma-create-new-file`.

## Example requests

```text
Convert these mobile screenshots into editable Figma screens in our existing file.
Reconstruct this dashboard mockup in Figma and reuse our current components.
Turn these light and dark state images into a maintainable component set and screen flow.
Match this screenshot in Figma, then compare the rendered result and fix visible differences.
```

## Workflow

1. Map source images to screens, states, themes, breakpoints, and scroll positions.
2. Inspect project design rules and the target Figma file before writing.
3. Identify required companion documentation, indexes, and the impact surface of shared assets.
4. Translate flat pixels into a semantic layout tree and fidelity strategy.
5. Reconstruct with Auto Layout, variables, styles, components, and editable assets.
6. Add only the states and interactions supported by the source or project requirements.
7. Pass layer, layout, sizing/positioning, and system-binding gates before final visual approval, then compare the rendered result again.
8. Regression-check shared-asset consumers and complete project-required handoff documentation.

## Boundaries

- Does not implement application code unless separately requested.
- Does not embed a full screenshot as the final design.
- Does not create or modify shared Figma assets without checking scope and consumers.
- Preserves a usable current version during broad revisions until the proposal passes structural and visual checks.
- Does not assume a fixed brand, frame size, file, page structure, or documentation directory.
- Does not claim pixel accuracy without a rendered comparison.

## Structure

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

## License

MIT
