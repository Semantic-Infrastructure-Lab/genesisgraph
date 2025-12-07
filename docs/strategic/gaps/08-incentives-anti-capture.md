# Gap #8: Incentive and Anti-Capture Design

**Priority:** 🔴 **CRITICAL**

**Status:** Planned for v0.8.0 (Nov 2026)

**Blocks:** Public infrastructure, decentralized deployments, long-term sustainability

---

## The Problem

GenesisGraph is **so powerful** that large actors will attempt to capture or fork it:

- **Cloud providers** (AWS, Azure, GCP) - Could create proprietary extensions
- **AI labs** (OpenAI, Anthropic, Google) - Could fork for competitive advantage
- **Aerospace primes** (Boeing, Lockheed) - Could create closed variants
- **Defense contractors** - Could classify portions

### Missing

- Public-goods funding model
- Rotation and term limits for maintainers
- Multi-stakeholder governance
- Anti-capture guardrails
- "Forkability norms" (like W3C DID Core)
- Independent electors or voting councils

### Historical Examples of Capture

- **OpenAPI Specification** → Swagger → SmartBear (partially captured)
- **Kubernetes** → Google influence → CNCF (escaped capture)
- **RSS** → Fragmentation → Dead
- **ActivityPub** → W3C process → Survived

---

## Impact

**Who This Blocks:**
- Independent organizations requiring vendor neutrality
- Public sector deployments
- Academic researchers
- Small/medium businesses

**Use Cases Affected:**
- Government procurement (requires open governance)
- Academic research (requires stable spec)
- Multi-vendor ecosystems
- Long-term institutional adoption

---

## Recommended Improvements

### 1. Create Multi-Stakeholder Governance

```yaml
governance_structure:
  foundation: GenesisGraph Foundation (501c6 nonprofit)
  board_composition:
    - seats_industry_ai: 2
    - seats_industry_manufacturing: 2
    - seats_industry_science: 2
    - seats_academia: 1
    - seats_government: 1
    - seats_civil_society: 1
  total_seats: 9
  term_limits: 3_years
  rotation: staggered_thirds
  voting_threshold:
    normal_changes: simple_majority
    breaking_changes: two_thirds
    governance_changes: three_quarters
```

### 2. Define Anti-Capture Rules

```markdown
## Anti-Capture Guardrails

1. **No Single-Entity Control**
   - No organization may hold >2 board seats
   - No organization may employ >30% of core maintainers

2. **Vendor Neutrality**
   - Reference implementations must be Apache 2.0
   - No proprietary extensions in core spec
   - All extensions must be public

3. **Fork Rights**
   - Spec licensed CC-BY 4.0 (unforkable copyright)
   - Trademark policy: "GenesisGraph" name protected
   - Compatible forks must use different name

4. **Transparency Requirements**
   - All meetings recorded and published
   - All votes public with rationale
   - Funding sources disclosed annually
```

### 3. Create Funding Model

```yaml
funding_sources:
  membership_dues:
    - platinum: $50k/year (2 votes in technical steering)
    - gold: $25k/year (1 vote)
    - silver: $10k/year (participation rights)
  grants:
    - government_research: $500k/year (NSF, NIST)
    - foundation_support: $200k/year (Sloan, Schmidt)
  services:
    - registry_hosting: $100k/year (cost recovery)
    - certification_program: $50k/year (vendor certifications)
total_annual_budget: $1M+
```

### 4. Define Succession Planning

- Lead maintainer: 2-year renewable term (max 3 terms)
- Technical steering committee: 9 members, staggered 3-year terms
- Emergency procedures for maintainer absence
- Fork procedures if foundation fails

### 5. Create Compatibility Certification

```bash
# Vendors can get "GenesisGraph Compatible" certification
gg certify-implementation \
  --implementation vendor-provenance-tool \
  --version 1.2.0 \
  --submit-to-foundation

# Foundation runs conformance tests
# Issues certification: "GenesisGraph Compatible v0.3"
```

### 6. Establish Trademark Policy

- "GenesisGraph" name controlled by foundation
- Compatible implementations: "XYZ for GenesisGraph"
- Incompatible forks: Must use different name
- Enforcement via community pressure, not lawsuits

---

## Implementation Plan

**Dependencies:**
- Legal entity formation (nonprofit incorporation)
- Initial funding secured
- Founding board members committed

**Effort:** 12-16 weeks
- Weeks 1-4: Legal entity formation (501c6)
- Weeks 5-8: Governance documentation
- Weeks 9-12: Founding member recruitment
- Weeks 13-16: Initial funding + launch

**Deliverables:**
- [ ] Foundation legally established
- [ ] Governance documents published
- [ ] Founding board elected (9 members)
- [ ] Initial funding secured ($500k+)
- [ ] Trademark policy active

---

## Success Criteria

**Organizational:**
- [ ] Nonprofit foundation operational
- [ ] Multi-stakeholder board active (9 seats, 5+ orgs)
- [ ] Governance documents published and followed
- [ ] Annual budget >$500k from diverse sources
- [ ] No single entity controls >25% of decision-making

**Technical:**
- [ ] Anti-capture rules enforced
- [ ] Transparency requirements met (meeting recordings, vote records)
- [ ] Certification program active
- [ ] Trademark policy protecting name

---

## Known Challenges

**Organizational Barriers:**
- Requires 3-5 founding organizations with aligned interests
- Legal complexity (nonprofit formation, international governance)
- Sustained funding commitment ($1M+ annually)
- Community buy-in and trust

**Risk Level:** 🔴 VERY HIGH (organizational, not technical)

**Mitigation:**
- Start with informal steering committee
- Formalize governance incrementally as ecosystem grows
- Build community consensus before foundation formation
- Secure diverse funding sources early

---

## Related Documentation

- [Roadmap v0.8](../roadmap.md#v080-nov-2026) - Governance establishment
- [Gap #4: Registry](04-governance-registry.md) - Infrastructure governance
- [Gap #10: Economic Model](10-economic-value-flows.md) - Funding mechanisms
- [Gaps Index](index.md) - All critical gaps

---

**Last Updated:** 2025-12-07
**Owner:** Foundation working group
**Target Version:** v0.8.0 (Nov 2026)
