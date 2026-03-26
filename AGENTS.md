# AGENTS.md - Stageplan Handling Standard

## Purpose
This file defines how agents must create and update ASCII stageplan diagrams and wiring maps.
Goal: predictable, editable, production-readable stageplots.

## Canonical View and Orientation
- Default perspective: audience view.
- `UPSTAGE` at top, `DOWNSTAGE` at bottom.
- Left/right always refer to the drawn page unless user explicitly changes perspective.
- Keep orientation stable across revisions unless user asks to mirror.

## Output Formats
- Primary format: ASCII-only stageplan diagrams.
- Optional export formats: Mermaid and Graphviz.
- ASCII remains the source of truth when multiple formats are present.

## Diagram Container
- Use a single outer stage box.
- Keep consistent horizontal width once established.
- Keep all stage objects inside the stage box unless explicitly marked as external notes or affixes.
- Labels outside the box:
  - `UPSTAGE` above
  - `DOWNSTAGE` below

## Object Notation
- Stage objects in square brackets: `[DRUMS]`, `[GUITAR PEDALBOARD]`, `[MIXER 1]`.
- Use uppercase object names for consistency.
- Use numbered suffixes for repeated devices: `AMP 1`, `AMP 2`, `MIXER 1`, `MIXER 2`.
- Keep object names stable between revisions unless user requests a rename.

## Layout Rules
- Respect row intent:
  - Backline/upstage row for amps/cabs.
  - Drum row centered unless requested otherwise.
  - Frontline/downstage row for vocals and foot-control devices.
- Preserve existing placements when editing; move only requested objects.
- When asked to shift object(s), preserve all unrelated spacing and alignment.
- Keep at least 1 space between object and stage border unless user requests edge flush.
- Centering means visual centering within current box width.

## Wiring Rules (ASCII)
- Use orthogonal wiring only (`x|y`): `-` and `|`, with `+` junctions.
- No diagonal segments.
- No broken paths: each wire must be visually continuous end-to-end.
- Use arrowheads only at destination when needed: `----->`.
- Split outputs:
  - Branch with `+` junction.
  - Keep branches visually distinct.
- Parallel vertical runs:
  - Honor requested spacing (for example gap `0`, gap `1`).
- Do not route wires through labels or object boxes.
- If collision is unavoidable, reroute using clear right-angle detours.

## Signal Description Block
- If requested, include a clean text wiring block below the diagram:
  - `SOURCE -> PROCESS -> DESTINATION`
- Keep this block consistent with drawn wiring.
- If user says "remove wiring," remove both drawn paths and optional wiring block unless asked otherwise.

## Detail Blocks (Outside Diagram)
- Use external detail sections for dense specs:
  - Drums details
  - Keys/noise details
- Format preference:
  - Plain bullet list or ASCII table-like block
  - Use Markdown tables only if explicitly requested.
- Do not duplicate details both inside and outside unless explicitly requested.

## Iterative Edit Protocol
When user asks for a small change:
1. Apply only the requested delta.
2. Keep unchanged geometry intact.
3. Re-check wire continuity.
4. Re-check alignment against previous version.
5. Return the full updated diagram, not a partial fragment.

## Validation Checklist
- Orientation labels present (`UPSTAGE`, `DOWNSTAGE`).
- Requested objects exist and are placed correctly.
- No unintended object movement.
- Wiring style matches requested constraints (`x|y`, spacing).
- No broken or ambiguous wire segments.
- Text description matches diagram exactly.

## Conflict Handling
- Prefer the latest explicit user instruction.
- Preserve all non-conflicting prior constraints.
- If two instructions are irreconcilable, ask one focused clarification and provide a recommended default.

## Quick Command Vocabulary (Recommended)
- `move <object> <direction> <n>`
- `center <object>`
- `wire <source> to <destination>`
- `split <source> to <dest1>, <dest2>`
- `remove wiring`
- `rename <old> to <new>`
