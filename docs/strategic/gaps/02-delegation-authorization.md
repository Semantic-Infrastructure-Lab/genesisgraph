# Gap #2: Delegation & Authorization Model

**Priority:** 🔴 **CRITICAL**

**Status:** Planned for v0.6.0 (May 2026)

**Blocks:** AI agent ecosystems, automated manufacturing, regulated workflows

---

## The Problem

GenesisGraph captures *what happened*, but not *whether the agent doing it was allowed to*.

This is a fundamental gap for AI agent ecosystems, manufacturing automation, and regulated workflows.

### Current State

```yaml
operations:
  - id: op_inference
    tool: llama3_70b@3.0
    # ❌ Missing: Was this model authorized to process this data?
    # ❌ Missing: Under what policy constraints?
    # ❌ Missing: What delegation chain allowed it?
```

### Missing Elements

- **Authorization proofs** - Who granted permission for operation O?
- **Delegation chains** - How did authority flow from owner → agent → tool?
- **Policy constraints** - What capability envelope was the agent operating within?
- **Delegation revocation** - What happens if permission is revoked mid-workflow?
- **Cross-organizational delegation** - How do permissions work across trust boundaries?

---

## Impact

**Who This Blocks:**
- AI agent developers building autonomous systems
- Healthcare organizations requiring HIPAA delegation proof
- Manufacturing facilities with certification requirements
- Research institutions with IRB compliance needs

**Real-World Scenarios Blocked:**

1. **AI Agent Authorization:**
   > "Prove this AI agent was authorized to access patient records under HIPAA delegation"

2. **Manufacturing Delegation:**
   > "Prove the CNC operator had valid certification when machining this aerospace part"

3. **Research Data Access:**
   > "Prove the postdoc had IRB approval when analyzing this dataset"

---

## Recommended Improvements

### 1. Add Delegation & Policy Objects

To core schema:

```yaml
operations:
  - id: op_inference
    tool: llama3_70b@3.0
    authorization:
      delegated_by: did:org:hospital-west
      delegation_chain:
        - grantor: did:org:hospital-west
          grantee: did:person:dr_sarah_chen
          capability: medical_data_access
          credential: vc:hipaa-delegation-2025
          valid_from: 2025-01-01T00:00:00Z
          valid_until: 2025-12-31T23:59:59Z
        - grantor: did:person:dr_sarah_chen
          grantee: did:model:llama3-70b-instruct
          capability: inference_with_phi
          constraints:
            max_records_per_day: 100
            data_retention: prohibited
      policy_evaluation:
        policy_id: hipaa-safe-harbor-v1
        decision: permit
        evaluator: did:svc:opa-policy-engine
        trace: base64:...  # OPA decision trace
```

### 2. Support Multiple Delegation Standards

- **ZCAP-LD** (W3C Authorization Capabilities)
- **Macaroons** (Google-style bearer tokens with caveats)
- **OAuth 2.0** (existing enterprise identity)
- **Verifiable Credentials** (DID-based permissions)

### 3. Create `gg-delegation-v1` Profile

- Required fields for delegation-aware provenance
- Policy evaluation trace requirements
- Revocation checking requirements

### 4. Integration with Policy Engines

- **OPA** (Open Policy Agent)
- **Cedar** (AWS policy language)
- Rego evaluation traces as attestations

---

## Implementation Plan

**Dependencies:**
- ✅ DID resolution (complete in v0.3)
- 🟡 VC support (partial in v0.3, needs extension)

**Effort:** 4-6 weeks
- Weeks 1-2: Delegation schema design + standards research
- Weeks 3-4: Implementation + OPA/Cedar integration
- Weeks 5-6: Testing + documentation + examples

**Deliverables:**
- [ ] Delegation objects in core schema
- [ ] `gg-delegation-v1` profile validator
- [ ] OPA integration examples
- [ ] HIPAA delegation tutorial
- [ ] AI agent authorization guide

---

## Success Criteria

A gap is considered "plugged" when:
- [ ] Delegation chains representable in provenance
- [ ] Policy evaluation traces captured
- [ ] Integration with 2+ policy engines (OPA, Cedar)
- [ ] Real-world pilot (healthcare or AI agent)
- [ ] Documentation includes delegation best practices

---

## Related Documentation

- [Roadmap v0.6](../roadmap.md#v060-may-2026) - Delegation implementation
- [Gap #9: AI Agent Integration](09-ai-agent-integration.md) - Builds on delegation
- [Gaps Index](index.md) - All critical gaps

---

**Last Updated:** 2025-12-07
**Owner:** Authorization working group
**Target Version:** v0.6.0 (May 2026)
