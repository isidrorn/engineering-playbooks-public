# Coding Best Practices

## Purpose

Use this checklist as a refresher for writing clean, maintainable production code — the things that slip when you're moving fast, working under pressure, or haven't written production code in a particular style for a while.

---

## Level 1 Checklist

### 🔍 Naming & Readability

- [ ] Names reveal intent (what, not how) — `calculateShippingCost`, not `calc`
- [ ] Abbreviations that aren't universally understood are avoided
- [ ] Boolean names read as questions: `isValid`, `hasPermission`, `canRetry`
- [ ] Method names describe what they DO, not what they're called FROM
- [ ] Classes named as nouns, methods as verbs, interfaces as capabilities (`Serializable`, `Comparable`)
- [ ] Naming conventions are consistent within the codebase (don't mix camelCase and snake_case)
- [ ] No magic numbers or strings — extracted to named constants

### ⚙️ Method & Class Design

- [ ] Methods do one thing and are short enough to understand at a glance
- [ ] Max 3-4 parameters — beyond that, introduce a parameter object
- [ ] Boolean parameters that change behavior avoided — prefer two well-named methods
- [ ] Early returns used to reduce nesting (guard clauses)
- [ ] Inputs validated at the boundary; internal calls trust their callers (fail fast, not fail everywhere)
- [ ] Immutability preferred — if it doesn't need to change, it's final/readonly
- [ ] Null isn't returned — use Optional, empty collections, or throw a meaningful exception instead

### ⚙️ Error Handling

- [ ] Specific exceptions are caught, not generic Exception/Throwable
- [ ] Logs include context (what was being attempted, what input caused it, what state was expected)
- [ ] Exceptions aren't swallowed silently — if you catch it, handle it or rethrow it
- [ ] Recoverable errors (retry, fallback) are distinguished from fatal errors (crash, alert)
- [ ] Error messages are written for the person debugging at 3am — IDs, values, and what to check next
- [ ] Exceptions aren't used for ordinary control flow

### 📝 Defensive Coding

- [ ] Validation happens at system boundaries (user input, external APIs, config values)
- [ ] Null/empty is checked wherever data crosses a trust boundary
- [ ] Timeouts are set on all external calls (HTTP, DB, cache, queue)
- [ ] Collection sizes are bounded when building from external data, to prevent OOM
- [ ] Resources are closed properly (try-with-resources, using statements, defer)
- [ ] Thread safety is documented explicitly — is this class safe to share across threads or not

### ✅ Code Hygiene

- [ ] No commented-out code — delete it, git remembers
- [ ] No TODOs without a ticket number attached
- [ ] No dead code — unused methods, unreachable branches, stale feature flags
- [ ] Dependencies kept up to date — stale dependencies are security debt
- [ ] Linter/formatter run before committing — style debates belong in config, not in review comments

---

## Notes

This is a refresher, not a style guide — where it conflicts with your team's actual conventions, the team's conventions win. Use it to catch the habits that erode quietly over time, not to relitigate settled style choices.
