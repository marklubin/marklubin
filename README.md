# Mark Lubin

Systems engineer. Interested in agent memory, information lifecycle, and cognitive architecture.

Most of my recent work is on one problem: what happens to agent memory over time. I built voice agents with persistent memory, and the hard part turned out not to be retrieval — it was lifecycle. What to keep, what to compress, what to forget, and when. I read the source code of eight major memory systems to see how others approached it. That turned into everything below.

**[marklubin.me](https://marklubin.me)** · [melubin@pm.me](mailto:melubin@pm.me)

---

## Projects

### [Kairix](https://github.com/marklubin/kairix)

Real-time voice AI agents with persistent memory. Three generations (28K + 53K lines Python). Each generation made the same problem more visible — retrieval worked fine, but memory degraded over sessions. Contradictions accumulated, stale context persisted, there was no lifecycle. This is what made me stop building agents and start studying memory.

### [Source-level teardown](https://marklubin.me/synix/articles/memory-analysis/)

I read the internals of Mem0, Letta/MemGPT, Cognee, Zep/Graphiti, LangMem, MemoryWeave, Motorhead, and A-MEM — write paths, read paths, storage backends, failure modes. The whole space operates on one tier of memory at one timescale. No system distinguishes between information that changes every turn and information that should persist for weeks. The retrieval problem has a dozen solutions. The lifecycle problem has zero.

### [LENS](https://github.com/marklubin/lens-benchmark)

Benchmark for agent memory that tests longitudinal coherence across sessions, not single-turn retrieval accuracy. 22 adapter implementations, 16 dataset scopes, 200+ evaluation runs, contamination-resistant dataset generation. SQLite with embeddings outperformed every purpose-built memory tool on longitudinal synthesis. LENS V2 runs every architecture as a policy on the Synix substrate.

### [CDR theory](https://marklubin.me/cdr.pdf)

Compress, Divide, Renew — a formal argument that agent memory requires three structural properties:

- **Compress.** Finite state, infinite input. By pigeonhole, you lose information. The data processing inequality makes it irreversible. The question is which information and how.
- **Divide.** Different information changes at different speeds. Tracking fast and slow signals with the same state and update rate causes aliasing. Rate-distortion bounds force timescale-separated partitions.
- **Renew.** Without active renewal, any bounded-state system tracking a non-stationary source degrades monotonically. This is what separates a system that maintains coherence from one that silently rots.

Five independent research programs — Complementary Learning Systems, cortical temporal hierarchy, deep temporal models, bounded-rational hierarchy, and autonomous learning architectures (Dupoux, LeCun & Malik, 2026) — all derive hierarchy and timescale separation from different axioms. None proves renewal. CDR closes that gap.

Core theorems proved in Lean 4. 11 theorems, zero `sorry`.

### [Synix](https://github.com/marklubin/synix)

Memory runtime where architectures are pipeline configurations, not products. Four tiers (execution, session, experience, identity), each with its own update rate, eviction policy, and consolidation rules. DAG-based transforms, incremental builds, full provenance. 26K lines Python.

LENS V2 reproduces every major memory architecture as a Synix pipeline declaration — the idea is that every existing memory system is a configuration on one substrate.

### [Aegis](https://github.com/marklubin/aegis-poc)

Colony communication protocol for autonomous agent networks. If single-agent memory is a substrate problem, multi-agent coordination is the next surface. How agents discover each other, negotiate, and maintain shared state without centralized control. [Reference spec](https://marklubin.me/synix/articles/aegis-brief/) + working proof of concept.

---

Before agent memory: 10 years of distributed systems, real-time audio, and voice AI.
