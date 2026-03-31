# Mark Lubin

Systems engineer. Interested in agent memory, information lifecycle, and cognitive architecture.

**[marklubin.me](https://marklubin.me)** · [melubin@pm.me](mailto:melubin@pm.me)

---

I built real-time voice agents with persistent memory ([Kairix](https://github.com/marklubin/kairix), three generations, 28K + 53K lines). Retrieval worked fine, but over enough sessions the memory started contradicting itself — stale context stuck around, preferences drifted without anything noticing. I couldn't find a clean way to handle that, and I got curious whether anyone else had.

I [read the source code](https://marklubin.me/synix/articles/memory-analysis/) of eight memory systems — Mem0, Letta/MemGPT, Cognee, Zep/Graphiti, LangMem, MemoryWeave, Motorhead, A-MEM. Write paths, read paths, storage backends, failure modes. All of them solve retrieval in different ways, but I didn't find one that distinguishes between information that changes every turn and information that should persist for weeks. The lifecycle question — what to keep, what to compress, when to forget — didn't seem to have an answer yet.

I wasn't sure if that was a tooling gap or something more fundamental, so I built [LENS](https://github.com/marklubin/lens-benchmark) — a benchmark that tests coherence across sessions rather than single-turn retrieval, which is what the existing benchmarks measure. 22 adapter implementations, 16 dataset scopes, 200+ evaluation runs, contamination-resistant dataset generation. The thing I didn't expect: a SQLite baseline with embeddings scored higher than the purpose-built tools on longitudinal synthesis. I'm still thinking about why.

Those results pushed me toward formalizing the problem. [CDR theory](https://marklubin.me/cdr.pdf) — Compress, Divide, Renew — is an argument that agent memory needs three structural properties:

- **Compress.** Finite state, infinite input. By pigeonhole, you lose information. The data processing inequality makes it irreversible. The question is which information and how.
- **Divide.** Different information changes at different speeds. Tracking fast and slow signals with the same state and update rate causes aliasing. Rate-distortion bounds suggest you need timescale-separated partitions.
- **Renew.** Without active renewal, any bounded-state system tracking a non-stationary source should degrade monotonically. This is the property I find most interesting — it's the one that none of the existing convergent research programs (Complementary Learning Systems, cortical temporal hierarchy, deep temporal models, bounded-rational hierarchy) prove, even though they all derive hierarchy and timescale separation independently.

I proved the core theorems in Lean 4 — 11 theorems, zero `sorry`. Though I think the more interesting question is whether the theory actually predicts system behavior in practice, which is partly why I built the next thing.

[Synix](https://github.com/marklubin/synix) is a memory runtime where architectures are pipeline configurations on a shared substrate. Four tiers (execution, session, experience, identity), each with its own update rate, eviction policy, and consolidation rules. DAG-based transforms, incremental builds, full provenance. 26K lines Python. LENS V2 runs every major memory architecture as a Synix pipeline declaration — the idea is that these are all configurations on one substrate. I haven't fully proven that yet, but so far nothing has broken the claim.

[Aegis](https://github.com/marklubin/aegis-poc) is a more recent thing — a coordination protocol for autonomous agent networks. If memory lifecycle matters for a single agent, I'm curious what the equivalent problem looks like when agents have to share state without centralized control. [Reference spec](https://marklubin.me/synix/articles/aegis-brief/) + working proof of concept.

---

Before agent memory: 10 years of distributed systems, real-time audio, and voice AI.
