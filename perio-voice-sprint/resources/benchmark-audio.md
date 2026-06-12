# Benchmark Audio & Reference Examples

This document lists all audio resources available to builders during the sprint.

---

## Official Benchmark Audio

Bernard Casse recorded standardized dictation clips specifically for this sprint. These are the **exact clips used during judging** — your solution must perform well against them.

> **Note:** Benchmark audio clips will be linked here once hosted. Check Discord `#perio-voice` for the download link or ask in the channel.

| Clip | Speed | Description |
|------|-------|-------------|
| `benchmark-slow.mp3` | ~80 WPM | Learning pace — deliberate pauses between measurements |
| `benchmark-normal.mp3` | ~140 WPM | Trained hygienist pace — fluid but not rushed |
| `benchmark-clinical.mp3` | ~200 WPM | Full clinical pace — the real target |

**Important:** Existing voice perio tools work fine at slow pace. The benchmark that matters is `benchmark-clinical.mp3`. Build to that standard.

---

## YouTube Reference Examples

Bernard curated these videos to show real-world periodontal charting in practice. Watch them to understand the clinical workflow, the pace, and what existing tools do (and fail to do).

### Example 1
**URL:** https://www.youtube.com/watch?v=X7sScHA_Hbs  
**What to notice:** Standard charting workflow, hygienist pace, how measurements are called out

### Example 2
**URL:** https://www.youtube.com/watch?v=EKXE20j9Uzs  
**What to notice:** Comparison of manual vs voice-assisted charting

### Example 3
**URL:** https://www.youtube.com/watch?v=hjG_gagQXpk  
**What to notice:** PMS-integrated voice charting — note where the UI lags behind speech

### Example 4
**URL:** https://www.youtube.com/watch?v=hEMtG7Khgmo  
**What to notice:** Clinical environment — background noise, interruptions, natural speech variation

### Example 5
**URL:** https://www.youtube.com/watch?v=_SRcolDW1ZE  
**What to notice:** How hygienists handle corrections and surface transitions in practice

---

## What to Observe in These Videos

When watching the examples, pay attention to:

1. **How the hygienist anchors** — they state a tooth number, then never repeat it
2. **The cadence between triplets** — at clinical pace there is almost no pause
3. **Where existing tools lag** — you'll see the UI falling behind the speaker
4. **Surface transition announcements** — brief, consistent phrases
5. **Background noise** — real operatories are not quiet rooms

---

## STT Engine Benchmarks

Based on Bernard's testing with the perio charting use case:

| Engine | Latency | Dental Term Accuracy | Notes |
|--------|---------|---------------------|-------|
| **ElevenLabs** | Medium | Best | Best out-of-box dental terminology recognition |
| **Deepgram Nova-3** | Best (<300ms) | Good | Lowest streaming latency, solid accuracy |
| **AssemblyAI Streaming** | Medium | Good | Strong streaming support |
| **OpenAI Whisper v3** | Slower | Good | Better for post-processing than live mode |
| **Custom fine-tuned** | Varies | Best (if trained) | Highest ceiling but requires domain data |

Free tiers on ElevenLabs and Deepgram are sufficient for development and testing. You do not need paid accounts to build and test your solution.

---

## Recording Your Own Test Audio

If you want to generate additional test audio beyond the benchmark clips, follow these rules from the dictation protocol:

1. Start with the anchor: *"Starting on tooth number 2"*
2. Speak pocket depth triplets at your target pace
3. Include at least one recession callout
4. Include at least one bleeding callout
5. Include at least one surface switch
6. Chart at least 8 consecutive teeth without re-anchoring

The benchmark clips use **female voice** at typical dental hygienist register. Testing with multiple voices and accents is a good robustness investment.

---

*Questions about audio resources? Post in Discord `#perio-voice`*
