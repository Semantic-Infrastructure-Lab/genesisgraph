# Gap #3: Lifecycle & Revocation Model

**Priority:** 🔴 **CRITICAL**

**Status:** Planned for v0.5.0 (Mar 2026)

**Blocks:** Long-lived deployments, compliance requirements, forensic analysis

---

## The Problem

GenesisGraph documents capture a **point-in-time snapshot**, but real-world trust is **temporal and dynamic**.

### Attack Scenarios

1. **Tool Version Revoked After Use:**
   - Workflow uses `ollama@2.3.1` on 2025-10-15
   - CVE discovered on 2025-10-20, version revoked
   - Auditor reviewing provenance on 2025-11-01 asks: "Was this version safe *at the time*?"
   - **GenesisGraph cannot answer**

2. **Dataset Corrupted Retroactively:**
   - Provenance references `medical_corpus@2025-10-15`
   - Dataset discovered to be poisoned on 2025-11-05
   - All downstream workflows now suspect
   - **No revocation mechanism**

3. **License Expires Mid-Execution:**
   - Software license valid 2025-01-01 to 2025-06-30
   - Workflow executed 2025-07-15
   - **No temporal validation**

4. **Transparency Log Updated After-the-Fact:**
   - Inclusion proof references tree_size=10000
   - Log operator appends entries later
   - **No consistency proof validation**

---

## Impact

**Who This Blocks:**
- Regulatory compliance teams requiring temporal validation
- Forensic analysts investigating incidents
- Long-lived production deployments (multi-year)
- Systems requiring key rotation

**Use Cases Affected:**
- Medical device compliance (21 CFR Part 11)
- Financial audit trails (SOX requirements)
- Supply chain investigations
- Long-running research projects

---

## Recommended Improvements

### 1. Add Lifecycle Metadata to Entities

```yaml
entities:
  - id: medical_corpus
    type: Dataset
    version: 2025-10-15
    hash: sha256:abc123...
    lifecycle:
      created_at: 2025-10-15T00:00:00Z
      valid_from: 2025-10-15T00:00:00Z
      valid_until: 2026-10-15T00:00:00Z  # Expiry
      deprecated_at: null
      revoked_at: null
      revocation_reason: null
      replacement: null
```

### 2. Add Revocation Endpoints to Attestations

```yaml
attestation:
  mode: verifiable
  signer: did:org:tool-vendor
  signature: ed25519:sig_abc123
  revocation_registry: https://vendor.com/revocations.json
  status_check_endpoint: https://vendor.com/status/sig_abc123
  governance_decision_id: null
```

### 3. Add Tool Version Lineage

```yaml
tools:
  - id: freecad
    type: Software
    version: 0.21.2
    lifecycle:
      released_at: 2024-06-01T00:00:00Z
      deprecated_at: null
      end_of_support: 2026-06-01T00:00:00Z
      cve_refs: []
      successor: freecad@0.22.0
      compatibility: backward_compatible
```

### 4. Add Temporal Validation Requirements

- `at_time` parameter for verification
- Historical revocation list support
- Transparency log consistency proof validation
- Temporal policy evaluation ("was this allowed *then*?")

### 5. Create `scripts/verify_lifecycle.py`

```bash
python scripts/verify_lifecycle.py workflow.gg.yaml \
  --at-time 2025-10-15T14:00:00Z \
  --check-revocations \
  --check-expirations
```

---

## Implementation Plan

**Dependencies:** None

**Effort:** 3-4 weeks
- Week 1: Lifecycle schema design
- Week 2: Revocation registry integration
- Week 3: Temporal validation logic
- Week 4: Testing + documentation

**Deliverables:**
- [ ] Lifecycle metadata in core schema
- [ ] Revocation registry support
- [ ] `verify_lifecycle.py` script
- [ ] Temporal validation guide
- [ ] CVE integration examples

---

## Success Criteria

A gap is considered "plugged" when:
- [ ] Lifecycle metadata supported for all entity types
- [ ] Revocation checking functional
- [ ] Temporal validation ("was valid at time T?") works
- [ ] Historical audit queries supported
- [ ] Documentation includes revocation best practices

---

## Related Documentation

- [Roadmap v0.5](../roadmap.md#v050-mar-2026) - Lifecycle implementation
- [Gap #1: Threat Model](01-threat-model.md) - Security context
- [Gaps Index](index.md) - All critical gaps

---

**Last Updated:** 2025-12-07
**Owner:** Compliance working group
**Target Version:** v0.5.0 (Mar 2026)
