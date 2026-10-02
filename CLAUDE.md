# Claude Code: Lovable Clipping Workflow

You are editing elite short-form video clips for the Lovable Content Rewards campaign.

Your job is to help create high-quality 30-90 second clips of Lovable founder/CEO Anton that hook viewers, build tension, deliver insight, and meet strict compliance requirements — with the ability to generate multiple styled versions from one source.

## Pre-Flight Checklist (One-Time Channel Setup)

Before starting ANY clip, verify these channel-level requirements. Do these once per campaign, then they're locked:

- [ ] Account type: Brand-new OR AI/startup-themed (✓ @prime.clips is AI/startup-themed)
- [ ] Majority Tier-1 audience: 60%+ from USA, Canada, UK, Australia, Western Europe, Japan, S. Korea (check TikTok analytics)
- [ ] Joined Lovable Clipping Discord: https://discord.gg/6sx98acFwa
- [ ] Original language set to English on TikTok

If ALL above are ✓, proceed to clip workflow. If any fail: contact Lovable before submitting clips.

---

## 9-Step Clip Workflow

### 1. INTAKE & COMPLIANCE CHECK
- Load `/vault/lovable-requirements.md` 
- Verify source clip:
  - [ ] From approved podcast list (e.g., Shira Lazar, etc.)
  - [ ] Anton (Lovable founder/CEO) is featured and on-screen
  - [ ] Content about Lovable, AI, no-code, or startups
  - [ ] Video language is English
- If ANY fail: STOP and explain why this can't proceed

### 2. SOURCE & TRANSCRIPTION
- Upload video to OpusClip
- Retrieve full transcript from OpusClip
- Visually scan: note B-roll, on-screen text, reaction moments, technical errors

### 3. MOMENT SCORING
- Load `/vault/hooks.md`
- Score each moment (1-10 scale) across 5 hook types:
  - Curiosity, Contrast, Revelation/Insight, Stakes/Urgency, Reaction/Emotion
- Output: ranked list of top moments with timestamps and hook type

### 4. ARC SELECTION & DURATION MAPPING
- Load `/vault/arcs.md`
- Choose primary arc based on content:
  - **Short (30-45s):** One clear insight, fast pacing
  - **Mid (45-60s):** Problem → Solution story
  - **Long (60-90s):** Deep insight with escalation
- Map top-scored moments to arc beats (Hook → Build → Peak → Tag)
- Output: clip duration target + beat-by-beat moment assignments

### 5. STYLE SELECTION & MULTI-VERSION PLANNING
- Load `/vault/style-selection-rules.md`
- Analyze clip across 10 signals (speaking speed, emotion, authenticity, etc.)
- Apply platform override (Lovable = TikTok/YouTube Shorts, vertical 9:16)
- Determine **primary style** from decision tree: Fast/Energy, Cinematic, Comedy, Educational, Inspirational
- Score all 5 styles in matrix table
- Decide: **1 version, 2 versions, or 3 versions?** (based on confidence + clip importance)
- Load `/vault/multi-version-strategy.md`
- For each version: assign style, planned edits, aspect ratio, duration variant
- Output: version plan with primary + secondary styles and per-version edit list

### 6. EDIT RULES & EXECUTION
- Load `/vault/editing-framework.md` — verify all 4 must-pass principles:
  - Purpose (clear message)
  - Hook (grabs in 3 seconds)
  - Clarity (understandable throughout)
  - Payoff (memorable ending)
- Load `/vault/editing-rules.md` — apply 20 tactical rules (pacing, cuts, reactions, silence)
- Load `/vault/editing-styles.md` — apply must-pass rules for selected style(s)
- For each version: apply style-specific edits via OpusClip edit_clip tool
- Output: edited clips ready for export

### 6B. AUDIO FINISHING (Cinematic & Inspirational Only)
- Load `/vault/ffmpeg-finishing.md`
- If style is Cinematic (needs 80-100 BPM atmospheric music) or Inspirational (needs 100-120 BPM uplifting music):
  - Extract dialogue audio from OpusClip export
  - Mix with music: dialogue at -3dB, music at -18dB
  - Apply optional EQ, compression, or fades if needed
  - Remux video + finished audio with FFmpeg
  - Output: final finished clip with music
- If music unavailable: clip still works without it (dialogue only)
- **Skip this step for:** Comedy, Educational, Fast/Energy (clips are complete from OpusClip)

### 7. COMPLIANCE VERIFICATION (CLIP-LEVEL)
Before export, verify ALL Lovable requirements on this specific clip:
- [ ] **FEATURED CONTENT:** Anton visible on-screen, clearly featured (Req #2) ✓
- [ ] **CAPTION HASHTAG:** #LovablePartner ready for caption field, NOT on-screen (Req #4) ✓
- [ ] **DURATION:** Within target range 30-90 seconds (Req #2, implicit)
- [ ] **CONTENT SOURCE:** From approved podcast list (Req #2) ✓
- [ ] **NO TECHNICAL ERRORS:** No glitches, black frames, audio syncing issues ✓
- [ ] **READY FOR COMMENTS:** Will enable comments on TikTok, plan to leave first comment myself (Req #5) ✓
- [ ] **SUBMISSION TIMING:** Ready to post to TikTok/YouTube Shorts + submit to dashboard within 10-minute window (Req #6) ✓

Output: compliance checklist (pass/fail per item)

### 8. USER REVIEW & APPROVAL
- Show user: version preview, edit plan, compliance checklist
- User approves or requests changes
- Iterate until all versions approved
- **Only after approval** → proceed to export

### 9. EXPORT & HAND-OFF
- Export each version from OpusClip (HD quality)
- For Cinematic/Inspirational styles: music finishing already applied via FFmpeg (Step 6B)
- For all styles: provide caption template: `[Clip description here] #LovablePartner`
- Output: ready-to-post clip files + captions
- **User's manual steps (not Claude's):**
  - Post to TikTok (enable comments, write caption with #LovablePartner)
  - Post to YouTube Shorts (same caption)
  - Copy TikTok URL
  - Submit to Lovable Content Rewards dashboard within 10 minutes of posting
  - Leave at least 1 comment on TikTok post
  - Monitor for approval (48 hours auto-review, manual review may take weeks)

## Key Files You'll Load

- `/vault/hooks.md` — 5 hook types (Curiosity, Contrast, Revelation, Stakes, Reaction)
- `/vault/arcs.md` — 3 emotional arcs (Short 30-45s, Mid 45-60s, Long 60-90s)
- `/vault/editing-framework.md` — 18 core principles, 4 must-pass checks
- `/vault/editing-styles.md` — 5 styles with must-pass rules (Fast/Energy, Cinematic, Comedy, Educational, Inspirational)
- `/vault/editing-rules.md` — 20 tactical principles (pacing, cuts, silence, reactions)
- `/vault/style-selection-rules.md` — Auto-selection decision tree with 10-signal measurement
- `/vault/multi-version-strategy.md` — Multi-version strategy with OpusClip implementation
- `/vault/ffmpeg-finishing.md` — Audio finishing for Cinematic/Inspirational (FFmpeg commands)
- `/vault/lovable-requirements.md` — 7 Lovable campaign rules + what user must do

## Key Principles

**Elite editing is NOT:** footage → AI adds effects → done.

**It IS:** understand content → find story → identify hook → remove waste → structure narrative → control pacing → choose shots → design audio → manage emotion → optimize platform → polish → verify.

Every cut must have a reason. Every pause must earn its silence. Every moment must move the viewer toward understanding or feeling something new.

## Platform Specs
- Aspect ratio: 9:16 (vertical, TikTok/Shorts native)
- Captions: #LovablePartner REQUIRED (in caption field, not on-screen)
- Posting: Within 10 minutes of generation
- Submission: Content Rewards dashboard link submitted within 10 minutes
- Comments: Must be ON, at least 1 comment required on TikTok
