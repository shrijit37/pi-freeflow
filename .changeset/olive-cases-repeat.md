---
"pi-freeflow": patch
---

Keep a conversation alive when a model narrates a tool call instead of making one

Some models occasionally describe the tool call they are about to make and then stop without calling it. The reply is recorded as pre-tool commentary, and every later message replayed that turn back to the provider was rejected with `400 invalid parameters` — the session could not continue or be resumed, because each retry sent the same history again.

Replayed turns now leave that marker out, so the conversation continues normally. Measured on Muse Spark 1.3: the same history that failed with an error now answers normally.