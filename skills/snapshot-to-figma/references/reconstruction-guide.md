# Reconstruction Guide

Use this guide after the official Codex Figma plugin, connection, and target-file write permission have been verified. It turns flat visual evidence into a reliable Figma structure and supplements the core workflow; project-specific standards still take precedence.

## 1. Inventory the reference set

Create a compact source map before designing:

| Source | Visible viewport | Screen/state | Theme | Crop or obstruction | Confidence |
| --- | --- | --- | --- | --- | --- |
| Image filename or label | Width × height | Inferred semantic name | Light/dark | Device chrome, clipped content, annotation | High/medium/low |

Multiple images may show the same screen at different scroll positions or states. Align shared landmarks before assuming they are separate screens. If two images conflict, prefer the one the user identifies as current; otherwise record the conflict.

## 2. Separate visual evidence from product inference

Classify observations:

- **Observed:** directly visible text, ordering, alignment, color relationships, dimensions, crop, or state.
- **System-derived:** supplied by the target design system, such as a known button component or semantic token.
- **Inferred:** scroll behavior, responsive resizing, hidden content, navigation result, or component reuse.
- **Unknown:** obscured text, unavailable asset, unshown state, or ambiguous interaction.

Do not silently turn an inference into a source fact. Use clearly labeled placeholders for unknown content and list high-impact assumptions in the handoff.

## 3. Derive geometry

Start with the content viewport rather than the raw bitmap if the image includes a bezel or system chrome.

1. Establish the source viewport and target frame.
2. Identify stable horizontal and vertical guides.
3. Segment large regions and repeated rows or columns.
4. Compare repeated distances to infer a spacing rhythm.
5. Determine which dimensions are fixed by an asset or control and which should grow with content or parent size.

Use a uniform content scale when translating between different viewport widths. Re-evaluate typography, stroke widths, icon sizes, radii, and minimum targets against the target system instead of scaling them mechanically.

Avoid false precision. A single compressed image rarely supports many distinct one-pixel spacing values. Prefer a small coherent scale consistent with repeated evidence and the current project.

## 4. Reconstruct typography

Identify text by role before measuring it: display, page title, section heading, body, label, caption, metadata, button label, numeric emphasis, or link.

- Reuse target text styles when their hierarchy and density match.
- Match line count, wrapping, truncation, alignment, and weight before fine-tuning size.
- Use readable source text when possible. Never replace all content with generic Latin filler when the source language is visible.
- If the exact font is unavailable, choose the project's approved fallback and disclose the substitution.
- Validate with short, long, empty, numeric-extreme, and large-text cases where relevant.

## 5. Reconstruct colors and effects

Map sampled appearance to semantic roles such as canvas, surface, primary action, strong text, muted text, border, warning, success, and scrim.

- Reuse semantically correct variables and styles before adding values.
- Do not create one token for every sampled anti-aliased pixel or compression artifact.
- Distinguish real fills from shadows, transparency, overlays, image content, and color-management shifts.
- Match contrast relationships as well as hue.
- Use effects only when visible evidence supports them; do not add fashionable decoration absent from the source.

## 6. Handle icons and images

- Search existing approved Figma assets first.
- Prefer editable vector icons with the correct optical weight and bounding box.
- Do not substitute emoji, Unicode glyphs, or unrelated icon families for UI icons.
- Preserve each image's aspect ratio, crop focus, corner treatment, overlay, and fallback rule.
- Do not redraw brand marks from memory. Request or reuse an approved asset; otherwise mark a temporary substitute.
- Do not use a full-screen bitmap as the final UI. A tightly scoped raster image may remain when the original content is inherently photographic or illustrative.

## 7. Infer component boundaries

A repeated visual pattern is a component candidate when it has a stable responsibility and varies through content, size, hierarchy, state, or icon placement. Prefer one component with explicit properties or variants over detached lookalikes.

Do not create a component for every wrapper. Region containers and one-off composition can remain semantic frames when they do not represent a reusable interface contract.

When an existing component is close but not identical:

1. Confirm whether the mismatch is an intended product difference or reference artifact.
2. Prefer supported properties or variants.
3. Change the shared component only after checking consumers and scope authorization.
4. Avoid detaching an instance merely to force fidelity.

Before changing a shared asset, identify its consumers, variants, nested instances, interactions, and nearby semantic tokens. Prefer adding a supported property or variant when it represents a real reusable distinction. For a broad revision, keep the current asset usable while validating a clearly labeled proposal; migrate only the intended consumers after the proposal passes QA.

## 8. Multiple screens and states

For a set of snapshots:

- identify shared shell, navigation, and reusable modules before building screens independently;
- name each screen and state semantically;
- keep comparable states aligned for review without making review layout part of the product frame;
- avoid duplicating shared elements as disconnected local components;
- distinguish scroll-position captures from true state variants.

When only one state is visible, reconstruct it first. Any additional loading, empty, error, offline, permission, or success state should come from user requirements or current-project rules, and should be labeled as derived rather than observed.

## 9. Comparison loop

Use the source and rendered Figma frame at the same effective viewport. A useful review order is:

1. Silhouette and major region bounds.
2. Shared alignment guides.
3. Text blocks and baselines.
4. Repeated spacing and component geometry.
5. Image crops and overlays.
6. Color, effects, strokes, and small icons.

Log material differences with their cause: intentional project-system alignment, unavailable asset/font, ambiguous source, tool limitation, or unresolved defect. Only the first four are acceptable at delivery, and intentional deviations must be visible in the handoff.

## 10. Audit maintainability before delivery

Expand the reconstructed layer tree and check four related questions before treating a visual match as complete:

1. **Responsibility:** Does each page, region, module, component, and content layer have a clear job? Remove duplicate containers and wrappers with no layout, style, clipping, state, or reuse purpose.
2. **Parent-owned layout:** Are alignment, distribution, growth, and wrapping expressed by the parent Auto Layout, constraints, Fill, Hug, and min/max behavior? Do not use child offsets or fake spacing to repair the wrong parent structure.
3. **Sizing and positioning:** Can content-dependent areas grow, and can each fixed dimension be traced to a frame baseline, asset, control requirement, or design-system rule? Keep absolute positioning only for true overlays or decoration.
4. **System binding:** Are recurring colors, typography, gaps, padding, radii, strokes, opacity, and common dimensions bound to the appropriate variables or styles? Promote a repeated new value only when it has stable semantic reuse; do not create a token for incidental sampled pixels.

After structural changes, render again. After shared-asset changes, inspect representative existing consumers in addition to the new frame.
