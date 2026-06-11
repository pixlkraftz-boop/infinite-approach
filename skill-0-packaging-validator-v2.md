# Skill 0: Packaging Validator (v2 — Concept-First)
**Position in pipeline:** Runs BEFORE Skill 1. No source enters deconstruction without a GREENLIGHT verdict.
**Trigger Phrase:** `Skill 0: Validate [Concept / Source]`

---

## PURPOSE

A video's view ceiling is set at the packaging layer, before a single line of script exists. This skill pressure-tests whether a candidate **concept** deserves production by generating competing title and thumbnail packages, gathering live market evidence through the connected research stack, and issuing a kill-or-greenlight verdict on data rather than instinct.

The unit of validation is the **concept** (the drawable mechanism), not the source it came from. A textbook, paper, or documented real-world system is raw material; the package sells the mechanism.

---

## EXECUTION PROTOCOL

### PHASE 0 — Concept Extraction
Before generating packages, state in one sentence the operational mechanism being sold (e.g. "atmospheric reentry converts kinetic energy to heat because the air cannot move out of the way fast enough" or "the rocket equation means every kilogram of payload requires exponentially more fuel"). If the candidate is a source rather than a concept, extract its strongest drawable mechanism first and validate that.

Gate question: **does the concept stand alone for a viewer who has never heard of the source?** If the concept only works with prior knowledge of the source material, it is an automatic KILL.

### PHASE 1 — Angle Generation
Generate 6 to 10 candidate packages for the concept. Each package = title + thumbnail concept + core promise.

Titles must be built from the frameworks in `title-formulas-skill.md`, prioritising the verified high-hook-score families:
- Mechanism frames ("How X Actually Works", "The System Behind Y", "The Engineering Behind X") for the channel's analytical register
- Reality frames ("The REALITY of X", "Why X Is Nothing Like You Think") for correcting misconceptions
- Failure frames ("Why X Always Fails at Y", "The Engineering Reason X Dies") for failure mode content
- Stakes frames ("The Equation That Decides X", "Why X Makes Y Impossible") for physics and mathematics content

Rules:
- Under 60 characters. Specific beats vague: real names, real figures, real physical quantities.
- **HARD RULE — the title sells the mechanism, never the source.** No textbook titles, no "explained" framings anchored to a source. "The Equation That Decides If You Ever Leave Orbit" is valid; "Tsiolkovsky Rocket Equation Explained" is weaker and does not prioritise in scoring. The source name may appear in the title only when the source itself is the famous entity (e.g. a mission, a spacecraft, a physical phenomenon) rather than a publication.
- The title must promise the *mechanism*, not the report of it.
- Title and thumbnail must complement, never duplicate.
- Content must be evergreen — not dependent on a news cycle or launch schedule.

### PHASE 2 — Thumbnail Concept (Channel Language)
Every thumbnail concept must be expressible in the channel's geometric monoline language: dark canvas, thin vector structures, one accent colour, at most one native schematic marking (an equation glyph, a unit, a force vector label). No faces required, no stock imagery, no CGI renders, no editor-styled caption text. The thumbnail is the first frame of the visual mechanism, not a poster for it.

For each package specify: focal geometry, accent colour placement, the single permitted schematic marking (if any), and the emotional read at thumbnail size (threat, mystery, mechanism, collapse, scale).

### PHASE 3 — Market Evidence Pass (Connected Tools)
Run the research stack before scoring. **Mechanism phrases are the primary keywords; source title and author are secondary signals.** Minimum evidence set:

1. **Keyword demand** — VidIQ `vidiq_keyword_research` on: 2 to 3 mechanism phrases first (e.g. "how reentry works", "rocket equation explained", "orbital mechanics", "why spacecraft fail", "black hole physics"), then the source title as a secondary check. Record volume, competition, and overall score for each.
2. **Proven outliers** — VidIQ `vidiq_outliers` and/or Algrow `search_viral_videos` (content_type longform) on the mechanism topic. Record the top 5 performers: views, outlier score, channel size, age. An outlier score of 2 or higher on a comparable video is positive demand evidence; 3+ is strong. Outliers on mechanism-framed videos weigh more than outliers on news-reaction videos.
3. **Competitive saturation** — NexLev `search_niche_finder_channels` or `search_videos` on the mechanism. Count credible recent treatments (under 2 years old, over 100K views). Note the visual format of the leaders: if every winner is a CGI cinematic or talking head, a code-rendered geometric treatment is a differentiation gap, not a saturation problem.
4. **Title-frame validation** — Algrow/NexLev `youtube_search` sorted by views on the leading candidate title's core phrase, to confirm the frame itself has pulled views before.

If tool calls fail or return nothing, say so explicitly and score the Demand axis conservatively. Never fabricate metrics.

### PHASE 4 — Scoring Matrix
Score each surviving package 0 to 10 on five axes:

| Axis | What it measures | Evidence source |
|---|---|---|
| **Demand Evidence** | Search volume + proven outlier views on adjacent content, mechanism-framed evidence weighted above news-reaction evidence | Phase 3 data only |
| **CTR Architecture** | Open loop strength, specificity, stakes, title-thumbnail complementarity | Framework fit |
| **Format Fit** | How naturally the mechanism renders as geometric animation (force diagrams, cycles, timelines, and equations score high; vibe-based or narrative-only content scores low) | Editorial judgment |
| **Competition Gap** | Inverse of credible recent treatments, adjusted for visual differentiation | Phase 3 data |
| **Evergreen Half-life** | Will this package still pull clicks in 3 years regardless of news cycles | Editorial judgment |

### PHASE 5 — Verdict Gate

- **GREENLIGHT:** total ≥ 38/50 AND no axis below 5 AND at least one piece of hard outlier evidence (a comparable video at outlier score ≥ 2). Proceed to Skill 1 with the winning package locked.
- **REWORK:** total 30–37, or strong demand with weak packaging. Regenerate angles in Phase 1; the concept survives, the packages die.
- **KILL:** total < 30, or zero demand evidence across all tool passes, or Format Fit below 4, or the concept fails the Phase 0 standalone test, or the concept is news-cycle dependent. The concept does not enter production. State the kill reason in one sentence.

---

## OUTPUT FORMAT

1. Concept statement (one sentence) and source credit line.
2. Package table: all candidates with title, thumbnail concept, one-line promise.
3. Evidence log: every tool call made, headline numbers returned, and any calls that failed.
4. Scoring matrix for the top 3 packages.
5. Verdict block: GREENLIGHT / REWORK / KILL, the locked winning package, and the single sentence of reasoning that would justify the decision to a sceptical channel owner.

---

## HARD RULES
- No verdict without the evidence log. Scores citing no data are void.
- The skill kills concepts. If the data says kill, the output says kill, regardless of how interesting the mechanism is.
- News-cycle dependent concepts ("Why SpaceX's latest launch matters") are killed before scoring. The channel is evergreen.
- Source-anchored titles ("X Explained" where X is a textbook or paper) are deprioritised in scoring.
- One winning package only. Ties are broken by Demand Evidence.
