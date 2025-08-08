# Ergo Cogito – the Thinker

*Second voice in the DECS‑stack*

Ergo Cogito receives events tagged by **Dubito**, loads only the context‑segment handles it needs, runs deep reasoning, and returns a complete answer package to **Ergo Sum**—but never speaks directly to the user.

---

## Core Role

1. **Gather**  – Resolve `tool_request.*` by invoking tool runners (search, weather API, cloud vision, etc.).
2. **Reason**  – Generate structured chain‑of‑thought, incorporate retrieved data, and assess its own confidence.
3. **Package** – Emit `answer.full` containing: markdown answer, provenance, confidence, and any follow‑up tool suggestions.

---

## Message Flow

| From   | To     | Topic prefix     | Purpose                       |
| ------ | ------ | ---------------- | ----------------------------- |
| Dubito | Cogito | `tool_request.*` | Data gaps to fill             |
| Dubito | Cogito | `context.*`      | Segment handles & search tags |
| Cogito | Dubito | `cogito.partial` | Streaming thoughts (optional) |
| Cogito | Sum    | `answer.full`    | Final answer bundle           |

All envelopes conform to **MCP**.

---

## What Ergo Cogito Does (and Doesn’t)

| ✓ Does                                                  | ✗ Doesn’t                                        |
| ------------------------------------------------------- | ------------------------------------------------ |
| Resolve tool requests and merge results into reasoning. | Speak to the user; Sum handles all outward text. |
| Produce chain‑of‑thought and confidence score.          | Enforce persona or long‑term goals.              |
| Stream partial thoughts for Dubito to monitor.          | Persist memory.                                  |

---

## Folder Layout (high‑level)

```
ergo_cogito/
  __init__.py
  think.py        # reasoning engine & planner
  tools.py        # wrappers for tool calls
  stream.py       # optional partial‑thought emitter
  README.md
```

---

