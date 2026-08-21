# Figma to WXA Skyline

[简体中文](README.md) | [English](README.en.md)

An Agent Skill for implementing selected Figma screens and components as native WeChat Mini Program pages using the Skyline renderer and glass-easel.

The skill coordinates Figma evidence, native WXML/WXSS/JS/TS implementation, Skyline configuration, component and scroll selection, Worklet/route behavior, visual comparison, and Mini Program validation.

## Required dependencies

### Official Codex Figma plugin

First install the official **Figma** plugin published by OpenAI from the Codex plugin directory, connect your Figma account, and confirm that the plugin can read every target node. If the plugin is missing, disconnected, or lacks permission, this skill stops before changing Mini Program code. Browser automation, a generic MCP server, or another host's Figma integration is not a substitute.

### Official WeChat Skyline skills

Install the complete official Skyline skill package first. Installing only selected sub-skills is not sufficient for this workflow.

```bash
npx skills add wechat-miniprogram/skyline-skills
```

It provides:

- `skyline-overview`
- `skyline-config`
- `skyline-components`
- `skyline-wxss`
- `skyline-worklet`
- `skyline-route`
- `skyline-scroll-api`

Then install this skill:

```bash
npx skills add tiyee/figma-skills --path skills/figma-to-wxa-skyline
```

Using pnpm for this repository skill:

```bash
pnpm dlx skills add tiyee/figma-skills --path skills/figma-to-wxa-skyline
```

Codex also needs write access to the target native Mini Program repository. WeChat DevTools and real devices are needed for full runtime validation.

## Example requests

```text
Use figma-to-wxa-skyline to implement this Figma home page in our existing Skyline Mini Program.
Turn these Figma cards into reusable glass-easel components and integrate them into this Skyline page.
Implement this Figma list with Skyline scroll-view, loading/empty/error states, and rendered comparison.
Recreate this Figma interaction using Worklet motion and verify it on device.
```

## Workflow

1. Verify that the official Codex Figma plugin is installed, connected, and able to read the exact target nodes, and that the complete official Skyline skill package is installed.
2. Read applicable repository instructions such as `AGENTS.md`, then identify the page registry, documentation gates, design baseline, reuse conventions, data boundaries, and checks that actually exist.
3. Resolve the exact Figma nodes, native Mini Program destination, Skyline configuration, scope, and validation environment.
4. Load `skyline-config`, `skyline-components`, and `skyline-wxss`; add migration, Worklet, route, or scroll skills only when relevant.
5. Map Figma layout, WXML, components, navigation, styles, assets, states, and prototype behavior to native Skyline responsibilities. When the repository requires a UI wiki or page specification first, complete it before code and keep it synchronized.
6. Implement registered WXML/WXSS/JSON/JS/TS pages and glass-easel components.
7. Run static checks, official Skyline checks, repository checks, and WeChat DevTools compilation that are actually available.
8. Compare the Skyline render with the exact Figma node and verify device-sensitive behavior.
9. Report evidence, assumptions, deviations, and unverified items.

The implementation guide and QA checklist further cover WXML structure and text nodes, component contracts and registration, navigation failure paths, WXSS units/tokens/Flex/text/isolation/compatibility, and separate evidence for static checks, Skyline tooling, DevTools, visual comparison, and real devices.

## Boundaries

- Produces native Skyline/glass-easel Mini Program source only.
- Does not produce WebView, Taro, uni-app, Remax, React, Vue, or web implementations.
- Does not silently migrate the whole application when one page needs Skyline.
- Does not use a flattened Figma screenshot as the page implementation.
- Does not invent APIs, credentials, payment/permission success, package scripts, tests, device results, or release status.
- Does not generalize one project's UI wiki, 750-unit conversion, navigation components, or data-layer conventions into defaults for every Skyline project.
- Does not edit Figma, upload code, or publish the Mini Program without separate authorization.

## Structure

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

## License

MIT
