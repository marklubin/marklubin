# Mark Lubin

Systems engineer working on agent memory infrastructure — how AI agents maintain, compress, and act on context across time.

I spent the last year and a half on one question: **what happens to agent memory over time?** I built voice agents with persistent memory, and the hard problem turned out not to be retrieval — it was lifecycle. What to keep, what to compress, what to forget, and when. I read the source code of eight major memory systems to see if anyone had solved it. They hadn't. So I started building.

**[marklubin.me](https://marklubin.me)** · [melubin@pm.me](mailto:melubin@pm.me) · [LinkedIn](https://linkedin.com/in/marklubin) · [X](https://x.com/marklubin)

---

## Body of work

The projects below trace a single thread: from building agents that needed memory, to discovering nobody had solved the lifecycle problem, to benchmarking the space, formalizing why it's hard, building a substrate that addresses it, and extending the ideas to multi-agent coordination.

### Kairix — where it started

**[marklubin/kairix](https://github.com/marklubin/kairix)** · 28K lines · Python

Real-time voice AI agents with persistent memory. Three generations: v1 was a custom cognitive engine, v2 rebuilt on Pipecat + Letta, KP3 (53K lines) was a full passage pipeline. Each generation made the same problem more visible — retrieval was fine, but memory degraded over sessions. Contradictions accumulated. Stale context persisted. There was no lifecycle.

This is what made me stop building agents and start studying memory.

### Source-level teardown — what everyone else built

**[Published on marklubin.me](https://marklubin.me/synix/articles/memory-analysis/)** · ~6,000 words

I read the source code of Mem0, Letta/MemGPT, Cognee, Zep/Graphiti, LangMem, MemoryWeave, Motorhead, and A-MEM. Not the docs — the actual write paths, read paths, storage backends, and failure modes.

What I found: the entire agent memory space operates on a single tier of memory at a single timescale. No system distinguishes between information that changes every turn and information that should persist for weeks. No system has principled lifecycle management. The retrieval problem has a dozen solutions. The lifecycle problem has zero.

Backed by 18 deep competitor analyses and 5 cross-competitor comparison studies totaling 60K+ words of research.

### LENS — measuring what matters

**[marklubin/lens-benchmark](https://github.com/marklubin/lens-benchmark)** · 356K lines (incl. test infrastructure) · 1,040 tests · Python

A benchmark for agent memory that tests longitudinal coherence across sessions — not single-turn retrieval accuracy, which is what every existing benchmark measures.

- 22 adapter implementations (every major memory tool + baselines)
- 16 dataset scopes (from single-session factual to multi-week identity evolution)
- 200+ scored evaluation runs
- Two-stage contamination-resistant dataset generation

The result that changed my thinking: SQLite with embeddings outperformed every purpose-built memory tool on longitudinal synthesis tasks. The tools are optimized for the wrong thing.

LENS V2 runs every architecture as a policy on the Synix substrate — proving substrate generality empirically.

### CDR theory — why lifecycle is a structural requirement

**[Position paper (PDF)](https://marklubin.me/cdr.pdf)** · Lean 4 proofs · arXiv submission in preparation

Compress, Divide, Renew (CDR) — a formal argument that agent memory systems require three structural properties:

1. **Compress.** Finite state, infinite input. By pigeonhole, you lose information — the only question is which information and how. The data processing inequality guarantees it's irreversible. Every compression stage is a one-way door.

2. **Divide.** Different information changes at different speeds. User preferences drift over weeks; conversation context changes every turn. Tracking these with the same state and update rate causes aliasing — fast changes blur slow patterns, slow updates miss fast signals. You need timescale-separated partitions. This isn't a design choice; it's forced by rate-distortion bounds.

3. **Renew.** Without active renewal, any bounded-state system tracking a non-stationary source degrades monotonically. Renewal is what distinguishes a system that maintains coherence from one that silently rots.

Five independent research programs — Complementary Learning Systems (McClelland), cortical temporal hierarchy (Hasson), deep temporal models (Friston), bounded-rational hierarchy (Genewein), and autonomous learning architectures (Dupoux, LeCun & Malik, 2026) — all derive hierarchy and timescale separation from different axioms. None of them proves renewal. CDR closes that gap.

The core theorems are proved in Lean 4: 11 theorems, zero `sorry`. Formal verification of memory system properties is rare in this space — I'm not aware of anyone else who's done it for agent memory.

### Synix — the substrate

**[marklubin/synix](https://github.com/marklubin/synix)** · 26K lines · Python

A memory runtime that treats memory architectures as pipeline configurations, not products.

- **Four tiers:** execution (ms → min), session (min → hrs), experience (hrs → wks), identity (wks → permanent). Each tier has its own update rate, eviction policy, and consolidation rules — matched to the timescale of the information it manages.
- **DAG-based transforms:** memory operations are nodes in a directed acyclic graph. Pipelines are declarative, composable, and reproducible.
- **Incremental builds:** only recompute what changed. Full provenance tracking.
- **Substrate generality:** LENS V2 reproduces every major memory architecture (Mem0, Letta, Cognee, etc.) as a Synix pipeline declaration. The claim: every existing memory system is a configuration on this one substrate.

### Aegis — multi-agent coordination

**[marklubin/aegis-poc](https://github.com/marklubin/aegis-poc)** · Reference spec (32K+ words) + working PoC

If single-agent memory is a substrate problem, multi-agent coordination is the next surface. Aegis is a colony communication protocol for autonomous agent networks — how agents discover each other, negotiate coordination, and maintain shared state without centralized control.

Reference specification covers theoretical foundations, node contracts, lifecycle management, and sample policies. The PoC implements the core protocol on Telegram with Claude Code agents.

---

## What I'm looking for

A research engineering role at a frontier lab where theory and systems come together — where I can both formalize how agent memory should work and build the infrastructure that proves it.

The work above is one program: the landscape analysis shows the gap, the benchmark proves it empirically, the theory explains why it exists, and the substrate demonstrates a solution. I want to bring this to a place where it connects to frontier models and real-scale agent deployments.

---

## Background

- 10+ years building production systems — distributed systems, real-time audio pipelines, voice AI
- ~110K lines of production code across this body of work
- 55+ foundation papers surveyed, citation network mapped
- Competitive landscape: 200+ agent memory companies analyzed, 29 profiled in depth
