# Lovable Campaign Requirements

Every clip package delivered for a Lovable campaign must satisfy all 7 requirements before handoff. These are non-negotiable. A package that fails any single requirement is returned to editing.

---

## Requirement 1 — Brand Voice Alignment

Every clip must reflect the campaign's defined brand voice. Before editing begins, obtain the brand voice brief from the campaign brief document. The clip's tone, pacing, and caption style must match the brief's voice descriptors (e.g., "authoritative but warm", "playful and punchy", "earnest and direct").

**Validation:** Read the first 10 seconds of the clip's caption aloud. Does it sound like the brand? Could it have come from their existing best-performing content?

**Deliverable check:** Brand voice brief referenced in editing notes? Y/N

---

## Requirement 2 — Platform-Native Format

Each clip must be exported in the correct native format for each target platform. Do not deliver a single master file and leave reformatting to the client. Deliver one file per platform per clip.

| Platform       | Ratio | Resolution | Max Duration | File Format |
|----------------|-------|------------|--------------|-------------|
| TikTok         | 9:16  | 1080×1920  | 60 s         | MP4 H.264   |
| Instagram      | 9:16  | 1080×1920  | 90 s         | MP4 H.264   |
| YouTube Shorts | 9:16  | 1080×1920  | 60 s         | MP4 H.264   |
| Twitter/X      | 1:1   | 1080×1080  | 60 s         | MP4 H.264   |
| LinkedIn       | 16:9  | 1920×1080  | 3 min        | MP4 H.264   |

**Validation:** Check every export file's metadata against the table above before packaging.

**Deliverable check:** All required platform files present and within spec? Y/N

---

## Requirement 3 — Caption File Included

Every video export must be accompanied by an SRT caption file with accurate timecodes. The SRT file is a campaign asset — it enables the client to republish, translate, or adapt captions independently.

**Format requirements:**
- UTF-8 encoding
- Timecode format: `HH:MM:SS,mmm --> HH:MM:SS,mmm`
- Maximum 2 lines per caption block
- Maximum 42 characters per line
- Minimum caption display duration: 0.8 seconds

**Validation:** Open the SRT in a text editor and verify encoding, line length, and timecode continuity.

**Deliverable check:** SRT file present for every video export? Y/N

---

## Requirement 4 — Hook-to-CTA Coherence

The clip's opening hook and its closing call-to-action must be logically coherent. A hook that promises a revelation must deliver that revelation before the CTA. A CTA that asks the viewer to "learn more" must have delivered enough value to motivate the click.

**CTA types and their required preceding payoff:**

| CTA Type          | Required Payoff                        |
|-------------------|----------------------------------------|
| "Follow for more" | At least one complete insight delivered |
| "Link in bio"     | Specific benefit of clicking named     |
| "Comment X"       | A question or prompt posed clearly     |
| "Share this"      | An emotion (awe, anger, laughter) felt |
| No explicit CTA   | Clip ends on a moment of clear value   |

**Validation:** State the hook promise. State what the clip delivered. Do they match?

**Deliverable check:** Hook promise fulfilled before CTA? Y/N

---

## Requirement 5 — Metadata Package

Every clip export must include a companion metadata file (JSON or plain text) containing the following fields. This metadata is used by the Lovable platform for publishing, tagging, and analytics.

**Required fields:**

```json
{
  "clip_id": "unique identifier",
  "source_video": "original file name or URL",
  "clip_title": "short descriptive title (max 60 chars)",
  "hook_type": "one of: Bold Claim | Open Loop | Empathy Mirror | Counterintuitive Insight | High-Stakes Moment",
  "arc_template": "one of: Fall & Rise | Insight Bomb | Stakes Climb",
  "duration_seconds": 0,
  "target_platforms": ["TikTok", "Instagram"],
  "campaign_id": "campaign identifier",
  "editing_score": "X/20",
  "export_date": "YYYY-MM-DD",
  "caption_file": "filename.srt"
}
```

**Validation:** Verify all fields are populated; no null values except where genuinely not applicable.

**Deliverable check:** Metadata JSON present and complete for every clip? Y/N

---

## Requirement 6 — Thumbnail Selected and Exported

Every clip must include a thumbnail image exported from the clip — not a stock image, not an AI-generated image. The thumbnail must be a single high-expression frame from within the clip itself.

**Thumbnail selection criteria:**
- Speaker face visible and expressive (eyes open, engaged, not mid-blink)
- Frame occurs within the clip's first 20 seconds
- Resolution: 1920×1080 (16:9) or 1080×1920 (9:16) depending on platform
- File format: JPG at 90% quality minimum
- No caption text visible on the thumbnail frame (export a clean frame)

**Optional:** Add a text overlay in the client's brand font — but only if requested in the campaign brief.

**Validation:** View thumbnail at 200% zoom. Skin tones accurate? Expression strong? No blur or compression artefacts?

**Deliverable check:** Thumbnail exported for every clip (per platform ratio)? Y/N

---

## Requirement 7 — Client Review Package Assembled

All deliverables must be packaged into a single organised folder structure before handoff. Do not deliver files as a flat dump. The folder structure signals professionalism and prevents client confusion.

**Required folder structure:**

```
[Campaign ID]_[Client Name]_Clips/
├── README.txt                    # Clip titles, platforms, usage notes
├── clip_01/
│   ├── clip_01_tiktok.mp4
│   ├── clip_01_instagram.mp4
│   ├── clip_01_youtube.mp4
│   ├── clip_01_twitter.mp4
│   ├── clip_01_captions.srt
│   ├── clip_01_thumbnail_916.jpg
│   ├── clip_01_thumbnail_169.jpg
│   └── clip_01_metadata.json
├── clip_02/
│   └── ...
└── campaign_metadata.json        # Aggregate metadata for all clips
```

**README.txt must include:**
- Campaign name and ID
- Clip count and titles
- Target platforms per clip
- Any client-specific usage notes or restrictions
- Handoff date

**Validation:** Open the folder as a first-time viewer. Is every file immediately locatable? Is the README complete?

**Deliverable check:** Folder structure correct, README complete, all files present? Y/N

---

## Handoff Checklist

| Requirement                          | Status (Y/N) |
|--------------------------------------|--------------|
| 1. Brand voice alignment             |              |
| 2. Platform-native format            |              |
| 3. Caption file included             |              |
| 4. Hook-to-CTA coherence             |              |
| 5. Metadata package                  |              |
| 6. Thumbnail selected and exported   |              |
| 7. Client review package assembled   |              |
| **All 7 requirements met?**          |              |

**A package may not be handed off unless all 7 boxes are checked.**
