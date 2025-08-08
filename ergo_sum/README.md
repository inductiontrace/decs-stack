# Ergo Sum – the Decider

*Third voice in the DECS‑stack*

Ergo Sum receives the fully‑reasoned output from **Ergo Cogito**, aligns it with user goals and persona, and decides what concrete action—or final reply—should close the loop.

<img width="50%" alt="a652cfca-0c57-45a5-a832-5449c9ce483d" src="https://github.com/user-attachments/assets/427ed964-f255-4cd8-aa33-b4ee7d2ed737" />

---

## Core Role

1. **Align**  – Check the answer against user preferences, safety policies, and project goals.
2. **Act**    – Choose an output mode:

   * `final.reply` – speak to the user.
   * `tool_call.*` – create files, trigger home‑automation, etc.
3. **Remember** – Emit `memory.write` for salient facts so future Dubito searches can find them.

---

## Message Flow

| From   | To           | Topic prefix      | Purpose                     |
| ------ | ------------ | ----------------- | --------------------------- |
| Cogito | Sum          | `answer.full`     | Completed reasoning bundle  |
| Sum    | Tools        | `tool_call.*`     | Execute side‑effects        |
| Tools  | Dubito       | `tool_response.*` | Success or error loops back |
| Sum    | User         | `final.reply`     | Chat / UI response          |
| Sum    | Memory store | `memory.write`    | Persisted knowledge         |

All envelopes conform to **MCP**.

---

## What Ergo Sum Does (and Doesn’t)

| ✓ Does | ✗ Doesn’t |
| ------ | --------- |
| Apply persona tone & safety (following intent) filters. | Perform deep reasoning (that’s Cogito). |
| Decide between speaking, writing files, or triggering automations. | Route or fetch new context (that’s Dubito). |
| Persist important facts via `memory.write`. | Handle low‑level tool errors; they loop back through Dubito. |

---

## Folder Layout (high‑level)

```
ergo_sum/
  __init__.py
  decide.py       # alignment & action selection
  persona.py      # tone & policy helpers
  memory.py       # write hooks to vector/graph store
  README.md
```

---

