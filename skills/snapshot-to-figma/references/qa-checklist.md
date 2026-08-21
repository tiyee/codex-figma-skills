# Figma Reconstruction QA

Use this checklist after a rendered comparison and before delivery. Mark only checks actually performed.

## Codex plugin

- The official Figma plugin published by OpenAI is installed in Codex and connected to Figma.
- The plugin has write access to the exact target file.
- Applicable plugin instructions such as `figma-use`, `figma-generate-design`, and `figma-generate-library` were loaded before their corresponding operations.

## Source and scope

- Every supplied image is mapped to a screen, state, breakpoint, theme, or scroll position.
- Device or browser chrome, annotations, and crop boundaries were not mistaken for product UI.
- The intended Figma file, page, frame, and scope were confirmed or reasonably inferred.
- Project guidance and relevant target-file conventions were inspected.
- Unreadable content, missing assets, and product assumptions are explicitly labeled.

## Layer structure

- The delivery is editable and not a flattened full-screen image.
- Layers are named by semantic role; no default copy/rectangle/frame names remain in maintained areas.
- Page, region, module, component, and content responsibilities are separated without redundant wrappers.
- No empty, transparent, blank-text, or dummy-instance spacer layers exist.
- Repeated UI uses components, instances, or a consistent repeated structure.
- Shared components were not detached or modified without checking impact and authorization.

## Structural and numeric gates

All four gates must pass before visual approval:

- **Responsibilities:** Every maintained wrapper has a layout, style, clipping, state, or reuse purpose; redundant and single-child wrappers without such a purpose were removed.
- **Parent-owned layout:** Alignment, distribution, wrapping, and elasticity are expressed through the correct parent Auto Layout, constraints, Fill, Hug, and min/max behavior rather than child nudges or fake spacing.
- **Sizing and positioning:** Fixed dimensions trace to a frame baseline, asset, control, touch-target, or explicit design-system rule; content-dependent areas can resize; absolute positioning is limited to genuine overlays or decoration.
- **System binding:** Existing semantic variables and styles are bound wherever applicable; repeated reusable values are modeled semantically; incidental sampled values did not become near-duplicate tokens.

## Layout and resizing

- Parent Auto Layout owns direction, alignment, distribution, padding, and true gaps.
- Fill, Hug, constraints, and min/max behavior express elasticity without child offset compensation.
- Absolute positioning appears only for genuine overlays or decoration.
- Fixed dimensions have a clear reason; content-dependent regions can grow or shrink appropriately.
- Scrolling, fixed headers or actions, clipping, safe areas, and overlays behave as intended.
- Long/short text, text wrapping, varied list counts, and relevant alternate widths do not break layout.

## Visual fidelity

- The rendered Figma frame was captured at the intended viewport and compared with the source at a common scale.
- Major region bounds, alignment guides, spacing rhythm, and content density match.
- Typography hierarchy, weight, line height, wrapping, truncation, and baseline relationships match.
- Component sizes, icon weight, image aspect ratio, crop, and focus match.
- Fills, text colors, borders, radii, opacity, elevation, and overlays match or have disclosed system-driven deviations.
- Structural fixes were not replaced with arbitrary local nudges.
- A fresh comparison was performed after the last material correction.

## Design system

- Existing semantic variables, styles, components, and variants are reused when applicable.
- Repeated new values use meaningful reusable tokens rather than near-duplicate constants.
- Component variants express real properties or states and do not duplicate lookalike masters.
- New assets follow target-file naming and organizational conventions.
- Fonts, icons, photos, logos, or illustrations substituted from the reference are disclosed.
- After a shared component, variant, variable, or style change, affected states and nested instances were checked, along with at least one representative existing consumer and the reconstructed frame.

## States, behavior, and accessibility

- Every state shown in the source is represented.
- Additional required states are included and distinguished from source-observed states.
- Applicable triggers, feedback, destinations, dismissals, return paths, and failures are specified.
- Touch targets follow the current platform guideline.
- Text contrast meets the current project accessibility requirement, normally at least WCAG AA for body text.
- Meaning is not conveyed by color alone; focus, error, disabled, and destructive behavior have non-color cues.
- Relevant long text, large text, empty, loading, error, offline, permissions, and extreme values were checked.

## Delivery

- Exact Figma file, page/frame name, and node ID are available for handoff.
- Required repository design documentation and indexes were updated, if the project uses them.
- Existing usable work remained available until broad changes passed review; any temporary Current/Proposed or scratch material is clearly labeled and handled according to project conventions.
- No unrelated Figma nodes, shared assets, or repository files were changed.
- The final report lists sources, states, system assets, validation, assumptions, substitutions, intentional deviations, and remaining decisions.
