# Style Selection Rules

How to choose the editing style (`editing-styles.md`) for a candidate clip. Run this **after** hook and arc assignment and **before** editing begins.

The process has four steps:

```
1. Extract content signals
        │
        ▼
2. Apply overrides (brief / platform)
        │
        ▼
3. Walk the decision tree  ──►  primary style
        │
        ▼
4. Score the matrix  ──►  confirm primary, pick secondary, set confidence
```

The output is a **primary style**, a **secondary style**, and a **confidence level** — the secondary style feeds `multi-version-strategy.md`.

---

## Step 1 — Extract Content Signals

Measure these from the transcript, audio, and video of the candidate segment.

| Signal | How to measure | Values |
|--------|----------------|--------|
| **S1 Purpose** | What the segment is trying to do | Teach / Move / Amuse / Provoke / Inspire |
| **S2 Speaking rate** | Words per minute from timecoded transcript | Slow < 130 · Medium 130–170 · Fast > 170 |
| **S3 Vocal energy** | Pitch and volume variance across the segment | Low / Medium / High |
| **S4 Laughter** | `[laughter]` tags, audible laughs, banter markers | None / Some / Strong (≥ 1 laugh from speaker or audience after a setup) |
| **S5 Emotional weight** | Personal disclosure, vulnerability, loss, struggle words | Low / Medium / High |
| **S6 Structure** | Shape of the content | List / Steps / Story / Argument / Banter |
| **S7 Arc** | From `arcs.md` | Fall & Rise / Insight Bomb / Stakes Climb |
| **S8 Hook type** | From `hooks.md` | Bold Claim / Open Loop / Empathy Mirror / Counterintuitive / High-Stakes |
| **S9 Visual quality** | Lighting, framing, B-roll availability | Basic (talking head only) / Good / Cinematic (strong B-roll, locations) |
| **S10 Ending energy** | Tone of the final 10 seconds | Triumphant / Reflective / Punchline / Actionable / Provocative |

Record all ten signals in the clip's working notes before continuing.

---

## Step 2 — Overrides

Check these first. An override sets the primary style directly; continue to Step 4 only to choose the secondary style.

| # | Override | Result |
|---|----------|--------|
| O1 | Campaign brief mandates a style | Use the mandated style. |
| O2 | Brand voice brief prohibits a style (e.g. "no comedy") | Remove that style from all further consideration. |
| O3 | Target is TikTok/Shorts only **and** the best usable cut is ≤ 30 s | Remove Cinematic from consideration. |
| O4 | Target is LinkedIn only | Remove Comedy unless the brief explicitly allows humour. |
| O5 | Source footage is talking-head only (S9 = Basic) | Cinematic is allowed only if S5 = High. |

---

## Step 3 — Decision Tree

Walk the questions in order. Stop at the first "yes".

```
Q1  Does the segment contain a setup → punchline with a real laugh (S4 = Strong)?
    ├─ YES ─► COMEDY
    └─ NO ──▼

Q2  Is the main purpose to teach (S1 = Teach) — steps, framework, definitions, data?
    ├─ YES ─► Is S2 = Fast AND S6 = List AND S3 = High?
    │           ├─ YES ─► FAST/ENERGY   (rapid-fire tips)
    │           └─ NO ──► EDUCATIONAL
    └─ NO ──▼

Q3  Is it a personal story with struggle (S5 = High, S7 = Fall & Rise or Stakes Climb)?
    ├─ YES ─► Does it end triumphant or with a rallying message (S10 = Triumphant)?
    │           ├─ YES ─► INSPIRATIONAL
    │           └─ NO ──► Is S9 = Good or Cinematic, or S10 = Reflective?
    │                       ├─ YES ─► CINEMATIC
    │                       └─ NO ──► INSPIRATIONAL
    └─ NO ──▼

Q4  Is the delivery high-energy (S2 = Fast or S3 = High) with a bold claim,
    hot take, or list (S8 = Bold Claim / Counterintuitive, S6 = List / Argument)?
    ├─ YES ─► FAST/ENERGY
    └─ NO ──▼

Q5  Is the purpose to inspire (S1 = Inspire) without a personal story?
    ├─ YES ─► INSPIRATIONAL
    └─ NO ──▼

Q6  No clear match ─► score the matrix in Step 4 and take the highest.
```

---

## Step 4 — Scoring Matrix

Score every remaining style to confirm the tree's answer and to find the secondary style. For each signal, add the points shown when the clip matches.

| Signal match                                | Fast/Energy | Cinematic | Comedy | Educational | Inspirational |
|---------------------------------------------|:-----------:|:---------:|:------:|:-----------:|:-------------:|
| S1 = Teach                                  | 1           | 0         | 0      | **3**       | 0             |
| S1 = Move                                   | 0           | **3**     | 0      | 0           | 2             |
| S1 = Amuse                                  | 1           | 0         | **3**  | 0           | 0             |
| S1 = Provoke                                | **3**       | 0         | 1      | 1           | 0             |
| S1 = Inspire                                | 1           | 1         | 0      | 0           | **3**         |
| S2 = Fast                                   | **2**       | 0         | 1      | 0           | 0             |
| S2 = Slow                                   | 0           | **2**     | 0      | 1           | 1             |
| S3 = High                                   | **2**       | 0         | 1      | 0           | 1             |
| S4 = Strong                                 | 0           | 0         | **3**  | 0           | 0             |
| S5 = High                                   | 0           | **2**     | 0      | 0           | **2**         |
| S6 = List / Steps                           | 1           | 0         | 0      | **2**       | 0             |
| S6 = Story                                  | 0           | **2**     | 1      | 0           | **2**         |
| S6 = Banter                                 | 0           | 0         | **2**  | 0           | 0             |
| S7 = Insight Bomb                           | **1**       | 0         | 0      | **1**       | 0             |
| S7 = Fall & Rise                            | 0           | 1         | 0      | 0           | **2**         |
| S7 = Stakes Climb                           | 1           | **1**     | 1      | 0           | 0             |
| S9 = Cinematic                              | 0           | **2**     | 0      | 0           | 1             |
| S10 = Triumphant                            | 0           | 0         | 0      | 0           | **2**         |
| S10 = Reflective                            | 0           | **2**     | 0      | 0           | 0             |
| S10 = Punchline                             | 0           | 0         | **2**  | 0           | 0             |
| S10 = Actionable                            | 1           | 0         | 0      | **2**       | 1             |

**Reading the result:**

- **Primary style** = the tree's answer from Step 3. If the matrix's top score beats the tree's answer by **≥ 4 points**, re-check the signals — one is probably mis-measured. If the signals are confirmed, use the matrix winner.
- **Secondary style** = the highest-scoring style other than the primary.
- **Confidence:**

| Gap between primary and secondary score | Confidence | Implication |
|-----------------------------------------|------------|-------------|
| ≥ 5 points                              | High       | Single version is enough; secondary version optional. |
| 2–4 points                              | Medium     | Produce primary + secondary versions (see `multi-version-strategy.md`). |
| 0–1 points                              | Low        | Produce primary + secondary, and consider a third version. |

---

## Compatibility Notes

Some style pairs make strong A/B partners; others are too similar to be worth testing against each other.

| Pair                          | Worth testing? | Why |
|-------------------------------|----------------|-----|
| Fast/Energy ↔ Educational     | Yes            | Same content, different pace — tests whether the audience wants speed or depth. |
| Cinematic ↔ Inspirational     | Yes            | Same story, reflective vs rallying ending. |
| Fast/Energy ↔ Inspirational   | Yes            | Hype vs emotional build on a motivational message. |
| Comedy ↔ Fast/Energy          | Yes            | Timing-led vs pace-led cut of a funny moment. |
| Cinematic ↔ Fast/Energy       | Only if S9 = Cinematic | Very different cuts — useful for platform splits (YouTube vs TikTok). |
| Comedy ↔ Cinematic            | Rarely         | Usually conflicting intent; only for deliberately deadpan content. |
| Educational ↔ Cinematic       | Rarely         | Only for documentary-style explainers with strong visuals. |

If the secondary style forms a "Rarely" pair with the primary, use the next-highest style as secondary instead.

---

## Output Record

Store the result in the clip's working notes and metadata:

```json
{
  "signals": {
    "purpose": "Inspire", "speaking_rate_wpm": 182, "vocal_energy": "High",
    "laughter": "None", "emotional_weight": "High", "structure": "Story",
    "arc": "Fall & Rise", "hook_type": "Empathy Mirror",
    "visual_quality": "Good", "ending_energy": "Triumphant"
  },
  "override_applied": null,
  "tree_result": "Inspirational",
  "matrix_scores": { "Fast/Energy": 5, "Cinematic": 6, "Comedy": 2, "Educational": 0, "Inspirational": 12 },
  "primary_style": "Inspirational",
  "secondary_style": "Cinematic",
  "confidence": "High"
}
```
