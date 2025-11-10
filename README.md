# The Circuit Model

A formal specification for distributed coordination and state evolution in decentralized systems.

## Overview

The Circuit Model provides a mathematical framework for managing distributed state machines without requiring global consensus. It represents systems as compositions of **items** (stateful entities) and **events** (atomic state transitions), enabling verifiable causality and compositionality across distributed actors.

## Key Components

- **Items**: Discrete stateful entities that evolve through events
- **Events**: Atomic transitions containing payloads, authorship proofs, and causal references
- **Circuits**: Compositions of items governed by deterministic rule sets
- **Adapters**: Pluggable storage and network backends for physical implementation

## Core Properties

- **Deterministic State Evolution**: States evolve through a well-defined transition function
- **Causal Consistency**: Events maintain hash-linked histories for verifiable ordering
- **Fork Resolution**: Deterministic merge operators handle divergent event sequences
- **Privacy Support**: Optional zero-knowledge proofs enable confidential transactions
- **Storage Agnostic**: Adapter architecture supports various backend implementations

## Mathematical Foundation

The model defines state transitions as:
```
σₜ = Ψ(σₜ₋₁, Eₜ)
```

Where events are structured as tuples containing payload, authorship, hash references, timestamps, and optional proofs.

## Documentation

See `circuits.md` for the complete formal specification and `circuits.pdf` for the full paper.
