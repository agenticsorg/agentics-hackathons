# Judging Criteria — Perio Voice Sprint

## Judging Panel

| Judge | Role | Responsibility |
|-------|------|----------------|
| **Bernard Casse, Ph.D.** | CEO, Trust AI | Technical & clinical accuracy — independently tests all submissions against benchmark audio at clinical pace. Casting vote in ties. |
| **Dragon** | Board Member, Agentics Foundation | Builder quality, code approach, community standards |
| **Nick Ruest** | Board Member, Agentics Foundation | Innovation, feasibility, overall solution design |

The panel deliberates collectively. In the event of a tie, Bernard's technical assessment of clinical performance is the deciding factor. The panel's decision is final and binding.

---

## Scoring Weights

| Weight | Criterion |
|--------|-----------|
| **40%** | Real-Time Latency |
| **40%** | Clinical Accuracy |
| **20%** | Robustness |

Winner = best combined score across all three criteria.

---

## Criterion 1 — Real-Time Latency (40%)

The system must feel live to the hygienist. Chart entries must appear within about 1 second of speech. The hygienist should never need to slow down.

| Threshold | Requirement |
|-----------|-------------|
| **Target** | Chart updates appear within **1.0s p95** of the spoken measurement being completed |
| **Hard ceiling** | System may not fall more than **2.0s behind** during fast continuous dictation |
| **Catch-up** | After a brief pause, must catch up within **3.0s** |
| **Test pace** | ~180–220 WPM, approximately 2–3 periodontal measurements per second |

**How it's tested:** Bernard will dictate at slow, normal, and clinical pace using the standardized benchmark audio. The time delta between spoken measurement completion and chart update will be measured for each submission.

---

## Criterion 2 — Clinical Accuracy (40%)

The system must correctly capture every measurement type across all 192 sites of a full-mouth chart.

| Field | Accuracy Target |
|-------|----------------|
| **Pocket depths** | ≥98% site accuracy across the standardized test set |
| **Recession / gingival margin** | ≥95% site accuracy |
| **Bleeding on probing flags** | ≥90–95% accuracy (varies with complexity of bleeding phrases in test set) |

Additional requirements:
- Missing teeth and implants must not cause downstream chart drift
- Surface transitions (facial → lingual) must be captured correctly
- Arch transitions must be handled without position loss

---

## Criterion 3 — Robustness (20%)

The system must complete a full-mouth chart without state collapse, regardless of noise, pauses, corrections, or edge cases.

**Pass requirements (all must be met — zero tolerance):**
- Zero unrecovered state collapses in the test run
- No ghost entries (measurements written to the wrong tooth)
- No skipped arch (jumping from upper to lower incorrectly)
- No permanent wrong-surface drift (continuing lingual readings on facial surface)
- No need to restart the session mid-chart

**Must handle:**
- Ordinary operatory background noise (equipment, brief conversation)
- Normal speech variation across different speakers
- Short pauses between teeth or between surfaces
- Correction commands: *"Correct tooth 14"*
- Non-sequential jumps: *"Tooth 19"* to skip ahead

---

## Judging Process

1. Bernard independently tests every submission against standardized benchmark audio clips (slow, normal, and clinical pace)
2. Panel reviews Bernard's technical assessment alongside the Loom demo and write-up
3. Panel scores each submission on the three criteria
4. Winner = highest combined weighted score
5. Winner announced on or around **July 7, 2026**

---

## Disqualifiers

Submissions will be disqualified for:
- Staged or pre-recorded demo output (Bernard tests independently — this will be caught)
- Solution requires local GPU or local compute
- Submission missing any of the three required components (repo, Loom, write-up)
- Late submission (after June 30, 2026 · 11:59 PM CT)
- Code that infringes third-party IP

---

## Prize Fallback

If no submission fully meets all criteria, the panel reserves the right to split the $5,000 among the highest-scoring submissions. The prize money is committed regardless of outcome — it will be distributed.

---

*Questions on judging criteria? Post in Discord `#perio-voice` or ask during a weekly check-in.*
