---
name: snapshot-to-figma
description: Use Codex with the official Figma plugin to reconstruct UI screenshots, mockups, or other design images as editable, maintainable Figma designs. Use when the user asks to convert visual references into Figma screens or components while preserving visual fidelity, semantic structure, Auto Layout, tokens, and reusable assets. Requires the official Codex Figma plugin. Do not use for implementing application code or merely embedding the source image in Figma.
---

# Snapshot to Figma

Turn one or more reference images into an editable Figma design that both resembles the source and behaves like a maintainable design-system artifact. The source image is visual evidence, not a layer hierarchy: reconstruct the underlying layout rather than tracing every pixel as unrelated shapes.

## Operating contract

- Keep the task in design scope. Do not implement application code unless the user separately requests it.
- Treat the user's current request as authoritative, then follow repository design guidance, then the target Figma file's established variables, styles, components, naming, and page structure.
- Discover the project's complete design-delivery contract before writing. A repository may require page specifications, indexes, change records, or other companion artifacts in the same delivery; update those when project instructions make them mandatory, but do not invent a documentation system where none exists.
- Use the reference image for visible content, hierarchy, proportions, and styling. Use project conventions for semantics, interaction, responsive behavior, and reusable primitives.
- Do not paste the full reference image into the delivery frame as the implementation. A labeled reference copy may exist temporarily in a scratch area, but it is not a finished design.
- Do not overwrite unrelated frames, shared components, variables, or styles. Preserve existing work and inspect references before changing shared assets.
- Do not claim pixel accuracy, token reuse, accessibility, or state coverage unless each was actually checked.

## Required Codex plugin and routing

The official Codex Figma plugin is mandatory. Before any Figma operation, verify that the plugin is installed in Codex, connected to Figma, and has write access to the target file. If the plugin, connection, or permission is missing, stop before writing or claiming delivery; tell the user to install or connect the official Figma plugin in Codex and grant the required file access.

Before the first Figma operation, load the applicable instructions supplied by the official plugin (the names may use a `figma:` namespace):

- Load `figma-use` before programmatic Figma reads or writes.
- Load `figma-generate-design` with `figma-use` for full screens, dialogs, drawers, or other composed views.
- Load `figma-generate-library` with `figma-use` when creating or changing variables, tokens, components, or variants.
- Load `figma-create-new-file` only when a new Figma file is actually required.
- Add platform- or motion-specific guidance only when the task requires it.

Do not substitute browser automation, a generic MCP server, or another host's Figma integration for this required Codex plugin. If plugin access is unavailable, a reconstruction specification may be provided only as an explicitly incomplete fallback, not as delivered Figma work.

Read [references/reconstruction-guide.md](references/reconstruction-guide.md) before reconstructing a reference. Read [references/qa-checklist.md](references/qa-checklist.md) before final delivery.

## Workflow

### 1. Resolve the source and target

Identify:

- every source image and which screen, viewport, theme, breakpoint, or state it represents;
- the intended platform and target frame size, if known;
- the target Figma file, page, and surrounding design system;
- whether the task is a new screen, a replacement, or an addition to an existing flow;
- required interactions, states, components, documentation, and handoff boundaries.

Also identify the project's sources of truth and their precedence. Read only the sections relevant to the task, but do not treat the screenshot as overriding explicit product requirements or current design-system rules. If a required companion artifact or index is part of the project contract, include it in scope from the beginning rather than adding it after design work.

Use an existing target file when the user or project provides one. Create a new file only when the user asks for one or no suitable target exists and creating one is clearly within scope. Ask a question only when a missing choice would materially change the information architecture, brand expression, or destination; otherwise use the least invasive reversible assumption and report it.

### 2. Inspect the reference and project context

View each source image at usable resolution. Record its dimensions and distinguish application UI from device bezels, operating-system chrome, browser chrome, annotations, shadows, and crop boundaries.

Read only the relevant project design documentation. Inspect the target Figma file before writing:

- page and frame organization;
- local variables, text and effect styles;
- reusable components and variants;
- comparable screens, naming, layout, and prototype conventions;
- existing assets such as icons, logos, illustrations, and photos.

For existing designs, map the impact surface before editing: shared component and variable consumers, nested instances, related states, prototype connections, companion documentation, and the frames that provide useful regression coverage. Do not use the reconstruction task as a reason to reorganize unrelated pages or assets.

Do not import conventions from the source image when they conflict with explicit current-project rules. Record material conflicts and the chosen resolution.

### 3. Build a reconstruction specification

Before creating nodes, translate pixels into a layout tree:

1. Screen frame and scrolling model.
2. Stable regions such as navigation, content, overlays, and bottom actions.
3. Repeated business modules such as cards, list rows, form groups, or metrics.
4. Reusable component instances.
5. Text, icons, images, and necessary decoration.

For each region, determine its responsibility, direction, alignment, distribution, padding, gap, resizing behavior, clipping, and fixed-versus-scrolling behavior. Every wrapper must have a layout, style, clipping, state, or reuse responsibility; remove single-child and duplicate wrappers that add none. Infer a spacing rhythm, typography roles, color roles, radii, strokes, and elevations from repeated evidence rather than recording every sampled value as a new token.

Separate facts from inferences. Preserve readable source copy; mark unreadable or cropped content as an explicit placeholder instead of inventing business facts.

### 4. Establish the fidelity strategy

Match in this order unless the user specifies otherwise:

1. frame, region geometry, and major alignment;
2. typography roles, line wrapping, and content density;
3. spacing, component dimensions, and image crops;
4. color, borders, radii, elevation, and icon treatment;
5. minor decorative detail.

Prefer the target design system's semantically equivalent component or token. If reuse creates a visible mismatch, decide whether the reference or the current project standard has priority from the task context. Do not detach instances or create near-duplicate tokens merely to hide a small mismatch; document a deliberate deviation when necessary.

When the source resolution differs from the target frame, derive one consistent scale from the content viewport. Do not independently stretch axes or blindly scale typography, strokes, and touch targets. Record the source crop and scaling assumption.

### 5. Reconstruct in maintainable layers

Build the screen section by section and verify each stable region before proceeding.

- Use semantic names based on role, never default layer names or coordinates.
- Use Auto Layout for page regions, stacks, rows, forms, and repeated content.
- Express alignment through parent layout; use gaps and padding only for real spacing.
- Use Fill container, Hug contents, constraints, min/max sizes, or nested layout for elasticity.
- Reserve absolute positioning for genuine overlays such as badges, floating actions, and decorative layers.
- Never use empty frames, invisible rectangles, blank text, or dummy instances as spacers.
- Reuse existing components and variables before creating new ones.
- Create a new component, variant, or semantic token only when it has clear reusable value.
- Keep raster imagery as image fills with an explicit crop rule. Recreate UI chrome, text, icons, and controls as editable objects rather than baking them into bitmaps.
- If an exact icon, logo, or photo asset is unavailable, use an existing approved asset or a clearly labeled temporary substitute and disclose it.

For repeated items, create a component or consistent list structure and test it with varied content. A single screenshot does not prove responsive behavior; encode the smallest reasonable behavior supported by its visual evidence and the target system.

When modifying a usable existing design, preserve the current version until the proposal passes comparison and structural checks. Make broad changes in a clearly labeled working area, then replace or archive only the intended target after validation. If current and proposed versions must coexist for review, label them unambiguously and do not clean up unrelated review material without authorization.

### 6. Add relevant states and interactions

Reconstruct every state shown by the supplied references. Add states not shown only when requested or required by the current project's design rules; distinguish them from source-observed states.

For interactive elements, document or prototype the trigger, immediate feedback, destination or result, dismissal/back behavior, and failure path when these are in scope. Forms need persistent labels and applicable focus, filled, error, disabled, and submitting states. Dangerous actions need explicit consequences and confirmation language.

Do not fabricate a product flow from ambiguous static evidence. Record unresolved product behavior as an assumption or question.

### 7. Iterate by rendered comparison

Render or screenshot the reconstructed frame at the target viewport and compare it with the source at a common scale. When possible, use side-by-side comparison first and an opacity overlay or difference view for precise alignment.

Fix discrepancies in descending impact:

- frame bounds, large regions, fixed areas, and scroll boundaries;
- alignment, spacing rhythm, component size, and content density;
- text style, baseline, wrapping, truncation, and line count;
- image aspect ratio and crop;
- fills, strokes, radii, shadows, and icons;
- minor decoration.

After every structural correction, render again. Do not compensate for an incorrect parent with child offsets or one-off spacing.

### 8. Verify and document

Run the full checklist in [references/qa-checklist.md](references/qa-checklist.md). Inspect both the rendered output and the layer/property structure; neither alone is sufficient. The structural gate must explicitly cover layer responsibility, parent-owned layout, fixed-versus-elastic sizing, absolute positioning, and variable/style binding before the visual comparison can pass.

After changing a shared component, variant, variable, or style, verify all affected states and nested instances, then inspect at least one representative existing consumer as well as the reconstructed result. A visually correct new frame is not evidence that a shared-asset change is safe.

If the repository has a design-documentation convention, or the user requested documentation, update the matching page document and index in the same delivery. Include the Figma file link, exact frame name and node ID, layout model, reused components and tokens, interactions, states, edge cases, assumptions, and change record. Do not invent a documentation directory when the project has no such convention and the user did not request one.

## Completion definition

The task is complete only when:

- the reconstruction is written to the intended Figma destination;
- delivery frames contain editable semantic layers rather than a flattened screenshot;
- the rendered result has been compared with the source and material discrepancies were corrected or disclosed;
- layout behavior, variables/styles, components, naming, assets, states, and accessibility were checked in proportion to scope;
- required project documentation was updated;
- unrelated Figma content and repository files were not changed.

Report the target Figma file and frame/node, source references used, completed states, reused or added system assets, comparison and QA performed, documented assumptions, substitutions, and any remaining user decisions.
