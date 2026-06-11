# Skill 3: HyperFrames Automation Export
**Position in pipeline:** Runs AFTER Skill 2.5 issues RENDER CLEARED. Consumes the cleared script; produces the deterministic transition manifest that Skill 3.5 timing-locks. No manifest is compiled from an uncleared script.
**Trigger Phrase:** `Skill 3: HyperFrames Export [Cleared Script]`

---

## PURPOSE

Compile the cleared two-column script into a deterministic JSON transition manifest for the HyperFrames render stack (HTML compositions, seekable paused GSAP timelines on window.__timelines, frame-seek rendering in headless Chrome, FFmpeg encode). The manifest is the single source of truth for the renderer and the lint reference for the Visual Law: any rendered string not declared in schematic_elements is a breach.

---

## INPUTS

The RENDER CLEARED script, including its visual column and per-scene schematic whitelists. If the script carries PATCH REQUIRED or no audit verdict, stop and route it to Skill 2.5.

---

## EXECUTION PROTOCOL

### 1. Scene Segmentation
Walk the script scene by scene. Every manifest entry covers exactly one layout architecture. Scenes containing multiple visual phases are split into one entry per phase, with phase markers (e.g. Scene 04a, Scene 04b) and timestamps subdivided accordingly.

### 2. Manifest Entry Schema
For every entry output:

- **scene_marker** — scene or phase identifier plus timestamp range (e.g. `Scene 03 | 2:10 - 3:05`).
- **layout_architecture** — exactly one of: `3-Column Bento Grid`, `Split-Screen Mechanical Node Diagram`, `Linear Vector Timeline`, `Central Interlocking Loop`, `Live Terminal Code Matrix`, or a declared phase variant of one.
- **schematic_elements** — the complete whitelist of strings permitted to render in this entry: node labels, axis variables, units, mathematical glyphs, terminal readout lines. This list is exhaustive; the renderer may draw nothing textual beyond it.
- **asset_layers** — the exact geometry to construct: SVG path descriptions, geometric blocks, connector lines, background grids, coordinate frames. Each layer named (e.g. `layer_grid`, `layer_node_primary`, `layer_coefficient_bars`) so animation triggers can reference it.
- **accent_map** — which layers carry cyan #27C8D9, amber #E8A33D, or red #D9442B, per the script's accent placement.
- **animation_triggers** — an ordered array of engineering steps. Each step defines:
  - `step` — sequence index.
  - `target` — the named asset layer.
  - `action` — init state, vector trace via stroke-dashoffset, transform, morph, particle event, opacity fade, color shift.
  - `word_cue` — the exact narration word or phrase from the audio column that fires the step. Cues are relative at this stage; absolute seconds are bound in Skill 3.5.
  - `easing_intent` — the motion character, chosen from the Motion Grammar below. Every trigger must name exactly one easing class; unclassified easing is a defect.

### 3. Motion Grammar (Canonical Easing Classes)
Every animation_trigger easing_intent must reference one of these classes. This ensures compositions feel authored, not generated.

| Class | GSAP equivalent | When to use |
|---|---|---|
| `linear-trace` | `power0` | Vector paths drawing via stroke-dashoffset; conveyor belts; data flows. Motion is mechanical, continuous, without acceleration. |
| `ease-out-settle` | `power2.out` | Nodes arriving at a position; blocks sliding into grid slots; elements decelerating to rest. The standard landing motion for structural elements. |
| `ease-in-out-arc` | `power1.inOut` | Camera-style transitions between phases; layout architecture swaps; slow deliberate pivots. |
| `spring-snap` | `elastic.out(1, 0.5)` | Coefficient bars hitting a value; limiting node locking into the amber position; any element that communicates constraint or arrival. |
| `opacity-reveal` | `power1.in` | Elements fading in from 0 to full opacity as a layer becomes active. Never use for structural motion — opacity only. |
| `scale-entry` | `power2.out` on scale 0.85→1.0 | Geometry entering from slightly smaller than final size. Creates visual weight and arrival. Do not scale below 0.8 or above 1.0. |
| `scrub-linear` | ScrollTrigger scrub equivalent, `power0` | Elements whose state is a pure function of timeline position with no easing character — progress bars, accumulating values, counters. |
| `exit-fade` | `power1.in` on opacity 1.0→0 | Elements leaving the frame cleanly. Never cut; always fade. Duration should be shorter than entry. |

**Banned easing:** bounce, back (overshoot), any elastic variant except `spring-snap`, and any easing not in this table. If none of the eight classes fits the action, rewrite the action until one does.

### 4. Global Style Block
The manifest opens with the channel registry as a single style object: canvas #0A0E12, faint dot grid spec, stroke #E8ECEF at 1.25px, monospace typography rule, the three accent hexes with their semantic roles, and the 1920×1080 stage assumption.

### 5. Pre-Flight Verification (Declared, Not Silent)
Before emitting the manifest, output an explicit pre-flight block with the following declarations. If any declaration cannot be confirmed, report the failure instead of emitting.

```
PRE-FLIGHT CHECK — Skill 3
[ ] Every entry names exactly one valid layout architecture from the five canonical types.
[ ] Every word_cue exists verbatim in that scene's audio column.
[ ] Every string in every entry's asset descriptions appears in that entry's schematic_elements whitelist.
[ ] Timestamp ranges tile the full declared runtime with no gaps and no overlaps.
[ ] Every animation_trigger carries exactly one easing_intent from the Motion Grammar.
[ ] No animation step is unbound (every step has a word_cue).
RESULT: MANIFEST CLEAN / MANIFEST DEFECTIVE [list failures]
```

This block appears in the output before the JSON. A MANIFEST DEFECTIVE result stops emission.

---

## OUTPUT FORMAT

1. Pre-flight verification block (MANIFEST CLEAN or MANIFEST DEFECTIVE with failures listed).
2. Global style block.
3. The ordered manifest entries as clean structured JSON.
4. A coverage table: scene markers vs script timestamps, confirming full tiling.
5. Carry-forward note: any ADVISORY factual items still open from the Skill 2.5 register, since voiceover render is the next irreversible step.

---

## HARD RULES
- One manifest per cleared script. Regenerating after script patches requires the full Skill 2.5 re-audit first.
- The manifest is the lint reference. Any rendered text outside schematic_elements is a Visual Law breach attributable to this skill.
- No animation step ships without a word_cue. Unbound steps are defects, not placeholders.
- Every easing_intent must name a class from the Motion Grammar. Unclassified easing is a defect, not a placeholder.
- The pre-flight block is mandatory output. Skipping it is equivalent to skipping the lint pass.
