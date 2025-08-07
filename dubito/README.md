# Dubito – the Doubter

*First voice in the DECS‑stack*

Dubito watches every inbound event (chat, image, sensor, API callback, and most importantly, Ergo Coigo's "certainty" levels) and asks a single question:

> **“What else do I need to answer this?”**

If the answer is **nothing**, Dubito passes the event along untouched.  Otherwise, it queues the missing pieces as `tool_request.*` messages so **Ergo Cogito** can fetch data or run specialised tools.

---

## What Dubito Does (and Doesn’t)

| ✓ Does                                                            | ✗ Doesn’t                                                     |
| ----------------------------------------------------------------- | ------------------------------------------------------------- |
| Tag each message with `conversation_id` & `context_handle`.       | Run large‑scale reasoning (that’s Cogito).                    |
| Decide when more context or tools are required.                   | Talk to the user directly.                                    |
| Publish `tool_request.*` (weather API, fs\_stat, cloud\_vision…). | Call output tools (file writes, actuators) – that’s Ergo Sum. |
| Publish handles to relevant conversation IDs for Coigo to search. | Store long‑term memory.                                       |
| Emit structured JSON logs for tracing.                            | Define its own transport or schema – it just uses MCP.        |

---

## Message Types

*All envelopes conform to **MCP**.*

### `tool_request.*`  (Dubito → Cogito / tool‑runner)

```jsonc
{
  "role": "tool_request",
  "topic": "weather_api",
  "conversation_id": "c-9f12",
  "context_handle": "h-882a",
  "payload": {
    "location": "Seattle, WA",
    "day": "2025-08-07"
  }
}
```

### `context.*`  (Dubito → Cogito)

Handles which allow Cogito to search for snippets of prior chat / memory deemed relevant.

---

## Logging

Every hop emits a JSON log line like:

```jsonc
{"ts":"2025-08-07T14:02:31Z","layer":"dubito","conversation_id":"c-9f12","event":"tool_request.weather_api","latency_ms":3.4}
```


## Configuration (minimal)

```yaml
certainty:
  threshold: 0.6  # below this, queue tool requests
memory_window:
  max_tokens: 2048
```

---

## Folder layout

```
dubito/
  __init__.py
  router.py        # gap detection & tool_request emitter
  confidence.py    # monitor Ergo Coigo's confidence level
  log.py           # structured logger helper
  README.md        # (this file)
```

---

## Open Questions

* Better heuristic for image‑vs‑text context relevance.
* Auto‑discovering new tool runners at runtime (see project Roadmap).

---

