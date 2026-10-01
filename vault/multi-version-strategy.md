# Multi-Version Strategy

How to produce 2–3 distinct versions of a clip from one source segment, each in a different editing style, so the campaign can test which treatment performs best and serve each platform its native cut.

---

## 1. How Many Versions

Decide the version count from the confidence level in `style-selection-rules.md` and the campaign tier.

| Confidence | Standard clip | Hero clip (campaign's top 1–3 moments) |
|------------|---------------|----------------------------------------|
| High       | 1 (primary)   | 2 (primary + secondary)                |
| Medium     | 2             | 3                                      |
| Low        | 2             | 3                                      |

**Hard cap: 3 versions per source segment.** Beyond three, versions start to converge and the extra effort doesn't produce new learning.

---

## 2. Version Roles

| Version | Role | Style | Purpose |
|---------|------|-------|---------|
| **V1 — Primary** | The best-guess cut | Primary style from the selection rules | The version you'd ship if you could only ship one. |
| **V2 — Contrast** | A genuinely different treatment | Secondary style from the selection rules | Tests a different hypothesis about what the audience wants. |
| **V3 — Wildcard** | A platform-native or hook-variant cut | Third-highest compatible style **or** V1's style with a different hook | Covers a platform V1/V2 don't suit, or tests the hook rather than the style. |

V2 must be a "Yes" pair with V1 in the compatibility table in `style-selection-rules.md`.

---

## 3. What Changes vs. What Stays Fixed

### Fixed across all versions (the "core")

- **The payoff line** — the single most important line in the segment.
- **Facts and claims** — no version may change the meaning of what the speaker said.
- **Brand voice** constraints from the campaign brief.
- **Technical QC** — every version passes all 20 rules in `editing-rules.md` on its own.

### Variable per version

| Variable | Fast/Energy | Cinematic | Comedy | Educational | Inspirational |
|----------|-------------|-----------|--------|-------------|---------------|
| In-point | Latest possible — mid-claim | Earlier — allow a quiet open | At the start of the setup | At the outcome statement | At the struggle |
| Out-point | Right on the strongest line | 1–2 s held after the last line | On the laugh / reaction | After the recap line | Within 5 s of the peak |
| Duration | 20–45 s | 60–120 s | 15–45 s | 45–90 s | 45–90 s |
| Hook type | Bold Claim / Counterintuitive | High-Stakes / Open Loop | Open Loop | Counterintuitive / Bold Claim | Empathy Mirror / High-Stakes |
| Music | 120–150 BPM, beat-cut | Sparse, swell at turn | None / minimal | Neutral, low | Builds to peak |
| Captions | Animated, 1–3 words | Clean sentence-case | Timed to withhold punch | Labels + keyword emphasis | Weight builds to peak |
| Cuts / 10 s | 5–8 | 1–2 | 2–4 | 2–3 | 1–2 → 3–5 |

---

## 4. Production Workflow

```
1. Lock the core
   └─ Mark the payoff line and any must-keep lines on the transcript.

2. Cut V1 (primary style) from the source
   └─ Full framework score + 20 rules.

3. Cut V2 from the SOURCE, not from V1
   └─ Re-choose in/out points, hook, and pacing for the V2 style.
   └─ Full framework score + 20 rules.

4. (If needed) Cut V3 from the SOURCE
   └─ Either a third style or V1 style with an alternate hook.

5. Distinctness check (Section 5)

6. Package all versions together (Section 7)
```

**Always re-cut from source.** Re-editing V1 into V2 inherits V1's in/out points and pacing decisions and produces a version that is the same clip with different music. Each version starts from the raw segment with fresh cut decisions.

Each version is scored independently against the 80-point framework using **its own style's critical sections**.

---

## 5. Distinctness Check

Versions must be meaningfully different. V2 (and V3) must differ from V1 on **at least 3** of the following:

| # | Difference | Threshold |
|---|------------|-----------|
| D1 | Duration | ≥ 20% longer or shorter |
| D2 | Average shot length | ≥ 50% longer or shorter |
| D3 | Opening line | Different first sentence |
| D4 | Hook type | Different hook from `hooks.md` |
| D5 | Ending | Different final line or final beat |
| D6 | Music | Different track or no music vs music |
| D7 | Caption style | Different caption treatment |

If a version fails the check, re-cut it further toward its style's extremes, or drop it.

---

## 6. Proven Pairings

### Fast/Energy (V1) ↔ Educational (V2)
- **Source shape:** list of tips or a framework.
- **V1:** top 3 points only, 25–35 s, punch-ins, beat-cut music.
- **V2:** all points with numbered labels, 60–75 s, recap ending.
- **Tests:** does this audience want the hit or the depth?

### Inspirational (V1) ↔ Cinematic (V2)
- **Source shape:** personal fall-and-rise story.
- **V1:** opens on the struggle, accelerates, ends on the rallying line.
- **V2:** opens quietly, holds on faces, ends on the reflective line with a held final frame.
- **Tests:** does the audience respond to energy or to intimacy?

### Comedy (V1) ↔ Fast/Energy (V2)
- **Source shape:** funny story or banter.
- **V1:** full setup, pauses for laughs, ends on the reaction.
- **V2:** compressed to the punchline and best reaction, under 20 s, text-driven.
- **Tests:** does the full timing or the instant payoff travel further?

### Fast/Energy (V1) ↔ Inspirational (V2)
- **Source shape:** motivational message or mindset shift.
- **V1:** hot-take framing, under 30 s.
- **V2:** builds from the problem to a single peak line, 60 s.
- **Tests:** hype vs emotional build.

### V3 Hook Variant (any style)
- Same style and body as V1; only the first 3 seconds change to a different hook type.
- Isolates the hook as the single tested variable.

---

## 7. Naming & Packaging

Versions live inside their clip's folder from `lovable-requirements.md` Req. 7:

```
clip_01/
├── v1_inspirational/
│   ├── clip_01_v1_tiktok.mp4
│   ├── clip_01_v1_instagram.mp4
│   ├── clip_01_v1_captions.srt
│   ├── clip_01_v1_thumbnail_916.jpg
│   └── clip_01_v1_metadata.json
├── v2_cinematic/
│   └── ...
└── versions.json            # summary of all versions for this clip
```

Each version's metadata extends the standard fields with:

```json
{
  "clip_id": "clip_01",
  "version_id": "clip_01_v2",
  "version_role": "Primary | Contrast | Wildcard",
  "editing_style": "Cinematic",
  "hook_type": "High-Stakes Moment",
  "framework_score": "68/75 (91%)",
  "distinct_from_v1": ["D1", "D2", "D3", "D5", "D6"],
  "recommended_platforms": ["YouTube", "Instagram"]
}
```

---

## 8. Platform Assignment

When versions are not being A/B tested on the same platform, route each to where its style fits best.

| Style          | First-choice platforms           | Avoid                   |
|----------------|----------------------------------|-------------------------|
| Fast/Energy    | TikTok, Shorts, Reels            | LinkedIn                |
| Cinematic      | YouTube, Instagram, LinkedIn     | TikTok (if > 60 s)      |
| Comedy         | TikTok, Reels, Twitter/X         | LinkedIn (unless brief allows) |
| Educational    | LinkedIn, YouTube, Instagram     | —                       |
| Inspirational  | Instagram, LinkedIn, TikTok      | —                       |

---

## 9. Testing & Learning

When versions are A/B tested on the same platform:

1. **Publish within the same time window** (same day and hour slot, or as a platform-native A/B test where available).
2. **Read results at 48 hours** and again at 7 days.
3. **Compare on these metrics**, in priority order:

| Metric | What it tells you |
|--------|-------------------|
| 3-second hold rate | Hook strength |
| Average % watched | Pacing and retention |
| Completion rate | Payoff and ending |
| Shares + saves per 1k views | Emotional / practical value |
| Comments per 1k views | Provocation and engagement |

4. **Declare a winner** only when it leads on **average % watched and at least one of shares/saves**, with a margin of ≥ 15%. Otherwise record the result as "no clear winner".
5. **Log the learning** in the campaign notes: source type, styles tested, winner, margin. After 5+ tests for a client, use the log to adjust their default primary style in the selection rules (e.g. "this audience prefers Educational over Fast/Energy for list content").
