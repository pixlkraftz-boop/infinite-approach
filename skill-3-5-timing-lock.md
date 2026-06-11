# Skill 3.5: Timing Lock
**Position in pipeline:** Final stage. Runs AFTER Skill 3, once the TTS voiceover is rendered. Consumes manifest v1 plus the audio; emits manifest v2 with absolute timing and HyperFrames composition guidance.
**Trigger Phrase:** `Skill 3.5: Timing Lock [Manifest + Voiceover]`

---

## PURPOSE

Convert the cue-relative manifest into an absolutely timed render specification. Every animation trigger's word_cue is resolved to timeline seconds against the real voiceover, so the headless renderer can seek any frame deterministically and the composition plays in lockstep with narration.

---

## INPUTS (HARD REQUIREMENT)

1. Manifest v1 from Skill 3 (must carry MANIFEST CLEAN status from the Skill 3 pre-flight).
2. The rendered TTS audio file, or its word-level timestamp data (word, start seconds, end seconds).

**If no audio or word-level timestamps are supplied, state that timing remains cue-relative and stop.** Do not estimate absolute times from word counts; estimated timing is a render defect.

---

## EXECUTION PROTOCOL

### 1. Cue Resolution
For every animation trigger, locate its word_cue in the word-level timestamps. Bind the trigger to the cue word's start time in absolute seconds. Where a cue phrase spans multiple words, bind to the first word's start. Flag any cue that cannot be located verbatim (narration drift between script and rendered audio) — these are BLOCKERS requiring either a manifest patch or an audio re-render decision by the owner.

### 2. Scene Duration Truth
Replace the manifest's estimated timestamp ranges with true scene durations derived from the audio: each scene runs from its first cue context to the start of the next scene's first narration word. Verify scenes still tile the full audio length with no gaps or overlaps. Report total true runtime vs the declared target.

### 3. Manifest v2 Emission
Emit the updated manifest: identical structure to v1, with every trigger carrying `time_abs` in seconds alongside its original word_cue, and every scene_marker carrying true start and end seconds.

### 4. Composition Guidance
Alongside manifest v2, emit HyperFrames-ready build guidance covering five areas:

**Timeline registration**
One paused GSAP timeline per composition, registered as `window.__timelines[composition_id]`. All trigger times positioned absolutely on the timeline; nothing autoplays. The engine seeks, it never plays.

**Stage**
1920×1080, canvas #0A0E12 per the global style block. Dot grid rendered as a CSS background pattern, not a DOM layer, so it never interferes with GSAP targets.

**Narration mount**
The voiceover as a native audio element with `data-start`, `data-duration`, and `data-track-index` set from the true runtime.

**Determinism rules**
No Math.random without a seeded generator. No Date.now dependencies. No CSS animations or CSS transitions outside the registered timeline — every visual state must be a pure function of timeline position. If an element needs to appear animated at a static frame, its state is computed from `time_abs`, never from a running clock.

**Per-scene element map**
Composition DOM structure mirroring the manifest's named asset layers, so each GSAP tween targets a stable selector. Layer naming convention: `[scene_marker]__[layer_name]` (e.g. `scene03__layer_node_primary`). No anonymous elements; every animated target is named.

### 5. Motion Implementation (GSAP Tween Specs)
For every animation trigger in the manifest, translate the `easing_intent` class into a concrete GSAP tween spec. Use the following translation table, which maps the Skill 3 Motion Grammar to implementation parameters:

| Easing class | GSAP ease string | Typical duration | Notes |
|---|---|---|---|
| `linear-trace` | `"none"` | match narration beat length | Drive via `strokeDashoffset`; set `strokeDasharray` equal to path length on init |
| `ease-out-settle` | `"power2.out"` | 0.4–0.6s | Standard for all structural arrivals; do not exceed 0.8s |
| `ease-in-out-arc` | `"power1.inOut"` | 0.6–1.0s | Reserved for phase transitions; do not use for small element motion |
| `spring-snap` | `"elastic.out(1, 0.5)"` | 0.5s | Amplitude 1, period 0.5 only — do not vary these values |
| `opacity-reveal` | `"power1.in"` | 0.3–0.5s | fromTo opacity 0→1 only; never combine with transform in same tween |
| `scale-entry` | `"power2.out"` | 0.4–0.5s | fromTo scale 0.85→1.0 only; combine with `opacity-reveal` as a staggered pair if needed |
| `scrub-linear` | `"none"` | driven by `time_abs` delta | Set tween duration equal to the time between the trigger and the next trigger on the same layer |
| `exit-fade` | `"power1.in"` | 0.2–0.35s | Always shorter than the entry duration for the same element |

**Banned in implementation:** `bounce`, `back`, `elastic` variants other than `elastic.out(1, 0.5)`, CSS `transition`, CSS `animation`, `requestAnimationFrame` loops outside the registered timeline.

**Stagger rule:** When multiple sibling layers animate on the same word_cue, stagger their `time_abs` by 0.06s per element. Never fire more than five elements simultaneously.

**Init state rule:** Every animated element must be set to its initial state (opacity 0, scale 0.85, strokeDashoffset at full path length, etc.) before the timeline starts. No element should be visible in its final state before its trigger fires.

### 6. Pre-Flight Verification (Declared, Not Silent)
Before emitting manifest v2 and composition guidance, output an explicit pre-flight block:

```
PRE-FLIGHT CHECK — Skill 3.5
[ ] All word_cues resolved to absolute seconds. Zero unresolved cues.
[ ] Scene timestamp ranges updated to true audio durations. Full tiling confirmed.
[ ] Every easing_intent translated to a concrete GSAP tween spec.
[ ] Every animated element has an init state declared before timeline start.
[ ] No CSS animations or CSS transitions present outside the registered GSAP timeline.
[ ] Stagger rule applied to all simultaneous triggers (max 5 elements, 0.06s stagger).
[ ] Layer naming convention [scene_marker]__[layer_name] applied throughout.
RESULT: COMPOSITION READY / COMPOSITION BLOCKED [list failures]
```

A COMPOSITION BLOCKED result stops emission. Every blocked item must have a ready-to-paste fix.

---

## OUTPUT FORMAT

1. Pre-flight verification block (COMPOSITION READY or COMPOSITION BLOCKED with fixes).
2. Cue resolution report: total triggers, bound count, any unresolved cues as BLOCKERS.
3. Runtime table: per-scene true durations vs manifest v1 estimates, plus total runtime vs target.
4. Manifest v2 (full JSON).
5. Composition guidance block with tween specs for every trigger.

---

## HARD RULES
- No absolute timing without real audio data. Cue-relative manifests never ship to render.
- Unresolved cues are BLOCKERS; the skill does not silently rebind to nearby words.
- Every easing_intent must be translated to a concrete tween spec. Untranslated intents are defects.
- The pre-flight block is mandatory. Skipping it voids the composition guidance.
- If the audio is re-rendered for any reason, Timing Lock re-runs in full. Partial re-locks are void.
