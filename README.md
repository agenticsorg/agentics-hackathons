# Agentics Foundation Hackathons

**Real problems. Real builders. Real outcomes.**

This repository is the official resource hub for Agentics Foundation hackathons and innovation sprints. It contains problem briefs, technical specifications, submission templates, and reference materials for each event.

> **Note:** This repo holds resources only. Code submissions are made via each builder's own GitHub repository — nothing is submitted here.

---

## Active Sprint

### 🦷 The Dental Innovation Sprint
**Real-Time Voice AI Challenge · $5,000 Winner Prize**

> Submissions open through **June 30, 2026 · 11:59 PM CT**

A focused voice AI sprint presented by the Agentics Foundation and Trust AI — creators of Isaac PracticeOS, the first AI-native dental Practice Management System.

**The challenge:** Build a real-time voice AI pipeline that captures periodontal measurements as a hygienist speaks — pocket depths, recession, bleeding flags — at full clinical speed, without lag, without parser drift, and without forcing the hygienist to slow down.

📋 **[Problem brief + technical spec →](./perio-voice-sprint/README.md)**
🏗️ **[Register on Builder Base →](https://www.builderbase.com/v2/event/agentics-foundation-presents-the-dental-innovation-sprint)**
💬 **[Join Discord →](https://discord.agentics.org)** · `#perio-voice`

---

## How It Works

### 1. Find the active sprint
Each sprint lives in its own folder in this repo. The folder contains the problem brief, technical specification, judging criteria, and any reference materials (benchmark audio links, dictation protocol, output spec).

### 2. Register
Register on Builder Base using the link in the sprint folder. Registration is always free.

### 3. Build in your own repo
Create a **private GitHub repository** for your solution. Add the judges listed in the sprint brief as collaborators so they can review your code during judging week.

### 4. Submit before the deadline
Each sprint specifies three required submission components:
- **GitHub repo** — your solution code + README with architecture overview and setup instructions
- **Loom demo video** — max 5 minutes, demonstrating live mode against the provided benchmark audio
- **200-word write-up** — your STT engine, sequencing approach, latency optimizations, and known limitations

Submit via the Builder Base event page before the stated deadline. Late submissions are not accepted.

### 5. Judging
Judges independently test all submissions against standardized benchmark audio. Winners are announced within one week of the submission deadline.

### 6. Prize + IP
Winners sign a standard IP relinquishment agreement before prize payment. The winning solution's code becomes the property of the challenge sponsor and is integrated into their live product. See the sprint's `TERMS.md` for full details.

---

## Repository Structure

```
agentics-hackathons/
│
├── README.md                        ← You are here
│
├── perio-voice-sprint/              ← Active: The Dental Innovation Sprint
│   ├── README.md                    ← Problem brief + full technical spec
│   ├── JUDGING.md                   ← Scoring criteria and judges
│   ├── TERMS.md                     ← Prize terms and IP agreement summary
│   ├── resources/
│   │   ├── dictation-protocol.md   ← Hygienist dictation rules for builders
│   │   ├── output-spec.md          ← Required JSON output structure
│   │   └── benchmark-audio.md      ← Links to benchmark audio clips
│   └── SUBMISSIONS.md              ← Links to submitted repos (added post-deadline)
│
└── _template/                       ← Template for future hackathons
    ├── README.md
    ├── JUDGING.md
    ├── TERMS.md
    └── resources/
```

---

## Hackathon Program

The Agentics Foundation runs three types of hackathons:

| Type | Description |
|------|-------------|
| **Partner Hackathons** | A company brings a real unsolved problem. Builders compete for a cash prize. Winning code ships into production. |
| **Hackathons for Good** | Mission-driven challenges solving real-world problems for nonprofits, healthcare, or underserved domains. |
| **Experience Hackathons** | Premium format events built around an immersive experience. |

Want to sponsor a hackathon or submit a challenge problem?
👉 [Submit a hackathon idea on CB Radio →](https://agentics.org) (VideoAsk link under CB Radio)

---

## About the Agentics Foundation

The Agentics Foundation is a global community of **100,000+ agentic AI builders** across **18+ chapters worldwide**. We run hackathons that produce real outcomes — not demo theater.

- 🌐 [agentics.org](https://agentics.org)
- 💬 [discord.agentics.org](https://discord.agentics.org)

---

## Contributing

This repo is maintained by the Agentics Foundation hackathon team. If you spot an error in a problem brief or spec, open an issue. Pull requests to the resources folders are welcome during the active sprint window.

---

*Agentics Foundation · agentics.org · Building the future of agentic AI, one sprint at a time.*
