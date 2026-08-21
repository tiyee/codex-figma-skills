---
name: figma-to-wxa-skyline
description: Use Codex to implement selected Figma screens and components as native WeChat Mini Program UI using the Skyline renderer and glass-easel. Use for Figma-to-code work targeting WXML, WXSS, JS/TS, Skyline scrolling, Worklet motion, and native Mini Program validation. Requires the official Codex Figma plugin and the complete wechat-miniprogram/skyline-skills package. Do not use for WebView, Taro, uni-app, Remax, web output, or writing designs back to Figma.
---

# Figma to WXA Skyline

Turn exact Figma frames and components into maintainable native WeChat Mini Program pages that run with Skyline and glass-easel. This skill owns design evidence, repository integration, implementation scope, visual comparison, and delivery. Delegate version-sensitive Skyline mechanics to the required official Skyline skills.

## Required dependencies

### Official Codex Figma plugin

The official Figma plugin published by OpenAI is mandatory. Before retrieving design context, verify that the plugin is installed in Codex, connected to Figma, and has read access to every exact target node. If the plugin, connection, or permission is missing, stop before editing application code; tell the user to install or connect the official Figma plugin in Codex and grant access. Do not substitute browser automation, a generic MCP server, or another host's Figma integration.

### Official Skyline skills

The complete [`wechat-miniprogram/skyline-skills`](https://github.com/wechat-miniprogram/skyline-skills) package is mandatory. Before implementation, verify these skills are installed and available:

- `skyline-overview`
- `skyline-config`
- `skyline-components`
- `skyline-wxss`
- `skyline-worklet`
- `skyline-route`
- `skyline-scroll-api`

If any are missing, stop before editing application code and install the complete package:

```bash
npx skills add wechat-miniprogram/skyline-skills
```

Do not copy their compatibility tables or detailed API guidance into the target repository. Load the installed version so decisions match the current Skyline guidance.

## Scope boundary

- Output native Mini Program source: WXML, WXSS, JSON, JavaScript or TypeScript, plus local assets and project documentation already required by the repository.
- The target page must use Skyline and glass-easel. Do not produce Taro, uni-app, Remax, React, Vue, HTML/CSS, or WebView implementation through this skill.
- An explicitly requested migration of the target page or package into Skyline is in scope. A whole-application renderer migration is not implied by a request to implement one Figma frame.
- Do not edit the source Figma file, upload code, submit a preview, or release a Mini Program unless separately authorized.
- Do not ship a rendered Figma frame as the page implementation or claim browser output proves Skyline behavior.

## Source-of-truth model

Use the source that owns each kind of fact:

- the current user request owns task scope and acceptance intent;
- applicable repository instructions such as `AGENTS.md` own project-local workflow, architecture, documentation, and validation rules;
- the exact selected Figma node and its screenshot own visual and prototype evidence;
- `app.json`, page JSON, project configuration, registered source files, and direct dependencies own runtime behavior;
- existing repository design/implementation notes own recorded decisions, but do not override newer working code or the confirmed Figma node;
- confirmed API contracts, services, models, and adapters own remote data shapes; mock and fixture data do not.

When sources conflict, keep the change reversible and scoped, preserve unrelated working behavior, update stale documentation only when the repository treats it as maintained, and disclose unresolved product decisions.

## Skill routing

Before the first Figma design-to-code operation, load `figma-design-to-code` from the official Codex Figma plugin before retrieving design context.

For every implementation task, load:

- `skyline-config` for renderer, glass-easel, application/page JSON, custom navigation, and scroll ownership;
- `skyline-components` for WXML component selection, text, images, forms, lists, `scroll-view`, and Skyline-native layout components;
- `skyline-wxss` before writing or reviewing WXSS.

Load additionally when applicable:

- `skyline-overview` when the target is not already Skyline, support/migration must be assessed, or fallback behavior matters;
- `skyline-worklet` for gesture-linked, scroll-linked, spring/decay, or other UI-thread motion;
- `skyline-route` for custom transitions, return gestures, half-screen routes, or container transitions;
- `skyline-scroll-api` for programmatic scrolling, refresh, two-level pull-down, or draggable-sheet control.

Read [references/implementation-guide.md](references/implementation-guide.md) before editing. Read [references/qa-checklist.md](references/qa-checklist.md) before delivery.

## Workflow

### 1. Confirm dependency, destination, and renderer scope

Verify the official Codex Figma plugin and the official Skyline skill package first. Then identify:

- the exact Figma file, page, frame/component node, variants, theme, and reference viewport;
- the native Mini Program root and target page/component paths;
- every applicable repository instruction file and any required pre-implementation artifact such as a page specification or design wiki;
- whether Skyline is enabled globally, by package, or by page;
- current `renderer`, `componentFramework`, `lazyCodeLoading`, `rendererOptions`, page navigation/scroll configuration, base-library target, and DevTools settings;
- required navigation, data, interactions, states, motion, assets, and acceptance criteria;
- available repository checks, WeChat DevTools access, and real-device access.

If the repository is Taro, uni-app, Remax, or another non-native source project, report that this skill is not the correct implementation path instead of silently converting its architecture. If the repository is native WebView and the requested target is Skyline, load `skyline-overview` and `skyline-config`, assess only the requested page/package, and surface migration choices that materially affect other pages.

### 2. Inspect exact Figma and repository evidence

Retrieve design context and a rendered image for every exact target node. Inspect variables, styles, component properties, text, assets, constraints, Auto Layout, clipping, scroll regions, overlays, and prototype connections. Do not start from file metadata or a neighboring frame when a specific node is required.

Read the smallest relevant repository set:

- applicable repository instructions from the repository root through the target path;
- application, package, page, and project JSON configuration;
- the registered target page and its direct dependencies;
- comparable Skyline pages and shared glass-easel components;
- global/local tokens and WXSS conventions;
- services, models, fixtures, state helpers, and tests used by the flow;
- maintained page/design notes and project instructions.

Check `git status` before editing and preserve unrelated user changes.

Summarize the project-local contract before planning: maintained source stack, page registry, documentation gates, design viewport/unit policy, navigation and scroll conventions, shared tokens/components/assets, mock-versus-service boundaries, and checks that actually exist. Project instructions can specialize this workflow, but values from one repository must not become universal Skyline assumptions.

### 3. Build an evidence and responsibility map

Map:

1. Figma frames and prototype links → registered pages, components, overlays, navigation, or unresolved behavior.
2. Auto Layout and constraints → Skyline Flex structure, fixed versus scrolling regions, safe areas, clipping, and content growth.
3. Figma components and variants → existing or new glass-easel components, properties, slots, events, and states.
4. Variables/styles → existing semantic tokens or scoped additions.
5. Text/content → WXML text nodes, bindings, localization, formatting, wrapping, truncation, and empty values.
6. Images/vectors → reusable assets, Figma exports, supported local SVG/raster assets, native components, or disclosed substitutes.
7. Prototype motion → static states, Worklet motion, Skyline route transitions, programmatic scroll, or an unresolved product decision.

Label each item as observed, repository-derived, inferred, or unknown. Figma proves appearance and visible state; it does not prove API fields, authorization, payment success, analytics, or production readiness.

### 4. Plan the Skyline page model

Before editing, decide:

- application/package/page configuration ownership;
- custom navigation and status/menu-button safe-area handling;
- the page's explicit `scroll-view` model and type, fixed regions, sticky behavior, nested scrolling, refresh, and keyboard interaction;
- Flex hierarchy, unit conversion, typography, tokens, component boundaries, assets, and state ownership;
- whether motion belongs in ordinary state transitions, Worklet, a Skyline route, or scroll APIs;
- the smallest code, configuration, asset, documentation, and validation change.

If the repository requires a page specification, UI wiki, or another artifact before implementation, create or update it first and keep it synchronized with structural, asset, state, or interaction decisions. Do not introduce such a documentation gate into a repository that does not already require one.

Follow the loaded official skills for current Skyline capabilities. Do not infer support from browser CSS or copy Figma coordinates into absolute positioning. Do not broaden page-level configuration into a global renderer migration unless the user requested it and the affected pages were assessed.

### 5. Implement native Skyline structure

- Configure the target as Skyline/glass-easel using `skyline-config`; preserve compatible existing options rather than replacing configuration wholesale.
- Use WXML, WXSS, page/component JSON, and JS/TS following the repository's native conventions.
- Use the explicit local scrolling model required by Skyline; do not rely on page-global scrolling or browser overflow behavior.
- Select `scroll-view`, list/grid/sticky/nested components, text truncation, image modes, inputs, and other primitives through `skyline-components`.
- Validate every non-trivial WXSS property/value through `skyline-wxss`; use Flex and Skyline components for unsupported web layout features.
- Keep visible text in supported text components, repeated data keyed by stable business identity, and component APIs semantic.
- Keep WXML declarative and structurally meaningful: no bare visible text in layout containers, empty spacing nodes, or responsibility-free wrappers; register every custom component and page at the repository-appropriate scope.
- Reuse established navigation/header components and route conventions when their responsibility matches; preserve safe-area/back behavior and handle navigation failures without inventing destinations.
- Reuse components, tokens, request clients, and assets when their responsibilities match. Do not force reuse across incompatible behavior or silently change shared consumers.
- Keep inherently photographic/illustrative content as scoped assets, but rebuild UI chrome, text, controls, and layout as editable source.

### 6. Implement states, behavior, and motion

Implement every state visible in the selected Figma scope plus states explicitly required by the task. Keep fixtures isolated from production services and never describe a simulated result as a connected backend capability.

Follow the repository's established data layers and request wrapper. Classify visible behavior as real integration, fixture/mock, local prototype state, placeholder, or unresolved; do not infer a backend contract from Figma, a design note, or a working mock.

For asynchronous flows, handle the relevant loading, success, empty, failure, retry, and completion paths; prevent duplicate actions and stale responses; dispose of owned timers, listeners, Worklet bindings, and other side effects on unload.

Use `skyline-worklet` only when motion needs UI-thread response. Use `skyline-route` only when the design calls for a page transition or gesture that the route system owns. Use `skyline-scroll-api` only for programmatic scroll behavior. Do not implement high-frequency gesture/scroll motion with repeated `setData`.

### 7. Validate static structure, Skyline runtime, and fidelity

Run only commands discovered from repository configuration. If the project has no package scripts or test runner, do not invent them.

At minimum:

- parse changed JSON and verify registered pages, components, imports, and asset paths;
- verify that repository-mandated design/implementation notes exist in the required order and agree with the final source;
- check Skyline/glass-easel and page navigation/scroll configuration through `skyline-config`;
- inspect WXML structure, supported components, text nodes, list keys, scroll ownership, and bindings through `skyline-components`;
- check changed WXSS through `skyline-wxss` and its prescribed tooling when available and authorized;
- run repository lint/type/tests/build steps that actually exist;
- compile in WeChat DevTools with the target Skyline/base-library settings when accessible;
- compare an implementation capture with the exact Figma node at the same logical viewport;
- check relevant iOS and Android sizes, safe areas, custom navigation, scrolling, keyboard, long text, and requested states;
- verify Worklet, route, and scroll behavior on a real device when their correctness depends on device input or rendering.

Static checks, DevTools compilation, simulator comparison, and real-device validation are separate evidence. Never claim one from another.

### 8. Deliver with evidence

Report:

- the Figma file/node and implemented page/component entry points;
- Skyline/glass-easel configuration added or reused;
- official Skyline skills loaded for the task;
- components, tokens, assets, states, interactions, scrolling, and motion completed;
- commands, DevTools targets, screenshots, and devices actually used;
- assumptions, substitutions, intentional differences, unresolved integrations, and unverified runtime behavior.

## Completion definition

Complete means the selected Figma scope is implemented as registered native Skyline/glass-easel source; required official Skyline skills informed the implementation; configuration, WXML, WXSS, scrolling, components, assets, data states, and motion are consistent; the result was compared with the exact design; available repository and Skyline checks ran; DevTools/device gaps are explicit; and no unrelated renderer migration, Figma write, credential, upload, submission, or release occurred.
