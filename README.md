# Mark Lubin

Research engineer working on cognitive architecture, information dynamics, and adaptive systems.

**[marklubin.me](https://marklubin.me)** · **[synix.dev](https://synix.dev)** · [mark@synix.dev](mailto:mark@synix.dev)

---

My work is centered on a question that remains unresolved: how should long-lived intelligent systems organize information, adapt under change, and remain coherent across time?

The hard problems appear when information has to endure, when earlier judgments accumulate consequences, and when a system must keep operating as conditions change. What should remain explicit and stable? What should be compressed? What should be allowed to decay? What should be reconstructed on demand? Getting these decisions wrong produces contradiction, amnesia, or rigid obsolete structure. Getting them right is an architectural problem, not a scaling problem. It is also, increasingly, a safety problem: you cannot trust, verify, or align a system whose internal organization is opaque, irreproducible, or silently degrading.

I started by looking at what exists. I [read the source code](https://marklubin.me/synix/articles/memory-analysis/) of eight major agent memory systems. Every one shares the same structural assumption: one flat namespace, one timescale, no lifecycle management. No system distinguishes between information that should persist for seconds and information that should persist for months. No system manages contradiction, consolidation, or decay as architectural concerns. None of them provide the observability needed to know when an agent's memory has drifted from the state you expect. [LENS](https://github.com/marklubin/lens-benchmark), my benchmark for long-horizon coherence, confirms this is not merely a tooling gap but a structural one.

[Synix](https://github.com/marklubin/synix) is a research and systems program aimed at that structural problem. It is the environment where I study differentiated structure, selective routing, [compression, and renewal](https://marklubin.me/cdr.pdf). The question I am working toward is whether the right structural constraints are sufficient for durable adaptive order to emerge through selection and specialization, rather than requiring explicit orchestration. A [recent talk](https://synix.dev/talk/) covers the motivation and early findings.

I think intelligence over long horizons is more a systems problem than an inference problem. It arises from the interaction of models, structure, deterministic processes, and coordination across levels. At larger scales, the same questions become questions of collective adaptive systems, where humans and agents organize shared state, develop specialized roles, and maintain continuity without centralizing all intelligence in one place.

Before this, I spent a decade at Amazon building distributed systems across AWS, Prime Video, and payments.
