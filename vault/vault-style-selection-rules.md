# Vault: Auto-Style Selection Rules

This document helps Claude automatically select the best editing style for any clip.

---

## 4-Step Style Selection Process

### STEP 1: MEASURE 10 SIGNALS

Scan the source video and rate each signal 1-10:

1. **Speaking Speed:** How fast is Anton talking? (1=slow & measured, 10=rapid-fire)
2. **Energy Level:** How energized does he seem? (1=calm & contemplative, 10=excited & animated)
3. **Emotional Intensity:** How emotionally charged is he? (1=neutral, 10=passionate/funny)
4. **Authenticity of Laughter:** Is he genuinely laughing? (1=no laughter, 10=genuine, contagious laugh)
5. **Information Density:** How many facts/concepts in this clip? (1=one simple point, 10=complex multi-step explanation)
6. **Visual Storytelling:** Is there a narrative arc (problem → solution)? (1=no story, 10=clear story)
7. **Moments of Wonder:** Does he express awe, revelation, or insight? (1=no, 10=multiple wow moments)
8. **B-Roll Availability:** How much supporting footage/graphics? (1=talking head only, 10=rich B-roll)
9. **Music Potential:** Does this need music to land? (1=no, 10=absolutely needs music)
10. **Humor Factor:** Is this funny or absurd? (1=serious, 10=hilarious)

---

### STEP 2: APPLY CAMPAIGN/PLATFORM OVERRIDES

Check for mandatory constraints:

- **Lovable Campaign:** Must feature Anton clearly, must include Lovable product/brand
- **Platform:** TikTok/YouTube Shorts = vertical 9:16, Shorts-friendly durations (30-90s)
- **Audio Constraints:** OpusClip can't add music natively; Cinematic/Inspirational need Premiere finishing

---

### STEP 3: WORK THROUGH THE DECISION TREE

Answer these 6 questions in order:

**Q1: Is this primarily funny?**
- If YES → PRIMARY: Comedy | Ask user about secondary style
- If NO → Go to Q2

**Q2: Is this complex information or a how-to?**
- If YES → PRIMARY: Educational | Ask user about secondary style
- If NO → Go to Q3

**Q3: Is this a story (problem → solution)?**
- If YES → PRIMARY: Cinematic | Ask user about secondary style
- If NO → Go to Q4

**Q4: Does it feel urgent or high-stakes (FOMO, competition, etc.)?**
- If YES → PRIMARY: Fast/Energy | Ask user about secondary style
- If NO → Go to Q5

**Q5: Is this about a big vision, belief shift, or call to action?**
- If YES → PRIMARY: Inspirational | Ask user about secondary style
- If NO → Go to Q6

**Q6: Fall-through: Does the clip need to grab fast (TikTok scroll)?**
- If YES → PRIMARY: Fast/Energy | Ask user about secondary style
- If NO → PRIMARY: Cinematic (balanced, flexible approach) | Ask user about secondary style

---

### STEP 4: SCORE ALL 5 STYLES IN MATRIX

Rate each style's fit for this clip (1-10 scale, where 10 = perfect fit):

| Style | Fit Score | Notes |
|-------|-----------|-------|
| Fast/Energy | ? | Speaking speed {1-10}, Energy {1-10}, Humor {1-10} |
| Cinematic | ? | B-roll {1-10}, Storytelling {1-10}, Emotional intensity {1-10} |
| Comedy | ? | Humor {1-10}, Authenticity of laughter {1-10} |
| Educational | ? | Info density {1-10}, Visual support {1-10} |
| Inspirational | ? | Wonder moments {1-10}, Music potential {1-10}, Vision {1-10} |

---

## Scoring Calculation

**FAST/ENERGY FIT:**
```
(Speed×0.3 + Energy×0.4 + Humor×0.2 + Music-potential×0.1) / 10
```
- Score 7-10: Strong fit
- Score 4-6: Possible fit (check primary style first)
- Score <4: Weak fit

**CINEMATIC FIT:**
```
(B-roll×0.3 + Storytelling×0.3 + Emotion×0.2 + Music-potential×0.2) / 10
```
- Score 7-10: Strong fit
- Score 4-6: Possible fit
- Score <4: Weak fit

**COMEDY FIT:**
```
(Humor×0.5 + Authentic-laughter×0.3 + Pacing-fit×0.2) / 10
```
- Score 7-10: Strong fit
- Score 4-6: Possible fit
- Score <4: Weak fit

**EDUCATIONAL FIT:**
```
(Info-density×0.4 + Visual-support×0.3 + Clarity×0.3) / 10
```
- Score 7-10: Strong fit
- Score 4-6: Possible fit
- Score <4: Weak fit

**INSPIRATIONAL FIT:**
```
(Wonder-moments×0.3 + Big-vision×0.3 + Music-potential×0.2 + Emotion×0.2) / 10
```
- Score 7-10: Strong fit
- Score 4-6: Possible fit
- Score <4: Weak fit

---

## Confidence Scoring

Based on the matrix scores, calculate **overall confidence:**

```
Max style fit score + (second-best score / 2) = Confidence
```

- **Confidence 8-10:** Strong recommendation (primary style clear, secondary clear)
- **Confidence 6-8:** Moderate recommendation (primary clear, secondary possible)
- **Confidence 4-6:** Weak recommendation (primary and secondary both viable; ask user)
- **Confidence <4:** Unclear (no style is a strong fit; ask user for direction)

---

## Multi-Version Recommendation

Based on confidence and clip importance:

**Confidence 8-10 + High Importance:**
- Generate 3 versions: Primary + Secondary + Tertiary (next-best fit)
- Example: Cinematic (primary, 9/10) + Inspirational (secondary, 7/10) + Educational (tertiary, 5/10)

**Confidence 6-8 + Medium Importance:**
- Generate 2 versions: Primary + Secondary
- Example: Comedy (primary, 8/10) + Fast/Energy (secondary, 6/10)

**Confidence 4-6 + Low Importance:**
- Generate 1 version: Primary style only
- Example: Educational (primary, 6/10)

**Confidence <4:**
- Ask user for style direction before proceeding
- Suggest: "No single style stands out. Would you prefer this as Comedy or Educational?"

---

## Example: Scoring a Real Clip

**Scenario:** Anton talking about how Lovable lets non-technical founders ship products in weeks, contrasted with traditional hiring timelines.

**Signal measurements:**
- Speaking speed: 7 (moderately fast)
- Energy level: 8 (very animated, excited)
- Emotional intensity: 7 (passionate about the opportunity)
- Authenticity of laughter: 4 (one laugh, not extended)
- Information density: 6 (a few key concepts)
- Visual storytelling: 8 (clear problem/solution arc)
- Moments of wonder: 6 (insight about speed advantage)
- B-roll availability: 7 (code demos available)
- Music potential: 7 (builds naturally)
- Humor factor: 3 (not particularly funny)

**Decision tree:**
- Q1 (Is this funny?): NO → Q2
- Q2 (Complex info?): Moderate, but more story → Q3
- Q3 (Is it a story?): YES → **PRIMARY: Cinematic**

**Matrix scoring:**
- Fast/Energy: (7×0.3 + 8×0.4 + 3×0.2 + 7×0.1) / 10 = **6.2** ← Possible fit
- Cinematic: (7×0.3 + 8×0.3 + 7×0.2 + 7×0.2) / 10 = **7.2** ← Strong fit ✓
- Comedy: (3×0.5 + 4×0.3 + 6×0.2) / 10 = **3.9** ← Weak fit
- Educational: (6×0.4 + 7×0.3 + 8×0.3) / 10 = **6.9** ← Possible fit
- Inspirational: (6×0.3 + 8×0.3 + 7×0.2 + 7×0.2) / 10 = **7.0** ← Strong fit ✓

**Confidence:** 7.2 + (7.0 / 2) = **10.7 capped at 10** = HIGH CONFIDENCE

**Recommendation:**
- PRIMARY: **Cinematic** (7.2/10)
- SECONDARY: **Inspirational** (7.0/10)
- TERTIARY: **Educational** (6.9/10)
- **MULTI-VERSION:** 2-3 versions recommended (high confidence + strong story)

---

## When to Override Auto-Selection

As Claude Code, you CAN override the auto-selection if:

1. **User explicitly requests a style:** "Make this as a Comedy" → Use Comedy, don't second-guess
2. **Campaign constraints force it:** Lovable requires Anton to be the focus → Cinematic works better than Fast/Energy
3. **Clip is low confidence:** If <4/10 overall, ask user rather than guessing
4. **Multiple signals conflict:** If signals are mixed, present primary + secondary equally to user

**Never override without explanation.** Always tell the user why you picked a style and what the alternative was.

