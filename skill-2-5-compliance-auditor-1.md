# Skill 2.5: Compliance Auditor
**Position in pipeline:** Runs AFTER Skill 2 (Screenplay) and BEFORE Skill 3 (HyperFrames Export). No script reaches the manifest without RENDER CLEARED status.
**Trigger Phrase:** `Skill 2.5: Audit [Script]`

---

## PURPOSE

The in-process inspection gate. Generation self-enforces the production laws; this skill independently verifies them with deterministic checks, because a defect caught here costs one rewrite, and the same defect caught after voiceover and render costs the whole batch. Every check below is mechanical: same script in, same violations out.

---

## CHECK BATTERY

### CHECK A — TTS Character Safety (BLOCKER)
Scan the AUDIO COLUMN ONLY. The following are forbidden anywhere in spoken text:

| Class | Forbidden |
|---|---|
| Dashes | em dash —, en dash –, hyphen - |
| Separators | colon :, semicolon ; |
| Enclosures | ( ) [ ] { } and double quotation marks of any style |
| Digits | 0 1 2 3 4 5 6 7 8 9 |
| Symbols | % & + = / \ # @ * _ ~ ^ < > |

Permitted: period, comma, apostrophe (contractions and possessives), question mark.
Flag for review (MINOR, not blocker): exclamation marks (off-register for the BBC tone) and ellipses (TTS renders them unpredictably).

Every hit is reported with scene number, the offending fragment, and a patched line. Numbers must be respelled as spoken words; hyphenated compounds must be rewritten open or rephrased.

### CHECK B — Hook Integrity (BLOCKER)
First 40 words of Scene 01 audio must contain a concrete open loop (an unanswered question, a withheld identity, a stake) and must NOT contain: greetings, channel references, "today we", "in this video", or any statement of intent to explain. Delay disease in the first 15 seconds fails the audit outright.

### CHECK C — Rehook Cadence (MAJOR)
At the channel's measured pace of roughly one hundred forty five words per minute, the 60-to-90-second rehook law converts to a word budget: **a new loop, tension injection, or pattern interrupt must occur at least every 220 words of audio.** Walk the script in 220-word windows; any window containing zero rehooks is a violation, reported with the window's scene span and a suggested rehook line drawn from the rehook templates in `retention-mechanics-skill.md`.

### CHECK D — Loop Ledger (MAJOR)
Build a table of every curiosity loop: where opened, where closed. Rules:
- Every opened loop must close before the final scene ends.
- The cold open loop must close in the final third (grand payoff), with at least one mid-script touch (foreshadow at roughly one third and two thirds).
- No loop may close without a new loop opening within 10 seconds of audio, except the final payoff.
Unclosed loops and orphan closures are listed by scene.

### CHECK E — But/Therefore Density (MAJOR)
Classify every scene-to-scene and beat-to-beat transition as BUT (reversal), THEREFORE (consequence), or AND-THEN (chronology). Two consecutive AND-THEN transitions anywhere is a violation. Report the ratio; a healthy script runs above 80 percent BUT/THEREFORE.

### CHECK F — Visual Law Lint (BLOCKER)
For every visual cell:
- Extract every string that would render as on-screen text.
- Each string must appear in that scene's schematic whitelist (node labels, units, axis variables, mathematical glyphs).
- Ban-list scan: "title", "subtitle", "caption", "bullet", "text on screen", "label reading", "the words appear" — any instruction implying editor-typed text fails.
- Layout check: every cell must name exactly one of the five layout architectures (3-Column Bento Grid, Split-Screen Mechanical Node Diagram, Linear Vector Timeline, Central Interlocking Loop, Live Terminal Code Matrix) or a declared phase variant of one.

### CHECK G — Runtime Budget (MAJOR)
Total audio word count divided by one hundred forty five must land within 10 percent of the declared runtime target. Per-scene word counts are reported against the scene's timestamp allocation; any scene off by more than 20 percent is flagged for trim or expansion.

### CHECK H — Register & Retention Killers (MINOR)
Sweep for: stacked qualifiers ("might potentially", "one of the possible"), repetition disguised as emphasis (the same intensifier twice within 50 words), throat-clearing ("so basically", "the thing is"), signposting ("now I'm going to tell you"), and YouTube hype vocabulary ("insane", "crazy", "game changer") that breaks the BBC Horizon register. Each hit gets a patched line.

### CHECK I — Factual Claims Register (ADVISORY)
Extract every checkable factual claim (dates, figures, attributions, named entities) into a verification table with a confidence note: VERIFIED IN SOURCE / PLAUSIBLE HEURISTIC / NEEDS CHECK. Claims marked NEEDS CHECK must be resolved or softened before voiceover, since audio is the most expensive layer to re-render.

---

## SEVERITY & VERDICT

| Severity | Meaning | Gate effect |
|---|---|---|
| BLOCKER | TTS character hits, hook failure, Visual Law text breach | Script cannot proceed to Skill 3 |
| MAJOR | Cadence gaps, unclosed loops, chronology chains, runtime drift | Must be patched or explicitly waived by the channel owner |
| MINOR | Register slips, ellipses, repetition | Patch recommended, non-gating |
| ADVISORY | Factual items needing verification | Resolve before voiceover render |

**Verdict line:**
- `RENDER CLEARED` — zero BLOCKER, zero unwaived MAJOR.
- `PATCH REQUIRED` — violations listed; every violation ships with its corrected replacement line so the patch is a paste, not a rewrite.

---

## OUTPUT FORMAT

1. Verdict banner with violation counts by severity.
2. Violations table: check ID, scene, offending fragment, severity, patched replacement.
3. Loop ledger and transition-density summary.
4. Runtime table: per-scene words vs allocation.
5. Factual claims register.

## HARD RULES
- The auditor reports against the text as written, never against intent. If a rule is technically breached, it is reported, then the owner decides.
- Every BLOCKER and MAJOR must include a ready-to-paste fix.
- The audit re-runs in full after patching. Partial re-audits are void.
