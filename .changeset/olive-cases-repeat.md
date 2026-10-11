---
"pi-freeflow": patch
---

Stop conversations from dying on request shapes the provider rejects

Three shapes that the provider answers with `400 invalid parameters` are now reshaped on the way out instead of failing the whole turn.

- **A model narrates a tool call instead of making one.** The reply is recorded as pre-tool commentary, and every later message replayed that turn back to the provider was rejected — the session could not continue or be resumed, because each retry sent the same history again.
- **A host asks for a specific tool or forces a tool call.** The free provider accepts only automatic tool selection, so an unsupported choice is dropped rather than sent. Nothing is imposed on a host that did not ask.
- **A tool name carries a character the provider rejects.** Spaces, colons and slashes are folded for the trip out and the caller's own name is restored on the way back, so the tool still runs under the name it was registered with. Names that are already accepted are sent exactly as they always were.

Measured on Muse Spark 1.3: the same three requests that each failed with an error now answer normally, and a well-formed tool set reaches the model byte-identical to before.