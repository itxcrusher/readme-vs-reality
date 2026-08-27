# Production Gates Behind the Demo

Twelve questions that separate what a system claims from what it enforces. They are design and review prompts, not an automated security standard, and they are domain-agnostic: the examples below lean Web3 because that is where they were developed, but each gate has an equivalent in any stack.

Run them on your own repository. Each gate states the question, the minimum evidence that answers it, and the symptom that shows it has failed.

## 1. Claim traceability

**Question:** What exact source and behavior support each public claim?

**Minimum evidence:** canonical source, exact commit, enforcing component, test or runtime evidence, and a scoped verdict.

**Failure symptom:** the README describes future intent, mock behavior, an API-only check, or a UI state as completed system truth.

## 2. Principal and action binding

**Question:** Who is authorized to perform the exact state change?

**Minimum evidence:** authenticated principal bound to action, target, parameters, domain or chain, nonce, expiry, and final mutation authority.

**Failure symptom:** caller-supplied identity, free-form action labels, direct-call bypass, reusable bearer proof, or authorization enforced only before a weaker downstream boundary.

## 3. Custody and role separation

**Question:** Which keys can spend value, change ownership, finalize outcomes, or act for users?

**Minimum evidence:** role inventory, least privilege, user-controlled authority where claimed, recovery and rotation plan, and explicit compromise impact.

**Failure symptom:** one server credential combines sponsorship, custody, ownership, administration, lifecycle, and oracle authority.

## 4. Replay and state consistency

**Question:** Can a legitimate action be replayed, raced, duplicated, or consumed on behalf of another actor?

**Minimum evidence:** scoped nonce, expiry, domain separation, idempotency, authoritative consumption, and adversarial state-transition tests.

**Failure symptom:** timestamps without contract enforcement, unsigned state transitions, duplicate seats or invoices, stale indexes, or state updated independently across layers.

## 5. Settlement truth

**Question:** Does the observed transfer satisfy the business obligation?

**Minimum evidence:** payer, destination, amount, asset, chain, intent identifier, finality, replay state, and reconciliation outcome.

**Failure symptom:** accepting any successful transaction, relying on an unbacked application balance, confusing token minting with reserves, or leaving refund/dispute states unreachable.

## 6. External truth and oracle authority

**Question:** Where does off-chain truth come from, and who can contest it?

**Minimum evidence:** data source, reporter authorization, freshness, manipulation resistance, dispute and correction path, and failure behavior.

**Failure symptom:** self-reporting, caller-selected outcomes, admin hot-wallet truth, mock feeds, model confidence presented as proof, or immutable storage of an unverified assertion.

## 7. Privacy and proof semantics

**Question:** What is hidden, from whom, and what does the proof actually bind?

**Minimum evidence:** statement definition, holder binding, verifier identity, nonce and expiry, metadata inventory, delegation rules, and presentation consumption or rotation.

**Failure symptom:** public identity data beside a privacy claim, shared cross-user events, bearer secrets, mock verification, or proof of one fact marketed as proof of a broader claim.

## 8. Economic invariants

**Question:** Which quantities must balance across every state transition?

**Minimum evidence:** conservation equations, entitlement rules, reserve model, rounding behavior, zero-winner and partial-failure paths, withdrawal bounds, and invariant tests.

**Failure symptom:** stranded funds, double claims, unbounded work, operator-selected winners, pool misattribution, or obligations not backed by assets.

## 9. Operational readiness

**Question:** Can the system survive real deployment conditions?

**Minimum evidence:** reproducible build, executed tests, CI, secret management, rate limiting suited to topology, monitoring, incident and upgrade paths, and dependency lifecycle.

**Failure symptom:** declared tests treated as passing, process-local controls in a distributed runtime, tracked generated output, hard-coded development endpoints, or a live demo with no recovery model.

## 10. Demand and buyer truth

**Question:** What behavior shows that a named user or buyer needs this workflow?

**Minimum evidence:** payment, procurement, repeated independent use, dependency, quantified workaround, or a bounded experiment with a kill rule.

**Failure symptom:** event placement, page visits, deployed examples, social praise, or builder activity used as a substitute for customer evidence.

## 11. Rights and provenance

**Question:** What can be studied, preserved, reused, modified, and redistributed?

**Minimum evidence:** canonical owner, repository and file-level licenses, attribution, component boundaries, copied-source relationships, and explicit permission where required.

**Failure symptom:** assuming public source is open source, treating a file-level header as a repository-wide grant, or assuming rebranding removes copyright.

## 12. What survives the audit

**Question:** Once you know what the system really enforces, what should happen to it?

**Minimum evidence:** an explicit decision to keep, rebuild, preserve, or delete, with the reason recorded and a condition that would reverse it.

**Failure symptom:** an audit that ends in a document nobody acts on, a rebuild that reproduces the original assumptions, or keeping everything because deleting feels irreversible.

Deciding this across a whole portfolio rather than one system is a longer process. That workflow is in [method.md](method.md).
