# Peer Review Checklist

## Purpose

Use this checklist when reviewing a peer's pull request. It's organized by concern area rather than workflow phase, so it works equally well for a quick pass on a small diff or a deep review of a risky change — scan the sections relevant to what's in front of you.

---

## Level 1 Checklist

### ✅ Correctness
□ Change actually does what the description/ticket says
□ Logic handles the stated edge cases, not just the happy path
□ No off-by-one, null/nil, or boundary errors in changed logic
□ Error paths return or propagate something callers can act on

### 🔍 Readability
□ Names describe intent, not implementation detail
□ Function/method does one thing and is sized to be understood at a glance
□ Comments explain *why*, not what the code already says
□ Diff is scoped to one logical change, not bundled with unrelated cleanup

### 💡 Domain
□ Business rule or invariant is correctly understood and enforced
□ Change doesn't silently break an assumption another part of the system relies on
□ Terminology matches the ubiquitous language used elsewhere in the codebase

### ⚙️ Performance
□ No obvious N+1 queries or unbounded loops over external calls
□ Data structures and algorithms fit the expected scale
□ Caching, if introduced, has a sane invalidation story
□ No unnecessary work happens on a hot path

### ⚙️ Concurrency
□ Shared state is protected or made immutable
□ Retries and timeouts are set at every new network/IO boundary
□ Idempotency holds if the operation can be retried or run twice
□ Race conditions considered for anything touching multiple threads/requests

### 🔍 Security
□ Input from outside the trust boundary is validated
□ AuthN/AuthZ checks are present and cannot be bypassed
□ No secrets, tokens, or PII logged or hardcoded
□ New dependencies are justified and not obviously abandoned/unmaintained

### ✅ Testing
□ Tests cover the new behavior and the edge cases called out in the diff
□ Tests assert behavior, not implementation details
□ Failure/error paths have test coverage, not just the happy path
□ Flaky or skipped tests aren't introduced quietly

### ✅ Observability
□ New failure modes are logged with enough context to debug from the log alone
□ Metrics/traces added for anything that could become a new failure point
□ Log level matches severity (no errors for expected conditions, no silent failures)

### 📝 Maintainability
□ Change doesn't add a pattern the codebase is actively moving away from
□ Documentation/README/config samples updated if behavior changed
□ Feature flag or config default is safe if left forgotten

---

## Notes

Not every section applies to every PR — a copy-change doesn't need a Concurrency pass. Match review depth to blast radius: shared libraries and payment/auth paths deserve every section; a UI label change doesn't.
