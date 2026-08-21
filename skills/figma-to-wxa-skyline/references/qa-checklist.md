# Figma to WXA Skyline QA

Use after implementation and rendered comparison. Mark only checks actually performed; list unavailable checks as unverified.

## Dependency and scope

- The official Figma plugin published by OpenAI is installed in Codex, connected to Figma, and can read every exact target node.
- `figma-design-to-code` from the official plugin was loaded before retrieving design context.
- The complete `wechat-miniprogram/skyline-skills` package is installed.
- `skyline-config`, `skyline-components`, and `skyline-wxss` were loaded.
- `skyline-overview`, `skyline-worklet`, `skyline-route`, and `skyline-scroll-api` were loaded when their scenarios applied.
- The output is native Skyline/glass-easel source, not WebView or framework-generated source.
- The exact Figma file/page/node, target page/component paths, states, and viewport are identified.
- Alternate mobile/desktop or multi-width frames were not selected by canvas position or adjacency.
- No whole-app renderer migration occurred from a page-scoped request.

## Facts and repository fit

- Every applicable repository instruction file was read, and its project-local workflow and validation gates were followed.
- The actual page registry, required design/implementation notes, unit policy, navigation/scroll conventions, and data layers were identified before editing.
- Visual facts come from the exact node; runtime facts come from registered configuration/source; data facts come from confirmed contracts.
- Existing page/design documentation was created or synchronized in the required order only when the repository requires it.
- User changes and unrelated pages/configuration remain intact.
- Existing components, tokens, assets, services, models, and utilities were reused when responsibilities match.
- Mock/fixture behavior is not described as a real backend capability.
- Project-specific rules such as a 750-unit conversion, custom navigation, or documentation gate were not generalized to unrelated repositories.

## Skyline configuration

- Target application/package/page configuration resolves to `renderer: "skyline"` and the required glass-easel setup according to `skyline-config`.
- Custom navigation, page scroll ownership, `rendererOptions`, base-library target, and DevTools settings were inspected.
- Page and component JSON parses; registrations, `usingComponents`, imports, and asset paths exist.
- A WebView-to-Skyline migration was assessed through `skyline-overview` rather than treated as a config toggle.

## WXML, components, and scrolling

- UI is real WXML/WXSS/components, not a full-frame screenshot.
- WXML remains declarative; non-trivial filtering, grouping, field adaptation, and formatting live in JS/TS or established utilities rather than template expressions or duplicated branches.
- Page, section, component, and content nodes have clear responsibilities; no empty text/view spacer, duplicated structure, or meaningless single-child wrapper remains.
- Visible text uses supported text components, follows the repository's whitespace/source-line convention, and does not appear as bare text in a generic layout container when local rules prohibit it.
- Truncation uses attributes supported by `skyline-components` on the text owner rather than browser `text-overflow` on a wrapper.
- Repeated data has stable business keys and virtualization-sensitive children follow required structure.
- Loading, populated, empty, error/retry, disabled, and other required branches do not duplicate the whole page shell unnecessarily.
- Component extraction/reuse is supported by matching responsibility, state, styling variability, and event contract rather than visual resemblance alone.
- Custom-component `properties`, slots, and semantic events form the public contract; parents do not depend on private child nodes.
- Every custom component is declared in the applicable `usingComponents`, and its source path exists at the intended scope.
- Primary scrolling has one explicit owner and a correct `scroll-view` type.
- List/grid/sticky/nested, horizontal, refresh, and programmatic scrolling follow the relevant Skyline skills.
- Page-global scrolling, browser overflow scrolling, unsupported web components, empty spacers, and coordinate-traced layout are absent.
- Custom navigation, fixed regions, safe areas, keyboard, and bottom actions do not overlap scroll content.

## Registration and navigation

- Every new/changed page has the repository-required native source siblings and is registered in `app.json` or the correct subpackage.
- The matching existing navigation/header component is reused when its responsibility fits; no overlapping duplicate was introduced for visual convenience.
- Status/capsule safe area, title/actions, fixed/scroll regions, back behavior, keyboard, and bottom safe area remain coordinated.
- Navigation uses confirmed destinations and the repository's history/routing conventions; visible Figma controls did not cause invented routes.
- Navigation failures are handled or disclosed rather than silently swallowed, and any fallback destination is product-confirmed.
- New subpackage boundaries have package-size, route, or repository-policy justification.

## WXSS and visual system

- Static layout, type, spacing, radii, icon, and illustration units follow the repository's coherent `rpx`/`px` policy; raw system `px`, physical hairlines, and native metrics are used only for justified exceptions.
- A 750-unit or other viewport conversion is applied only to the confirmed logical design frame, not blindly to screenshots, system chrome, hairlines, native controls, or image crops.
- Static styles live in WXSS; inline styles represent genuine runtime values only.
- Flex direction, parent-owned alignment, wrapping, and sizing follow configured Skyline behavior and project conventions.
- Semantic groups use a single wrapping container where practical; responsive columns prefer relative/percentage widths unless fixed geometry has evidence.
- Padding, margin, or supported gap values represent real spacing rather than compensating for incorrect alignment.
- Fixed dimensions have design/platform evidence; content, Flex growth, percentages, or tokens are used when they express the intent.
- Every non-trivial property/value was checked through `skyline-wxss`; browser CSS support was not assumed.
- Gradients, masks, filters, background images, transitions/animations, transforms, shorthand properties, overflow, truncation, `calc`, and `env` were checked when used.
- Unsupported grid/sticky/overflow behavior was replaced with supported Flex or Skyline components; scrolling is not delegated to `overflow: auto/scroll`.
- Empty/transparent spacers, broad absolute positioning, detached Figma coordinates, and scattered corrective offsets are absent.
- Existing semantic tokens are reused; shared token changes were checked against consumers.
- Scoped class selectors follow repository ordering conventions; tag/global selectors and glass-easel style leakage were checked.
- Shared styles used inside custom components are imported or exposed through the repository's explicit isolation mechanism rather than assumed to penetrate.
- Text can wrap/truncate/grow without fixed `height` or `min-height` clipping; line height establishes vertical rhythm.
- Assets use stable local paths, correct format/crop/scale, and acceptable package size.
- No temporary Figma URL, emoji stand-in, memory-drawn logo, or oversized unoptimized image ships.

## Data, behavior, and motion

- Required loading, populated, empty, error, retry, selected, disabled, permission, and success states are implemented.
- Short/long text, zero/large values, missing images, varied list counts, and repeated actions were checked where relevant.
- Async behavior prevents duplicate actions and stale overwrites and disposes of owned side effects on unload.
- Sensitive capabilities use an existing authorized integration or remain explicitly unintegrated.
- UI-thread motion uses `skyline-worklet`; route transitions use `skyline-route`; programmatic scrolling uses `skyline-scroll-api` when applicable.
- Worklet/route/scroll behavior respects configured base-library support and is not simulated through high-frequency `setData`.

## Fidelity and validation

- Every changed JSON file parses; registered pages/subpackages, `usingComponents`, imports, assets, and required source siblings resolve.
- WXML hierarchy, bindings, conditionals, components, text nodes, list keys/direct children, scroll ownership, and safe-area/fixed-region responsibilities were statically checked.
- WXSS units, tokens, Flex alignment/wrapping, fixed dimensions, selectors/isolation, text growth, property/value support, and asset styling were statically checked.
- Async states, duplicate-action/stale-response protection, and unload cleanup were statically checked where relevant.
- Repository commands were discovered from configuration; absent npm/test/build commands were not invented.
- Skyline-specific checks prescribed by the loaded official skills ran against changed files when tooling was available and authorized; no dependency or lockfile was added solely to make an optional check run.
- WeChat DevTools compiled the target in Skyline mode, or this remains explicitly unverified.
- DevTools warnings/errors for WXML, WXSS, components, glass-easel, Worklet, routes, and runtime behavior were recorded and resolved or disclosed.
- The implementation capture was compared with the exact Figma node at the same logical viewport.
- Safe areas, region bounds, alignment, spacing, typography, images, colors, borders, radii, effects, states, and motion match or have disclosed deviations.
- Top status/capsule geometry, bottom safe area, long content/text, loading/empty/failure/retry, scrolling/sticky/nested behavior, keyboard, taps, forms, authorization, navigation/back, repeated actions, and unload were exercised where relevant.
- Relevant iOS and Android sizes were checked; simulator and real-device results are distinct, and gesture/route/Worklet/permission/network behavior is device-tested when required for confidence.
- A fresh visual comparison was made after the last structural correction.
- A one-viewport visual match that depends on extra wrappers, blank placeholders, hard-coded coordinates, or scattered offsets was rejected as structurally incomplete.
- Static inspection, Skyline tooling, DevTools compile, simulator, visual comparison, and real-device evidence are reported separately; unavailable layers remain unverified.

## Delivery

- The report names Figma evidence, code entry points, Skyline configuration, loaded official skills, reused/added components and assets, implemented states/motion, and validation performed.
- Assumptions, substitutions, intentional deviations, unresolved integrations, and unverified runtime/device behavior are explicit.
- No unrelated Figma writes, credentials, uploads, submissions, releases, or source changes occurred.
