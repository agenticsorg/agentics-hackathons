# Hygienist Dictation Protocol

Your parser must handle everything in this document. These are the real rules a trained dental hygienist follows when dictating periodontal measurements. No dental background needed — just understand the grammar.

---

## The Basics

### Tooth numbering
Teeth are numbered 1–32 in the Universal Numbering System:
- Teeth 1–16: upper arch (right to left from the patient's perspective)
- Teeth 17–32: lower arch (left to right)

### Surfaces
Each tooth has two sides that get charted:
- **Facial / buccal** — the side facing the cheek or lips (outside)
- **Lingual / palatal** — the side facing the tongue (inside)

### Measurement sites
Each surface has **3 measurement sites:**
1. **Mesial** — toward the front of the mouth
2. **Buccal / facial (mid)** — the middle of the surface
3. **Distal** — toward the back of the mouth

So each tooth = 6 measurements total (3 facial + 3 lingual).

---

## Dictation Rules

### 1. Anchor once at the start
The hygienist states the starting tooth number **once**. After that, they do not repeat tooth numbers for sequential teeth.

```
"Starting on tooth number 2"
"Tooth number 2"
```

### 2. Pocket depths as three-number triplets
Pocket depths are spoken as three numbers representing mesial, middle/buccal, distal — in that order.

```
"3 2 3"
"3, 2, 3"
```

Each number is a pocket depth in millimeters.

### 3. Sequential tooth increment — no announcement
After the anchor, the hygienist moves tooth by tooth without saying the tooth number. **Your parser must count.**

```
"Starting on tooth 2"
"3 2 3"        ← tooth 2 measurements
"4 2 3"        ← tooth 3 measurements (inferred)
"2 3 2"        ← tooth 4 measurements (inferred)
```

### 4. Surface transitions
When switching from facial to lingual (or vice versa), the hygienist announces it explicitly:

```
"Switch to lingual"
"Switching to lingual"
"Switch to facial"
"Switching to facial"
```

This resets the measurement sequence for the current tooth on the new surface.

### 5. Recession
Recession is announced with the amount and the specific site(s):

```
"One millimeter recession on the buccal"
"One millimeter recession on the buccal and mesial"
"One millimeter recession on all sites"
"Two millimeter recession on the facial"
```

### 6. Bleeding on probing
Bleeding is announced where it occurred:

```
"Bleeding on probing mesial"
"Bleeding on probing distal and mesial"
"Bleeding on probing buccal"
"Bleeding on probing everywhere"
"Bleeding on probing on the distal"
```

### 7. Corrections
When the hygienist made a mistake and needs to fix a specific tooth:

```
"Correct tooth 14"
```

This resets the parser to tooth 14 for re-entry.

### 8. Non-sequential jumps
When the hygienist needs to skip to a specific tooth (e.g., skipping a missing tooth or jumping to the other arch):

```
"Tooth 19"
"Tooth number 13"
```

This re-anchors the parser at the stated tooth.

### 9. Missing teeth
Missing teeth should be **marked before recording begins**. The parser must skip them in the sequence and not cause downstream drift.

---

## Example Dictation Sequence

```
"Starting on tooth number 2"
"3 2 3"                                    ← tooth 2, facial
"4 2 3"                                    ← tooth 3, facial
"2 millimeter recession on the buccal"     ← tooth 3 modifier
"3 2 3"                                    ← tooth 4, facial
"bleeding on probing mesial"               ← tooth 4 modifier
"4 2 3"                                    ← tooth 5, facial
"5 2 3"                                    ← tooth 6, facial
"6 2 4"                                    ← tooth 7, facial
"switch to lingual"                        ← switch surfaces, back to tooth 2
"2 2 2"                                    ← tooth 2, lingual
"3 2 3"                                    ← tooth 3, lingual
...
```

---

## What Makes This Hard

### The triplet vs. tooth number ambiguity
`"3 2 2"` — is this:
- Tooth #3 followed by two more measurements? ❌
- A pocket depth triplet: mesial=3, buccal=2, distal=2? ✅

Without context (the anchor and count), this is ambiguous. Your parser must use the anchor + sequential count to resolve it.

### Incomplete stream tokens
The STT engine may deliver partial results mid-utterance. `"3 2 2"` might arrive as:
- `"3"` → `"3 2"` → `"3 2 2"` (fine)
- `"3 2"` then `"2"` as a separate token (tricky)
- `"3"` then `"22"` (problematic)

Your parser must handle all of these without losing position.

### Speed variation
At slow pace: the hygienist pauses slightly between numbers — easier to parse.  
At clinical pace: measurements run together with minimal pause — harder.

The benchmark audio includes examples at all three speeds. Your solution must perform at clinical pace.

---

## Dental Terminology Your STT Must Handle

Common terms that STT engines frequently mistranscribe:

| Correct | Common mistranscription |
|---------|------------------------|
| buccal | buckle, vocal, buccle |
| mesial | measle, medial |
| distal | thistle, distant |
| lingual | lingo, lingual ✓ (usually fine) |
| gingival | gingivol, gingival ✓ |
| recession | recession ✓ (usually fine) |
| probing | probing ✓ (usually fine) |

Bernard's testing found **ElevenLabs** currently handles dental terminology best. Other engines may require post-processing to correct these terms.

---

## What Your Parser Does NOT Need to Handle (in live mode)

- Implant-specific notation (better supported in audio recording mode)
- Suppuration
- Furcation involvement
- Long conversational descriptions during charting

Keep phrases short and consistent. Live mode is optimized for speed.

---

*Source: Trust AI · Isaac PracticeOS · dictation protocol v1.0 · provided by Bernard Casse*
