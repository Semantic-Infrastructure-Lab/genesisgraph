# Gap #4: Governance and Registry Infrastructure

**Priority:** 🟡 **HIGH**

**Status:** Planned for v0.8.0 (Nov 2026)

**Blocks:** Cross-organization interoperability, ecosystem sustainability

---

## The Problem

GenesisGraph assumes a world where tool metadata, profile validators, and schemas are available—but doesn't describe **how they are published, verified, versioned, curated, or deprecated**.

### Current Gaps

| Need | Current State | Gap |
|------|--------------|-----|
| **Tool Registry** | Ad-hoc DIDs | No canonical registry, no verification |
| **Profile Registry** | Namespace URLs | No actual hosting, no governance |
| **Schema Versioning** | Git tags | No formal compatibility guarantees |
| **Deprecation Process** | Undefined | No migration paths |
| **Curator Model** | Single maintainer | No sustainability plan |
| **Dispute Resolution** | None | No process for conflicts |

### Real-World Scenario

> **User:** "Where do I find the official `gg-ai-basic-v1` profile validator?"
>
> **Current Answer:** "Uh, check the GitHub repo?"
>
> **Enterprise Answer Needed:** "https://registry.genesisgraph.dev/profiles/gg-ai-basic-v1 (signed by did:org:genesisgraph-foundation)"

---

## Impact

**Who This Blocks:**
- Tool vendors needing official metadata hosting
- Organizations requiring verified profile validators
- SDK developers needing schema discovery
- Enterprises requiring governance documentation

**Use Cases Affected:**
- Multi-vendor integration
- Schema migration planning
- Compliance framework selection
- Registry-based tool verification

---

## Recommended Improvements

### 1. Define Registry Infrastructure

```yaml
registry_architecture:
  name: GenesisGraph Unified Registry
  components:
    - tool_registry:
        url: https://registry.genesisgraph.dev/tools
        backend: Rekor (Sigstore)
        authentication: DID-based
    - profile_registry:
        url: https://registry.genesisgraph.dev/profiles
        backend: Transparency log
        governance: Multi-stakeholder committee
    - schema_registry:
        url: https://registry.genesisgraph.dev/schemas
        versioning: Semver with compatibility metadata
```

### 2. Create Registry Publishing Process

```bash
# Tool vendor publishes tool metadata
gg registry publish tool \
  --did did:web:vendor.com \
  --metadata freecad-v0.21.2.json \
  --sign-with key.pem

# Registry returns transparency log entry
Published: https://registry.genesisgraph.dev/tools/freecad@0.21.2
Rekor entry: b64:abc123...
Merkle inclusion proof: b64:def456...
```

### 3. Define Governance Model

- **Registry Operators:** Multi-party witness network (similar to CT)
- **Change Control Board:** 9 members across industries (AI, manufacturing, science, government)
- **Voting Process:** 2/3 majority for breaking changes
- **Term Limits:** 3-year rotation
- **Dispute Resolution:** Escalation path to independent arbitrator

### 4. Schema Compatibility Guarantees

```yaml
schema_version: 0.2.0
compatibility:
  backward_compatible_with: [0.1.0, 0.1.1]
  forward_compatible_with: [0.2.1]
  breaking_changes: []
  deprecations:
    - field: operation.legacy_params
      deprecated_in: 0.2.0
      removed_in: 0.3.0
      replacement: operation.parameters
```

### 5. Create Foundation Governance Documents

- `GOVERNANCE.md` - Decision-making process
- `REGISTRY_OPERATIONS.md` - Registry SLA, security
- `COMPATIBILITY_POLICY.md` - Semver + migration guides
- `DISPUTE_RESOLUTION.md` - Conflict handling

---

## Implementation Plan

**Dependencies:**
- Domain registration (registry.genesisgraph.dev)
- Infrastructure setup (hosting, transparency logs)

**Effort:** 8-12 weeks
- Weeks 1-4: Registry infrastructure deployment
- Weeks 5-8: Governance documentation + processes
- Weeks 9-12: Testing + pilot programs

**Deliverables:**
- [ ] Registry infrastructure live
- [ ] Tool/profile/schema publishing working
- [ ] Governance documents published
- [ ] Multi-stakeholder committee formed
- [ ] Registry API documentation

---

## Success Criteria

A gap is considered "plugged" when:
- [ ] Registry infrastructure operational
- [ ] Publishing process documented and tested
- [ ] Governance model active (committee formed)
- [ ] 10+ tools/profiles published to registry
- [ ] Schema versioning with compatibility checks

---

## Related Documentation

- [Roadmap v0.8](../roadmap.md#v080-nov-2026) - Registry implementation
- [Gap #8: Anti-Capture](08-incentives-anti-capture.md) - Governance context
- [Gaps Index](index.md) - All critical gaps

---

**Last Updated:** 2025-12-07
**Owner:** Infrastructure working group
**Target Version:** v0.8.0 (Nov 2026)
