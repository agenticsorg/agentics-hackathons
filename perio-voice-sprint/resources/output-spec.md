# Output Specification — Perio Voice Sprint

Your solution must emit structured JSON in real time as the hygienist speaks. This document defines the required output format.

---

## Delivery Model

Emit **per measurement** as it's recognized — do not buffer per tooth. The judge evaluates latency from the moment the spoken measurement is completed to when the JSON event arrives at the consumer.

Use a **WebSocket** that streams events as the hygienist speaks. Each event is a single JSON object on its own line (newline-delimited JSON / NDJSON).

---

## Event Types

### 1. Pocket Depth Entry

Emitted each time a complete triplet is parsed for a tooth.

```json
{
  "event": "pocket_depth",
  "tooth": 4,
  "surface": "facial",
  "mesial": 3,
  "buccal": 2,
  "distal": 3,
  "timestamp_ms": 1234567890
}
```

| Field | Type | Description |
|-------|------|-------------|
| `event` | string | Always `"pocket_depth"` |
| `tooth` | integer | Universal tooth number (1–32) |
| `surface` | string | `"facial"` or `"lingual"` |
| `mesial` | integer | Pocket depth in mm at mesial site |
| `buccal` | integer | Pocket depth in mm at mid/buccal site |
| `distal` | integer | Pocket depth in mm at distal site |
| `timestamp_ms` | integer | Unix timestamp in milliseconds when event was emitted |

---

### 2. Recession Entry

Emitted when recession is called out for a tooth.

```json
{
  "event": "recession",
  "tooth": 4,
  "surface": "facial",
  "sites": ["buccal", "mesial"],
  "amount_mm": 2,
  "timestamp_ms": 1234567890
}
```

| Field | Type | Description |
|-------|------|-------------|
| `event` | string | Always `"recession"` |
| `tooth` | integer | Universal tooth number (1–32) |
| `surface` | string | `"facial"` or `"lingual"` |
| `sites` | array of strings | One or more of: `"mesial"`, `"buccal"`, `"distal"`, `"all"` |
| `amount_mm` | integer | Recession amount in millimeters |
| `timestamp_ms` | integer | Unix timestamp in milliseconds |

---

### 3. Bleeding on Probing

Emitted when bleeding is called out.

```json
{
  "event": "bleeding",
  "tooth": 4,
  "surface": "facial",
  "sites": ["distal"],
  "timestamp_ms": 1234567890
}
```

| Field | Type | Description |
|-------|------|-------------|
| `event` | string | Always `"bleeding"` |
| `tooth` | integer | Universal tooth number (1–32) |
| `surface` | string | `"facial"` or `"lingual"` |
| `sites` | array of strings | One or more of: `"mesial"`, `"buccal"`, `"distal"`, `"everywhere"` |
| `timestamp_ms` | integer | Unix timestamp in milliseconds |

---

### 4. Surface Switch

Emitted when the hygienist announces a surface transition.

```json
{
  "event": "surface_switch",
  "to_surface": "lingual",
  "current_tooth": 2,
  "timestamp_ms": 1234567890
}
```

---

### 5. Correction

Emitted when the hygienist issues a correction command.

```json
{
  "event": "correction",
  "tooth": 14,
  "timestamp_ms": 1234567890
}
```

---

### 6. Parser State (optional but valued)

If your system emits parser state updates, use this format. Not required but helpful for debugging and gives judges confidence in your implementation.

```json
{
  "event": "state",
  "current_tooth": 7,
  "current_surface": "facial",
  "anchor_tooth": 2,
  "teeth_completed_facial": [2, 3, 4, 5, 6],
  "timestamp_ms": 1234567890
}
```

---

## Complete Example Stream

A hygienist starts on tooth 2, charts facial surface, calls recession and bleeding, then switches to lingual:

```json
{"event":"pocket_depth","tooth":2,"surface":"facial","mesial":3,"buccal":2,"distal":3,"timestamp_ms":1000}
{"event":"pocket_depth","tooth":3,"surface":"facial","mesial":4,"buccal":2,"distal":3,"timestamp_ms":1800}
{"event":"recession","tooth":3,"surface":"facial","sites":["buccal","mesial"],"amount_mm":2,"timestamp_ms":2100}
{"event":"pocket_depth","tooth":4,"surface":"facial","mesial":3,"buccal":2,"distal":3,"timestamp_ms":2900}
{"event":"bleeding","tooth":4,"surface":"facial","sites":["distal"],"timestamp_ms":3200}
{"event":"pocket_depth","tooth":5,"surface":"facial","mesial":4,"buccal":2,"distal":3,"timestamp_ms":3900}
{"event":"surface_switch","to_surface":"lingual","current_tooth":5,"timestamp_ms":4500}
{"event":"pocket_depth","tooth":2,"surface":"lingual","mesial":2,"buccal":2,"distal":2,"timestamp_ms":5300}
```

---

## Latency Measurement

Latency is measured from:
- **Start:** The moment the last spoken syllable of a complete measurement is detected (e.g., the final digit of a triplet)
- **End:** The moment the corresponding JSON event is received by the WebSocket consumer

The judge's test harness will measure p95 latency across a full-mouth chart dictation at clinical pace.

---

## What the Integration Will Do

Bernard's team will consume your WebSocket stream and map each event to the Isaac PracticeOS chart data model. They are not integrating your codebase — they are integrating your output format. Correct, consistent JSON is more valuable than impressive code.

**If your output deviates from this spec:** the integration will fail. Implement the spec exactly. If you believe a field should be different, document your reasoning in your write-up.

---

## API Contract

Your solution should expose a WebSocket endpoint at a stable cloud URL:

```
wss://your-solution.your-domain.com/perio-stream
```

Or alternatively a REST endpoint that accepts audio and streams back JSON events via Server-Sent Events (SSE).

No authentication is required for the submission. Bernard's team will test it as-is.

---

*Output spec v1.0 · Agentics Foundation × Trust AI · Perio Voice Sprint 2026*
