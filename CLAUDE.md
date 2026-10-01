# CLIPS-SOLO — Lovable Clipping Workflow

## Purpose

This repo drives an automated, AI-assisted video-clipping pipeline that surfaces the highest-impact short-form clips from long-form content, cuts each one in the editing style that best fits its content (in 1–3 versions), and packages them into Lovable campaign assets.

## Workflow Overview

```
Long-form video
      │
      ▼
 1. Transcript + Timecodes
      │
      ▼
 2. Hook Detection  ─────────────────►  vault/hooks.md
      │
      ▼
 3. Emotional Arc Mapping  ──────────►  vault/arcs.md
      │
      ▼
 4. Auto-Style Selection  ───────────►  vault/style-selection-rules.md
      │   (primary + secondary style, confidence)
      ▼
 5. Version Planning  ───────────────►  vault/multi-version-strategy.md
      │   (1–3 versions, roles, pairings)
      ▼
 6. Edit each version in its style  ─►  vault/editing-styles.md
      │
      ▼
 7. Craft check (18 principles)  ───►  vault/editing-framework.md
      │
      ▼
 8. Technical QC (20 rules)  ────────►  vault/editing-rules.md
      │
      ▼
 9. Lovable Campaign Package  ───────►  vault/lovable-requirements.md
```

## Directory Structure

```
CLIPS-SOLO/
├── CLAUDE.md                        # This file — workflow guide for Claude
├── vault/
│   ├── hooks.md                     # 5 hook types for clip openers
│   ├── arcs.md                      # 3 emotional arc templates
│   ├── style-selection-rules.md     # Decision tree: content signals → style
│   ├── editing-styles.md            # 5 editing styles and their rules
│   ├── multi-version-strategy.md    # Producing 2–3 versions per source segment
│   ├── editing-framework.md         # 18 core editing principles
│   ├── editing-rules.md             # 20 technical QC rules
│   └── lovable-requirements.md      # 7 Lovable campaign requirements
└── README.md
```

## Claude's Role

When working in this repo, Claude should:

1. **Reference vault files first** before making any clipping or editing decisions.
2. **Apply hooks** from `vault/hooks.md` to evaluate whether a clip's opening seconds earn attention.
3. **Map each clip** to one of the three arcs in `vault/arcs.md` before choosing a style.
4. **Auto-select the style** for every clip using `vault/style-selection-rules.md` — never pick a style by feel.
5. **Plan versions** with `vault/multi-version-strategy.md` based on the selection confidence and clip tier.
6. **Edit each version** to its style's rules in `vault/editing-styles.md`.
7. **Score each version** against the 18 principles in `vault/editing-framework.md`: ≤ 2 misses, all non-negotiables (Purpose, Hook, Clarity, Payoff) pass, and every critical principle for its style passes.
8. **QC each version** against the 20 rules in `vault/editing-rules.md` (≥ 16/20, mandatory rules 3, 5, 7, 20).
9. **Validate the package** against all 7 requirements in `vault/lovable-requirements.md` before export.

## Auto-Style Selection

Run for every candidate clip after hook and arc assignment.

1. **Extract the 10 content signals** (purpose, speaking rate, vocal energy, laughter, emotional weight, structure, arc, hook type, visual quality, ending energy).
2. **Apply overrides** — campaign brief mandates or prohibitions, and platform constraints.
3. **Walk the decision tree** (Q1–Q6) to get the primary style.
4. **Score the matrix** to confirm the primary, pick the secondary, and set confidence (High / Medium / Low).
5. **Record** signals, scores, styles, and confidence in the clip's working notes and metadata.

| Style          | Typical trigger                                           |
|----------------|-----------------------------------------------------------|
| Comedy         | Setup → punchline with a real laugh                       |
| Educational    | Teaching steps, frameworks, definitions, or data          |
| Fast/Energy    | High-energy hot takes, rapid-fire lists                   |
| Inspirational  | Struggle → turning point → triumphant/rallying ending     |
| Cinematic      | Emotional, reflective personal story with strong visuals  |

## Multi-Version Generation

| Confidence | Standard clip | Hero clip |
|------------|---------------|-----------|
| High       | 1 version     | 2 versions |
| Medium     | 2 versions    | 3 versions |
| Low        | 2 versions    | 3 versions |

- **V1 Primary** = primary style. **V2 Contrast** = secondary style (must be a compatible pair). **V3 Wildcard** = third style or V1 with an alternate hook.
- **Re-cut every version from the source**, never from another version.
- **Keep the core fixed** (payoff line, facts, brand voice); vary in/out points, hook, duration, pacing, music, and captions.
- **Distinctness check:** each extra version differs from V1 on ≥ 3 of D1–D7.
- **Max 3 versions** per source segment.
- Package versions as `clip_NN/vN_<style>/` with per-version metadata and a `versions.json` summary.

## Clip Selection Criteria

- **Duration:** set by the style (15–120 s); never exceed 3 minutes.
- **Hook window:** First 3 seconds must match one of the 5 hook types.
- **Arc fit:** The clip must map cleanly to one of the 3 arc templates.
- **Energy:** Audio waveform peak must appear within the first 10 seconds.
- **Captions:** Burned-in captions required for all exports, styled per the editing style.

## Output Formats

| Platform   | Ratio  | Max Duration | Caption Style  | Best-fit styles                       |
|------------|--------|--------------|----------------|---------------------------------------|
| TikTok     | 9:16   | 60 s         | Bold, centered | Fast/Energy, Comedy, Inspirational    |
| Instagram  | 9:16   | 90 s         | Bold, centered | Inspirational, Cinematic, Comedy      |
| YouTube    | 16:9   | 3 min        | Lower-third    | Cinematic, Educational                |
| Twitter/X  | 1:1    | 60 s         | Bold, centered | Comedy, Fast/Energy                   |
| LinkedIn   | 16:9   | 3 min        | Lower-third    | Educational, Inspirational, Cinematic |

## Session Checklist

- [ ] Transcript ingested and timecoded
- [ ] Hook type identified for each candidate clip
- [ ] Arc template assigned
- [ ] Content signals extracted and style auto-selected (primary, secondary, confidence)
- [ ] Version count and roles planned; distinctness check passed
- [ ] Each version edited to its style's rules
- [ ] Each version checked against the 18 principles (≤ 2 misses, non-negotiables and style-critical principles pass)
- [ ] Each version passed technical QC (≥ 16/20, mandatory rules met)
- [ ] Lovable requirements validated (7/7)
- [ ] Exports generated in all target formats, packaged per version
