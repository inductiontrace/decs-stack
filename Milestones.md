# DECS‑stack Roadmap

> *Everything here is aspirational and subject to change as we dog‑food the stack.*  Each milestone should deliver a shippable slice that adds real value for early adopters while exercising the full Dubito → Cogito → Sum loop.

---

## Milestone 0 · "Hello DECS" (M0)

| Target date      | Deliverables         | Notes                                                               |
| ---------------- | -------------------- | ------------------------------------------------------------------- |
| **T0 + 2 weeks** | *Core repo skeleton* | Folder layout `/dubito`, `/cogito`, `/sum`, plus basic MCP wiring.  |
|                  | *In‑proc event bus*  | Simplest viable transport—`asyncio.Queue`—to keep dev friction low. |
|                  | *Weather demo*       | `tool_request.weather_api` → local stub → chat reply.               |

---

## Milestone 1 · "Observability First" (M1)

| Target date      | Deliverables              | Notes                                                                                               |
| ---------------- | ------------------------- | --------------------------------------------------------------------------------------------------- |
| **T0 + 6 weeks** | Structured JSON logs      | `layer`, `conversation_id`, `latency_ms`.                                                           |
|                  | Prometheus exporter       | Counters: `dubito_tool_requests_total`, `cogito_tokens_generated_total`, `sum_memory_writes_total`. |
|                  | Grafana starter dashboard | Latency histogram + per‑layer request counts.                                                       |

---

## Milestone 2 · "Dynamic Tools" (M2)

| Target date       | Deliverables                | Notes                                                                      |
| ----------------- | --------------------------- | -------------------------------------------------------------------------- |
| **T0 + 10 weeks** | Runtime capability registry | Tool runners announce themselves over MCP; Dubito discovers via heartbeat. |
|                   | Home‑automation demo        | Occupancy sensor event → `tool_request.home_rules` → rule evaluation.      |
|                   | File‑system demo            | `fs_stat`, `fs_create`, `fs_write` tool runners.                           |

---

## Milestone 3 · "Streaming UI" (M3)

| Target date       | Deliverables       | Notes                                                            |
| ----------------- | ------------------ | ---------------------------------------------------------------- |
| **T0 + 14 weeks** | Web dashboard      | Live diagram of conversation flow; colour‑coded confidence bars. |
|                   | Time‑travel replay | Play back a full interaction for debugging.                      |

---

## Milestone 4 · "Persona Packs" (M4)

| Target date       | Deliverables              | Notes                                                                     |
| ----------------- | ------------------------- | ------------------------------------------------------------------------- |
| **T0 + 18 weeks** | Pluggable persona modules | YAML‑defined tone & style schemes applied by Ergo Sum.                    |
|                   | Memory importance tagging | `memory.write` gains `importance` field; low‑importance items TTL‑pruned. |

---

## Milestone 5 · "Distributed Transports" (M5)

| Target date       | Deliverables          | Notes                                          |
| ----------------- | --------------------- | ---------------------------------------------- |
| **T0 + 24 weeks** | Kafka adapter         | MCP over Kafka topics for large installations. |
|                   | Redis‑Streams adapter | Lightweight on‑prem option.                    |

---

## Stretch Goals

| Idea                                     | Rationale                                                                   |
| ---------------------------------------- | --------------------------------------------------------------------------- |
| WASM sandbox for user‑supplied enrichers | Safe execution of custom enrichment code.                                   |
| Auto‑scaling Dubito shards               | Horizontal scaling when many concurrent conversations.                      |
| On‑device fallback (mobile)              | Thin Dubito running on‑device, offloading Cogito to cloud only when needed. |

---

## Versioning & Release cadence

* **Semantic Versioning** for public APIs (MCP roles & payloads).  Breaks bump **major**.
* Milestones target \~4‑week sprints; hot‑fix releases are tagged `x.y.z‑patchN`.

---

*Last updated: 2025‑08‑07*
