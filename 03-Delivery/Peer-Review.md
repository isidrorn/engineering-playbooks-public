# Peer Review

## Purpose

Use this checklist when reviewing a peer's pull request. It's organized by concern area rather than workflow phase, so it works equally well for a quick pass on a small diff or a deep review of a risky change — scan the sections relevant to what's in front of you.

---

## Level 1 Checklist

### ✅ Correctness

- [ ] Change actually does what the description/ticket says
- [ ] Logic handles the stated edge cases, not just the happy path
- [ ] No off-by-one, null/nil, or boundary errors in changed logic
- [ ] Error paths return or propagate something callers can act on
- [ ] Time zone handling checked wherever dates/times cross a boundary (storage, display, comparison)
- [ ] Integer overflow or precision loss checked in arithmetic, especially money or large counters
- [ ] Race conditions checked in any state transition (status fields, workflow steps, cache updates)

### 🔍 Readability

- [ ] Names describe intent, not implementation detail
- [ ] Function/method does one thing and is sized to be understood at a glance
- [ ] Comments explain *why*, not what the code already says
- [ ] Diff is scoped to one logical change, not bundled with unrelated cleanup
- [ ] Magic numbers/strings extracted to named constants
- [ ] No dead code or commented-out code left behind

### 💡 Domain

- [ ] Business rule or invariant is correctly understood and enforced
- [ ] Change doesn't silently break an assumption another part of the system relies on
- [ ] Terminology matches the ubiquitous language used elsewhere in the codebase

### ⚙️ Performance

- [ ] No obvious N+1 queries or unbounded loops over external calls
- [ ] Data structures and algorithms fit the expected scale
- [ ] Caching, if introduced, has a sane invalidation story
- [ ] No unnecessary work happens on a hot path
- [ ] DB migrations checked for table locks under load (large `ALTER TABLE`, missing `CONCURRENTLY`, etc.)
- [ ] New queries have supporting indexes, not a sequential scan waiting to happen
- [ ] In-memory collections that grow from external input have a bound (no unbounded caches/lists)

### ⚙️ Concurrency

- [ ] Shared state is protected or made immutable
- [ ] Retries and timeouts are set at every new network/IO boundary
- [ ] Idempotency holds if the operation can be retried or run twice
- [ ] Race conditions considered for anything touching multiple threads/requests
- [ ] Read-modify-write sequences are atomic (no check-then-act without a lock/CAS/transaction)
- [ ] `@Transactional` (or the language/framework equivalent) is present wherever multiple writes must succeed or fail together

### 🔍 Security

- [ ] Input from outside the trust boundary is validated
- [ ] AuthN/AuthZ checks are present and cannot be bypassed
- [ ] No secrets, tokens, or PII logged or hardcoded
- [ ] New dependencies are justified and not obviously abandoned/unmaintained
- [ ] New dependencies' licenses are compatible with this project (not just checked for maintenance activity)
- [ ] Dynamic SQL/query construction is parameterized, not string-concatenated
- [ ] URL/webhook handling validates destinations to prevent SSRF (no fetching arbitrary user-supplied URLs server-side unchecked)

### ✅ Testing

- [ ] Tests cover the new behavior and the edge cases called out in the diff
- [ ] Tests assert behavior, not implementation details
- [ ] Failure/error paths have test coverage, not just the happy path
- [ ] Flaky or skipped tests aren't introduced quietly
- [ ] Tests are isolated — no shared mutable state or ordering dependency between tests
- [ ] Assertions check the actual outcome, not just "no exception was thrown"

### ✅ Observability

- [ ] New failure modes are logged with enough context to debug from the log alone
- [ ] Metrics/traces added for anything that could become a new failure point
- [ ] Log level matches severity (no errors for expected conditions, no silent failures)

### 🔄 Backward Compatibility

- [ ] API contract changes are additive or versioned, not silently breaking existing callers
- [ ] DB migration is reversible, or the irreversibility is a deliberate, called-out decision
- [ ] Config format changes tolerate old config still in place during rollout
- [ ] Serialization format changes (wire format, event schema, cache format) are readable by both old and new code during deploy

### 📝 Maintainability

- [ ] Change doesn't add a pattern the codebase is actively moving away from
- [ ] Documentation/README/config samples updated if behavior changed
- [ ] Feature flag or config default is safe if left forgotten

---

## Notes

Not every section applies to every PR — a copy-change doesn't need a Concurrency pass. Match review depth to blast radius: shared libraries and payment/auth paths deserve every section; a UI label change doesn't.
