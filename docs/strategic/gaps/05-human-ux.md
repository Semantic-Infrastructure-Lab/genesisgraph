# Gap #5: Human-Oriented UX Patterns

**Priority:** 🟡 **HIGH**

**Status:** Planned for v0.9.0 (Jan 2027)

**Blocks:** Mainstream adoption, regulatory auditors, compliance officers

---

## The Problem

GenesisGraph is **technically complete** but **UX-incomplete**.

For mainstream users (engineers, manufacturers, scientists, compliance officers), the current documentation assumes deep cryptography knowledge.

### User Confusion Examples

1. **"How do I prove a thing happened without revealing my IP?"**
   - Current: "Read §9.2 on selective disclosure, choose Level B or C, implement Merkle commitments..."
   - Needed: `gg template create --pattern sealed-manufacturing`

2. **"How do I redact parameters safely?"**
   - Current: "Set `_redacted: true` and create claim envelopes..."
   - Needed: `gg redact workflow.gg.yaml --keep-claims --hide-params`

3. **"What will be revealed before I sign?"**
   - Current: Manual review of YAML
   - Needed: `gg preview-disclosure workflow.gg.yaml --level B`

4. **"What is a sealed subgraph vs partial disclosure?"**
   - Current: Read 886-line spec
   - Needed: 2-minute interactive tutorial

---

## Impact

**Who This Blocks:**
- Non-cryptographer engineers implementing provenance
- Compliance officers reviewing workflows
- Manufacturers needing quick templates
- Decision-makers evaluating adoption

**Use Cases Affected:**
- Rapid prototyping (hours vs days)
- Compliance officer self-service
- Non-technical stakeholder review
- Adoption by small/medium businesses

---

## Recommended Improvements

### 1. Create Opinionated Templates

```bash
gg template list
# Available templates:
# - ai-inference-basic
# - ai-inference-redacted
# - manufacturing-iso9001
# - manufacturing-sealed-cam
# - science-reproducible-figure
# - agent-delegation-audit

gg template create ai-inference-redacted \
  --output my-workflow.gg.yaml \
  --model llama3-70b \
  --hide-prompts

# Generates pre-configured Level B template
```

### 2. Create Interactive CLI

```bash
gg init
# 🎯 What are you trying to prove?
# 1. AI pipeline with hidden prompts
# 2. Manufacturing compliance without revealing toolpaths
# 3. Scientific reproducibility
# 4. Multi-agent delegation audit
# Choose [1-4]: 1

# ✅ Template: ai-inference-redacted
# 🔒 Privacy level: B (parameters hidden, claims visible)
# 📝 Created: workflow.gg.yaml
```

### 3. Create Disclosure Preview Tool

```bash
gg preview workflow.gg.yaml --persona auditor

# 👁️ What an auditor will see:
# ✅ Policy compliance claims: temperature ≤ 0.3 ✓
# ✅ Human reviewer: did:person:dr_sarah_chen
# ✅ Model version: llama3-70b@3.0
# ❌ Exact prompt: HIDDEN
# ❌ Fine-tuning details: HIDDEN
# ❌ Retrieval strategy: HIDDEN
```

### 4. Create Profile Wizards

```bash
gg profile wizard manufacturing

# 🏭 Manufacturing Profile Setup
# Industry standard: [ISO-9001 / AS9100D / FDA-21CFR / Custom]
# Choose: ISO-9001

# Required attestations:
# ✓ Calibration certificates
# ✓ Material traceability
# ✓ QC inspection
# ✓ Human approver signature

# IP protection needed? [yes/no]: yes
# → Using Level C (sealed subgraph)
```

### 5. Create Best-Practice Guides

- `docs/guides/HOW_TO_REDACT_SAFELY.md`
- `docs/guides/MULTISIG_BEST_PRACTICES.md`
- `docs/guides/SEALED_SUBGRAPH_TUTORIAL.md`
- `docs/guides/TRANSPARENCY_LOG_SETUP.md`

### 6. Create Video Tutorials

- "5-minute intro to GenesisGraph"
- "Proving AI work without revealing prompts"
- "Manufacturing compliance with IP protection"
- "Setting up multi-party attestations"

---

## Implementation Plan

**Dependencies:**
- CLI implementation (basic features exist in v0.3)

**Effort:** 6-8 weeks
- Weeks 1-2: Template system + interactive init
- Weeks 3-4: Disclosure preview tool + profile wizards
- Weeks 5-6: Best-practice guides
- Weeks 7-8: Video tutorials + user testing

**Deliverables:**
- [ ] 6+ opinionated templates
- [ ] Interactive CLI (`gg init`, `gg preview`)
- [ ] Profile wizard system
- [ ] 4+ best-practice guides
- [ ] 4+ video tutorials (5-10 min each)

---

## Success Criteria

A gap is considered "plugged" when:
- [ ] Non-cryptographers can create provenance in <1 hour
- [ ] Compliance officers can review without technical help
- [ ] User testing shows 80%+ task completion
- [ ] Video tutorials have 1000+ views
- [ ] Templates used in 50%+ of new projects

---

## Related Documentation

- [Roadmap v0.9](../roadmap.md#v090-jan-2027) - UX improvements
- [Quickstart Guide](../../getting-started/quickstart.md) - Current getting started
- [Gaps Index](index.md) - All critical gaps

---

**Last Updated:** 2025-12-07
**Owner:** UX working group
**Target Version:** v0.9.0 (Jan 2027)
