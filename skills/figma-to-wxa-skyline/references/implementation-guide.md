# Figma to WXA Skyline Implementation Guide

Use this guide after the official Codex Figma plugin, connection, and exact-node read permission have been verified. Use the mandatory official `wechat-miniprogram/skyline-skills` package for current configuration, component, WXSS, Worklet, route, and scroll API mechanics.

## 1. Establish the implementation record

Read every applicable repository instruction file before using local examples as precedent. Turn those instructions and the maintained source into a compact project contract:

| Project concern | Inspect | Use in this task |
| --- | --- | --- |
| Maintained architecture | project instructions, source extensions, project config | Confirm native WXML/WXSS/JSON/JS or TS ownership |
| Page truth and destination | `app.json`, subpackages, target source | Resolve whether the page is registered and reachable |
| Documentation gate | required page specs, design wiki, implementation notes | Create/update in the mandated order and keep synchronized |
| Design baseline | exact Figma node, viewport, repository unit policy | Select the correct mobile/desktop variant and conversion basis |
| Reuse system | global styles, tokens, shared components, assets, comparable pages | Reuse only matching responsibilities and conventions |
| Data boundary | services, request wrapper, models, constants, mock/fixtures | Separate confirmed integration from prototype data |
| Validation | real scripts, Skyline tooling, DevTools/device access | Claim only checks actually performed |

Treat project-specific rules as local policy, not general Skyline law. For example, a repository may require a UI wiki before code, use `app.json` as its page registry, standardize custom navigation, or define `1px → 1rpx` for a confirmed 750-unit mobile frame. Follow those rules there, but do not copy them into unrelated projects without evidence.

Keep a compact evidence map:

| Evidence | Native Skyline target | Authority | Notes |
| --- | --- | --- | --- |
| Figma frame/component node | Registered page/component path | Exact node + repository | Theme, state, viewport |
| Auto Layout/constraint | Flex/scroll/fixed structure | Exact node + Skyline rules | Observed versus inferred |
| Figma variable/style | Existing/new semantic token | Repository first | Scope and fallback |
| Component variant | glass-easel property/event/slot/state | Design + code contract | Reuse decision |
| Prototype connection | Navigation/route/Worklet/scroll behavior | Prototype + product contract | Do not infer backend success |
| Image/vector | Local asset/native component/style shape | Figma + repository | Format, crop, package cost |

Record unresolved product behavior before coding around it. A visible control does not prove a route, permission, service response, or business rule.

If the repository requires page implementation notes before code, complete that artifact first. Update the existing note when the design or code changes materially. Do not introduce a wiki, naming convention, or documentation gate into a repository that does not already use one.

## 2. Pass the native Skyline gate

This skill targets native Mini Program source. Confirm that maintained source uses WXML/WXSS/JSON/JS or TS rather than a framework compiler. If Taro, uni-app, Remax, React, Vue, or another generator owns the source, stop and route the request to that stack.

Inspect:

- the Mini Program root and page registry;
- global, package, and page renderer configuration;
- `componentFramework`, `lazyCodeLoading`, and `rendererOptions`;
- page navigation and scroll ownership;
- project base-library and DevTools configuration;
- existing Skyline pages, custom navigation, safe-area utilities, and glass-easel components.

Use the repository's actual page registry as runtime evidence. A directory, mock screen, screenshot, or design note does not by itself prove that a page is registered or reachable.

Load `skyline-config` and follow its current requirements. Do not replace the full application configuration with a canned template. Preserve established compatible options, use page/package scope when only part of the app is targeted, and assess affected pages before any global renderer change.

If the project is native WebView and the user explicitly wants the target converted, load `skyline-overview`. Treat migration as more than toggling `renderer`: check navigation, page scrolling, components, WXSS, runtime APIs, transitions, fallback policy, and target client support.

## 3. Translate layout intent into Skyline structure

Map Figma structure to runtime behavior rather than coordinates:

| Figma intent | Skyline implementation direction |
| --- | --- |
| Vertical/horizontal Auto Layout | Explicit Flex container and direction |
| Gap/padding | Parent-owned spacing supported by current WXSS guidance |
| Fill container | Flex growth, parent sizing, or percentage width |
| Hug contents | Natural content size plus padding |
| Clip content | Supported clipping on the owning boundary |
| Fixed top/bottom region | Page shell outside the primary scroll viewport |
| Long content | Explicit Skyline `scroll-view` model |
| Sticky region | Skyline sticky components selected via `skyline-components` |
| Overlay/sheet | Positioned layer, portal/sheet, or route primitive supported by Skyline |
| Gesture-linked movement | Worklet/shared values when UI-thread response is required |

Use absolute positioning only for genuine overlap, badges, masks, and decoration. Do not trace the entire Figma frame with fixed coordinates, empty spacer nodes, transparent placeholders, or repeated corrective offsets.

### Units

Follow the repository's unit policy. For a full-width logical Figma frame of width `W`, a possible starting point for viewport-relative geometry is:

```text
rpx = figma_value × 750 / W
```

Do not apply that formula to screenshot device pixels, system chrome, physical hairlines, native control metrics, or desktop-to-mobile information architecture. Check text, images, fixed controls, safe areas, and at least the relevant narrow/reference/wide devices separately.

When a Figma file contains multiple widths or alternate versions, use the task's exact node. If no node is specified and the variants are materially different, inspect enough context to explain the ambiguity and obtain confirmation rather than choosing by canvas position or neighboring frames.

### Custom navigation and safe areas

Skyline page configuration and custom navigation requirements come from `skyline-config`. Determine whether the Figma frame includes status bar, capsule/menu button, navigation, tab bar, or home indicator. Do not recreate operating-system chrome as arbitrary content.

Reuse existing navigation and viewport utilities. Derive system geometry from current APIs/project helpers rather than fixed device offsets. Ensure fixed actions, scroll content, keyboard, and bottom safe area do not overlap.

## 4. Design the scroll architecture before markup

Load `skyline-components` for every scrollable page. Decide:

- the one container that owns primary vertical scrolling;
- the required explicit `scroll-view` type;
- which children must be direct items for list virtualization/style sharing;
- whether list/grid/sticky primitives require custom mode;
- whether tabs or child lists require nested mode;
- whether horizontal scrolling, refresh, load-more, keyboard, or a draggable sheet changes the model;
- whether programmatic control requires `skyline-scroll-api`.

Do not rely on page-global scroll, `overflow: auto/scroll`, browser sticky positioning, or `Page.onPageScroll`. Avoid nested scroll views without an explicit coordination model. Treat Figma captures at different scroll offsets as evidence of one page unless they represent distinct product states.

## 5. Map visual tokens through Skyline WXSS

Load `skyline-wxss` before writing styles. Inspect `rendererOptions` because Skyline defaults may differ from browser expectations and may be changed by project configuration.

### Units and tokens

- Follow the repository's established `rpx`/`px` policy consistently within a static style group. For a confirmed 750-unit mobile design, `1 design unit → 1rpx` may be the repository's starting rule; otherwise use the viewport formula above.
- Prefer `rpx` for viewport-relative layout, typography, spacing, radii, icons, and illustrations when that matches the project. Reserve `px` for runtime geometry returned by system APIs, safe-area/menu-button calculations, physical hairlines, native-component requirements, and other project-documented exceptions.
- When system API values participate in design-space layout, convert them deliberately using the current viewport rather than mixing raw `px` with `rpx` geometry.
- Prefer existing semantic colors, type roles, spacing, radii, shadows, and utility classes. Promote a repeated cross-page value to the repository's shared token layer only when that layer exists and affected consumers were considered.
- Keep static styles in WXSS. Use inline `style` only for genuine runtime values, not as a shortcut around reusable classes or token decisions.

When design fidelity conflicts with an established token, determine whether the task prioritizes the reference or the existing system. A local value can be appropriate for a one-off design; changing a shared token requires consumer review.

### Layout and sizing

- Use Flex and current supported values; browser support does not prove Skyline support. Do not use CSS Grid unless the loaded official guidance explicitly says the configured environment supports it.
- Let the parent own alignment through `justify-content`, `align-items`, `align-content`, direction, and wrapping. Do not reproduce alignment with per-child offsets.
- Keep one semantic group in one wrapping Flex container where possible. Prefer relative/percentage item widths for responsive columns; use fixed widths only when the design or platform behavior requires them.
- Use `padding`, `margin`, or supported gap behavior for actual content spacing, not to compensate for an incorrect parent layout.
- Do not add empty or transparent spacer nodes, meaningless wrappers, detached coordinates, or broad absolute positioning to trace a Figma frame. Use positioning for genuine overlap, badges, masks, decoration, and anchored controls.
- Do not fix a dimension when content sizing, Flex growth, percentages, or an existing token expresses the intent. Check content growth and smaller/wider viewports whenever a fixed dimension is justified.
- Use Skyline components for scrolling, sticky behavior, lists/grids, and other semantics that ordinary WXSS does not own. Do not substitute browser `position: sticky` or `overflow: auto/scroll`.
- Validate clipping and overflow through `skyline-wxss`; keep scrolling in the chosen `scroll-view` owner.

### Typography

Keep user-visible text in supported text components and follow `skyline-components` for inline mixing, overflow, and `max-lines`. Match role, weight, line height, wrapping, truncation, and alignment before micro-adjusting size.

Confirm font availability in the Mini Program runtime. Test source-language copy, long/short labels, numbers, empty values, and dynamic content. Do not convert important text to an image or substitute visible Chinese copy with generic placeholder text.

- Do not give a text node fixed `height` or `min-height` merely to establish vertical rhythm; use a compatible `line-height` and allow wrapping/font differences to grow safely.
- Put truncation semantics on the supported text component using the attributes prescribed by `skyline-components`; do not rely on a wrapping view's browser `text-overflow` behavior.
- Keep visible literal/bound text in the repository's required WXML form. If its instructions require text content and tags on one source line to avoid rendered indentation whitespace, preserve that convention.

### Selectors, isolation, and compatibility

- Prefer scoped class selectors. Avoid broad tag/global selectors, especially when `tagNameStyleIsolation` or glass-easel isolation settings can widen their effect.
- Follow the repository's ordering convention when combining shared utility classes with business classes.
- Do not assume application-level utility classes cross a custom-component boundary. Use the repository's established explicit import, shared-style, or isolation mechanism and verify the resolved result.
- Validate gradients, masks, filters, background images, animations/transitions, transforms, shorthand properties, overflow, text decoration/truncation, `calc`, `env`, and other non-trivial properties or values through the installed `skyline-wxss` guidance.
- When the installed tooling prescribes a WXSS check, run it only against the changed files with the actual Mini Program root. Do not add package dependencies or lockfiles merely to make an optional check available.

When the target environment already provides the matching CLI and the loaded official guidance confirms its current syntax, a scoped check may look like:

```bash
npx skyline-cli wxss check --json --miniprogram-root . --files <changed-wxss-files>
```

Treat this as an availability-dependent check, not permission to install tooling or assume a package runner exists.

## 6. Author WXML, components, and navigation

### WXML structure

- Keep WXML declarative: structure, supported component attributes, event bindings, conditions, lists, slots, and simple display bindings belong here. Move non-trivial filtering, sorting, grouping, field adaptation, and formatting to page/component JS/TS or an established utility.
- Put every user-visible literal or bound text value in a supported text component. Do not place bare text directly in a generic layout container.
- Keep a text component's opening tag, content, and closing tag on one source line when whitespace from line breaks/indentation could render or when repository instructions require that convention.
- Do not add empty `<view>`, empty `<text>`, transparent placeholder, or contentless node merely to create spacing. Express spacing in the responsible parent style.
- Give every wrapper a concrete layout, style, semantic, state, clipping, or interaction responsibility. Remove wrappers that only wrap; do not flatten nodes whose separate responsibilities matter.
- Keep repeated content in one data-driven structure with a stable business `wx:key`. Preserve direct-child requirements imposed by the selected list/grid/virtualization component.
- Keep state branches explicit enough to distinguish loading, populated, empty, error, retry, disabled, and other required states without duplicating the full page shell.

### Page and component boundaries

Reuse an existing component only when responsibility, behavior, states, and event contract match. Configure it through existing properties and slots rather than copying markup.

Create a component when it repeats, owns meaningful behavior/lifecycle, or needs a stable properties/events/slots contract. Keep one-off page composition local; do not mirror every Figma group as a component.

For native components:

- use the repository's native page/component constructors and lifecycle conventions; ordinary native entries use `Page({})` and `Component({})` unless the repository already owns a compatible abstraction;
- register at the narrowest project-appropriate scope;
- declare every used custom component in the applicable `usingComponents` configuration and verify the path exists;
- expose clear `properties`, slots, and semantic `triggerEvent` outputs rather than leaking internal nodes or incidental implementation state;
- keep internal data and lifecycle effects encapsulated;
- avoid parent dependence on private component nodes;
- verify global token/style access against current style isolation rather than assuming inheritance.

Do not create a shared component solely because two screenshots contain similar rectangles. Reuse/extract only when responsibility, state model, styling variability, and interaction contract can remain coherent for all consumers.

### Registration and navigation

- Treat `app.json` and any declared subpackages as the page registry. A page folder is incomplete until the required native source files exist and the route is registered at the correct scope.
- Reuse the repository's established navigation/header component whose responsibility matches the page class. Preserve its capsule/status safe-area handling, title/action contract, and back behavior; do not add a competing header with overlapping purpose for visual convenience.
- Keep custom navigation, fixed headers/actions, the scroll viewport, keyboard avoidance, and bottom safe area coordinated as one page shell.
- Use the repository's established routing helpers or native navigation API appropriate to the intended history behavior. Do not invent a destination from a visible Figma control.
- Handle navigation rejection/failure according to project conventions. A back action may use an established semantic fallback only when the desired destination is confirmed; do not silently swallow failures or guess a route.
- Consider subpackages when repository policy, package size, or route depth justifies them. Do not introduce a new package boundary for one simple page without evidence.

## 7. Export and own assets

For each visual decide whether to reuse a repository asset, export the exact Figma node, use a native component, build a simple supported shape, or disclose a temporary substitute.

Use semantic filenames and the repository's asset ownership pattern. Preserve aspect ratio, focal crop, transparency, and corner treatment. Check package cost for large images and animations. Do not hotlink temporary Figma URLs, redraw brand marks from memory, use emoji/Unicode as a final icon, or embed a full-screen raster as the implementation.

## 8. Implement behavior and data boundaries

Connect existing routes, services, models, request wrappers, formatters, stores, and analytics only where their contracts are confirmed. Keep mock/fixture data isolated and visibly distinct from production services.

Record each data-backed region as confirmed remote data, repository constant, mock/fixture, local UI state, placeholder, or unresolved. A registered page that renders convincing sample data is not evidence that its business capability is connected.

Implement states shown in Figma and those explicitly required by the task. For relevant asynchronous flows:

- model loading, populated, empty, error, retry, and completion states;
- prevent duplicate actions and stale-response overwrite;
- minimize the size and frequency of `setData` updates;
- clean up timers, listeners, Worklet bindings, and other owned side effects on unload.

Do not add login, payment, user-data, location, camera, privacy, or other sensitive capabilities merely because their controls are visible. Use an established authorized product flow or implement only the UI shell and report the missing integration.

## 9. Route motion to the correct Skyline system

Use Figma prototype/motion evidence to choose ownership:

- simple state feedback → supported WXSS transition/animation after `skyline-wxss` validation;
- direct gesture or scroll-linked response → `skyline-worklet`;
- page transition, return gesture, half-screen route, or container transition → `skyline-route`;
- programmatic refresh, scroll, or sheet position → `skyline-scroll-api`.

Do not invent motion absent from the design or product requirements. Do not drive high-frequency gestures through repeated cross-thread `setData`. Verify Worklet and route assumptions against the configured base library and real input when possible.

## 10. Validate in evidence layers

### Static

- Parse every changed JSON file. Verify registered page/subpackage paths, `usingComponents`, imports, assets, and required source siblings exist.
- Verify Skyline/glass-easel, navigation, page scroll ownership, and renderer options with `skyline-config`.
- Inspect WXML responsibilities: meaningful page/section/component/content hierarchy; supported components; valid bindings and conditionals; stable business keys; virtualization-sensitive direct children; no empty spacer nodes or duplicated structures; visible text in supported text nodes and the repository-required source form.
- Inspect layout responsibilities: one primary scroll owner; fixed, sticky, scrolling, keyboard, and safe-area regions are explicit; parent Flex alignment and wrapping replace corrective child offsets; no unjustified detached/absolute coordinate tracing.
- Inspect size/style consistency: correct design baseline; coherent units; no fixed-height text clipping; repeated values use appropriate tokens/utilities; selectors respect isolation; no unsupported browser-only property/value assumptions.
- Inspect changed WXSS with `skyline-wxss` and its prescribed CLI when available and authorized. Scope the command to changed WXSS files and do not install dependencies solely for the check.
- Inspect async state coverage, duplicate-action/stale-response protection, and cleanup of timers, listeners, Worklet bindings, and other owned effects.
- Run existing repository lint, type, tests, and build commands only when they actually exist. Absence of `package.json` or a runner means using direct checks, not inventing npm commands.

### Runtime

Compile the target with WeChat DevTools using the intended Skyline renderer and base library. Record WXML, WXSS, component, glass-easel, Worklet, and runtime warnings/errors. A parsed file is not evidence of successful compilation.

Exercise relevant navigation, back/dismiss, scrolling, nested/sticky/list behavior, input and keyboard, forms, authorization, loading/empty/failure/retry states, repeated submission, and unload behavior. Check top capsule/status geometry and bottom safe areas on representative iOS and Android sizes. Use a real device for gesture, route, Worklet, permission, network, login, and other behavior whose simulator evidence is insufficient.

### Visual and interaction

Capture the implementation at the same logical viewport as the exact Figma node. Compare page shell and safe areas first, then region geometry, spacing, typography, images, colors/effects, and motion. Re-render after structural corrections.

Check relevant iOS and Android sizes, long content, custom navigation, scrolling, sticky/nested behavior, input/keyboard, state changes, back/dismiss behavior, and device-sensitive motion. Simulator and real-device results must be reported separately.

Compare the material loading, populated, empty, failure, selected/disabled, and interaction states for which design evidence exists. If a close screenshot depends on extra wrappers, scattered offsets, hard-coded coordinates, or blank placeholders, treat the structure as failing even if one viewport looks correct.

Report evidence in separate layers: static inspection, Skyline tooling, DevTools compilation, simulator rendering, exact-node visual comparison, and real-device behavior. An unavailable layer remains unverified; success in one layer must not be promoted into another.

## 11. Authoritative references

- [Official Skyline skills](https://github.com/wechat-miniprogram/skyline-skills)
- [Official Skyline examples](https://github.com/wechat-miniprogram/awesome-skyline)
- [Official Mini Program component/API examples](https://github.com/wechat-miniprogram/miniprogram-demo)
- [Official Skylint migration checker](https://github.com/wechat-miniprogram/skylint)
- [Official glass-easel repository](https://github.com/wechat-miniprogram/glass-easel)

Use installed official skills and current documentation for version-sensitive capability or minimum-version questions. Do not freeze their full support matrix in this skill.
