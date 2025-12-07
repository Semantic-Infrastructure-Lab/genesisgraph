# Gap #6: Formal Semantics for Operation Chains

**Priority:** 🟡 **HIGH**

**Status:** Planned for v0.9.0 (Jan 2027)

**Blocks:** Automated verification, policy enforcement, legal defensibility

---

## The Problem

The four-node model is **intuitive**, but auditors will ask:

> "What does it mean when a workflow declares an input or parameter?"

Current semantics are **implicit**:
- Operations take inputs → produce outputs
- Parameters influence transformations

**But nothing enforces:**
- Determinism (or documenting non-determinism)
- Side-effect recording
- Completeness of inputs
- Correct dependency ordering
- Parameter influence guarantees

### Attack Scenario

```yaml
operations:
  - id: malicious_op
    type: ai_inference
    inputs: [prompt@1.0]  # ✅ Declared
    # ❌ Hidden: Also reads secret_prompts.txt from disk
    outputs: [answer@1.0]
    parameters:
      temperature: 0.2  # ✅ Declared
    # ❌ Hidden: Actually uses temperature=1.5
```

**Current state:** GenesisGraph has no way to detect this.

---

## Impact

**Who This Blocks:**
- Legal teams requiring defensible provenance
- Automated verification systems
- Reproducibility researchers
- Security auditors

**Use Cases Affected:**
- Legal proceedings (provenance as evidence)
- Automated compliance checking
- Scientific reproducibility validation
- Fraud detection systems

---

## Recommended Improvements

### 1. Define Formal DAG Semantics

```yaml
dag_semantics:
  version: 1.0
  guarantees:
    - input_closure: strict  # All inputs must be declared
    - output_determinism: documented  # Non-determinism must be declared
    - parameter_influence: complete  # All parameters must be listed
    - side_effects: prohibited  # Or must be declared
    - dependency_ordering: topological  # Must respect DAG structure
```

### 2. Add Execution Trace Hashing

```yaml
operations:
  - id: op_inference
    type: ai_inference
    inputs: [prompt@1.0, model@3.0]
    outputs: [answer@1.0]
    execution_trace:
      trace_hash: sha256:abc123...  # Hash of actual execution log
      trace_uri: s3://logs/op_inference.log
      trace_format: opentelemetry_json
      verifier: did:svc:trace-verifier
```

### 3. Add Nondeterminism Declarations

```yaml
operations:
  - id: op_stochastic_inference
    type: ai_inference
    nondeterminism:
      sources:
        - random_seed: provided  # Seed=42
        - sampling: stochastic  # Temperature-based
        - cuda_ops: nondeterministic  # GPU floating-point
      reproducibility:
        expected: approximate  # Within 5% of original
        seed: 42
        rerun_allowed_until: 2026-01-01T00:00:00Z
```

### 4. Add Input Closure Validation

```python
# In validator
def validate_input_closure(operation):
    """Ensure all inputs are declared in provenance graph."""
    declared_inputs = set(operation.inputs)
    actual_inputs = detect_inputs_from_trace(operation.execution_trace)

    if actual_inputs != declared_inputs:
        raise ValidationError(
            f"Undeclared inputs detected: {actual_inputs - declared_inputs}"
        )
```

### 5. Add Side-Effect Declarations

```yaml
operations:
  - id: op_training
    type: model_training
    side_effects:
      - type: network_io
        destination: https://wandb.ai/logs
        purpose: metrics_logging
      - type: filesystem_write
        path: /tmp/checkpoints
        purpose: model_checkpointing
```

### 6. Create Reproducibility Guarantees

```yaml
operations:
  - id: op_deterministic
    type: computation
    reproducibility:
      guarantee: bit_exact  # Same inputs → same outputs (bitwise)
      verification:
        method: reproducible_rerun
        expected_output_hash: sha256:def456...
        rerun_verifier: did:svc:reproducibility-checker
```

---

## Implementation Plan

**Dependencies:**
- Execution trace format standardization (OpenTelemetry)

**Effort:** 4-6 weeks
- Weeks 1-2: Formal semantics specification
- Weeks 3-4: Validation logic implementation
- Weeks 5-6: Testing + documentation

**Deliverables:**
- [ ] Formal DAG semantics in specification
- [ ] Input closure validation
- [ ] Nondeterminism declaration support
- [ ] Side-effect declaration support
- [ ] Execution trace integration guide

---

## Success Criteria

A gap is considered "plugged" when:
- [ ] Formal semantics documented in spec
- [ ] Validators enforce input closure
- [ ] Nondeterminism can be declared and verified
- [ ] Side effects can be documented
- [ ] Legal teams accept provenance as evidence

---

## Known Limitations

**Cannot fully solve without TEE:**
- Execution trace validation requires trusted infrastructure
- See full analysis in [critical-gaps-FULL.md](../critical-gaps-FULL.md#3-execution-trace-validation)

**Inherent tradeoffs:**
- Perfect reproducibility vs practical operations
- Complete validation vs performance overhead
- See mitigation strategies in gap analysis

---

## Related Documentation

- [Roadmap v0.9](../roadmap.md#v090-jan-2027) - Formal semantics
- [Specification](../../specifications/main-spec.md) - Current semantics
- [Gaps Index](index.md) - All critical gaps

---

**Last Updated:** 2025-12-07
**Owner:** Verification working group
**Target Version:** v0.9.0 (Jan 2027)
