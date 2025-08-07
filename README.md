# DECS-Stack

*A three‑voice architecture inspired by “Dubito, ergo cogito, ergo sum.”*

<img width="50%" alt="0349b659-c272-4c54-b72a-b228559f97ab" src="https://github.com/user-attachments/assets/68c46743-bbdc-4d1f-af58-9452cfd63cd1" />

*Dubito → Ergo Cogito → Ergo Sum*
| Layer | Folder | Role |
|-------|--------|------|
| Dubito | `/dubito` | Real-time sensing, certainty scoring, tool lookup |
| Ergo Cogito | `/ergo_cogito` | Core LLM reasoning & planning |
| Ergo Sum | `/ergo_sum` | Goal management, long-term memory, output polishing |

1. **Dubito – the Doubter**
   Constantly asks, *“Do I have enough information?  Am I certain enough? What else do I need in order to be sure?”*  Queues requests for thought, includes references for tools.
2. **Ergo Cogito – the Thinker**
   Gathers context, reasons, calls read-only tools.
3. **Ergo Sum – the Decider**
   Acts on Cogito’s context provided. Calls output tools. (reply, create a file, trigger an automation, or store new memory.)

Together they form a feedback loop where *doubt* drives search, *thought* refines knowledge, and *decision* closes the loop with the user or the outside world.

```
┌──────────────┐                                            ┌──────────────┐
│   user / io  │                                            │  actuators   │
└──────┬───────┘                                            └─────┬────────┘
       │                                                          │
       ▼              context.*                                   │
┌──────────────────┐  tool_request.*  ┌──────────────────┐        │
│   Dubito         │ ───────────────▶ │  Ergo Cogito     │        │
│  (doubt / route) │ ◄─────────────── │  (think & act)   │◄───────┘
└──────────────────┘                  └──────────────────┘
                                            │  create context / plan
                                            ▼
                                ┌──────────────────┐
                                │   Ergo Sum       │
                                │ (output / goals) │
                                └──────────────────┘
                                         │ final.reply / tool_call.*
                                         ▼
                                (tool responses loop back via Dubito)
```

For roadmap, implementation details, and layer‑specific docs, see the `/docs` folder and individual layer READMEs.
