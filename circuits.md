**The Circuit Model: A Formal Specification of Events and Items in Distributed Systems**

Gabriel B. Rondon ([me@grondon.com](mailto:me@grondon.com))

Robson…

**Abstract**

This paper introduces the formal structure of circuits as a general model for distributed coordination and state evolution.  
A circuit represents a composition of items and events, where items describe discrete stateful entities, and events represent  
atomic transitions that affect those states. The model focuses on mathematical consistency, verifiable causality, and compositionality  
without reliance on global consensus. This specification defines the primitives, transition functions, and synchronization semantics  
that govern the operation of circuits as distributed state machines.

**1\. Introduction**

Distributed systems often require coordination between autonomous agents operating over shared or partially shared data.  
The notion of a circuit emerges as a minimal abstraction that allows multiple actors to publish, modify, and synchronize  
state changes in a verifiable manner. Rather than a single ledger or authority, circuits describe relational domains where  
items evolve independently but can reference and influence each other through structured events. This model provides a foundation  
for composable and causally consistent data coordination.

**2\. Formal Definitions**

Let Σ be the set of all possible item states, and E the set of all valid events. Each item i ∈ I maintains a local state σₜ ∈ Σ  
that evolves through events applied over time.

The basic state transition is defined as:

* σₜ₊₁ \= Ψ(σₜ, Eₜ)

where Ψ : Σ × E → Σ is a deterministic transition function mapping a prior state and event into a new state.  
Each event is represented by the tuple:

* Eᵢ \= (ρᵢ, δᵢ, hᵢ₋₁)

where ρᵢ is the payload, δᵢ is the author or proof of origin, and hᵢ₋₁ is the hash reference to the previous event.  
The event hash is defined recursively as:

* hᵢ \= H(ρᵢ, δᵢ, hᵢ₋₁)

The cumulative state hash of an item summarizes all events up to time t:

* Σₜ₊₁ \= H(Σₜ, Eₜ)

**3\. Synchronization and Causality**

Circuits enable asynchronous publication of events by multiple actors. When two event sequences share a common ancestor  
but diverge, a fork condition arises:

* Eᵢᵃ, Eⱼᵇ ⇒ fork if hᵢ₋₁ᵃ ≠ hⱼ₋₁ᵇ

Merging such divergent branches is handled by a merge operator M, producing a resolved event:

* M(Eᵢᵃ, Eⱼᵇ) → Eₖ

The merge operator may rely on deterministic resolution strategies, vector timestamps, or contextual priority rules  
defined by each circuit’s logic. Thus, causality is preserved without global ordering.

**4\. Composition of Circuits**

A circuit C is defined as the tuple:

* C \= (ℛ, I₀, I₁, …, Iₙ)

where ℛ represents the set of rules governing event validation and composition. The validation function is expressed as:

* V\_C(Eᵢ) \= { true, if Eᵢ satisfies ℛ; false otherwise }

Circuits can reference each other through their items or through shared validation schemas, enabling modular  
and hierarchical data coordination structures. Composition occurs when one circuit subscribes to another’s item events  
as valid triggers for its own transition functions.

**5\. Properties and Integrity**

The circuit model ensures the following properties:

* • Deterministic replay — given an initial state and event log, any node can reconstruct the same state.  
* • Causal integrity — all events maintain cryptographic linkage ensuring lineage and immutability.  
* • Local validation — rules ℛ define event acceptance at circuit scope, allowing domain-specific enforcement.  
* • Compositionality — circuits can be combined or nested, forming higher-level coordination systems.

**6\. Discussion**

The circuit model abstracts the minimal mathematical conditions required for distributed verifiable state management.  
It generalizes the concept of event-driven systems, representing causality as a sequence of cryptographically linked transitions.  
While implementation details may vary, the formal properties remain invariant: every item is a deterministic state machine,  
every event is a valid transformation, and every circuit defines a verifiable local universe of rules and relationships.

**References**

\[1\] Gabriel B. Rondon, “On Circuits and Distributed Event Coordination”, 2025\.

\[2\] Lamport, L., “Time, Clocks, and the Ordering of Events in a Distributed System”, CACM, 1978\.

\[3\] Milner, R., “Communicating and Mobile Systems: The π-Calculus”, Cambridge University Press, 1999\.

