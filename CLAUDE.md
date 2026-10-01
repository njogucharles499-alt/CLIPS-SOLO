# CLIPS-SOLO — Lovable Clipping Workflow

## Purpose

This repo drives an automated, AI-assisted video-clipping pipeline that surfaces the highest-impact short-form clips from long-form content and packages them into Lovable campaign assets.

## Workflow Overview

```
Long-form video
      │
      ▼
 Transcript + Timecodes
      │
      ▼
 Hook Detection  ──►  vault/hooks.md
      │
      ▼
 Emotional Arc Mapping  ──►  vault/arcs.md
      │
      ▼
 Clip Selection & Editing  ──►  vault/editing-rules.md
      │
      ▼
 Lovable Campaign Package  ──►  vault/lovable-requirements.md
```

## Directory Structure

```
CLIPS-SOLO/
├── CLAUDE.md                   # This file — workflow guide for Claude
├── vault/
│   ├── hooks.md                # 5 hook types for clip openers
│   ├── arcs.md                 # 3 emotional arc templates
│   ├── editing-rules.md        # 20 elite editing principles
│   └── lovable-requirements.md # 7 Lovable campaign requirements
└── README.md
```

## Claude's Role

When working in this repo, Claude should:

1. **Reference vault files first** before making any clipping or editing decisions.
2. **Apply hooks** from `vault/hooks.md` to evaluate whether a clip's opening second earns attention.
3. **Map each clip** to one of the three arcs in `vault/arcs.md` before finalizing the cut.
4. **Score clips** against all 20 rules in `vault/editing-rules.md`; a clip must pass ≥16/20.
5. **Validate outputs** against all 7 requirements in `vault/lovable-requirements.md` before export.

## Clip Selection Criteria

- **Duration:** 30–90 seconds optimal; never exceed 3 minutes.
- **Hook window:** First 3 seconds must match one of the 5 hook types.
- **Arc fit:** The clip must map cleanly to one of the 3 arc templates.
- **Energy:** Audio waveform peak must appear within the first 10 seconds.
- **Captions:** Burned-in captions required for all exports.

## Output Formats

| Platform   | Ratio  | Max Duration | Caption Style  |
|------------|--------|--------------|----------------|
| TikTok     | 9:16   | 60 s         | Bold, centered |
| Instagram  | 9:16   | 90 s         | Bold, centered |
| YouTube    | 16:9   | 3 min        | Lower-third    |
| Twitter/X  | 1:1    | 60 s         | Bold, centered |

## Session Checklist

- [ ] Transcript ingested and timecoded
- [ ] Hook type identified for each candidate clip
- [ ] Arc template assigned
- [ ] Editing rules scored (≥16/20)
- [ ] Lovable requirements validated (7/7)
- [ ] Exports generated in all target formats
