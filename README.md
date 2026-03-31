# Mark Lubin

Software engineer. I think about agent memory, cognitive architecture, and information lifecycle.

**[marklubin.me](https://marklubin.me)** · [melubin@pm.me](mailto:melubin@pm.me)

---

I got here through building agents that needed to persist across sessions ([Kairix](https://github.com/marklubin/kairix), three generations). Retrieval was solved. The part nobody had a good answer for was what happens to memory over time — what should stay, what should be compressed, what should be forgotten.

I [read the internals](https://marklubin.me/synix/articles/memory-analysis/) of eight major memory systems — Mem0, Letta/MemGPT, Cognee, Zep/Graphiti, LangMem, MemoryWeave, Motorhead, A-MEM. Write paths, read paths, storage backends, failure modes. None of them distinguish between information that changes every turn and information that should persist for weeks, or a lifetime. They all use one flat namespace at one timescale.

I built [LENS](https://github.com/marklubin/lens-benchmark) to test whether this was a tooling gap or something deeper — a benchmark that tests coherence across sessions rather than single-turn retrieval. 22 adapters, 16 dataset scopes, 200+ evaluation runs. A SQLite baseline with embeddings scored higher than the purpose-built tools on longitudinal synthesis. I think that points at something structural.

Agents have to throw things away. Context windows fill up, you can't keep everything, and the way an agent decides what to discard shapes what it becomes over time. That's one problem.

A different problem is that today's conversation and long-term user preferences need to be stored differently and updated at different rates. If you use the same store and the same update cycle for both, one overwrites the other.

And a third is that whatever memory strategy you pick will stop working as the world changes. Without periodic rebuilding, memory quietly goes stale.

I've been calling these [compress, divide, and renew](https://marklubin.me/cdr.pdf).

The interesting part is what falls out of them. When you give agents the ability to divide, they don't just partition into fixed tiers — they start to specialize on their own, developing structure based on what they actually handle. And the same three problems show up again inside each partition, at every level. Several independent research programs have arrived at the hierarchy part from completely different directions, but the renewal part — what keeps these systems from degrading over time — doesn't seem to have been addressed.

[Synix](https://github.com/marklubin/synix) is where I test these ideas. It's a memory runtime where architectures are pipeline configurations on a shared substrate. Four tiers, each with its own lifecycle rules. When you set up the right constraints and let agents run, they specialize, routing between them emerges, and colonies develop generational structure — none of which is explicitly programmed. I've been reproducing existing memory systems as configurations on this substrate to see whether they're really all instances of one system. So far nothing has broken that, but I don't think it's fully proven.

More recently I've been thinking about what this looks like past single agents — how autonomous systems discover each other, develop shared state, and produce collective behavior without central control. [Aegis](https://github.com/marklubin/aegis-poc) is an early attempt at that.

The ideas are converging around adaptive dynamical systems, structural invariants, self-modification and governance mechanisms — and for the multi-agent case, something closer to collective self-organization than traditional distributed systems.

---

Before this: 10 years building production software — distributed systems, real-time audio, AI infrastructure.
