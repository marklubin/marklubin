# Mark Lubin

Software engineer. I think about agent memory, cognitive architecture, and information lifecycle.

**[marklubin.me](https://marklubin.me)** · [melubin@pm.me](mailto:melubin@pm.me)

---

I got here through building agents that needed to persist across sessions ([Kairix](https://github.com/marklubin/kairix), three generations). Retrieval was solved. The part nobody had a good answer for was what happens to memory over time — what should stay, what should be compressed, what should be forgotten.

I [read the internals](https://marklubin.me/synix/articles/memory-analysis/) of eight major memory systems — Mem0, Letta/MemGPT, Cognee, Zep/Graphiti, LangMem, MemoryWeave, Motorhead, A-MEM. Write paths, read paths, storage backends, failure modes. None of them distinguish between information that changes every turn and information that should persist for weeks, or a lifetime. They all use one flat namespace at one timescale.

I think this points at something structural. Agents have to throw things away — context windows fill up, you can't keep everything — and the way an agent decides what to discard shapes what it becomes over time. That's not a cache hierarchy problem, where every tier holds the same data at different speeds. Different kinds of information need different retention policies, different update rates, and different compression strategies. Today's conversation and a user's long-term preferences aren't the same data moving through faster and slower storage — they're fundamentally different things that degrade in different ways.

And strategies that were adaptive in the past might not be adaptive now. The way an agent decided what to keep last month was based on what mattered then — but the world moved, and those decisions compound. Each one is irreversible. Nothing in any existing system notices when its own memory strategy has gone stale. The only fix is to periodically rebuild from raw material.

I've been calling these three problems [compress, divide, and renew](https://marklubin.me/cdr.pdf).

The [LENS benchmark](https://github.com/marklubin/lens-benchmark) results are what convinced me. I built it to test coherence across sessions rather than single-turn retrieval — 22 adapters, 16 dataset scopes, 200+ evaluation runs. A SQLite baseline with embeddings scored higher than every purpose-built memory tool on longitudinal synthesis. I think that's because the dedicated tools actively transform and compress information in ways that hurt coherence across sessions, while SQLite just stores and retrieves without mangling anything. The tools are solving single-turn retrieval well but degrading the very information you need for multi-session reasoning.

The interesting part is what falls out of compress, divide, and renew when you implement them. When you give agents the ability to divide, they don't just partition into fixed tiers — they start to specialize on their own, developing structure based on what they actually handle. And the same three problems show up again inside each partition, at every level.

[Synix](https://github.com/marklubin/synix) is where I test these ideas. It's a memory runtime where architectures are pipeline configurations on a shared substrate. Four tiers, each with its own lifecycle rules. In the runs I've done so far, agents specialize, routing between them emerges, and colonies develop generational structure — I don't have published results on this yet, but the behavior has been consistent. I've also been reproducing existing memory systems as configurations on this substrate to see whether they're really all instances of one system. So far nothing has broken that.

More recently I've been thinking about what this looks like past single agents — how autonomous systems discover each other, develop shared state, and produce collective behavior without central control. [Aegis](https://github.com/marklubin/aegis-poc) is an early attempt at that.

The ideas are converging around adaptive dynamical systems, structural invariants, self-modification and governance mechanisms — and for the multi-agent case, something closer to collective self-organization than traditional distributed systems.

---

Before this: 10 years building production software — distributed systems, real-time audio, AI infrastructure.
