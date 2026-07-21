# Database Design

## Purpose

Use this checklist when designing a new data store for a service, adding a major new entity to an existing one, or reviewing someone else's schema before it ships. It walks through modeling, engine choice, indexing, transactions, migrations, scaling, and operations so the decisions that are painful to reverse — primary key format, consistency model, sharding key — get made deliberately instead of by default.

---

## Level 1 Checklist

### 💡 Data Modeling

- [ ] Normalization vs denormalization trade-off made deliberately per table, not applied uniformly across the schema
- [ ] Entity relationships and cardinality mapped out (1:1, 1:N, N:N) before tables are drawn
- [ ] OLTP vs OLAP access shape identified — transactional correctness and analytical scan performance pull schema design in opposite directions
- [ ] Primary key format chosen deliberately: natural vs surrogate, sequential vs UUID — weigh index fragmentation (random UUIDs bloat clustered indexes) against volume exposure (sequential IDs reveal row counts)
- [ ] Soft delete vs hard delete policy decided per entity, including how soft-deleted rows are excluded from default queries (partial index on `deleted_at IS NULL`, not a filter everyone has to remember)
- [ ] Audit/versioning columns defined up front (created_at, updated_at, updated_by, row version) — retrofitting them onto a live table is far more expensive than adding them at design time
- [ ] Schema evolution strategy exists: how new optional fields, renamed columns, and split tables get introduced without a flag day
- [ ] Foreign key constraints used deliberately, not skipped by default for "flexibility" — know what integrity check is being given up if they're omitted

### 💡 Engine & Storage Choice

- [ ] Storage engine matched to actual access pattern, not to team familiarity: relational (joins, ACID), document (nested/variable schema, denormalized reads), key-value (single-key lookups at extreme scale), columnar (analytical aggregation over few columns, many rows), graph (traversal-heavy relationships)
- [ ] ACID vs BASE trade-off understood and chosen deliberately for this workload, not inherited from whatever the team used last time
- [ ] Polyglot persistence considered per bounded context — it's fine for one service to use two different stores for two different access patterns, as long as each has a clear owner and sync/consistency story
- [ ] For any distributed store, the CAP trade-off actually made is named (which is sacrificed under partition: availability or consistency) and matches what the business actually needs
- [ ] Vendor/engine lock-in risk acknowledged if proprietary features (stored procs, engine-specific extensions) are used

### 🔍 Indexing & Query Performance

- [ ] Every index backs an actual, observed query predicate — not a guess at what might be queried someday
- [ ] Composite index column order matches query patterns (equality columns before range columns, most selective first where equally used)
- [ ] Covering indexes considered for hot read paths to avoid a second lookup back to the base table
- [ ] Over-indexing cost acknowledged — every index slows every write and consumes storage; indexes are a deliberate spend, not a free safety net
- [ ] Query plans reviewed for the important paths — confirm index usage, catch unexpected full/sequential scans before they hit production volume
- [ ] N+1 query patterns identified and prevented (batch loading, joins, or explicit eager-fetch) rather than discovered in a profiler after launch
- [ ] Pagination strategy chosen deliberately: offset pagination (simple, but degrades and can skip/duplicate rows under concurrent writes) vs keyset/cursor pagination (stable and fast at depth, but can't jump to an arbitrary page)
- [ ] Selectivity of key indexed columns checked — a low-cardinality column (boolean, small enum) rarely earns its own index

### 💡 Transactions & Consistency

- [ ] Isolation level chosen deliberately per workload, not left at the default — understand what anomaly each level still permits (dirty read, non-repeatable read, phantom read, write skew) and whether the app tolerates it
- [ ] Long-running transactions avoided — they hold locks, block vacuum/cleanup, and grow undo/redo state; batch large operations instead
- [ ] Distributed transactions (two-phase commit across stores) avoided where a saga or eventual-consistency pattern with compensating actions would do
- [ ] Optimistic vs pessimistic locking chosen per contention profile — optimistic (version column, retry on conflict) for low contention, pessimistic (explicit locks) for hot rows with frequent conflicting writes
- [ ] Idempotency designed in for retried writes (idempotency key, upsert semantics) — retries are a certainty, not an edge case
- [ ] Deadlock possibility considered wherever a transaction touches more than one row/table — is there a consistent acquisition order?

### ⚙️ Migrations & Schema Change

- [ ] Backward-compatible migration pattern used (expand/contract: add the new shape, dual-write or backfill, cut over readers, then remove the old shape) rather than drop-and-recreate
- [ ] Large-table migrations don't take a blocking lock on production — online schema change tooling or manual batching used for adding columns/indexes on large tables
- [ ] Every migration has a tested reverse path, or an explicit documented reason why it's irreversible (e.g., destructive data change)
- [ ] Migration tested against production-like data volume and shape before running against production — a migration that's instant on a dev seed can lock a table for minutes at real scale
- [ ] DDL statements audited for long-held locks (e.g., adding a NOT NULL column with a default can rewrite the whole table on some engines) and scheduled or batched accordingly
- [ ] Rollout order sequenced correctly against application deploys (schema change before or after code deploy, matching the expand/contract phase)

### ⚙️ Scaling

- [ ] Read replicas considered for read-heavy load, with replication lag implications made explicit to callers (can this read tolerate staleness, or does it need the primary?)
- [ ] Connection pooling sized to the actual workload (concurrent request count, not guesswork) — too few starves throughput, too many exhausts the database's connection limit
- [ ] Partitioning/sharding key chosen for even distribution across the expected access pattern, not convenience — see `Scalability-Decision-Framework.md` for the broader trade-off
- [ ] Caching layer in front of the database has a deliberate invalidation strategy (TTL, write-through, explicit bust on write) — a cache without an invalidation story is a consistency bug waiting to happen
- [ ] Hot partition / hot key risk assessed — is there a key (tenant, user, timestamp bucket) that will receive disproportionate traffic and skew the shard/partition it lands on?
- [ ] Row count and payload size growth modeled 12-24 months out, not sized only to current-day traffic

### ✅ Operational

- [ ] Backup/restore actually tested end to end (restore drill completed, not just backup job green) — see `Disaster-Recovery.md`
- [ ] Replication lag monitored and alerted on, with a defined threshold tied to what depends on it (read replicas, failover)
- [ ] Slow query log reviewed on a cadence, not just after an incident
- [ ] Connection limits and statement timeouts configured explicitly — an unbounded query or connection leak shouldn't be able to take the whole database down
- [ ] Credentials scoped per service with least privilege, and rotated on a schedule (not "set once at provisioning and never touched again")
- [ ] Storage and capacity growth projected against current provisioning, with a trigger point for when to scale up/out

---

## Notes

The primary key format, the consistency model, and the sharding key are the three decisions in this list that are genuinely expensive to reverse once data exists — spend disproportionate thought on those before anything else. Revisit the Indexing and Scaling sections whenever query patterns or traffic assumptions change materially; an index set that was correct at launch quietly becomes wrong as usage evolves.
