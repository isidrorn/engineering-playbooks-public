# Testing Strategy

## Purpose

Use this checklist when designing or auditing a test strategy — what to test, at what level, and how to keep the suite healthy and trustworthy over time. It's for the moment you're deciding how a feature or system *should* be tested, not for writing an individual test.

---

## Level 1 Checklist

### 💡 Test Pyramid

- [ ] Unit tests are fast, isolated, and cover logic and edge cases — the bulk of the suite
- [ ] Integration tests verify component boundaries (DB, API, message broker) against real infrastructure
- [ ] End-to-end tests are minimal and cover critical user journeys only — they're expensive to maintain
- [ ] Contract tests verify API contracts between producer and consumer services where applicable
- [ ] Suite shape checked for being top-heavy (too many E2E, not enough unit) and rebalanced if so

### 🔍 What to Test

- [ ] Business logic and domain rules — the actual value the system provides
- [ ] Edge cases: nulls, empty collections, boundary values, max/min, unicode, time zones
- [ ] Error handling: what happens when dependencies fail, time out, or return unexpected data
- [ ] Concurrency: thread safety, race conditions, deadlocks
- [ ] Security: input validation, access control, injection attempts
- [ ] Performance: response time under load for critical paths, not every endpoint
- [ ] Data migrations: integrity verified before and after, not just "the script ran without erroring"

### ⚙️ Test Quality

- [ ] Tests assert behavior, not implementation (test WHAT, not HOW)
- [ ] Each test has a single clear reason to fail
- [ ] Tests are independent — no shared mutable state, no order dependency
- [ ] Test names describe the scenario and expected outcome
- [ ] Test data is explicit in the test, not hidden in shared fixtures
- [ ] Mocking avoided for things you don't own — use integration tests for third-party boundaries instead
- [ ] Flaky tests are fixed or deleted, never left ignored — a flaky suite trains people to ignore failures

### ✅ Test Infrastructure

- [ ] Tests run in CI on every PR, not just locally before merge
- [ ] Test suite completes in reasonable time (under ~10 min for unit, under ~30 min for full)
- [ ] Integration tests use test containers or embedded instances, not shared staging databases
- [ ] Code coverage is measured but not worshipped — 80% is a signal, 100% is a trap
- [ ] Mutation testing considered for critical business logic, where line coverage alone can mislead

---

## Notes

Revisit this checklist whenever a bug ships that tests should have caught — that's a signal about where the strategy has a gap, not just a signal to add one more test.
