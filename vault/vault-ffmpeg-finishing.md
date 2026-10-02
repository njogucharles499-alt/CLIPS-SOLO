# Vault: FFmpeg Audio Finishing for Cinematic & Inspirational Clips

FFmpeg handles all audio post-processing for Cinematic and Inspirational versions after OpusClip export.

---

## When to Use FFmpeg

**Cinematic clips (60-90s):**
- Add atmospheric background music (80-100 BPM, building)
- Apply color grading in Premiere (if available)
- Ensure dialogue sits at -3dB, music at -18dB

**Inspirational clips (60-90s):**
- Add uplifting music (100-120 BPM, crescendo)
- Apply warm color grading in Premiere (if available)
- Ensure dialogue clear, music supports

**Comedy, Educational, Fast/Energy:**
- Optional (clips work as-is from OpusClip)
- Use FFmpeg only if adding SFX or music finishing

---

## FFmpeg Workflow

### Step 1: Source Files

After OpusClip export, you'll have:
```
clip-primary.mp4         (video + dialogue, no music)
music-cinematic.mp3      (80-100 BPM, full length)
clip-primary.srt         (optional: subtitle file)
```

### Step 2: Audio Extraction & Analysis

Extract existing audio to process:
```bash
ffmpeg -i clip-primary.mp4 -q:a 9 -n audio-dialogue.mp3
```

Check audio levels:
```bash
ffmpeg -i audio-dialogue.mp3 -af volumedetect -f null -
```
Output shows max volume (target: -3dB for dialogue)

### Step 3: Audio Mixing (Dialogue + Music)

Create a stereo mix: dialogue at -3dB, music at -18dB:

```bash
ffmpeg -i audio-dialogue.mp3 \
  -i music-cinematic.mp3 \
  -filter_complex "[0]volume=0.707[a];[1]volume=0.126[b];[a][b]amix=inputs=2:duration=first[out]" \
  -map "[out]" -q:a 9 -n audio-mixed.mp3
```

**Volume math:**
- Dialogue -3dB = 0.707 × original
- Music -18dB = 0.126 × original

### Step 4: Optional Audio Filters

If dialogue needs clarity or music needs shaping:

**Dialogue EQ (boost presence, 2-4kHz):**
```bash
ffmpeg -i audio-dialogue.mp3 \
  -af "equalizer=f=3000:t=h:w=100:g=3" \
  -q:a 9 -n audio-dialogue-eq.mp3
```

**Compression (control peaks):**
```bash
ffmpeg -i audio-mixed.mp3 \
  -af "compand=attacks=0:decays=0.5:points=-80/-80|-24/-20|0/0" \
  -q:a 9 -n audio-mixed-compressed.mp3
```

**Fade in/out (smooth starts/ends):**
```bash
ffmpeg -i audio-mixed.mp3 \
  -af "afade=t=in:st=0:d=1,afade=t=out:st=59:d=1" \
  -q:a 9 -n audio-mixed-faded.mp3
```

### Step 5: Remux with Video

Combine finished audio back with video:

```bash
ffmpeg -i clip-primary.mp4 \
  -i audio-mixed-faded.mp3 \
  -c:v copy \
  -c:a aac -b:a 192k \
  -map 0:v:0 -map 1:a:0 \
  -shortest \
  -n clip-cinematic-finished.mp4
```

**Flags:**
- `-c:v copy` → don't re-encode video (fast)
- `-c:a aac -b:a 192k` → encode audio as AAC, 192 kbps (good quality)
- `-map 0:v:0 -map 1:a:0` → use video from input 0, audio from input 1
- `-shortest` → end at shortest stream's duration
- `-n` → don't overwrite

### Step 6: Verify Output

Check the finished clip:
```bash
ffprobe clip-cinematic-finished.mp4 -show_format -show_streams | grep -E "(duration|bit_rate|codec_name)"
```

Expected:
- Duration: 60-90 seconds
- Video codec: h264 (from OpusClip)
- Audio codec: aac
- Audio channels: 2 (stereo)

---

## Music Library Requirements

For clips to sound professional, you need:

**Cinematic music:**
- 80-100 BPM, instrumental, atmospheric
- Build/resolve structure (quiet → crescendo → resolve)
- Duration: match clip length (60-90 seconds)
- Format: MP3 or WAV

**Inspirational music:**
- 100-120 BPM, instrumental, uplifting
- Builds to crescendo (motivational arc)
- Duration: match clip length (60-90 seconds)
- Format: MP3 or WAV

**Sources:**
- Epidemic Sound (subscription)
- Artlist (subscription)
- Free Music Archive (royalty-free)
- YouTube Audio Library (free, YouTube clips)

---

## Batch Processing Script

For multiple clips:

```bash
#!/bin/bash
# process-clips.sh
# Usage: ./process-clips.sh source-dir output-dir

SOURCE_DIR=$1
OUTPUT_DIR=$2

for clip in "$SOURCE_DIR"/*-primary.mp4; do
  base=$(basename "$clip" -primary.mp4)
  music="${SOURCE_DIR}/${base}-music.mp3"
  
  if [ ! -f "$music" ]; then
    echo "Skipping $base (no music file)"
    continue
  fi
  
  # Extract dialogue
  ffmpeg -i "$clip" -q:a 9 -n "${OUTPUT_DIR}/${base}-dialogue.mp3"
  
  # Mix audio
  ffmpeg -i "${OUTPUT_DIR}/${base}-dialogue.mp3" \
    -i "$music" \
    -filter_complex "[0]volume=0.707[a];[1]volume=0.126[b];[a][b]amix=inputs=2:duration=first[out]" \
    -map "[out]" -q:a 9 -n "${OUTPUT_DIR}/${base}-mixed.mp3"
  
  # Remux with video
  ffmpeg -i "$clip" \
    -i "${OUTPUT_DIR}/${base}-mixed.mp3" \
    -c:v copy -c:a aac -b:a 192k \
    -map 0:v:0 -map 1:a:0 \
    -shortest -n \
    "${OUTPUT_DIR}/${base}-finished.mp4"
  
  echo "✓ Finished: $base"
done
```

---

## Integration with CLAUDE.md Workflow

**Step 6 (EDIT RULES & EXECUTION) now has two paths:**

**Path A: Comedy, Educational, Fast/Energy**
- Export from OpusClip → done
- No FFmpeg needed

**Path B: Cinematic, Inspirational**
- Export from OpusClip as base video
- Use FFmpeg to add music + audio finishing
- Output: final clip ready to post

**Workflow addition:**

```
### 6B. AUDIO FINISHING (Cinematic/Inspirational Only)

If style is Cinematic or Inspirational:
1. Get music file (80-100 BPM for Cinematic, 100-120 BPM for Inspirational)
2. Extract dialogue audio: ffmpeg -i [clip] audio-dialogue.mp3
3. Mix audio: dialogue -3dB + music -18dB
4. Optional: apply EQ/compression/fades
5. Remux with video: ffmpeg -i [clip] -i [audio] [finished.mp4]
6. Verify output duration matches clip

If music unavailable: clip still works without it (just dialogue).
```

---

## Estimated Processing Time

| Task | Time |
|------|------|
| Extract audio | 10-20s |
| Mix audio | 30-60s |
| Remux video+audio | 20-40s |
| **Total per clip** | ~2-3 minutes |

**For 3-version batch:**
- OpusClip editing: 5-10 minutes (parallel)
- FFmpeg finishing: 6-9 minutes (sequential)
- **Total: ~15-20 minutes per source video**

---

## Troubleshooting

**"FFmpeg not found"**
```bash
which ffmpeg
# If blank, install: apt install ffmpeg
```

**"Could not write header for output file"**
- Check file permissions in output directory
- Use `-n` flag (don't overwrite existing files)

**Audio out of sync**
- Use `-shortest` flag (ensure streams match duration)
- Check frame rates match between video/audio

**Audio too quiet/loud**
- Adjust volume filters: 0.707 = -3dB, 0.5 = -6dB, 0.126 = -18dB
- Verify with ffprobe: `ffprobe -show_entries frame=pkt_dts_time [file]`

**Music doesn't match clip length**
- Trim music: `ffmpeg -i music.mp3 -t 75 -q:a 9 music-75s.mp3`
- Loop music: `ffmpeg -i music.mp3 -filter_complex "aloop=loop=2" music-looped.mp3`

---

## Next: Testing

Ready to test FFmpeg with a real Anton clip? 

1. Export a Cinematic version from OpusClip
2. Get a matching music file (80-100 BPM)
3. Run the FFmpeg workflow above
4. Verify the finished clip sounds good

