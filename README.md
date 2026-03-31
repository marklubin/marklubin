# Mark Lubin

Software engineer. I think about agent memory, cognitive architecture, and information lifecycle.

**[marklubin.me](https://marklubin.me)** · [melubin@pm.me](mailto:melubin@pm.me)

---

I got here through building agents that needed to persist across sessions ([Kairix](https://github.com/marklubin/kairix), three generations). The retrieval part was solved — the part nobody had a good answer for was what happens to memory over time. What should persist, what should compress, what should be forgotten, and what forces should drive those transitions.

I [read the internals](https://marklubin.me/synix/articles/memory-analysis/) of eight major memory systems — Mem0, Letta/MemGPT, Cognee, Zep/Graphiti, LangMem, MemoryWeave, Motorhead, A-MEM. Write paths, read paths, storage backends, failure modes. They all solve retrieval in different ways, but none of them distinguish between information that changes every turn and information that should persist for weeks. The lifecycle question didn't seem to have an answer yet.

I wasn't sure if that was a tooling gap or something more fundamental, so I built [LENS](https://github.com/marklubin/lens-benchmark) — a benchmark that tests coherence across sessions rather than single-turn retrieval. 22 adapters, 16 dataset scopes, 200+ evaluation runs. A SQLite baseline with embeddings scored higher than the purpose-built tools on longitudinal synthesis. That was unexpected and I'm still not sure I fully understand why, but it pushed me toward thinking the problem is structural.

I think the problem comes down to [three things](https://marklubin.me/cdr.pdf). Any agent that persists through unbounded experience with bounded state has to lose information — and the way it loses information defines what it becomes. It can't track fast-changing and slow-changing information at the same rate without aliasing one against the other. And whatever scheme it uses to manage all this will degrade over time as the world shifts underneath it, so without active rebuilding the system silently rots. I call these compress, divide, and renew.

But division isn't just about partitioning into timescale-matched tiers. It's also about adaptive specialization — agents differentiating through scope drift, developing structure that nobody programmed. And the pattern is scale-invariant: the same three problems recur at every level of the hierarchy. Several independent research programs arrive at hierarchy and timescale separation from completely different starting points. The renewal question — what actually keeps these systems coherent over time — is the one I find most interesting, and the one that seems least addressed.

[Synix](https://github.com/marklubin/synix) is where I test these ideas. It's a memory runtime where architectures are pipeline configurations on a shared substrate — four tiers, each with its own dynamics and lifecycle rules. The interesting thing is what emerges when you implement the constraints as pressure equations rather than explicit orchestration: agents specialize, routing emerges, colonies develop generational structure, all without anyone programming it. I've been reproducing existing memory systems as policies on this substrate to see whether they're really all configurations on one system. So far nothing has broken the claim, but I don't think it's fully proven either.

More recently I've been pulling on what this looks like past single agents. If memory lifecycle is a substrate problem for one agent, what's the equivalent when agents have to discover each other, develop shared state, and produce collective behavior without central control? [Aegis](https://github.com/marklubin/aegis-poc) is an early attempt — a coordination protocol for autonomous agent networks. The broader question I'm interested in is whether the right substrate with the right pressures is enough for cognitive structure to emerge on its own, or whether that's naive.

The threads I keep coming back to: generational garbage collection as a model for memory lifecycle. Dynamical systems as a lens for how information moves through cognitive architecture. Societies of mind and what emerges when you give agents the right substrate and get out of the way.

---

Before agent memory: 10 years building production software — distributed systems, real-time audio, AI infrastructure.
