# Design Patterns

## Purpose

A refresher for choosing the right design pattern when one is actually warranted — the classic Gang of Four catalog plus the modern patterns that show up constantly in production systems. This is a lookup table for "what's this shape of problem called and what's the standard solution," not a tutorial. See [OOP Design](OOP-Design.md) for the principles that tell you whether you need a pattern at all.

---

## Level 1 Checklist

### 🔍 Creational (object creation)

- [ ] **Factory Method**: a class can't anticipate which concrete type it needs to create — defer instantiation to subclasses
- [ ] **Abstract Factory**: a family of related objects must be created together and stay consistent (e.g. one UI toolkit's widgets)
- [ ] **Builder**: construction has many optional parameters or must happen in steps — avoid telescoping constructors
- [ ] **Prototype**: creating a new object by copying an existing one is cheaper than building from scratch
- [ ] **Singleton**: exactly one instance must exist — use sparingly, it's global mutable state in a trench coat; prefer DI-managed single instances over this pattern
- [ ] **Object Pool**: object creation is expensive (connections, threads) and reuse is safe — pair with strict lifecycle management to avoid leaking stale state
- [ ] **Dependency Injection**: a class needs a collaborator but shouldn't construct it — pass it in instead, so the caller controls wiring and tests can substitute fakes

### 🔍 Structural (composing objects)

- [ ] **Adapter**: an existing interface doesn't match what the client expects — wrap it instead of modifying it
- [ ] **Bridge**: an abstraction and its implementation need to vary independently (avoid a combinatorial class explosion)
- [ ] **Composite**: clients need to treat individual objects and groups of objects uniformly (trees, nested structures)
- [ ] **Decorator**: behavior needs to be layered onto an object dynamically without subclass explosion
- [ ] **Facade**: a subsystem is complex and most callers only need a simple, curated entry point
- [ ] **Flyweight**: many similar objects are consuming memory — extract and share the immutable shared state
- [ ] **Proxy**: access to an object needs to be controlled, deferred, or augmented (lazy loading, access control, remote calls, caching)
- [ ] **Module/Namespace**: related functionality needs a clear boundary and controlled public surface — often replaces several of the above at the package level

### 🔍 Behavioral (communication between objects)

- [ ] **Strategy**: interchangeable algorithms/behaviors need to be swapped at runtime
- [ ] **Observer / Pub-Sub**: producers shouldn't need to know about their consumers, and there may be many
- [ ] **Command**: an action needs to be encapsulated as an object — enables queuing, undo/redo, logging of operations
- [ ] **Chain of Responsibility**: a request should pass through a series of handlers until one handles it (middleware, validation pipelines)
- [ ] **Template Method**: the algorithm's skeleton is fixed but individual steps vary by subtype
- [ ] **State**: an object's behavior changes based on internal state, and state transitions are a first-class concern
- [ ] **Mediator**: many objects communicate with each other in a tangled way — centralize the coordination
- [ ] **Iterator**: a collection's traversal logic should be decoupled from its internal structure
- [ ] **Memento**: an object's state needs to be captured and restored later without violating encapsulation
- [ ] **Visitor**: a new operation needs to be added across a stable set of types without modifying them
- [ ] **Interpreter**: a small language or rule set needs to be parsed and evaluated (rare — usually a real parser/DSL library is the better answer)
- [ ] **Null Object**: a "do nothing" default is cleaner than scattering null checks across every caller

### ⚙️ Modern & Architectural Patterns

- [ ] **Repository**: data access logic needs to be abstracted behind a collection-like interface, decoupling domain logic from the persistence mechanism
- [ ] **Unit of Work**: multiple repository operations need to commit or roll back together as one transaction
- [ ] **CQRS**: read and write models have diverged enough in shape or scale that separating them removes real friction — don't reach for this by default
- [ ] **Event Sourcing**: the sequence of state changes is itself valuable (audit, replay, temporal queries) — accept the operational complexity this brings
- [ ] **Circuit Breaker**: a failing dependency should stop being hammered with retries and fail fast until it recovers
- [ ] **Retry with Backoff**: a transient failure is likely to succeed on a later attempt — pair with jitter and a max-attempt cap
- [ ] **Bulkhead**: one failing dependency or workload shouldn't be able to exhaust resources needed by others
- [ ] **Saga**: a business transaction spans multiple services and needs compensating actions instead of a distributed transaction
- [ ] **Specification**: business rules for selecting/matching objects need to be composed and reused (e.g. `isEligible.and(isActive)`)
- [ ] **Anti-Corruption Layer**: integrating with a legacy or external system whose model shouldn't leak into your domain — translate at the boundary
- [ ] **Strangler Fig**: replacing a legacy system incrementally by routing traffic to the new implementation piece by piece — see [Monolith to Microservices](Monolith-to-Microservices.md)

### ✅ Selection Heuristics

- [ ] Named the actual problem before naming the pattern — pattern-first thinking is a smell
- [ ] Checked three concrete use cases exist before generalizing into a pattern (premature abstraction is worse than duplication)
- [ ] Confirmed the pattern reduces complexity here, not just relocates it or adds indirection for its own sake
- [ ] Preferred the simplest pattern that solves the problem — Strategy over a mini plugin framework, a function over a Command object, when either would do
- [ ] Checked whether the language/framework already gives you this for free (first-class functions often replace Strategy/Command/Visitor)
- [ ] Verified the team will recognize the pattern — an obscure pattern nobody else can maintain is a liability, not a solution

---

## Notes

Patterns are named solutions to recurring problems, not a checklist to apply. The goal of knowing this catalog is recognition speed — when a shape of problem shows up, you should recall the name and its trade-offs in seconds, not derive a solution from scratch. If nothing here fits cleanly, plain code is usually the right answer.
