# Vault: Multi-Version Strategy (OpusClip Implementation)

This document describes how to generate 1-3 styled versions of a single source clip using OpusClip's native tools and constraints.

---

## How Many Versions?

Decision matrix based on confidence + importance:

| Confidence | Importance | Versions | Primary | Secondary | Tertiary |
|-----------|-----------|----------|---------|-----------|----------|
| 8-10 | High | 3 | ✓ | ✓ | ✓ |
| 8-10 | Medium | 2 | ✓ | ✓ | — |
| 6-8 | High | 2 | ✓ | ✓ | — |
| 6-8 | Medium | 1-2 | ✓ | ? | — |
| <6 | Any | 1 | ✓ | — | — |

**Important:** Version 3 is dropped first if credits run short (see credit budget rules at end).

---

## Copy vs. Resubmit: Decision Tree

When creating a version, decide: **Duplicate this clip** (copy + edits) **or Resubmit the video** (new submission)?

```
Does the version:
├─ Shorter than original (15-30 sec vs 90 sec original)? 
│  └─ AND use the same aspect ratio (9:16)?
│     └─ AND start at same point or later?
│        └─ YES: Use COPY + EDITS (cheaper, faster)
│           NO: Use RESUBMIT (new submission)
│
└─ Longer, earlier start, OR different aspect ratio?
   └─ YES: Use RESUBMIT (new submission)
      NO: Use COPY + EDITS
```

### COPY + EDITS (Cheaper)

**When to use:** Shortening or restyling the original without extending it

**How it works:**
1. Use `opusclip_duplicate_clip(clip_id)` → creates exact copy of the original clip
2. Use `opusclip_edit_clip(clip_id, edits=[...])` → apply style-specific edits to the copy
3. Export the edited clip

**Cost:** ~50 credits per edit (vs. 18+ credits per minute for new submission)

**OpusClip constraint:** Edits can only SHORTEN or REARRANGE. Cannot extend.

### RESUBMIT (More Expensive)

**When to use:** Creating a version that's longer, starts earlier, or uses a different aspect ratio

**How it works:**
1. Use `opusclip_submit_project(...)` → submit same video (or time range) with different settings
2. Wait for clips to generate
3. Export the new submission

**Cost:** ~18 credits per minute of submitted video (we always submit just the segment to save credits)

**Aspect ratio note:** Each aspect ratio (9:16, 1:1, 16:9) requires separate submission

---

## Per-Style Settings & Edit Lists

### FAST/ENERGY

**When to use:** Quick hype moment, announcement, energized insight

**Duration:** 30-45 seconds

**OpusClip Submit Settings (if resubmitting):**
```
{
  "clip_length_range": [30, 45],
  "aspect_ratio": "9:16",
  "auto_hook": true,
  "filler_removal": true,
  "time_range": [start_timestamp, end_timestamp]
}
```

**Edit List for Copy + Edits:**
```
edits = [
  {"type": "remove_filler_words"},
  {"type": "remove_pauses", "min_duration": 1.0},
  {"type": "caption", "style": "fast", "uppercase": false},
  {"type": "trim", "start": 0, "end": 45}  // Ensure under 45s
]
```

**Music & SFX:** OpusClip cannot add these natively. If needed, export to Premiere or use post-processing.

**Cinematic elements:** NO color grading, zooms, or B-roll additions in OpusClip (use post-processing).

---

### CINEMATIC

**When to use:** Deep insight, strategic story, brand moment

**Duration:** 60-90 seconds

**OpusClip Submit Settings (if resubmitting):**
```
{
  "clip_length_range": [60, 90],
  "aspect_ratio": "9:16",
  "auto_hook": true,
  "filler_removal": false,  // Keep natural pauses
  "time_range": [start_timestamp, end_timestamp]
}
```

**Edit List for Copy + Edits:**
```
edits = [
  {"type": "caption", "style": "cinematic", "uppercase": false, "position": "bottom"},
  {"type": "hold_reaction", "threshold": 3.0},  // Hold reactions 3+ seconds
  {"type": "trim", "start": 0, "end": 90}  // Ensure under 90s
]
```

**⚠️ REQUIRES PREMIERE FINISHING:**
- Add cinematic music (100-110 BPM, building/resolving)
- Apply color grading (establish mood: cool/warm, saturation, contrast)
- Add subtle B-roll transitions if available

**Export from OpusClip as:** HD video file, then finish in Premiere

---

### COMEDY

**When to use:** Funny moment, absurd contrast, humorous insight

**Duration:** 30-60 seconds

**OpusClip Submit Settings (if resubmitting):**
```
{
  "clip_length_range": [30, 60],
  "aspect_ratio": "9:16",
  "auto_hook": true,
  "filler_removal": false,  // NEVER remove filler in comedy (breaks timing)
  "time_range": [start_timestamp, end_timestamp]
}
```

**Edit List for Copy + Edits:**
```
edits = [
  {"type": "hold_reaction", "threshold": 1.5},  // Hold laugh/reaction 1.5+ seconds
  {"type": "add_silence", "position": "after_punchline", "duration": 1.0},  // 1s pause after laugh
  {"type": "caption", "style": "fast", "uppercase": false},
  {"type": "trim", "start": 0, "end": 60}  // Ensure under 60s
]
```

**Music & SFX:** Playful, bouncy (110-130 BPM). Can be added in OpusClip or post-processing.

**Finished entirely in OpusClip** (no Premiere needed unless adding sound design)

---

### EDUCATIONAL

**When to use:** Explanation, how-to, multi-step learning

**Duration:** 45-90 seconds

**OpusClip Submit Settings (if resubmitting):**
```
{
  "clip_length_range": [45, 90],
  "aspect_ratio": "9:16",
  "auto_hook": true,
  "filler_removal": false,  // Keep natural pauses for processing info
  "time_range": [start_timestamp, end_timestamp]
}
```

**Edit List for Copy + Edits:**
```
edits = [
  {"type": "remove_filler_words", "aggressive": false},  // Light, not aggressive
  {"type": "caption", "style": "plain", "uppercase": false, "position": "bottom"},  // Plain (not karaoke)
  {"type": "hold_reaction", "threshold": 2.0},  // Let teaching moments breathe
  {"type": "trim", "start": 0, "end": 90}
]
```

**Music & SFX:** Steady, supporting (90-110 BPM). Should not compete with dialogue.

**Finished entirely in OpusClip** (no Premiere needed)

**Note:** Plain captions (not karaoke) require a custom template created in OpusClip web app. See "Caption Templates" section below.

---

### INSPIRATIONAL

**When to use:** Big vision, belief shift, call to action, leadership moment

**Duration:** 60-90 seconds

**OpusClip Submit Settings (if resubmitting):**
```
{
  "clip_length_range": [60, 90],
  "aspect_ratio": "9:16",
  "auto_hook": true,
  "filler_removal": false,  // Keep natural pauses (they're intentional)
  "time_range": [start_timestamp, end_timestamp]
}
```

**Edit List for Copy + Edits:**
```
edits = [
  {"type": "caption", "style": "cinematic", "uppercase": false, "position": "bottom"},
  {"type": "add_silence", "position": "after_major_statement", "duration": 0.5},  // 0.5s pause for weight
  {"type": "hold_reaction", "threshold": 3.0},  // Hold confident moments 3+ seconds
  {"type": "trim", "start": 0, "end": 90}
]
```

**⚠️ REQUIRES PREMIERE FINISHING:**
- Add inspirational music (100-120 BPM, building, uplifting)
- Apply color grading (warmer = hope, brighter = confidence)
- Possibly add B-roll of the future state

**Export from OpusClip as:** HD video file, then finish in Premiere

---

## Version Differences: The 3+ Dimension Rule

Each version MUST differ from the others in 3 or more of these 7 dimensions:

1. **Length** (30s vs 45s vs 60s)
2. **Opening line / hook** (different moment starts)
3. **Aspect ratio** (9:16 vs 1:1 vs 16:9)
4. **Music style** (fast/energetic vs slow/cinematic vs playful)
5. **Pacing** (cuts per 10 seconds: 1-2 vs 3-4 vs 5+)
6. **Captioning** (karaoke vs plain vs overlay text)
7. **B-roll / visual focus** (talking head only vs heavy B-roll vs visual contrast)

**Example:** Cinematic (9:16, 90s, 2 cuts/10s, cinematic music) vs. Fast/Energy (9:16, 45s, 4 cuts/10s, upbeat music) = 3 differences ✓

**Example:** Cinematic (9:16, 90s) vs. Cinematic (1:1, 90s) = only 1 difference (aspect ratio) ✗ Not acceptable

---

## OpusClip Workflow Summary

### Step 1: Submit Source Video
```
opusclip_submit_project(
  video_file_path="source.mp4",
  time_range=[start, end],  // Always submit just the segment
  clip_length_range=[target_min, target_max],
  aspect_ratio="9:16",
  auto_hook=true
)
```

### Step 2: Check Processing Status
```
opusclip_list_projects()
opusclip_list_clips(project_id=X)  // Wait for clips to generate
```

### Step 3: Score & Select Clip
Review transcript and clips. Select the best clip for primary version.

### Step 4: Create Versions

**For Primary + Secondary versions:**
```
// Primary version: apply style-specific edits
opusclip_duplicate_clip(clip_id=primary_clip_id)
opusclip_edit_clip(
  clip_id=duplicate_id,
  edits=[primary_style_edits]
)

// Secondary version: another duplicate with different edits
opusclip_duplicate_clip(clip_id=primary_clip_id)
opusclip_edit_clip(
  clip_id=duplicate_id,
  edits=[secondary_style_edits]
)
```

**For Tertiary version (if needed):**
```
// Resubmit for different aspect ratio or length
opusclip_submit_project(
  video_file_path="source.mp4",
  time_range=[start, end],
  clip_length_range=[tertiary_target_min, tertiary_target_max],
  aspect_ratio="1:1"  // Different ratio
)
```

### Step 5: Export Each Version
```
opusclip_export_clip(
  clip_id=X,
  format="HD"  // or "4K" if available on plan
)
```

### Step 6: Finish Cinematic/Inspirational in Premiere
- If style is Cinematic or Inspirational: add music + color grading in Premiere
- If style is Comedy/Educational/Fast/Energy: clips are done as-is (or post-process as needed)

### Step 7: Export & Hand Off
Ready for posting to TikTok/YouTube Shorts

---

## Caption Templates

**Current status:** Your account has 2 preset templates (both word-by-word karaoke, portrait mode)

**What OpusClip can do natively:**
- Word-by-word karaoke captions (good for Fast/Energy, Comedy)
- Customize caption color, position, uppercase

**What OpusClip CANNOT do:**
- Plain captions (needed for Educational, Cinematic, Inspirational)
- Custom caption styles beyond color/position

**Solution:** Create a plain caption template in OpusClip web app
1. Go to OpusClip web dashboard → Settings → Caption Templates
2. Create new template: "Plain Captions" (not karaoke)
3. Set style: white text on semi-transparent dark box
4. Use in future Educational/Cinematic/Inspirational versions

---

## Credit Budget Rules

Your account: **900 credits/month** (~1 credit per source minute)

### Estimated Costs

| Submission Type | Calculation | Cost |
|---|---|---|
| New submission (2-min segment) | 2 min × 18 = 36 | ~36 credits |
| Copy + edits (1 version) | Flat rate | ~50 credits |
| Copy + edits (all 3 versions from 1 primary) | 3 × 50 = 150 | ~150 credits |
| 3 new submissions (3 different aspect ratios) | 3 × 36 = 108 | ~108 credits |

### Budgeting Strategy

**Recommended per clip:**
- 1 source submission: ~36 credits
- 2-3 versions via copy + edits: ~100-150 credits
- **Total per clip: ~150-180 credits**

**For 900-credit monthly budget:**
- Budget allows **5-6 fully-produced clips per month** (3 versions each)

### If Credits Run Short

**Priority order (drop from lowest priority first):**
1. Drop tertiary (third) version first
2. Keep primary + secondary only
3. If still short: keep primary only
4. Never skip the primary version; stop submissions instead

**Credit check before each batch:**
```
opusclip_get_usage()  // Check remaining credits
```

---

## Premiere Export for Cinematic/Inspirational

After OpusClip export, Cinematic and Inspirational versions need Premiere finishing:

**Music:** 
- Cinematic: 80-100 BPM, atmospheric, builds and resolves
- Inspirational: 100-120 BPM, uplifting, builds to crescendo

**Color grading:**
- Cinematic: Match mood (cool for serious, warm for hopeful)
- Inspirational: Brighter, warmer, high contrast for confidence

**B-roll (if available):**
- Cinematic: Prove key claims (show the problem/solution)
- Inspirational: Show the vision (aspirational imagery)

**Export:** Final 9:16 vertical video, HD or 4K

---

## Example: Creating 2 Versions of One Clip

**Scenario:** Anton explaining why no-code is the future (high confidence, 2-version approach)

**Source submission:**
- Video segment: 2 minutes (Shira Lazar podcast)
- Submitted to OpusClip as 2-minute clip
- OpusClip generates 3-5 clip options
- Claude selects best clip as primary

**Version 1 (Primary: Cinematic)**
- Copy primary clip
- Apply cinematic edits (hold reactions, plain captions)
- Export to HD
- Send to Premiere: add building music, warm color grade
- Final output: 9:16, 60-75 seconds, cinematic style

**Version 2 (Secondary: Educational)**
- Copy primary clip again
- Apply educational edits (light filler removal, plain captions, slower pacing)
- Export to HD
- Done (no Premiere needed)
- Final output: 9:16, 60 seconds, educational style

**Total cost:** ~180 credits (36 submit + 100 edits)

**Differences:**
- Length: 75s vs 60s ✓
- Music: cinematic vs none ✓
- Pacing: 2 cuts/10s vs 2.5 cuts/10s (minor)
- Purpose: storytelling vs learning ✓

Result: 2 distinct versions, ready for posting

