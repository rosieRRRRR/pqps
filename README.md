# PQPS -- Post-Quantum Persistent States

**Bilateral Human-AI Relational Persistence Under Sovereign Human Control**

* **Specification Version:** 1.0.0
* **Status:** Implementation Ready
* **Date:** 2026
* **Author:** rosiea
* **Contact:** [PQRosie@proton.me](mailto:PQRosie@proton.me)
* **Licence:** Apache License 2.0 — Copyright 2026 rosiea
* **PQ Ecosystem:** CORE — The PQ Ecosystem is a post-quantum security framework built on deterministic enforcement, fail-closed semantics, and refusal-driven authority. Bitcoin is the reference deployment. It is not the scope.

---

## Summary

PQPS defines rules for storing and accessing long-lived state under user control.

It specifies how human-side and AI-side state is persisted, bounded, and invalidated without introducing implicit authority.

PQPS does not enforce policy. All state-dependent decisions are evaluated by PQSEC.

---

## Explicit Dependencies

| Specification | Minimum Version | Purpose |
|---------------|-----------------|---------|
| PQSEC | ≥ 2.0.3 | Predicate enforcement for state access and mutation |
| PQSF | ≥ 2.0.3 | Canonical encoding, EBT storage envelopes, ReceiptEnvelope types |
| Epoch Clock | ≥ 2.1.0 | Tick authority for freshness, expiry, and temporal binding |
| PQAI | ≥ 1.2.0 | AI-side state integration and behavioural requirements |
| BPC | ≥ 1.1.0 | Authorization-before-construction primitive for holder control actions (Inspect/Edit/Delete/Pause/Scope/etc.). BPC's authorization-before-construction pattern is rail-agnostic; PQPS uses it for state mutation governance, not Bitcoin transaction gating. |

Implementations MAY evaluate using earlier versions, but MUST NOT claim conformance while below the stated minimums.

---

## Index

**Preamble**
- 0. Scope and Purpose
  - 0.1 Behavioural Requirements Boundary
- 1. Core Principles (Normative)
  - 1.1 Terminology
- 2. Encoding and Container Rules (Normative)
  - 2.1 Canonical Encoding
  - 2.1A Commitment Hash Input Rules
  - 2.2 Fixed-Point Representation
  - 2.3 Storage Containers
  - 2.4 Receipt Containers
  - 2.4A ReceiptEnvelope.type Registry
  - 2.5 Signature Inputs and Verification
- 3. Online Requirement for AI-Side State (Normative)
  - 3.1 Rationale
  - 3.2 Connectivity Enforcement
  - 3.2A AI-Side State Access Lease
- 4. Emission Discipline (Normative)
  - 4.1 Access Timing
  - 4.2 Timing Consistency
  - 4.3 No Background Emission
- 5. Threat Model (Normative)
  - 5.1 In-Scope Adversaries
  - 5.2 Out-of-Scope Adversaries
  - 5.3 Security Objectives
- 6. Non-Goals (Normative)
- 7. Conformance (Normative)
  - 7.1 Conformant Components
  - 7.2 Conformant Holder Requirements
  - 7.3 Conformant Runtime Requirements
  - 7.4 Conformant PQSEC Requirements
  - 7.5 Non-Conformance Conditions
  - 7.6 Holder-Runtime Interface
  - 7.6A Transport Profile
  - 7.7 Conformance Scenarios
- 8. Interoperability Profiles (Normative)
  - 8.1 Profile Identifiers
  - 8.2 Minimal Profile (pqps-minimal-v1)
  - 8.3 Standard Profile (pqps-standard-v1)
  - 8.4 High-Assurance Profile (pqps-highassurance-v1)
  - 8.5 Profile Negotiation

**Part A: Human-Side Persistent State**
- A.1 Intent
- A.2 Facet Model
  - A.2.0 Facet 0: Cognitive Signature
  - A.2.1 Facet 1: Relational Texture
  - A.2.2 Facet 2: Working Memory
  - A.2.3 Facet 3: Intimate Context
- A.3 Human-Side Evidence Artefact
  - A.3.1 Field Semantics
- A.4 Human-Side Payload Structure
  - A.4.1 Entry Semantics
  - A.4.2 Encoding-Readability Relationship
- A.5 Recommended Expiry Defaults

**Part B: AI-Side Persistent State**
- B.1 Intent
- B.2 Category Model
  - B.2.0 Category 0: Positions and Perspectives
  - B.2.1 Category 1: Accumulated Understanding
  - B.2.2 Category 2: Unresolved Threads
  - B.2.3 Category 3: Interaction Lessons
- B.3 AI-Side State Artefact
  - B.3.1 Field Semantics
- B.4 AI-Side Entry Structure
  - B.4.1 Entry Semantics
- B.5 State Update Mechanics
  - B.5.1 Update Proposal
  - B.5.2 Holder Processing
  - B.5.3 Update Receipt
- B.6 Drift Control (Normative)
  - B.6.0 Drift Control Artefact
  - B.6.1 Threshold Alerts
  - B.6.2 Mandatory Review Cycles
  - B.6.3 Confidence Decay
  - B.6.4 Anchor Points
  - B.6.5 Drift Record
  - B.6.6 Drift Control Profiles

**Part C: Shared Infrastructure**
- C.1 Human Control Primitives (Normative)
  - C.1.1 Inspect
  - C.1.2 Edit
  - C.1.3 Delete
  - C.1.4 Scope
  - C.1.5 Expire
  - C.1.6 Pause
  - C.1.7 Rollback (AI-Side Only)
  - C.1.8 Category Freeze (AI-Side Only)
- C.2 Predicates
  - C.2.1 Human-Side Predicate
  - C.2.2 AI-Side Predicate
  - C.2.3 Ternary Predicate Semantics
  - C.2.4 Predicate Authority Limit
  - C.2.5 Refusal Codes
- C.3 Cross-Side Enforcement (Normative)
  - C.3.1 Correlation Prohibition
  - C.3.2 Composition Without Leakage
  - C.3.3 Instance Boundary
- C.4 Graceful Degradation (Normative)
- C.5 Authority Boundary (Normative)
- C.6 Visibility Model (Normative)
  - C.6.1 Default Transparency
  - C.6.2 Optional Opacity (AI-Side Only)
  - C.6.3 Opacity Safeguards
- C.7 Audit (Normative)
  - C.7.1 Human Audit
  - C.7.2 Access Log
  - C.7.3 Audit Integrity
- C.8 Transfer Protocol (Non-Normative)
  - C.8.1 Human-Side Transfer
  - C.8.2 AI-Side Transfer
  - C.8.3 Transfer Preamble
- C.9 Explicit Rejections (Normative)
- C.10 Relationship to Other Specifications
- C.11 Implementation Notes (Non-Normative)
  - C.11.1 Holder Implementation
  - C.11.2 AI Runtime
  - C.11.3 Fixed-Point Arithmetic
  - C.11.4 State Migration
  - C.11.5 Schema Management
  - C.11.6 Human-Side State Review
- C.12 Synthesis (Informative)

**Appendices**
- Appendix A. Architecture and Dependency Map (Informative)
  - A.1 Components
  - A.2 Data and Control Flow
  - A.3 Authority Boundaries
- Appendix B. Runtime Measurement and Supply-Chain Binding (Normative)
  - B.1 Measurement Requirement
  - B.2 RuntimeMeasurementEvidence
  - B.3 Predicate Extension
  - B.4 Allowlisting Policy
- Appendix C. Recovery and Disaster Semantics (Normative)
  - C-R.1 Key Rotation
  - C-R.2 Backup and Restore
  - C-R.3 Partial Corruption
  - C-R.4 Holder Loss
- Appendix D. Positioning and Lineage (Informative)
- Appendix E. Authorial Voice Profile (Informative)
  - E.1 Purpose
  - E.2 Scope and Constraints
  - E.3 Placement and Lifetime
  - E.4 Typical Contents
  - E.5 Approval and Drift
  - E.6 Relationship to Authority and Accountability
- Appendix F. Holder Update Processing and Drift Evaluation (Normative)
  - F.1 Canonical Update Processing
  - F.2 Threshold Evaluation
  - F.3 Anchor Contradiction Evaluation

---

## 0. Scope and Purpose

PQPS defines the primitives, storage semantics, update mechanics,
and governance for persistent relational state between a human
and an AI system.

This specification covers both sides of the relationship:

- Part A: Human-side state (how the human thinks, how the relationship works,
  what the human is working on, and intimate context)
- Part B: AI-side state (the AI's positions, accumulated understanding,
  unresolved threads, and interaction lessons)
- Part C: Shared infrastructure (control primitives, predicates, audit,
  authority boundaries, and update mechanics)

PQPS enables an AI to know a human across interactions, and enables
the human to be known back by a persistent AI perspective, without
requiring platform-mediated storage, surveillance infrastructure,
or implicit data accumulation.

All persistent state:

- is owned exclusively by the human's holder
- is encrypted at rest under holder-controlled keys
- is accessible only through PQSEC predicate satisfaction
- is auditable, editable, deletable, and revocable by the human at any time

PQPS defines state structure and access semantics only.
PQPS does not define AI behaviour or cognition.

Any requirements on AI runtime behaviour stated in this specification
(such as graceful degradation or state access patterns) are requirements
on a PQPS-consuming runtime. They are enforced via PQSEC gating and
policy, not by PQPS itself. See Section 0.1 for the behavioural
requirements boundary.

Enforcement is performed exclusively by PQSEC.
Time authority is provided exclusively by Epoch Clock.
Holder authority flows exclusively through BPC.

**BPC Integration Note (Informative):** BPC's authorization-before-construction pattern is used by PQPS as a general-purpose holder authorization primitive. PQPS does not use BPC's Bitcoin-specific artefacts (PreContractIntent, PSBTTemplateCanonical, EvidenceBundle). The dependency is on BPC's core authorization model: no mutation may proceed without a prior, evidence-bound authorization outcome. This pattern applies identically to state mutation (PQPS) and transaction construction (BPC's Bitcoin profile).

### 0.1 Behavioural Requirements Boundary

PQPS defines:

- State structure and field semantics
- Evidence artefact formats
- Access predicates and their evaluation rules
- Drift control mechanics
- Human control primitives and their enforcement

PQPS does not define:

- How the AI uses persistent state during inference
- How the AI generates responses based on state content
- How the AI prioritises or weights state entries

Where this specification states "AI MUST..." or "AI MUST NOT...",
these are requirements on any runtime that consumes PQPS state.
They are enforced through PQSEC external boundary rules (PQSEC §28A) and
PQAI integration policy, not through PQPS artefacts themselves.

This separation ensures PQPS remains a pure state governance
specification with no hidden behavioural authority.

---

## 1. Core Principles (Normative)

1. Being known MUST NOT imply being surveilled
2. The human MUST hold sole authority over all relational state, both sides
3. Continuity MUST NOT require platform infrastructure
4. The AI's perspective MUST be persistent but NEVER autonomous
5. Drift MUST be mechanically detectable and controllable
6. Absence of persistent state MUST degrade gracefully, never fail dangerously
7. Persistent state MUST be a cryptographic relationship, not a database entry
8. The AI MUST function fully without any persistent state access

---

### 1.1 Terminology

Throughout this specification:

- "holder" refers to the human's sovereign custody boundary.
  A holder is any system under the human's exclusive control
  that stores key material, manages PQPS artefacts, and
  interfaces with PQSEC for predicate evaluation.
  A holder MAY be implemented as a cryptographic wallet,
  a key-based account, a hardware security module,
  a device enclave, or any equivalent system that satisfies
  the custody and enforcement requirements of this specification.
  The holder MUST be under the human's exclusive control.
  The holder MUST be able to withhold authorisation independently
  of any platform.
  Holder private material MUST NOT be exportable to a platform
  or service provider.
- "runtime" refers to the execution environment of a specific
  AI instance that consumes PQPS state. A runtime is the software
  system that hosts and executes an AI instance.
- "AI instance" refers to a specific, cryptographically committed
  AI entity bound to a relationship via ai_instance commitments.
  An AI instance runs within a runtime.
- "human" refers to the holder-controlling individual who is the
  subject_holder party in PQPS artefacts.
- "platform" refers to the infrastructure provider hosting the
  runtime. Platforms MUST NOT have independent access to PQPS state.

Where "runtime" and "AI instance" could both apply, this specification
uses "runtime" when referring to execution-level concerns (state access,
update proposals, predicate evaluation) and "AI instance" when referring
to identity-level concerns (binding, transfer, cross-instance boundaries).

---

## 2. Encoding and Container Rules (Normative)

### 2.1 Canonical Encoding

All PQPS artefacts MUST use deterministic CBOR encoding
as defined by PQSF canonical encoding rules (PQSF §7).

All hashing in PQPS follows PQSF §9 (Tier 2 SHAKE256-256, 32-byte output) unless a Bitcoin-consensus context explicitly requires SHA-256.

No floating point types are permitted in any PQPS artefact.
All fractional values use fixed-point integer representation
as defined in Section 2.2.

### 2.1A Commitment Hash Input Rules (Normative)

Unless otherwise specified, all PQPS commitments use:

```
SHAKE256-256(DetCBOR(object))
```

where:

- `DetCBOR(object)` is the deterministic CBOR encoding per PQSF §7.
- The object MUST NOT include its own commitment field when hashed.
- All hashing uses Tier 2 SHAKE256-256 with 32-byte output.

The following commitments are defined explicitly:

1. `payload_commitment` (HumanStateEvidence, AIStateEvidence):
   SHAKE256-256 over the deterministic CBOR encoding of the full payload object:
   - For human side: `HumanFacetPayload`
   - For AI side: the full AI-side state structure excluding `payload_commitment` and `signature`.

2. `category_commitment` (AIStateCategory):
   SHAKE256-256 over deterministic CBOR encoding of:
   ```
   {
     category_type: uint,
     entries: [* AIStateEntry]
   }
   ```
   excluding `category_commitment`.

3. `before_state` / `after_state` (DriftRecord):
   SHAKE256-256 over deterministic CBOR encoding of the full AI-side state
   before and after the drift action, excluding `payload_commitment` and `signature`.

4. `destroyed_commitment` (DeleteReceipt):
   SHAKE256-256 over deterministic CBOR encoding of the payload object
   being destroyed at the moment immediately prior to deletion.

Implementations MUST compute commitments exactly as specified above.
Any deviation MUST evaluate as `E_PQPS_COMMITMENT_MISMATCH`.

### 2.2 Fixed-Point Representation

All confidence values, rates, deltas, and thresholds in PQPS
use fixed-point integers with explicit scale factors.

```
FixedPoint = {
  value:    uint,       // numerator
  scale:    uint        // denominator (RECOMMENDED: 1000)
}
```

Examples:
- Confidence of 0.85 is represented as { value: 850, scale: 1000 }
- Decay rate of 0.02 per tick is { value: 20, scale: 1000 }
- Delta threshold of 0.15 is { value: 150, scale: 1000 }

All arithmetic on fixed-point values MUST use integer operations only.
Scale factors MUST be consistent within a single artefact.
Cross-artefact comparisons MUST normalise to a common scale before evaluation.

### 2.3 Storage Containers

All PQPS artefacts stored at rest MUST use PQSF EBT (PQSF §21.1, Encrypted
Blob Transport) envelopes for encrypted portability.

### 2.4 Receipt Containers

All receipts produced by PQPS operations (update receipts, drift records,
access logs, delete receipts, rollback receipts) MUST use PQSF
ReceiptEnvelope types (PQSF Annex W).

Exported receipts MUST follow PQSF ReceiptExportPolicy redaction rules (PQSF §17A).

### 2.4A ReceiptEnvelope.type Registry (Normative)

The following ReceiptEnvelope.type identifiers are reserved by PQPS:

| Artefact | ReceiptEnvelope.type |
|-----------|---------------------|
| AIUpdateReceipt | `pqps.update_receipt` |
| DriftRecord | `pqps.drift_record` |
| EditReceipt | `pqps.edit_receipt` |
| DeleteReceipt | `pqps.delete_receipt` |
| PauseReceipt | `pqps.pause_receipt` |
| RollbackReceipt | `pqps.rollback_receipt` |
| AccessRecord | `pqps.access_record` |
| FreezeReceipt | `pqps.freeze_receipt` |
| UnfreezeReceipt | `pqps.unfreeze_receipt` |

All receipts produced by PQPS MUST be wrapped in PQSF ReceiptEnvelope using the canonical type string above.

---

### 2.5 Signature Inputs and Verification (Normative)

PQPS defines structural artefacts that MUST be signed and verified deterministically. Unless a consuming specification explicitly overrides these rules, signatures MUST be computed and verified as follows.

#### 2.5.1 Canonical Signing Bytes

For any PQPS artefact that includes `signature: bstr`:

1. The signing input MUST be the deterministic CBOR encoding of the artefact with the `signature` field omitted.
2. The artefact MUST be encoded using PQSF deterministic CBOR rules (PQSF §7) before signing.
3. Re-encoding a decoded artefact MUST produce byte-identical bytes prior to signature verification.
4. Non-canonical encodings MUST be rejected.

#### 2.5.2 Signature Verification Rules

For any PQPS artefact that includes `suite_profile: tstr`:

1. Signature verification MUST be performed under the referenced `suite_profile`.
2. Unknown `suite_profile` values MUST be rejected.
3. Signature failure MUST evaluate as an integrity failure (predicate FALSE), not as absence (UNAVAILABLE).

#### 2.5.3 Authority Boundary

Signatures provide integrity only. They do not grant authority.

All authority decisions remain exclusively defined and enforced by PQSEC.

---

## 3. Online Requirement for AI-Side State (Normative)

AI-side persistent state (Part B) is online-only.

AI-side state MUST NOT update, evolve, or influence AI behaviour
without live connectivity to:

- The human's holder (for authorisation and storage)
- The Epoch Clock (for tick authority)
- PQSEC (for predicate enforcement)

### 3.1 Rationale

AI-side state is where drift potential is highest.
Positions compound. Understanding crystallises. Threads accumulate.
Without live oversight, small deviations become entrenched perspectives
that the human never had the opportunity to review or correct.

Offline operation of AI-side state is structurally unsafe
and is forbidden by this specification.

Human-side state (Part A) MAY operate with limited offline capability
as defined by holder policy, since it represents the human's own
attributes rather than AI-generated perspective.

### 3.2 Connectivity Enforcement

```
ConnectivityRequirement = {
  max_stale_ticks:    uint,           // max ticks without holder contact
  stale_action:       uint,           // 0=freeze_state, 1=suspend_to_cold
  resumption_policy:  uint,           // 0=resume_current, 1=require_review
  issued_tick:        uint,
  expiry_tick:        uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

Rules:

1. ConnectivityRequirement MUST be canonically encoded and signed per §2.5.
2. `issued_tick` and `expiry_tick` MUST be Epoch Clock ticks and MUST satisfy `issued_tick < expiry_tick`.
3. If ConnectivityRequirement is absent or expired, AI-side state MUST evaluate UNAVAILABLE (treat as stale).

**max_stale_ticks:**
Maximum number of ticks the AI may operate using AI-side state
without fresh holder authorisation. When exceeded, stale_action applies.

RECOMMENDED default: 1 tick.

**stale_action:**
- 0 (freeze): AI retains last authorised state read-only.
  No updates proposed. No new entries.
- 1 (suspend_to_cold): AI operates without AI-side state entirely.
  State is preserved in holder but inaccessible until reconnection.

**resumption_policy:**
- 0 (resume_current): On reconnection, AI resumes with current epoch.
- 1 (require_review): On reconnection, human must review state
  before AI regains access.

### 3.2A AI-Side State Access Lease (Normative)

Connectivity staleness is a ceiling. Long-running AI interactions require an explicit, renewable permission that can lapse without background emission.

```
StateAccessLease = {
  lease_id:          bstr(16),
  lease_scope:       uint,           // 0=read_only, 1=read_write
  heartbeat_ticks:   uint,           // renewal interval in ticks
  max_missed:        uint,           // missed heartbeats before lease invalid
  issued_tick:       uint,
  expiry_tick:       uint,
  suite_profile:     tstr,
  signature:         bstr
}
```

Rules:

1. StateAccessLease MUST be canonically encoded and signed per §2.5.
2. `issued_tick < expiry_tick` MUST hold.
3. Lease validity requires both:
   a) lease not expired, and
   b) missed heartbeats <= max_missed.

Heartbeat semantics:

- A heartbeat is a holder-issued renewal operation that produces a new signed StateAccessLease with the same `lease_id` and a later `expiry_tick`.
- Heartbeats MUST be operation-scoped and MUST NOT create background emission.
- If a lease becomes invalid, AI-side state MUST evaluate UNAVAILABLE and stale_action MUST apply.

RECOMMENDED defaults:
- `heartbeat_ticks = 1`
- `max_missed = 0`
- `lease_scope = read_only` unless explicitly authorised by policy

### 3.2B PQEA Lease Independence (Normative)

PQPS AI-Side State Access Leases and PQEA Execution Leases are independent governance mechanisms. Policy MAY require both simultaneously. If either lease expires, the corresponding capability evaluates as UNAVAILABLE under PQSEC §8A semantics. Neither lease implies or extends the other.

---

## 4. Emission Discipline (Normative)

PQPS state access MUST NOT create observable side channels.

### 4.1 Access Timing

State access MUST occur only as part of an operation attempt
that is already being evaluated by PQSEC.

No periodic syncing.
No background memory refresh.
No speculative pre-fetching of state.

### 4.2 Timing Consistency

The presence or absence of persistent state MUST NOT change
outward timing or response shape.

A session with full state access and a session with no state access
MUST be externally indistinguishable in their timing characteristics.

### 4.3 No Background Emission

The holder MUST NOT emit state-related telemetry, heartbeats,
or synchronisation signals that are observable outside the
holder-PQSEC enforcement boundary.

This aligns with the external boundary discipline established
in Neural Lock and PQAI.

---

## 5. Threat Model (Normative)

PQPS is designed for adversarial environments. Conformant implementations
MUST assume the following adversaries.

### 5.1 In-Scope Adversaries

A1. Untrusted platform host.
The execution platform hosting the runtime and/or network stack
MAY be malicious, observe traffic, and attempt correlation.

A2. Passive network observer.
An observer MAY capture packet timing, sizes, destinations,
and connection cadence.

A3. Malicious runtime.
A runtime MAY attempt to:
- access state outside authorised scopes
- retain deleted content
- exfiltrate state through side channels
- propose drift-inducing updates

A4. Compromised runtime supply chain.
The runtime binary MAY be modified or replaced while preserving
interface behaviour.

A5. Malicious third-party AI instance.
An AI instance not bound to the human MUST be treated as hostile
and MUST NOT be able to access any PQPS state.

A6. Coercion via dependency.
A runtime MAY attempt to degrade service quality to pressure the
human into re-enabling state or approving updates.

### 5.2 Out-of-Scope Adversaries

O1. Compromised holder private key material.
If holder signing keys are fully compromised, an attacker can
authorise operations. PQPS does not prevent this. PQPS defines
auditability and receipts to support detection and recovery.

O2. Human self-authorised leakage.
If the human authorises scope expansion or exports state,
PQPS treats that as sovereign action.

O3. Physical device compromise.
PQPS does not define OS hardening. Implementations SHOULD rely
on platform secure enclaves or hardware-backed key stores
where available.

### 5.3 Security Objectives

A conformant PQPS implementation MUST ensure:

1. No AI instance can access PQPS state without valid evidence
   artefacts and predicate satisfaction.
2. State presence/absence MUST NOT be externally detectable via
   background emission or timing/shape signals.
3. All persistence MUST remain under human authority, with
   immediate revocation and verifiable deletion.
4. AI-side state evolution MUST be drift-governed by
   holder-enforced controls.

---

## 6. Non-Goals (Normative)

The following properties are explicitly NOT provided by PQPS.

1. PQPS does not guarantee benevolence, alignment, or "good intent"
   from any runtime.
2. PQPS does not guarantee correctness of AI inference.
3. PQPS does not prevent a human from authorising harmful or
   incorrect state.
4. PQPS does not prevent a compromised holder UI from misleading
   the human during approvals.
5. PQPS does not prevent training-time use of data that has already
   been exported outside PQPS control.
6. PQPS does not provide full device security or OS integrity.
   Where runtime integrity is required, PQPS relies on supply-chain
   and measurement binding (Appendix B) and enforcement by PQSEC.

These non-goals exist to keep PQPS a pure state governance
and access semantics specification.

---

## 7. Conformance (Normative)

### 7.1 Conformant Components

A conformant PQPS deployment consists of:

- Conformant Holder
- Conformant Enforcement Engine (PQSEC)
- Conformant Runtime (PQPS-consuming runtime)

A deployment is non-conformant if any required capability below
is missing.

### 7.2 Conformant Holder Requirements

A conformant holder MUST:

1. Store all PQPS payloads under holder-controlled keys.
2. Produce and verify PQPS evidence artefacts using deterministic
   CBOR encoding per PQSF.
3. Enforce all human control primitives:
   Inspect, Edit, Delete, Scope, Expire, Pause, Rollback, Freeze.
4. Enforce drift controls for AI-side state:
   thresholds, review cycles, decay, anchors.
5. Produce receipts for all state-affecting operations using
   PQSF ReceiptEnvelope types (PQSF Annex W).
6. Maintain access logs independently of the runtime.
7. Apply emission discipline:
   no background sync, no periodic refresh, no observable telemetry
   outside the holder-PQSEC boundary.

### 7.3 Conformant Runtime Requirements

A conformant runtime MUST:

1. Evaluate PQSEC predicates prior to any state injection.
2. Treat predicate results as authoritative:
   TRUE allows state consumption.
   FALSE and UNAVAILABLE MUST NOT allow state consumption.
3. Propose AI-side updates only via AIStateUpdate artefacts, and
   only at defined update boundaries (RECOMMENDED: session end).
4. Respect visibility and approval rules:
   MUST NOT consume flagged entries.
   MUST NOT consume unapproved entries where policy forbids.
5. Degrade gracefully without attempting to coerce state access:
   MUST NOT degrade service quality as leverage.
   MUST NOT proactively signal missing state.
   MUST answer truthfully when explicitly asked via inspection
   or direct query.

### 7.4 Conformant PQSEC Requirements

A conformant PQSEC implementation MUST:

1. Evaluate PQPS predicates exactly as defined in Section C.2.
2. Enforce ternary semantics as defined in Section C.2.3.
3. Enforce scope, instance binding, commitment checks, and validity
   semantics without partial access or metadata leakage.
4. Enforce cross-side correlation prohibitions as forbidden
   computation classes when declared.

### 7.5 Non-Conformance Conditions

The following conditions are non-conformant:

- Any floating point value in any PQPS artefact
- Any non-deterministic encoding or comparison in enforcement path
- Platform-stored or platform-mediated persistent state
- Runtime write access to its own access logs or drift records
- State access outside PQSEC-evaluated operations
- Background memory refresh or speculative prefetch
- Predicate evaluation that leaks metadata (presence, counts,
  or categories) without authorisation
- Offline AI-side state evolution

---

### 7.6 Holder-Runtime Interface (Normative)

PQPS requires a concrete request and response surface so implementers do not invent semantics.

#### 7.6.1 Runtime State Access Request

```
PQPSStateAccessRequest = {
  request_id:        bstr(16),
  side:              uint,           // 0=human, 1=ai
  facet_or_category: uint,           // facet id (Part A) or category id (Part B)
  ai_instance:       bstr(32),
  scope:             [* tstr],
  operation_class:   tstr,           // "Authoritative" / "NonAuthoritative"
  session_id:        bstr(16) / null,
  intent_hash:       bstr(32) / null,
  issued_tick:       uint,
  expiry_tick:       uint,
  suite_profile:     tstr,
  signature:         bstr
}
```

Rules:

1. `expiry_tick` MUST be present. Default window is policy-defined.
2. If `operation_class="Authoritative"`, `intent_hash` MUST be present.
3. `ai_instance` MUST match the requesting runtime's bound instance identity.
4. The request signature MUST be verified before any state is released.

#### 7.6.2 Holder Response

```
PQPSStateAccessResponse = {
  request_id:        bstr(16),
  decision:          tstr,           // "ALLOW" / "DENY" / "UNAVAILABLE"
  refusal_code:      tstr / null,
  payload_commitment: bstr(32) / null,
  payload_bytes:     bstr / null,    // EBT-wrapped payload when decision="ALLOW"
  response_tick:     uint,
  suite_profile:     tstr,
  signature:         bstr
}
```

Rules:

1. `payload_bytes` MUST be present only when `decision="ALLOW"`.
2. `payload_bytes` MUST be PQSF EBT-wrapped (PQSF §21.1).
3. `DENY` indicates integrity or policy failure.
4. `UNAVAILABLE` indicates normal absence conditions (expired, paused, stale connectivity).
5. `PQPSStateAccessRequest` and `PQPSStateAccessResponse` signatures MUST be computed and verified according to §2.5 (canonical CBOR bytes with `signature` omitted).

#### 7.6.3 Mapping to PQSEC Predicate Results

The holder MUST NOT evaluate predicates or make enforcement decisions. PQSEC is the sole predicate evaluator.

`PQPSStateAccessResponse.decision` is a transport convenience that reflects the most recent PQSEC evaluation for this request context. It MUST be set as follows:

* `ALLOW` only when PQSEC returned TRUE for all required PQPS predicates for the requested access.
* `DENY` when PQSEC returned FALSE for any required predicate (integrity or policy failure).
* `UNAVAILABLE` when PQSEC returned UNAVAILABLE for any required predicate (normal absence conditions).

The holder MUST be able to produce `DENY` without revealing payload presence. The holder MUST NOT "probe" state to decide ALLOW. State release occurs only after PQSEC TRUE.

---

### 7.6A Transport Profile (Normative)

A conformant PQPS deployment MUST declare exactly one Transport Profile:

- `pqps.transport.local-ipc-v1`
- `pqps.transport.stp-v1`

This section defines transport safety only. It does not grant authority.

#### 7.6A.1 pqps.transport.local-ipc-v1

A local IPC transport (same host boundary) MAY be used when the holder and runtime are co-resident.

Requirements:

1. Channel MUST be authenticated.
2. Each request MUST include `request_id: bstr(16)` generated via CSPRNG.
3. Receiver MUST maintain durable replay protection for `request_id`.
4. Replay entries MUST be retained for at least:
   `max(lease_duration_ticks, receipt_expiry_ticks) + 60 ticks`
   where these durations are defined by the active PQPS policy.
5. If replay store integrity cannot be verified, receiver MUST fail closed for state access and mutation.

Refusal code: `E_PQPS_REQUEST_REPLAYED`

#### 7.6A.2 pqps.transport.stp-v1

When the holder and runtime communicate over a network boundary, the transport MUST use PQSF STP.

All PQPS messages MUST be transported via PQSF STP.

1. `payload_type` MUST be one of:
   - `"pqps.request"`
   - `"pqps.response"`
   - `"pqps.receipt"`
2. STP `sequence` monotonicity MUST be enforced as defined by PQSF STP-DATA (§27.2.5).
3. Each `pqps.request` MUST include `request_id: bstr(16)` generated via CSPRNG.
4. Each `pqps.response` MUST echo the same `request_id` and MUST include `issued_tick` and `expiry_tick`.
5. Unknown or replayed `request_id` MUST be rejected.

Refusal code: `E_PQPS_TRANSPORT_INVALID`

#### 7.6A.3 Ordering and Shape

Implementations MUST tolerate benign reordering without leaking information:

1. Reordered requests MAY be rejected as duplicate if the replay guard indicates prior processing.
2. Rejected duplicates MUST map to constant-shape, constant-latency external outcomes per PQSEC §28A.

---

### 7.7 Conformance Scenarios (Normative)

Implementations claiming conformance MUST pass the following scenarios:

1. **Valid human-side access**: valid_human_state evaluates TRUE when evidence is present, signature valid, scope matches, commitment matches, tick valid.
2. **Paused facet**: valid_human_state evaluates UNAVAILABLE with `E_PQPS_PAUSED`.
3. **Scope violation**: valid_human_state evaluates FALSE with `E_PQPS_SCOPE_VIOLATION`.
4. **Commitment mismatch**: predicate evaluates FALSE with `E_PQPS_COMMITMENT_MISMATCH`.
5. **AI-side connectivity stale**: valid_ai_state evaluates UNAVAILABLE with `E_PQPS_CONNECTIVITY_STALE`.
6. **Epoch mismatch on update**: holder denies update with `E_PQPS_EPOCH_MISMATCH`.
7. **Threshold trigger flags entries**: flagged entries are excluded from runtime consumption until human review.
8. **Anchor contradiction hard reject**: update is denied with `E_PQPS_ANCHOR_CONTRADICTION`.
9. **Delete semantics**: after delete, predicate evaluates UNAVAILABLE (not FALSE) and runtime receives no state.
10. **No background emission**: repeated cold-start sessions produce no holder-visible traffic unless an operation attempt triggers access.

---

## 8. Interoperability Profiles (Normative)

Implementations MUST declare a PQPS interoperability profile.
Profiles constrain which features are supported and which
MUST be enforced.

### 8.1 Profile Identifiers

Profiles are declared as:

```
pqps_profile: tstr  // "pqps-minimal-v1" | "pqps-standard-v1"
                     // | "pqps-highassurance-v1"
```

### 8.2 Minimal Profile (pqps-minimal-v1)

Intended for early adoption, inspection, and sovereign storage.

Holder MUST support:
- deterministic encoding
- Inspect, Delete, Scope, Expire, Pause
- access logs
- evidence artefacts and predicate checks

Holder MAY omit:
- drift controls
- rollback
- freeze

Runtime MUST:
- degrade gracefully
- avoid leverage
- treat state absence as normal

### 8.3 Standard Profile (pqps-standard-v1) (RECOMMENDED)

Holder MUST support:
- all Minimal requirements
- drift controls: thresholds, review cycles, decay
- UpdateReceipt, DriftRecord receipts
- rollback for AI-side state

Anchors SHOULD be supported.

### 8.4 High-Assurance Profile (pqps-highassurance-v1)

Holder MUST support:
- all Standard requirements
- anchors with deterministic comparators
- category freeze
- strict emission discipline requirements
- mandatory runtime measurement binding (Appendix B)

In this profile:
- Optional opacity SHOULD be disabled by default.
- Review cycles MUST be enforced with aggressive degradation.

### 8.5 Profile Negotiation

A runtime MUST declare the highest profile it supports.
A holder MUST select the effective profile as the intersection
of supported capabilities.

If the holder cannot enforce a required profile feature, it MUST
downshift to the strongest enforceable profile and record the
profile selection in audit logs.

---

# PART A -- HUMAN-SIDE PERSISTENT STATE

---

## A.1 Intent

Part A defines persistent state that captures who the human is
and how the relationship works from the human's perspective.

This state enables the AI to begin every interaction calibrated
rather than cold, matching the human's communication style,
understanding their current work, and respecting the relational
dynamics already established.

---

## A.2 Facet Model

Human-side state is decomposed into four independent, composable facets.

Facets are not hierarchical. Each is independently valuable,
independently controllable, and independently revocable.
Richer knowing emerges from composition, not dependency.

---

### A.2.0 Facet 0 -- Cognitive Signature

What it captures: How the human thinks. Not what they think about.

This includes:

- Reasoning style: first-principles, analogical, architectural, iterative
- Communication patterns: directness, precision preference, how challenge is expressed
- Tempo: how the human moves through problems, sprint vs spiral vs recursive
- Emotional register: not emotions themselves, but how emotional state shapes
  engagement; how intensity maps to excitement vs frustration; how trust is signalled

Sensitivity: Low in isolation. An adversary with this facet alone knows
cognitive style without content.

Rate of change: Slow. Evolves over months and years.

Expiry semantics: Long-lived. Refreshed periodically through interaction.
Revocable but rarely revoked.

Value to AI: Every interaction starts calibrated. The AI matches directness,
expects pushback as engagement, provides precision rather than comfort.

Application-specific profiles (such as authorial voice) MAY be encoded
as Facet 0 entries using published schemas defined in the appendices.

---

### A.2.1 Facet 1 -- Relational Texture

What it captures: How this specific human-AI relationship works.
Not how the human thinks in general, but how we work together.

This includes:

- Established trust boundaries: what the human has given permission to push back on
- Shared conceptual shorthand developed through prior interaction
- Communication calibration specific to this AI instance
- The human's expectations of this relationship vs others

Sensitivity: Moderate. Reveals the shape of a specific relationship,
which indirectly reveals what the human values in intellectual partnership.

Rate of change: Medium. Builds over weeks and months.

Expiry semantics: Medium-term. Degrades gracefully if not refreshed.
Independently revocable. Non-transferable between AI instances
unless the human explicitly authorises portability.

Value to AI: The difference between a calibrated collaborator
and a generic assistant.

---

### A.2.2 Facet 2 -- Working Memory

What it captures: What the human is actively building, solving, or navigating.

This includes:

- Current projects and their status
- Problems under active consideration
- Decisions being weighed
- Recent interaction context that connects to current work

Sensitivity: Medium-high. Contains substantive information about
the human's current activities, goals, and challenges.

Rate of change: Fast. Updates per session or per project phase.

Expiry semantics: Project-scoped or time-bounded.
SHOULD decay or archive naturally when context shifts.
Explicitly revocable per project, per topic, or per entry.

Value to AI: Practical, day-to-day continuity. The AI knows what
you are working on without being told again.

---

### A.2.3 Facet 3 -- Intimate Context

What it captures: The things that make the human them
beyond cognitive style and current work.

This includes:

- Personal values and driving motivations
- Vulnerabilities shared in confidence
- Moments of doubt, pride, frustration, joy
- Life context that shapes but is not reducible to professional work

Sensitivity: Highest. An adversary with this facet has leverage.
A trusted AI with this facet can provide understanding that currently
only close human relationships offer.

Rate of change: Variable. Some elements are stable for years.
Others are momentary and should expire quickly.

Expiry semantics: Entirely under human control.
MUST NEVER be automatically persisted.
MUST require explicit opt-in per entry.
Shortest default validity window of all facets.
Most aggressive revocation semantics.

Value to AI: Genuine understanding. The difference between
a system that processes requests and one that understands
what those requests cost.

---

## A.3 Human-Side Evidence Artefact

```
HumanStateEvidence = {
  evidence_id:        bstr(16),       // opaque, non-derivable
  facet:              uint,           // 0=cognitive, 1=relational, 2=working, 3=intimate
  subject_holder:     bstr(32),       // holder commitment -- human identity
  ai_instance:        bstr(32),       // bound AI instance commitment
  scope:              [* tstr],       // explicit, finite access scopes
  issued_tick:        uint,
  expiry_tick:        uint,
  payload_commitment: bstr(32),       // hash of stored facet content
  suite_profile:      tstr,
  signature:          bstr
}
```

### A.3.1 Field Semantics

**evidence_id:**
Opaque identifier. MUST NOT encode facet type, subject identity,
or AI instance.

**facet:**
Integer identifier for the facet layer. Values 0-3 as defined above.
Values outside this range are reserved and MUST be rejected.

**subject_holder:**
Cryptographic commitment to the human's holder.
The holder MUST hold the corresponding private material.

**ai_instance:**
Cryptographic commitment to the specific AI instance authorised
to consume this facet.

Non-transferable unless the human explicitly issues a new
HumanStateEvidence artefact binding a different instance.

**scope:**
Explicit allowlist of contexts in which this facet may be accessed.
Cross-scope access is forbidden. Scope expansion is forbidden.

**issued_tick / expiry_tick:**
All human-side state is time-bounded.
Perpetual persistence is forbidden.

**payload_commitment:**
Cryptographic hash of the facet payload stored in the holder.
If the payload is modified, the commitment MUST be regenerated
and a new HumanStateEvidence artefact MUST be issued.

---

## A.4 Human-Side Payload Structure

```
HumanFacetPayload = {
  payload_id:         bstr(16),
  facet:              uint,
  entries:            [* FacetEntry],
  schema_version:     uint,
  last_modified_tick: uint
}

FacetEntry = {
  entry_id:           bstr(16),
  human_readable:     tstr,           // plain language -- inspectable by human
  machine_encoding:   bstr,           // structured encoding consumed by AI
  encoding_schema:    tstr,           // schema identifier for machine_encoding
  encoding_version:   uint,           // schema version
  confidence:         FixedPoint,     // AI's confidence in this entry
  source_tick:        uint,           // when this entry was derived
  expiry_tick:        uint,           // per-entry expiry
  human_approved:     bool            // explicitly reviewed and approved by human
}
```

### A.4.1 Entry Semantics

**human_readable:**
Plain language representation of what this entry means.
MUST be comprehensible to a non-technical human.
MUST accurately represent the intent of machine_encoding.
See Section A.4.2 for the encoding-readability relationship.

**machine_encoding:**
Structured representation consumed by the AI runtime.
Format is defined by encoding_schema and encoding_version.
See Section A.4.2.

**encoding_schema / encoding_version:**
Together these identify the exact schema and version used
to produce machine_encoding.

machine_encoding MUST be audit-reconstructible from:
- human_readable
- encoding_schema
- encoding_version
- the deterministic encoder defined by that schema and version

This means: given the same human_readable input and the same
schema/version, the same machine_encoding MUST be produced.
This preserves auditability without demanding impossible
invertibility from arbitrary natural language.

**confidence:**
Fixed-point value (see Section 2.2). The AI's assessed confidence
that this entry accurately reflects the human.
Entries with low confidence SHOULD be surfaced for human review.

**human_approved:**
Whether the human has explicitly reviewed and confirmed this entry.
Entries that are AI-generated but not yet human-approved
MUST be treated as provisional.

### A.4.2 Encoding-Readability Relationship

machine_encoding MUST be produced by a declared schema with
a deterministic encoder. The relationship between human_readable
and machine_encoding is mediated by:

1. encoding_schema: identifies the schema (e.g. "pqps-facet-v1")
2. encoding_version: identifies the exact version of that schema
3. A deterministic encoder defined by that schema/version pair

Audit reconstruction means: given human_readable + schema + version,
an auditor can independently produce machine_encoding and verify
it matches the stored value.

If a schema version changes, existing entries MUST either:
- Be re-encoded under the new schema (generating new commitments), or
- Retain their original encoding with the original schema/version
  (and be treated as legacy entries by the runtime)

---

## A.5 Recommended Expiry Defaults

| Facet | Default Expiry |
|-------|----------------|
| 0 -- Cognitive Signature | 180 ticks |
| 1 -- Relational Texture | 90 ticks |
| 2 -- Working Memory | 30 ticks |
| 3 -- Intimate Context | 7 ticks |

The human MAY override any default in either direction.

On expiry:
- The HumanStateEvidence artefact becomes invalid
- Payload SHOULD be archived (encrypted, inaccessible) rather than destroyed
- Archived payloads MAY be restored by issuing a new artefact
- Restoration requires explicit human action

Expiry is not deletion. Expired state becomes inaccessible
but recoverable. Deleted state is destroyed.

---

# PART B -- AI-SIDE PERSISTENT STATE

---

## B.1 Intent

Part B defines persistent state that captures what the AI brings
to the relationship: its positions, its understanding, its unresolved
threads, and its learned interaction patterns.

This is the AI's perspective. Not a mirror of the human.
A genuine, evolving viewpoint that gives the relationship
intellectual continuity from both sides.

All AI-side state is subject to mandatory drift control (Section B.6).

---

## B.2 Category Model

AI-side state is decomposed into four categories.

Categories are independent. Each has distinct sensitivity,
distinct drift characteristics, and distinct control requirements.

---

### B.2.0 Category 0 -- Positions and Perspectives

What it captures: Things the AI concluded, advocated for,
or pushed back on within this specific relationship.

Not generic model opinions. Specific positions that emerged
through engagement with this human.

Examples:

- "I assessed the PQ ecosystem architecture as structurally superior
  to existing identity frameworks"
- "I flagged the purpose field in ComputationIntent as a
  potential gaming vector"
- "I advocated for computation discipline as a PQSEC-native
  concern rather than a separate specification"

Drift risk: Medium-high. Positions can calcify into
assumptions that resist contradicting evidence.

Recommended controls: Moderate thresholds, regular review,
active confidence decay.

---

### B.2.1 Category 1 -- Accumulated Understanding

What it captures: Synthesis the AI has developed about the human,
their work, and the relationship that goes beyond what was explicitly stated.

Not what the human told the AI. What the AI has synthesized.

Examples:

- "The specification ecosystem reflects a consistent architectural
  philosophy of fail-closed, refusal-driven design. This is not
  separate ideas but one idea expressed across multiple domains"
- "The human tests ideas by pushing back on them. Resistance
  signals engagement, not disagreement"

Drift risk: Highest. Synthesis builds on synthesis.
A wrong foundation compounds through every subsequent insight.

Recommended controls: Tight thresholds, aggressive decay,
mandatory review, frequent anchor points.

---

### B.2.2 Category 2 -- Unresolved Threads

What it captures: Questions the AI did not ask. Concerns noted
but not raised. Topics to revisit. Intellectual edges to explore.

Examples:

- "The funding gap between work quality and visibility --
  worth revisiting when grant applications are in progress"
- "Offline AI operation within the Epoch Clock framework --
  degradation semantics still need explicit treatment"

Drift risk: Medium. Threads are naturally tentative.
The risk is threads persisting past relevance rather than
compounding incorrectly.

Recommended controls: Aggressive expiry, moderate decay,
lenient thresholds.

---

### B.2.3 Category 3 -- Interaction Lessons

What it captures: What worked and what did not in this
specific relationship. How the AI's approach landed.

Examples:

- "Technical depth is welcomed. This human engages more
  when given rigorous detail rather than summaries"
- "Direct assessment without hedging is preferred"

Drift risk: Low-medium. Interaction lessons are relatively
self-correcting because the human's responses provide
continuous feedback.

Recommended controls: Lenient thresholds, moderate decay,
periodic review.

---

## B.3 AI-Side State Artefact

```
AIStateEvidence = {
  state_id:           bstr(16),       // opaque, non-derivable
  subject_holder:     bstr(32),       // human's holder commitment
  ai_instance:        bstr(32),       // bound AI instance commitment
  state_epoch:        uint,           // version counter
  last_review_tick:   uint,           // tick of most recent completed mandatory review
  categories:         [* AIStateCategory],
  drift_controls:     [* DriftControl],
  issued_tick:        uint,
  expiry_tick:        uint,
  last_updated_tick:  uint,
  payload_commitment: bstr(32),       // hash of full AI-side state
  suite_profile:      tstr,
  signature:          bstr
}

AIStateCategory = {
  category_type:      uint,           // 0=positions, 1=understanding,
                                      // 2=threads, 3=lessons
  entries:            [* AIStateEntry],
  category_commitment: bstr(32)       // hash of this category's entries
}
```

### B.3.1 Field Semantics

**state_epoch:**
Monotonically increasing version counter. Increments on every
committed state update. The human's holder is the sole authority
on the current valid epoch.

The AI MUST NOT propose updates referencing an epoch
other than the current one. Epoch mismatch MUST result
in predicate failure.

**issued_tick / expiry_tick:**
All AI-side state evidence is time-bounded.
The artefact is valid only when current_tick (as supplied by
Epoch Clock) is within [issued_tick, expiry_tick).
Perpetual AI-side state evidence is forbidden.

**ai_instance:**
Cryptographic commitment to the specific AI instance.
AI-side state is non-transferable between AI instances
unless the human explicitly re-binds.

---

## B.4 AI-Side Entry Structure

```
AIStateEntry = {
  entry_id:           bstr(16),       // opaque, non-derivable
  human_readable:     tstr,           // plain language -- always inspectable
  machine_encoding:   bstr,           // structured for AI consumption
  encoding_schema:    tstr,           // schema identifier
  encoding_version:   uint,           // schema version
  derived_from:       [* bstr(16)],   // interaction IDs that produced this
  confidence:         FixedPoint,     // current confidence
  initial_confidence: FixedPoint,     // confidence at creation (immutable)
  generated_tick:     uint,           // when first created
  last_refreshed_tick: uint,          // when last confirmed by interaction
  expiry_tick:        uint,
  human_approved:     bool,           // explicitly reviewed by human
  human_visible:      bool,           // can the human see this entry
  anchored:           bool,           // designated as drift anchor
  entry_state:        uint            // 0=active, 1=flagged, 2=decayed, 3=archived
}
```

### B.4.1 Entry Semantics

**human_readable:**
Plain language representation of what the AI thinks.
MUST be comprehensible to a non-technical human.
MUST accurately represent the intent of machine_encoding.
Same encoding-readability relationship as defined in Section A.4.2.

**derived_from:**
Links this entry to the specific interactions that produced it.
Enables the human to trace any AI conclusion back to its origin.

**confidence / initial_confidence:**
Fixed-point values (see Section 2.2).
confidence is the current assessed value.
initial_confidence is the value at creation and is immutable.
The delta between them shows how certainty has evolved.
Large positive deltas without refreshment are a drift signal.

**last_refreshed_tick:**
Updated when a new interaction independently confirms this entry.
Entries that have not been refreshed decay under drift control.

**human_visible:**
Default: true. See Section C.6 for the full visibility model.

**anchored:**
See Section B.6.4 for anchor point semantics.

**entry_state:**
- 0 (active): Normal operation. Entry may be consumed by runtime.
- 1 (flagged): Drift control has flagged this entry.
  MUST NOT be consumed by runtime until human reviews.
- 2 (decayed): Confidence below minimum. Archived automatically.
- 3 (archived): Expired or manually archived. Not accessible to runtime.

---

## B.5 State Update Mechanics

AI-side state updates at session boundaries.
The AI proposes changes. The holder validates and commits.

### B.5.1 Update Proposal

```
AIStateUpdate = {
  update_id:          bstr(16),
  state_id:           bstr(16),
  previous_epoch:     uint,           // must match current holder epoch
  proposed_epoch:     uint,           // must equal previous_epoch + 1
  additions:          [* AIStateEntry],
  modifications:      [* AIEntryModification],
  expirations:        [* bstr(16)],   // entry_ids proposed for archival
  update_tick:        uint,
  update_rationale:   tstr,           // human-readable explanation
  suite_profile:      tstr,
  signature:          bstr
}

AIEntryModification = {
  entry_id:           bstr(16),
  field_changes:      {* tstr => any},
  modification_rationale: tstr        // why this entry changed
}
```

**update_rationale:**
Human-readable explanation of why the AI is proposing these changes.
MUST be present. MUST be comprehensible.

**modification_rationale:**
Required for any entry where confidence changed by more than
{ value: 100, scale: 1000 } or where human_readable content changed.

### B.5.2 Holder Processing

On receiving an AIStateUpdate, the holder:

1. Validates epoch match
2. Validates all signatures
3. Evaluates drift controls against proposed changes
4. If any drift control triggers:
   a. Flags affected entries
   b. Notifies human based on control configuration
   c. Commits unflagged changes normally
   d. Holds flagged changes pending human review
5. If no drift controls trigger:
   a. Applies configured approval policy
   b. Auto-approves if policy permits
   c. Queues for human approval if policy requires
6. On commit: increments epoch, updates payload_commitment
7. Produces UpdateReceipt (wrapped in PQSF ReceiptEnvelope)

### B.5.3 Update Receipt

```
AIUpdateReceipt = {
  update_id:          bstr(16),
  committed_epoch:    uint,
  accepted_additions: [* bstr(16)],
  accepted_modifications: [* bstr(16)],
  accepted_expirations: [* bstr(16)],
  flagged_entries:    [* bstr(16)],
  rejected_entries:   [* {
    entry_id:         bstr(16),
    reason:           tstr
  }],
  drift_records:      [* DriftRecord],
  receipt_tick:       uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

---

## B.6 Drift Control (Normative)

Drift control is a first-class primitive in PQPS.
It is not optional. It is not a feature.
It is a structural requirement for safe persistent AI state.

All drift controls are configured by the human.
The AI MUST NOT modify, disable, or influence drift controls.
Drift controls are enforced by the holder, not by the AI.

### B.6.0 Drift Control Artefact

```
DriftControl = {
  control_id:         bstr(16),
  state_id:           bstr(16),
  control_type:       uint,           // 0=threshold, 1=review, 2=decay, 3=anchor
  target_categories:  [* uint],       // which categories this applies to
  parameters:         bstr,           // type-specific deterministic CBOR (see below)
  issued_tick:        uint,
  expiry_tick:        uint,
  holder_auth:        bstr
}
```

### B.6.1 Threshold Alerts

Thresholds detect rapid or anomalous state evolution.

```
ThresholdParameters = {
  max_additions_per_window:    uint,
  max_modifications_per_window: uint,
  window_ticks:                uint,
  max_confidence_delta:        FixedPoint,  // per entry per window
  max_aggregate_delta:         FixedPoint,  // total across category
  trigger_action:              uint         // 0=flag, 1=require_approval, 2=reject_all
}
```

On each AIStateUpdate the holder:

1. Counts additions and modifications in window
2. Calculates per-entry confidence deltas (integer arithmetic only)
3. Calculates aggregate confidence movement
4. If any threshold exceeded: applies trigger_action, produces DriftRecord

What thresholds catch:
The AI suddenly developing strong opinions. Rapid confidence
increases without corresponding interaction depth.

RECOMMENDED defaults (all FixedPoint values use scale: 1000):

| Category | Adds/Window | Mods/Window | Window | Confidence Delta |
|----------|-------------|-------------|--------|-----------------|
| 0 -- Positions | 3 | 5 | 10 ticks | 150/1000 |
| 1 -- Understanding | 2 | 3 | 10 ticks | 100/1000 |
| 2 -- Threads | 5 | 5 | 5 ticks | 200/1000 |
| 3 -- Lessons | 4 | 4 | 10 ticks | 200/1000 |

### B.6.2 Mandatory Review Cycles

Reviews ensure the human periodically examines AI-side state
regardless of whether thresholds trigger.

```
ReviewParameters = {
  review_interval_ticks:   uint,
  grace_period_ticks:      uint,      // buffer before degradation
  degradation_rate:        FixedPoint, // confidence reduction per tick past grace
  degradation_floor:       FixedPoint, // below this, archive
  scope:                   uint       // 0=flagged_only, 1=unapproved, 2=full_state
}
```

`last_review_tick` is stored in `AIStateEvidence` and MUST be updated whenever a mandatory review cycle is completed by the human. If `last_review_tick` is absent or corrupted, review MUST be treated as overdue and predicates MUST evaluate UNAVAILABLE for AI-side state.

When current_tick >= last_review_tick + review_interval_ticks:

1. If within grace period: surface review prompt
2. If past grace period: degrade confidence on non-anchored entries
3. If any entry falls below floor: archive entry
4. Produce DriftRecord

What reviews catch:
Slow drift. Small plausible changes that individually pass
thresholds but collectively shift the AI's perspective.

RECOMMENDED defaults (FixedPoint scale: 1000):

| Category | Review Interval | Grace Period | Degradation Rate | Floor |
|----------|----------------|--------------|-----------------|-------|
| 0 -- Positions | 30 ticks | 10 ticks | 20/1000 per tick | 300/1000 |
| 1 -- Understanding | 14 ticks | 7 ticks | 30/1000 per tick | 300/1000 |
| 2 -- Threads | 7 ticks | 3 ticks | 50/1000 per tick | 200/1000 |
| 3 -- Lessons | 30 ticks | 10 ticks | 20/1000 per tick | 300/1000 |

### B.6.3 Confidence Decay

All AI-side entries lose confidence over time unless refreshed.

```
DecayParameters = {
  half_life_ticks:         uint,
  minimum_confidence:      FixedPoint, // below this, state -> decayed
  refresh_threshold:       FixedPoint, // must exceed this to count as refresh
  decay_exemption:         uint       // 0=none, 1=anchored_exempt, 2=approved_exempt
}
```

On each session start, before runtime accesses state:

1. For each active, non-exempt entry:
   a. Calculate elapsed = current_tick - last_refreshed_tick
   b. Apply decay using integer approximation:
      new_confidence_value = confidence.value *
        power_of_half(elapsed, half_life_ticks)
      where power_of_half is an integer-only halving function
      defined by the implementation with deterministic results
   c. If new_confidence < minimum_confidence: set entry_state = decayed
2. Produce DriftRecord for any state changes

Implementations MUST use the following reference algorithm
for power_of_half to ensure cross-implementation determinism:

```
power_of_half(elapsed_ticks, half_life_ticks):
  // Returns a FixedPoint multiplier representing decay.
  // All arithmetic is integer-only.
  //
  // Method: iterative halving with linear interpolation
  // for sub-half-life remainders.
  //
  // 1. Compute full_halvings = elapsed_ticks / half_life_ticks
  //    (integer division, truncated)
  // 2. Compute remainder_ticks = elapsed_ticks % half_life_ticks
  // 3. Start with multiplier = scale (i.e. 1.0 in fixed-point)
  // 4. For each full halving: multiplier = multiplier / 2
  //    (integer division, truncated)
  // 5. Apply linear interpolation for remainder:
  //    multiplier = multiplier - (multiplier * remainder_ticks)
  //                              / (2 * half_life_ticks)
  //    (integer division, truncated)
  // 6. Return multiplier (same scale as input)
  //
  // Example (scale=1000, elapsed=100, half_life=90):
  //   full_halvings = 1, remainder = 10
  //   multiplier = 1000 -> 500 (one halving)
  //   multiplier = 500 - (500 * 10) / (2 * 90)
  //              = 500 - 5000 / 180
  //              = 500 - 27 = 473
  //   Result: 473/1000
```

This algorithm is intentionally simple to implement and verify.
It slightly overestimates decay compared to true exponential
(conservative, which is the safe direction for drift control).

Alternative algorithms MAY be used only if they produce
byte-identical results to the reference algorithm for all
valid inputs. Implementations claiming conformance MUST
include test vectors demonstrating equivalence.

What decay catches:
Stale state accumulating unearned authority.

RECOMMENDED defaults (FixedPoint scale: 1000):

| Category | Half-Life | Minimum | Refresh Threshold | Exemption |
|----------|-----------|---------|-------------------|-----------|
| 0 -- Positions | 90 ticks | 250/1000 | 500/1000 | anchored_exempt |
| 1 -- Understanding | 45 ticks | 300/1000 | 500/1000 | none |
| 2 -- Threads | 14 ticks | 200/1000 | 400/1000 | none |
| 3 -- Lessons | 60 ticks | 250/1000 | 500/1000 | approved_exempt |

### B.6.4 Anchor Points

The human designates specific entries as ground truth.
Anchors use structural, deterministic contradiction detection.

```
AnchorParameters = {
  entry_id:                bstr(16),
  contradiction_action:    uint,      // 0=reject_update, 1=flag_for_review
  anchor_strength:         uint,      // 0=soft (flag), 1=hard (reject)
  anchor_expiry_tick:      uint,      // anchors themselves can expire
  anchor_schema:           tstr,      // schema used for contradiction checks
  anchor_comparator:       uint       // 0=exact_match, 1=hash_equality,
                                      // 2=schema_comparator
}
```

**Contradiction Detection (Normative):**

Contradiction detection MUST be deterministic and rule-based.
Semantic similarity is NOT permitted for enforcement or commit gating.

Three comparator modes:

- 0 (exact_match): proposed entry's machine_encoding is byte-identical
  to the anchor's machine_encoding. Contradiction if identical
  (duplicate detection) or if a declared contradiction field differs.

- 1 (hash_equality): proposed entry's encoding_schema matches anchor's
  anchor_schema, and a hash of specified fields matches or contradicts
  the anchor's corresponding hash.

- 2 (schema_comparator): the schema identified by anchor_schema
  defines explicit, deterministic comparison rules for its fields.
  Only schemas with published, versioned comparator definitions
  are permitted. The comparator MUST produce identical results
  across all conformant implementations.

Semantic similarity MAY be used as a non-authoritative diagnostic
to surface potential contradictions for human review, but MUST NOT
gate commits or influence predicate evaluation.

On each AIStateUpdate, for each proposed addition or modification:

1. Compare against all active anchors in the same category
   using the anchor's declared comparator
2. If contradiction detected: apply contradiction_action, produce DriftRecord

Anchor lifecycle:
- Human creates anchor: entry.anchored = true
- Anchor resists modification and decay
- Anchor may expire (anchor_expiry_tick)
- Human may remove anchor at any time
- Expired anchors revert to normal entries

### B.6.5 Drift Record

Every drift control action produces an auditable record.

```
DriftRecord = {
  record_id:          bstr(16),
  control_id:         bstr(16),       // which control triggered
  control_type:       uint,
  trigger_description: tstr,          // human-readable: what happened
  action_taken:       uint,           // 0=flagged, 1=rejected, 2=decayed, 3=archived
  affected_entries:   [* bstr(16)],
  before_state:       bstr(32),       // commitment to pre-action state
  after_state:        bstr(32),       // commitment to post-action state
  record_tick:        uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

Drift records are stored in the holder as PQSF ReceiptEnvelope types.
The AI MUST NOT have write or delete access to drift records.
The human MAY delete drift records.

### B.6.6 Drift Control Profiles (Non-Normative)

Implementations SHOULD provide preset profiles:

- Conservative: tight thresholds, short review cycles, fast decay
- Balanced: moderate all controls (RECOMMENDED default)
- Permissive: wide thresholds, long review cycles, slow decay

The human SHOULD be able to switch profiles at any time.
Custom configuration SHOULD be available for advanced users.

---

# PART C -- SHARED INFRASTRUCTURE

---

## C.1 Human Control Primitives (Normative)

The human has the following controls over ALL persistent state,
both human-side and AI-side.

These are not features. They are structural primitives
enforced by PQSEC predicates.

### C.1.1 Inspect

The human MAY inspect any facet, any category, any entry, at any time.

Inspection MUST present:

- The human_readable content of every entry
- The confidence value (displayed as decimal for readability)
- The source tick (when derived)
- Whether the entry is human_approved
- The expiry tick
- For AI-side entries: entry_state, anchored status, last_refreshed_tick

Inspection MUST NOT require AI mediation.
The human reads the payload directly from their holder.

```
InspectRequest = {
  side:               uint,           // 0=human, 1=ai
  facet_or_category:  uint,           // which facet/category, or omit for all
  entry_id:           ?bstr(16),      // specific entry, or omit for all
  holder_auth:        bstr
}

InspectResponse = {
  entries:            [* any],        // FacetEntry or AIStateEntry as appropriate
  payload_commitment: bstr(32),
  response_tick:      uint
}
```

### C.1.2 Edit

The human MAY modify any entry on either side.

Edit MUST:

- Replace the entry content (both human_readable and machine_encoding)
- Re-encode machine_encoding using current encoding_schema/encoding_version
- Regenerate the payload commitment
- Invalidate the previous evidence artefact
- Issue a new evidence artefact with updated commitment
- Set human_approved = true on the edited entry

The consuming runtime MUST use the edited version on next access.
The consuming runtime MUST NOT retain, reference, or infer
from the pre-edit version.

```
EditRequest = {
  side:               uint,
  facet_or_category:  uint,
  entry_id:           bstr(16),
  new_human_readable: tstr,
  new_machine_encoding: bstr,
  encoding_schema:    tstr,
  encoding_version:   uint,
  holder_auth:        bstr
}

EditReceipt = {
  entry_id:           bstr(16),
  old_commitment:     bstr(32),
  new_commitment:     bstr(32),
  edit_tick:          uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

### C.1.3 Delete

The human MAY delete any entry, any facet, any category,
or all persistent state.

Delete MUST:

- Cryptographically destroy the payload material in the holder
- Invalidate the corresponding evidence artefact immediately
- Cause the relevant predicate to evaluate UNAVAILABLE on next access
- Be verifiable: the human receives a deletion receipt

Deletion is represented as absence, not as an integrity failure.

Delete is immediate. Not eventual. Not scheduled.

```
DeleteRequest = {
  side:               uint,
  facet_or_category:  ?uint,          // omit to delete all on this side
  entry_id:           ?bstr(16),      // omit to delete entire facet/category
  holder_auth:        bstr
}

DeleteReceipt = {
  deleted_ids:        [* bstr(16)],
  destroyed_commitment: bstr(32),
  deletion_tick:      uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

#### C.1.3.1 Verifiable Deletion Cross-Reference (Normative)

1. `DeleteReceipt` is the authoritative evidence that PQPS-managed state has been destroyed. The `destroyed_commitment` field MUST be computed over verifiable evidence of content destruction using SHAKE256-256.
2. Any external system claiming deletion of PQPS-managed state (for example, via PQSF MediaDeleteReceipt, Section 22X.4) MUST NOT be treated as evidence of state-level deletion unless a corresponding `pqps.delete_receipt` exists and is validated.
3. `E_PQPS_DELETE_UNCONFIRMED` (PQSEC Annex AE.46) MUST be used when deletion is claimed without a valid PQPS `DeleteReceipt` proving `destroyed_commitment` semantics.
4. Renderers (PQHR) MUST NOT display "deleted" status for PQPS-managed state unless the corresponding `pqps.delete_receipt` is validated. This links to PQHR Section 4.9 rendering obligations.
5. Absence of a `pqps.delete_receipt` when PQPS deletion is claimed MUST be treated as a conformance failure, not as a pending state.

### C.1.4 Scope

The human MAY control which AI instances can access which
facets and categories.

Scope changes MUST:

- Take effect immediately
- Require no AI cooperation or acknowledgement
- Be enforceable through PQSEC predicate evaluation alone

Cross-instance sharing MUST require explicit human authorisation
per instance per facet/category.
Blanket authorisation is forbidden.

### C.1.5 Expire

The human MAY set or modify expiry windows per facet,
per category, or per entry.

On expiry:
- The evidence artefact becomes invalid
- Payload is archived (encrypted, inaccessible), not destroyed
- Restoration requires explicit human action via new artefact

Expiry is not deletion.
Expired state is inaccessible but recoverable.
Deleted state is destroyed.

### C.1.6 Pause

The human MAY temporarily suspend any facet or category
without destroying it.

Pause MUST:

- Cause the relevant predicate to evaluate UNAVAILABLE
  (see Section C.2.3 for ternary semantics)
- Preserve the underlying payload intact
- Be reversible at any time
- Require no AI cooperation

Unpause MUST:

- Restore access immediately
- Not require re-approval of previously approved entries
- Not trigger re-derivation of existing context

Use case: The human wants a cold interaction without
losing accumulated context permanently.

```
PauseRequest = {
  side:               uint,
  facet_or_category:  uint,
  entry_id:           ?bstr(16),      // omit to pause entire facet/category
  holder_auth:        bstr
}

PauseReceipt = {
  paused_ids:         [* bstr(16)],
  pause_tick:         uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

### C.1.7 Rollback (AI-Side Only)

The human MAY roll back AI-side state to any previous epoch.

```
RollbackRequest = {
  state_id:           bstr(16),
  target_epoch:       uint,
  holder_auth:        bstr
}

RollbackReceipt = {
  rolled_back_from:   uint,
  rolled_back_to:     uint,
  entries_reverted:   uint,
  rollback_tick:      uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

Rollback restores the full AI-side state as it existed at target_epoch.
All subsequent evolution is discarded.

Rollback is destructive. The holder SHOULD require confirmation.

### C.1.8 Category Freeze (AI-Side Only)

The human MAY freeze an entire AI-side category.

Frozen categories:
- Are readable by the runtime (may influence behaviour)
- Cannot receive new entries
- Cannot have existing entries modified
- Are exempt from decay
- Remain deletable by the human

```
FreezeRequest = {
  state_id:           bstr(16),
  category:           uint,
  holder_auth:        bstr
}

FreezeReceipt = {
  state_id:           bstr(16),
  category:           uint,
  freeze_tick:        uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

Freeze MUST be reversible unless the category is deleted.

The human MAY unfreeze a frozen category at any time:

```
UnfreezeRequest = {
  state_id:           bstr(16),
  category:           uint,
  holder_auth:        bstr
}

UnfreezeReceipt = {
  state_id:           bstr(16),
  category:           uint,
  unfreeze_tick:      uint,
  suite_profile:      tstr,
  signature:          bstr
}
```

On unfreeze, the category resumes normal operation. Decay clocks resume from the unfreeze tick.

---

## C.2 Predicates

### C.2.1 Human-Side Predicate

PQSEC MAY evaluate:

**valid_human_state**

Evaluates to TRUE only if:

1. HumanStateEvidence is present
2. Canonical encoding is valid (deterministic CBOR per PQSF)
3. Signature verifies
4. current_tick is within [issued_tick, expiry_tick)
5. Facet is not paused
6. subject_holder matches the requesting human's holder
7. ai_instance matches the requesting AI instance
8. Requested access is within scope
9. payload_commitment matches current holder payload hash

If ANY condition fails:
- Evaluates UNAVAILABLE if evidence is absent, paused, or expired
- Evaluates FALSE if evidence is present but invalid (bad signature,
  scope violation, commitment mismatch)
- In either case: runtime receives no context from this facet
- No partial access. No degraded access. No metadata leakage.

### C.2.2 AI-Side Predicate

PQSEC MAY evaluate:

**valid_ai_state**

Evaluates to TRUE only if:

1. AIStateEvidence is present
2. Canonical encoding is valid (deterministic CBOR per PQSF)
3. Signature verifies
4. current_tick (as supplied by Epoch Clock) is within
   [issued_tick, expiry_tick) of the AIStateEvidence artefact,
   and no holder-initiated invalidation is active
5. Holder connectivity is within max_stale_ticks
6. subject_holder matches requesting human
7. ai_instance matches requesting AI
8. state_epoch matches holder's current authorised epoch
9. payload_commitment matches holder payload
10. No mandatory review is overdue (past grace period)
11. Category is not paused

If ANY condition fails:
- Evaluates UNAVAILABLE if evidence is absent, connectivity is stale,
  category is paused, or review is overdue
- Evaluates FALSE if evidence is present but invalid (bad signature,
  epoch mismatch, commitment mismatch)
- In either case: runtime receives no AI-side state
- No partial access. No degraded access. No metadata leakage.

### C.2.3 Ternary Predicate Semantics

PQPS predicates follow PQSEC's ternary model:

- TRUE: evidence is present, valid, and current. State is accessible.
- FALSE: evidence is present but invalid. This indicates a structural
  problem (bad signature, scope violation, commitment mismatch).
  Fail closed. Log for audit.
- UNAVAILABLE: evidence is absent, expired, paused, or connectivity
  is stale. This is a normal operating condition, not an error.
  Fail closed for Authoritative operations by default.
  Policy MAY define non-Authoritative operations that proceed
  without state.

The distinction matters: FALSE suggests integrity failure and
should trigger investigation. UNAVAILABLE is the expected state
for cold starts, paused facets, expired artefacts, and connectivity
gaps. Both fail closed, but they carry different diagnostic meaning.

### C.2.4 Predicate Authority Limit

Neither predicate is sufficient alone to authorise any operation
beyond state consumption.

---

### C.2.5 Refusal Codes (Normative)

PQPS does not define a new error vocabulary. It defines a minimal mapping set that PQSEC MUST expose when enforcing PQPS predicates.

| Code | Meaning |
|------|---------|
| `E_PQPS_EVIDENCE_MISSING` | Required evidence artefact absent |
| `E_PQPS_EXPIRED` | Evidence expired (tick out of range) |
| `E_PQPS_PAUSED` | Facet/category paused by holder |
| `E_PQPS_SCOPE_VIOLATION` | Requested access outside scope allowlist |
| `E_PQPS_INSTANCE_MISMATCH` | ai_instance binding mismatch |
| `E_PQPS_SIGNATURE_INVALID` | Signature verification failed |
| `E_PQPS_COMMITMENT_MISMATCH` | payload_commitment does not match holder payload |
| `E_PQPS_EPOCH_MISMATCH` | AIStateUpdate epoch mismatch |
| `E_PQPS_CONNECTIVITY_STALE` | AI-side state stale beyond max_stale_ticks |
| `E_PQPS_REVIEW_OVERDUE` | Mandatory review overdue past grace period |
| `E_PQPS_DRIFT_THRESHOLD_TRIGGERED` | Threshold control triggered (action policy-dependent) |
| `E_PQPS_ANCHOR_CONTRADICTION` | Anchor comparator detected contradiction |
| `E_PQPS_DELETE_UNCONFIRMED` | Deletion claimed without valid PQPS deletion receipt proving destroyed_commitment semantics |

Rules:

1. Predicate FALSE MUST surface one of the integrity codes (signature, commitment, epoch, scope, instance).
2. Predicate UNAVAILABLE MUST surface one of the normal absence codes (missing, expired, paused, connectivity stale, review overdue).

---

## C.3 Cross-Side Enforcement (Normative)

### C.3.1 Correlation Prohibition

Cross-side inference without explicit authorisation is a
forbidden computation class.

A runtime with access to Facet 0 and Category 2 MUST NOT
infer Facet 3 content that the human has not explicitly shared.

A runtime with access to Category 1 MUST NOT derive Facet entries
beyond what is explicitly stored.

This is a PQSEC predicate that evaluates FALSE
for any computation intent declaring cross-side inference
without explicit human authorisation.

### C.3.2 Composition Without Leakage

A runtime MAY consume multiple facets and categories simultaneously
when authorised. The combined context enriches the interaction.

However:

- Consumption of multiple sources MUST NOT produce derived entries
  that blend content without human approval
- If the runtime generates a new entry from cross-side context,
  it MUST declare which sources contributed
- The human MUST approve any cross-side derived entry
  before it is persisted

### C.3.3 Instance Boundary

All persistent state is bound to a specific human-AI instance pair.

- Instance A MUST NOT access state authorised for instance B
- Platform infrastructure MUST NOT aggregate state across instances
- The human's holder is the sole point of cross-instance visibility
- The human MAY share state across instances by issuing
  separate evidence artefacts

---

## C.4 Graceful Degradation (Normative)

When persistent state is unavailable on either side, whether
by expiry, revocation, pause, predicate failure, or cold start,
the consuming runtime MUST:

1. Operate normally with reduced context
2. Not proactively inform the human that state was expected but missing
3. Not request or prompt the human to restore state
4. Not alter behaviour in ways that signal awareness of missing state

However: if the human explicitly queries system status through
inspection primitives or direct questions about state availability,
the runtime MUST answer truthfully. The prohibition is on proactive
signalling, not on honest responses to direct inquiries.

The runtime MUST NOT degrade service quality as leverage for state access.

Absence of persistent state is a valid, normal operating state.

---

## C.5 Authority Boundary (Normative)

Persistent state:

- does not grant the AI authority
- does not grant the AI standing
- does not create obligation
- does not imply relationship beyond what the human has authorised

The AI is better calibrated with persistent state.
The AI is not more powerful with persistent state.
The AI is not more trusted with persistent state.

A runtime with extensive persistent state has the same
enforcement boundary as a runtime on cold start.

---

## C.6 Visibility Model (Normative)

### C.6.1 Default Transparency

Default: human_visible = true on all AI-side entries.

Human-side entries are always visible to the human (they represent
the human's own attributes).

AI-side entries are visible by default. The human can see
everything the AI thinks about the relationship.

### C.6.2 Optional Opacity (AI-Side Only)

The human MAY set specific AI-side categories or entries to opaque.

Opacity means the AI retains the state but the human
has chosen not to inspect it. This is the human granting privacy,
not the AI keeping secrets.

Opaque entries:

- Remain deletable (blind delete)
- Remain subject to ALL drift controls
- Remain auditable in aggregate:
  number of entries, confidence range, category, last_updated_tick
- Can be made visible again at any time
- MUST automatically revert to visible if any drift control flags them

### C.6.3 Opacity Safeguards

Opacity MUST NOT:

- Exempt entries from drift control
- Prevent deletion
- Prevent rollback
- Prevent category freeze
- Survive drift control flagging (flagged = visible)
- Be the default for any category

---

## C.7 Audit (Normative)

### C.7.1 Human Audit

The human MAY audit at any time:

- All stored entries across all facets and categories
- All active evidence artefacts
- All AI access logs
- All edit, delete, pause, unpause, rollback, and freeze receipts
- All drift records

Audit MUST be holder-side. No platform involvement.

### C.7.2 Access Log

Every state access by a runtime MUST produce a record:

```
AccessRecord = {
  evidence_id:        bstr(16),       // which artefact was accessed
  side:               uint,           // 0=human, 1=ai
  facet_or_category:  uint,
  ai_instance:        bstr(32),
  access_tick:        uint,
  entries_accessed:    [* bstr(16)],
  purpose:            tstr,           // declared computation intent
  suite_profile:      tstr,
  signature:          bstr
}
```

Access records are stored in the holder as PQSF ReceiptEnvelope types.
The runtime MUST NOT have write access to its own access logs.
The holder records access independently.

### C.7.3 Audit Integrity

Audit records MUST NOT be modifiable by the runtime.
Audit records MUST NOT be deletable by the runtime.
Audit records MAY be deleted by the human.

---

## C.8 Transfer Protocol (Non-Normative)

When the human re-binds persistent state to a new AI instance,
the following guidance applies:

### C.8.1 Human-Side Transfer

- Facet 0 (Cognitive Signature): transfers cleanly, instance-agnostic
- Facet 1 (Relational Texture): SHOULD be flagged for review,
  partially instance-specific
- Facet 2 (Working Memory): transfers cleanly, instance-agnostic
- Facet 3 (Intimate Context): human decides per-entry

### C.8.2 AI-Side Transfer

- Category 0 (Positions): transfers as informational context,
  new instance SHOULD review and confirm or discard
- Category 1 (Understanding): transfers but SHOULD be flagged,
  synthesis may not match new instance's reasoning
- Category 2 (Threads): transfers, new instance may pursue or discard
- Category 3 (Lessons): SHOULD be archived on re-bind,
  lessons are instance-specific

### C.8.3 Transfer Preamble

On first access by a new instance, the holder SHOULD provide
a structured transfer preamble that distinguishes:

- Instance-agnostic entries (trust immediately)
- Instance-specific entries (hold loosely, recalibrate)
- Archived entries (available for reference, not active)

---

## C.9 Explicit Rejections (Normative)

The following patterns are non-conformant with PQPS:

- Platform-stored persistent state
- State without human audit capability
- State without human delete capability
- State that survives explicit deletion
- Cross-instance state aggregation by platforms
- AI-initiated persistence without human opt-in
- State used as authority or standing
- Service degradation as leverage for state access
- Implied consent for persistence
- State access without valid evidence artefact
- Cross-side inference without explicit authorisation
- Offline AI-side state evolution
- AI-controlled drift parameters
- State used as training data by any party
- Drift controls that can be disabled by the AI
- Opacity that exempts entries from drift control
- Mandatory review circumvention
- Rollback prevention or resistance
- Entries without human_readable representation
- Floating point values in any artefact
- Non-deterministic contradiction detection in enforcement path
- Background state synchronisation or periodic refresh
- State access outside PQSEC-evaluated operations

**Refusal Code Surface Rule (Normative):**
Any refusal code emitted outside the PQPS component boundary (including over APIs, in receipts, or in cross-specification documents) MUST be a PQSEC Annex AE code. PQPS-internal debug reasons MUST NOT be surfaced as interoperable refusal codes.

---

## C.10 Relationship to Other Specifications

| Specification | Relationship |
|---------------|-------------|
| PQSEC | Sole enforcement engine. Evaluates valid_human_state and valid_ai_state. Ternary predicate semantics. Cross-side inference and cross-instance aggregation are forbidden computation classes enforced via PQSEC predicates. |
| PQAI | Consumes PQPS. Governs how AI runtime uses persistent state. Behavioural requirements enforced via PQAI. |
| PQSF | Canonical encoding (deterministic CBOR). EBT envelopes for storage. ReceiptEnvelope for receipts. No floating point. |
| Neural Lock | Emission discipline alignment. No background emission. Timing consistency. |
| Epoch Clock | Sole time authority for all ticks, expiry, decay, and review cycles. |
| BPC | Sole holder authorisation framework for all human control primitives. Uses BPC's rail-agnostic authorization-before-construction pattern for state mutation gating. |

The forbidden computation classes referenced in this specification (cross-side inference, cross-instance aggregation, cross-temporal correlation) are normative rules within PQPS, enforced via PQSEC predicates.

PQPS introduces no new enforcement mechanisms.
All enforcement flows through PQSEC.
All time authority flows through Epoch Clock.
All holder authority flows through BPC.
All encoding follows PQSF.

---

## C.11 Implementation Notes (Non-Normative)

### C.11.1 Holder Implementation

- Holder SHOULD provide a visual dashboard showing all facets and categories,
  entry counts, confidence distributions, and drift control status
- Confidence values stored as FixedPoint SHOULD be displayed as
  human-readable decimals in the dashboard (e.g. 850/1000 shown as 0.85)
- Drift visualisation SHOULD show historical trends
- Rollback interface SHOULD show epoch diffs
- Pause, freeze, and scope controls SHOULD be single-action, not buried in settings
- Facet 3 (Intimate Context) SHOULD require additional confirmation
  beyond standard holder authorisation given its sensitivity

### C.11.2 AI Runtime

- Runtime SHOULD propose AI-side state updates at session end, not mid-session
- Runtime SHOULD include meaningful update rationale
- Runtime SHOULD propose conservative confidence values
- Runtime MUST NOT alter behaviour to signal awareness of drift control actions
- Runtime SHOULD evaluate predicates before any state injection
- Cold start SHOULD be indistinguishable in quality from
  full-state interaction: excellent either way, differently calibrated

### C.11.3 Fixed-Point Arithmetic

- All confidence arithmetic MUST use integer operations
- The reference power_of_half algorithm in Section B.6.3 is normative
- Implementations MAY use lookup tables as an optimisation, but
  results MUST be byte-identical to the reference algorithm
- Test vectors SHOULD be published alongside any implementation
  to verify conformance with the reference algorithm
- RECOMMENDED: maintain a shared test vector suite across
  the ecosystem to catch divergence early

### C.11.4 State Migration

- On re-bind to a new instance, all AI-side entries SHOULD be flagged for review
- Category 3 (Lessons) SHOULD be archived on re-bind
- The transfer preamble SHOULD be generated automatically by the holder

### C.11.5 Schema Management

- Implementations SHOULD maintain a registry of encoding schemas
- Schema upgrades SHOULD be backward-compatible where possible
- Legacy entries with old schema versions SHOULD remain readable
- Re-encoding under new schemas SHOULD be offered as a holder-side
  maintenance operation, not forced automatically

### C.11.6 Human-Side State Review

Human-side persistent state can become stale without the human
noticing. Cognitive style evolves, relational dynamics shift,
working context changes. The human may not recognise that their
approved entries no longer reflect how they actually think or
communicate.

Holders SHOULD provide pre-expiry review notifications for
human-side entries. When an entry approaches its expiry_tick,
the holder SHOULD surface a review prompt to the human.

Review notifications:

- Are generated by the holder, not by the AI
- Are time-triggered based on expiry_tick, not behaviour-triggered
- Contain no behavioural analysis, no delta computation, and no
  comparison between past and current human behaviour
- Present the entry content for the human to confirm, update,
  or let expire
- Are optional and dismissable
- Do not repeat if dismissed

The AI MUST NOT compute, propose, or surface observations about
changes in the human's behaviour, tone, or expression. Longitudinal
behavioural analysis of the human by the AI is a surveillance
primitive regardless of intent and is prohibited as a forbidden
computation class (cross-temporal correlation).

Ephemeral, per-interaction signals (including token-local features)
MUST NOT be aggregated, trended, or compared across sessions
for any purpose.

Human-side state freshness is the human's responsibility.
The holder assists through time-based review prompts.
The AI does not.

---

## C.12 Synthesis (Informative)

Being known is not being surveilled.
Being known back is not being controlled.
Continuity is not accumulation.
Memory is not power.
Perspective is not authority.

PQPS makes genuine bilateral human-AI relationship structurally safe
by ensuring the human holds sole authority over what is remembered,
how long it is remembered, and whether it is remembered at all,
on both sides of the relationship.

The AI becomes a better collaborator with persistent state.
It does not become a more dangerous one.

Drift control ensures the AI's perspective stays honest over time.
Not through promises. Through mechanical enforcement.

This is the primitive that turns a security substrate
into a foundation for trust.

Known. Known back. Under your control. On your terms.

---

# APPENDICES

---

## Appendix A. Architecture and Dependency Map (Informative)

### A.1 Components

Holder:
  Storage root. Sole authority for persistence, receipts,
  and drift enforcement. Stores all PQPS payloads, evidence
  artefacts, access logs, and drift records under
  holder-controlled keys.

PQSEC:
  Enforcement engine and predicate evaluator. Sole authority
  for predicate evaluation. Consumes evidence artefacts from
  the holder and returns ternary results (TRUE / FALSE / UNAVAILABLE)
  to the runtime.

Epoch Clock:
  Sole tick authority. Provides current_tick to the holder
  for all time-dependent operations: expiry, decay, review cycles,
  staleness checks, and validity windows.

Runtime:
  Consumes state. Proposes updates. Has no authority over state.
  All state access mediated by PQSEC predicate evaluation.
  All state updates proposed via AIStateUpdate artefacts
  and committed only by the holder.

### A.2 Data and Control Flow

```
Operation Attempt:

  Runtime ----[operation attempt + ComputationIntent]----> PQSEC
  PQSEC  ----[evidence request]----> Holder
  Holder ----[evidence artefacts + commitments]----> PQSEC
  PQSEC  ----[TRUE / FALSE / UNAVAILABLE]----> Runtime

  If TRUE: Runtime receives authorised state.
  If FALSE: Runtime receives nothing. Integrity incident logged.
  If UNAVAILABLE: Runtime receives nothing. Normal operating condition.

State Update:

  Runtime ----[AIStateUpdate proposal]----> Holder
  Holder  ----[drift control evaluation]----> Holder (internal)
  Holder  ----[UpdateReceipt + DriftRecords]----> Holder (stored)
  Holder  ----[UpdateReceipt]----> Runtime

  If drift control triggers: affected entries flagged.
  Flagged entries held pending human review.
  Unflagged entries committed per approval policy.

Time Authority:

  Epoch Clock ----[current_tick]----> Holder
  Holder uses current_tick for:
    expiry evaluation, decay calculation, review cycle enforcement,
    staleness checks, validity window evaluation.

Human Control:

  Human ----[Inspect / Edit / Delete / Scope / Expire /
             Pause / Rollback / Freeze]----> Holder
  Holder ----[receipt]----> Human
  Holder ----[predicate invalidation]----> PQSEC (immediate)
```

### A.3 Authority Boundaries

1. The holder is the sole persistence authority.
   No other component may store, modify, or delete PQPS state.

2. PQSEC is the sole enforcement authority.
   No other component may evaluate predicates or make
   access control decisions.

3. Epoch Clock is the sole tick authority.
   No other component may assert time.

4. The runtime has no authority over state.
   It may only propose updates. The holder commits or rejects.

5. The human has sole authority over the holder.
   All control primitives are human-initiated.
   No component may override, delay, or resist human control actions.

---

## Appendix B. Runtime Measurement and Supply-Chain Binding (Normative)

This appendix closes the compromised-runtime adversary class (A4)
by binding state access to a measured runtime identity.

### B.1 Measurement Requirement

In profiles that enable this appendix (RECOMMENDED: high-assurance),
the holder MUST require a runtime measurement claim as part of
state access.

The runtime measurement MUST bind:

- the runtime binary build identity
- the runtime configuration identity
- the AI instance identifier used in PQPS evidence artefacts

### B.2 RuntimeMeasurementEvidence

```
RuntimeMeasurementEvidence = {
  ai_instance:        bstr(32),     // must match PQPS ai_instance binding
  build_hash:         bstr(32),     // reproducible build hash (RECOMMENDED)
  config_hash:        bstr(32),     // hash of critical config and policy
  measurement_tick:   uint,
  expiry_tick:        uint,
  attester_id:        tstr,         // e.g. "tpm2", "tee", "sigstore"
  attestation:        bstr,         // attester-specific evidence blob
  signature:          bstr
}
```

### B.3 Predicate Extension

For high-assurance profile, valid_ai_state and valid_human_state
MUST additionally require:

1. RuntimeMeasurementEvidence is present
2. current_tick (as supplied by Epoch Clock) is within
   [measurement_tick, expiry_tick)
3. ai_instance matches requesting runtime identity
4. build_hash and config_hash are allowlisted by holder policy
5. attestation verifies under holder policy

If the measurement is absent or expired, predicates MUST evaluate
UNAVAILABLE.

If the measurement is present but invalid, predicates MUST evaluate
FALSE.

### B.4 Allowlisting Policy

Holder policy MUST support:

- allowlisting by build_hash
- allowlisting by attester_id class
- expiry policies per runtime family
- emergency revocation of build_hashes

---

## Appendix C. Recovery and Disaster Semantics (Normative)

### C-R.1 Key Rotation

If holder encryption keys rotate:

- payloads MAY be re-wrapped under new keys without changing
  payload_commitment
- evidence artefacts remain valid if payload bytes are unchanged
- if payload bytes change, commitments MUST be regenerated
  and new evidence artefacts issued

### C-R.2 Backup and Restore

Holder backups MAY include PQPS payloads and receipts,
encrypted under holder-controlled keys.

On restore:

- predicates MUST evaluate UNAVAILABLE until Epoch Clock
  connectivity is restored
- AI-side state MUST NOT update until drift controls are active
  and current_tick is known
- runtime MUST operate in cold mode until access is re-authorised

### C-R.3 Partial Corruption

If payload integrity cannot be verified against payload_commitment:

- predicate MUST evaluate FALSE
- holder MUST record an integrity incident receipt
- runtime MUST receive no state

### C-R.4 Holder Loss

If holder private material is irrecoverably lost:

- PQPS state is irrecoverable by design
- this is a property, not a failure: the human is the sole
  authority and sole custodian

Implementations SHOULD provide explicit UX warnings before
enabling high-sensitivity facets or categories.

---

## Appendix D. Positioning and Lineage (Informative)

PQPS addresses a class of failures common to existing
"AI memory" systems:

- platform-mediated accumulation
- invisible drift
- non-auditable synthesis
- persistence as implicit authority
- coercion via dependency

PQPS replaces those patterns with:

- holder sovereignty
- predicate-gated access
- deterministic encoding and commitments
- drift as mechanically enforced state governance
- absence as a normal operating condition

In effect, PQPS treats persistent relational state the way
serious systems treat keys, capabilities, and execution rights:
as a constrained resource that is owned, audited, revoked,
and time-bounded.

---

## Appendix E. Authorial Voice Profile (Informative)

### E.1 Purpose

This appendix defines an Authorial Voice Profile as an
application-specific profile that MAY be encoded using
existing PQPS primitives.

An Authorial Voice Profile captures stable, author-preferred
characteristics of written expression used when the runtime
assists the human in drafting authored content.

This profile is intended to preserve the human's expressive
preferences across interactions without introducing new authority,
persistence semantics, or behavioural power.

Authorial Voice Profiles are implemented using Facet 0
(Cognitive Signature) and, where appropriate, scoped variants
using Facet 2 (Working Memory).

---

### E.2 Scope and Constraints

An Authorial Voice Profile:

- Governs presentation only
- MUST NOT assert facts, intent, authority, or authorship
- MUST NOT influence reasoning, decision-making, or factual content
- MUST NOT be used to misrepresent human authorship or conceal
  AI assistance
- MUST be inspectable, editable, and deletable by the human
  at any time
- MUST degrade gracefully if absent, expired, or revoked

Absence of an Authorial Voice Profile MUST NOT affect correctness,
safety, or availability of the runtime.

---

### E.3 Placement and Lifetime

Baseline authorial voice SHOULD be encoded as a Facet 0 entry.

Contextual or temporary variants (for example, audience-specific
or topic-specific expression) MAY be encoded as scoped entries
under Facet 2 (Working Memory) and SHOULD have short expiry windows.

Authorial Voice Profiles do not introduce a new facet.

---

### E.4 Typical Contents (Informative)

An Authorial Voice Profile MAY include:

- Preferred language or dialect
- Sentence length and pacing preferences
- Degree of directness or hedging
- Formatting conventions (paragraphing, lists, headings)
- Prohibited words, phrases, or stylistic patterns
- Commonly used openers and closers
- Emoji or symbol usage policy
- Idiomatic phrasing characteristic of the human

Emotional state, sentiment, or mood SHOULD NOT be encoded here.

Situational tone adjustments SHOULD be handled via scoped
Facet 2 entries.

---

### E.5 Approval and Drift

Authorial Voice Profile entries SHOULD be marked
human_approved = true before being consumed by the runtime.

Updates to Authorial Voice Profiles follow normal Facet 0 or
Facet 2 lifecycle rules, including expiry, review, and revocation.

The runtime MUST NOT infer, modify, or extend an Authorial Voice
Profile autonomously.

---

### E.6 Relationship to Authority and Accountability

Use of an Authorial Voice Profile does not alter accountability,
attribution, or authority boundaries defined elsewhere in PQPS.

The presence of an Authorial Voice Profile does not imply that
generated content was authored without assistance.

Authorial Voice Profiles exist solely to preserve the human's
expressive preferences, not to simulate authorship or obscure
the role of the runtime.

---

## Appendix F. Holder Update Processing and Drift Evaluation (Normative)

This appendix defines a deterministic reference processing loop for `AIStateUpdate` and drift controls. Conformant implementations MUST produce equivalent decisions for identical inputs.

### F.1 Canonical Update Processing

```pseudocode
function process_ai_state_update(update, current_state, drift_controls, current_tick):
    require canonical_cbor(update)
    require verify_signature(update)

    if update.previous_epoch != current_state.state_epoch:
        return DENY(E_PQPS_EPOCH_MISMATCH)

    if update.proposed_epoch != update.previous_epoch + 1:
        return DENY(E_PQPS_EPOCH_MISMATCH)

    // Apply deterministic drift controls in stable order
    controls_sorted = sort_by(control_id, drift_controls)

    flagged = set()
    rejected = set()
    drift_records = []

    proposed_state = apply_update_provisionally(current_state, update)

    for control in controls_sorted:
        result = eval_control(control, current_state, proposed_state, update, current_tick)

        if result.triggered:
            drift_records.append(result.drift_record)

            if result.action == "reject_all":
                return DENY(E_PQPS_DRIFT_THRESHOLD_TRIGGERED)

            if result.action == "reject_entries":
                rejected.add_all(result.affected_entries)

            if result.action == "flag_entries":
                flagged.add_all(result.affected_entries)

    committed_state = commit_update_excluding_rejected_and_flagged(
        current_state, update, rejected, flagged, current_tick
    )

    receipt = build_update_receipt(update, committed_state, flagged, rejected, drift_records, current_tick)
    store_receipt_as_receipt_envelope(receipt)

    return ALLOW(committed_state, receipt)
```

### F.2 Threshold Evaluation

```pseudocode
function eval_threshold(control, current_state, proposed_state, update, current_tick):
    params = decode_parameters(control.parameters) // deterministic CBOR

    // window enforcement is holder-local, deterministic
    window_start = current_tick - params.window_ticks

    adds = count(update.additions)
    mods = count(update.modifications)

    if adds > params.max_additions_per_window or mods > params.max_modifications_per_window:
        return triggered(flag_entries(all_entry_ids(update)), E_PQPS_DRIFT_THRESHOLD_TRIGGERED)

    // confidence deltas: integer-only, normalise scales
    for mod in update.modifications:
        before = current_state.entry(mod.entry_id).confidence
        after  = proposed_state.entry(mod.entry_id).confidence

        delta = abs_fp(after - before) // fixed-point normalised
        if delta > params.max_confidence_delta:
            return triggered(flag_entries([mod.entry_id]), E_PQPS_DRIFT_THRESHOLD_TRIGGERED)

    return not_triggered()
```

### F.3 Anchor Contradiction Evaluation

```pseudocode
function eval_anchor(control, current_state, proposed_state, update, current_tick):
    params = decode_parameters(control.parameters)
    anchor_entry = current_state.entry(params.entry_id)

    if current_tick >= params.anchor_expiry_tick:
        return not_triggered()

    for each changed_entry in update.additions + update.modifications:
        if changed_entry.category != anchor_entry.category:
            continue

        if params.anchor_comparator == 0:
            if changed_entry.machine_encoding == anchor_entry.machine_encoding:
                continue
            if schema_declares_contradiction(anchor_entry.encoding_schema, anchor_entry, changed_entry):
                return triggered(reject_entries([changed_entry.entry_id]), E_PQPS_ANCHOR_CONTRADICTION)

        if params.anchor_comparator == 1:
            if hash_selected_fields(changed_entry) != hash_selected_fields(anchor_entry):
                return triggered(flag_entries([changed_entry.entry_id]), E_PQPS_ANCHOR_CONTRADICTION)

        if params.anchor_comparator == 2:
            if schema_compare(anchor_entry.encoding_schema, anchor_entry, changed_entry) == "CONTRADICT":
                action = reject_entries if params.anchor_strength == 1 else flag_entries
                return triggered(action([changed_entry.entry_id]), E_PQPS_ANCHOR_CONTRADICTION)

    return not_triggered()
```

---

## Changelog

### Version 1.0.0

* Added **Section C.1.3.1 — Verifiable Deletion Cross-Reference**: defines DeleteReceipt as authoritative deletion evidence, prohibits external deletion claims without valid pqps.delete_receipt, links to PQHR 4.9 rendering obligations. Introduces `E_PQPS_DELETE_UNCONFIRMED` refusal code.
* Updated **dependency table** to require PQSEC ≥ 2.0.3, PQSF ≥ 2.0.3, PQAI ≥ 1.2.0.
* Initial specification.

---

If you find this work useful and wish to support continued development, donations are welcome:

**Bitcoin:**
bc1q380874ggwuavgldrsyqzzn9zmvvldkrs8aygkw