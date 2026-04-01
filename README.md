# Mark Lubin

Research engineer working on cognitive architecture, information dynamics, and adaptive systems.

**[marklubin.me](https://marklubin.me)** · **[synix.dev](https://synix.dev)** · [melubin@pm.me](mailto:melubin@pm.me)

---

My work is concerned with the organization of information in long-lived intelligent systems, and with the ways that organization shapes reasoning, adaptation, and collective behavior across time. I am interested in how systems decide what matters, how they form durable internal structure from experience, how that structure changes as conditions change, and how coherence can be preserved without freezing a system into rigidity.

The difficult problems do not usually appear at the level of single-turn competence. They appear when information has to endure, when earlier judgments accumulate consequences, and when a system must continue acting under changing conditions. What should remain explicit and stable, what should be compressed, what should be allowed to decay, what should be reconstructed, and what should be re-evaluated from underlying material rather than merely inherited from prior state?

I am especially interested in architectures that treat information not as a flat store but as something differentiated by role, timescale, and consequence. Transient details, working abstractions, durable preferences, procedural traces, and world structure change at different rates, carry different costs when distorted, and call for different forms of retention, compression, and renewal. I [read the internals](https://marklubin.me/synix/articles/memory-analysis/) of eight major memory systems to see how the field approaches this. None of the systems I examined differentiate information by timescale. They all use one flat namespace, one update rate, one retention policy. [LENS](https://github.com/marklubin/lens-benchmark), my benchmark for long-horizon coherence, evaluates whether agent behavior degrades across extended interaction histories. The results suggest that this is not merely a tooling gap but a structural one.

This has led me toward a broader view of intelligence as a systems problem. The more interesting frontier, to me, lies not in the indefinite enhancement of a single core model but in architecture: the interaction between models, external structure, deterministic processes, learned policies, and mechanisms for revision and coordination. The right question is where intelligence is actually needed in a system, not how to maximize it everywhere.

[Synix](https://github.com/marklubin/synix) is where I build and test these ideas. It began as a programmable memory runtime, where architectures are pipeline configurations with differentiated tiers, each with its own retention, [compression, and renewal](https://marklubin.me/cdr.pdf) rules. It is evolving toward something more general: a substrate for adaptive systems that can coordinate across agents, develop shared structure, and maintain coherence without centralized control. The question I am working on now is whether the right structural constraints are enough for higher-order organization to develop on its own, through selective pressure and specialization, rather than requiring explicit orchestration.

Before this, I spent a decade at Amazon building distributed systems across AWS, Prime Video, and payments. That background still shapes the way I think. I am drawn to systems that must survive real constraints, accumulate operational history, and continue functioning under scale, drift, and partial failure. The through-line is architecture. What changed is that the systems in question are no longer only technical infrastructures, but ones that must organize, adapt, and persist.
