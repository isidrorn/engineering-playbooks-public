# OOP Design

## Purpose

Use this checklist when making structural object-oriented design decisions — class boundaries, inheritance vs composition, responsibility placement. It's a refresher on SOLID and coupling/cohesion for an engineer who knows this material but hasn't had to apply it deliberately in a while. For choosing a specific design pattern, see [Design Patterns](Design-Patterns.md).

---

## Level 1 Checklist

### 🔍 SOLID Principles

- [ ] Single Responsibility: does each class have one reason to change, or is it quietly doing two jobs?
- [ ] Open/Closed: can new behavior be added without modifying existing, tested code?
- [ ] Liskov Substitution: can any subtype replace its parent without breaking callers' expectations?
- [ ] Interface Segregation: are interfaces focused, or do implementors have to stub out methods they don't need?
- [ ] Dependency Inversion: do high-level modules depend on abstractions, or are they wired directly to concrete implementations?

### 💡 Coupling & Cohesion

- [ ] Is this class doing too many unrelated things? (low cohesion — split it)
- [ ] Does changing one class force changes in many others? (high coupling — find the shared assumption and isolate it)
- [ ] Are there circular dependencies between packages/modules?
- [ ] Is the Law of Demeter respected? (don't reach through objects: `a.getB().getC().doThing()`)
- [ ] Are implementation details leaking through the public API (return types, exceptions, or parameters that expose internals)?
- [ ] Composition preferred over inheritance where there's no true "is-a" relationship — is inheritance here for code reuse (wrong reason) or genuine substitutability (right reason)?

### ✅ Common Traps

- [ ] Premature abstraction: has this abstraction been justified by at least three concrete cases, or is it speculative?
- [ ] God class/service: any class with 20+ methods or 500+ lines is a signal to look for a seam to split it
- [ ] Anemic domain model: are these objects just data bags with getters/setters, with all the behavior living elsewhere?
- [ ] Over-engineering: is this solving a problem the system doesn't have yet?
- [ ] Stringly-typed code: are raw strings standing in for what should be an enum or a value object?
- [ ] Mutable shared state: could this be immutable, especially anywhere touched by concurrent code?
- [ ] Deep inheritance hierarchies: more than 2-3 levels deep is a sign to reconsider the design, not add a fourth level

---

## Notes

None of this is a rulebook to satisfy mechanically — SRP and "no god classes" are both proxies for the same underlying question: when this needs to change six months from now, how much of the system will have to move with it? Optimize for that, not for checkbox compliance.
