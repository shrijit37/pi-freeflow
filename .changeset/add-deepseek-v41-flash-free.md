---
"pi-freeflow": minor
---

A new free model on the OpenCode Zen lane: DeepSeek V4.1 Flash

`deepseek-v4.1-flash-free` joins the picker, bringing the catalog to 35 models (11 OpenCode, 14 Kilo, 2 Cline, 8 OVHcloud). No account, no key, no setup — it is keyless like every other Zen free model.

It reads images, and it thinks at every depth the host offers.

Its context window is a full million tokens, measured rather than copied. The published figure for this exact model says 200,000, which is wrong — that number belongs to a different, paid DeepSeek model with a confusingly similar name. Against the real one, a marker planted in the middle of a prompt is still recalled past one million prompt tokens, and the service turns an oversized request away well past that. So one million is what the model can actually use.

Two limits worth knowing before you pick it:

- **It is not available on the Responses API.** Requests sent that way are refused with a protocol error. It works on chat completions, which is what hosts use by default, but a host pinned specifically to Responses will not see it.
- **The output budget is 32,768 tokens.** Asking for more is accepted without complaint, but a completion forced to run that long comes back cut off at exactly 32,768, so the higher ceiling is not real.

You can reach it as `freeflow/deepseek-v4.1-flash` or in full as `freeflow/deepseek-v4.1-flash-free`.