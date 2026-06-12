# The Perio Voice Sprint
## Real-Time Periodontal Charting Challenge

**Presented by:** Agentics Foundation × Trust AI  
**Sponsor:** Bernard Casse, Ph.D. — CEO, Trust AI ([trustdentistry.ai](https://trustdentistry.ai))  
**Platform:** [Builder Base](https://www.builderbase.com/v2/event/agentics-foundation-presents-the-dental-innovation-sprint)  
**Prize:** $5,000 USD via ACH  
**Submissions close:** June 30, 2026 · 11:59 PM CT  

---

## The Challenge in One Sentence

Build a real-time voice AI pipeline that transcribes periodontal measurements as a hygienist speaks — at full clinical speed — without lag, without parser drift, and without forcing the hygienist to slow down.

---

## Background

Trust AI's **Isaac PracticeOS** is the first AI-native dental Practice Management System. It replaces the 8–10 disconnected tools a typical dental practice uses today with a single AI system. One of its core features is voice-driven periodontal charting — a hygienist speaks measurements aloud and the system fills in the chart automatically.

The system already has an **audio mode** that works: record the full session, then process it. The missing piece is **live mode**: the chart updating in real time as the hygienist speaks, within ~1 second, at full clinical pace.

Bernard Casse has spent significant engineering effort on this problem. Current cloud STT solutions fall short. The sprint exists because this is worth solving — and solving it well.

> *"If you do it right, we'll have something that's truly state of the art. No one else has something like this."*  
> — Bernard Casse, CEO · Trust AI

---

## What Is Periodontal Charting?

A dental hygienist uses a thin probe to measure the depth of the pocket between each tooth and the surrounding gum tissue. These measurements are taken at **6 sites per tooth × 32 teeth = 192 measurement sites** per patient.

At each site, the hygienist calls out:
- **Pocket depth** in millimeters (a three-number triplet: mesial, buccal, distal)
- **Recession** in millimeters if present
- **Bleeding on probing** if observed

Healthy pocket depth: ≤3mm  
Periodontal disease indicated: 5–9mm

The hygienist dictates continuously at clinical pace. A second person (or system) records every reading. This sprint is about making the system fast enough to keep up.

---

## How Hygienists Dictate

The hygienist **anchors once** at the start:
> *"Starting on tooth number 2"*

Then races through measurements — **never repeating the tooth number** between sequential teeth:
> *"3 2 3, 4 2 3, 2 millimeter recession on the buccal, bleeding on probing distal, 3 2 3, switch to lingual, 2 2 2..."*

The system must infer tooth position from sequential count alone.

**Clinical pace:** approximately **180–220 words per minute**, 2–3 measurements per second.

See `resources/dictation-protocol.md` for the complete set of rules a hygienist follows and that your parser must handle.

---

## The Three Failure Modes

Every existing voice perio tool fails in at least one of these ways. Your solution must eliminate all three.

### 1. Latency
Current cloud STT buffers 3–5 seconds behind live speech. By the time the chart updates, the hygienist is several teeth ahead and has lost track of where she is. The chart must feel **live**.

**Target:** ≤1.0s p95 from spoken measurement to chart update.

### 2. Implicit Sequencing
Hygienists never announce each tooth number — only the starting point. The parser must count from the anchor and infer which tooth is being measured at each triplet. A common failure: `"3 2 2"` gets misread as tooth #3 instead of pocket depths `[3, 2, 2]`.

### 3. Stream Incompleteness
Real-time STT engines deliver tokens in fragments. `"3 2 2"` might arrive as `"3 2"` then `"2"`. The parser must handle incomplete, ambiguous partial streams and recover state correctly — without waiting for the complete utterance.

---

## What You're Building

A **cloud-hosted voice AI pipeline** that:

| Requirement | Detail |
|-------------|--------|
| **Input** | Live browser audio — 16 kHz PCM over WebSocket from `getUserMedia` |
| **Output** | Structured JSON emitted in real time — see `resources/output-spec.md` |
| **Latency** | ≤1.0s p95 · Hard ceiling: 2.0s · Catch-up after pause: ≤3.0s |
| **Deployment** | Cloud-hosted · Browser-accessible · No local GPU required |
| **STT engine** | Any — ElevenLabs, Deepgram, AssemblyAI, Whisper, custom model |
| **Stack** | Any language or framework — Bernard's team refactors the winner |
| **Noise** | Must handle ordinary operatory background noise and brief conversation |

Your deliverable is a **standalone API** (REST or WebSocket endpoint). You are not integrating with Isaac PracticeOS — Bernard's engineering team does that. You prove it works.

---

## Judging

See `JUDGING.md` for full criteria, thresholds, and judge panel details.

**Summary:**
- 40% — Real-time latency
- 40% — Clinical accuracy
- 20% — Robustness

**Judge:** Bernard Casse tests every submission independently against standardized benchmark audio at slow, normal, and clinical pace.

---

## Submission Requirements

Three things required before **June 30, 2026 · 11:59 PM CT**:

1. **GitHub repository** — public, or private with judges added as collaborators. Must include a README with architecture overview and setup instructions that work without your local machine.
2. **Loom demo video** — max 5 minutes. Must show live mode running against at least one benchmark audio clip. No staged or pre-recorded output.
3. **200-word write-up** — STT engine used, sequencing approach, latency optimizations, known limitations. Honest beats polished.

**To submit:** open a PR adding your row to `SUBMISSIONS.md` in this repo.

---

## IP & Prize Terms

The $5,000 prize is paid via ACH immediately upon the winner signing the IP relinquishment agreement. The winning solution's code becomes the property of Trust AI and will be integrated into Isaac PracticeOS.

See `TERMS.md` for the full summary. The complete Terms & Conditions PDF is available on Builder Base.

---

## Resources

| Resource | Description |
|----------|-------------|
| `resources/dictation-protocol.md` | Complete hygienist dictation rules your parser must handle |
| `resources/output-spec.md` | Required JSON output structure |
| `resources/benchmark-audio.md` | Benchmark audio clips and YouTube reference examples |
| `JUDGING.md` | Judging criteria, thresholds, and panel |
| `TERMS.md` | Prize terms and IP agreement summary |
| `SUBMISSIONS.md` | Submission registry — open a PR to submit |

**Discord:** [discord.agentics.org](https://discord.agentics.org) · `#perio-voice`  
**Builder Base:** [Register here](https://www.builderbase.com/v2/event/agentics-foundation-presents-the-dental-innovation-sprint)  
**Questions:** Post in Discord or join the weekly check-ins with Bernard.

---

*Agentics Foundation × Trust AI · agentics.org · trustdentistry.ai*
