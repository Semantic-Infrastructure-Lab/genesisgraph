# SDK Development Guide

**📍 This guide has been reorganized for better navigation**

The complete SDK development guide (formerly 1368 lines) has been split into focused chapters.

---

## Quick Navigation

**Start here:** [sdk-guide/index.md](sdk-guide/index.md)

**Chapters:**
1. [Quick Start](sdk-guide/01-quick-start.md) - 30-minute overview
2. [Core Data Model](sdk-guide/02-data-model.md) - Entities, Operations, Tools, Attestations
3. [Validation & Schema](sdk-guide/03-validation.md) - Schema validation, error handling
4. [Selective Disclosure](sdk-guide/04-selective-disclosure.md) - A/B/C levels, Merkle trees
5. [Identity & Signing](sdk-guide/05-identity-signing.md) - DID resolution, signatures
6. [Transparency Logs](sdk-guide/06-transparency-logs.md) - RFC 6962 integration
7. [Profiles & Extensions](sdk-guide/07-profiles.md) - Industry-specific validators
8. [Integration Patterns](sdk-guide/08-integration-patterns.md) - CI/CD, APIs, plugins

---

## Why Reorganized?

**Before:**
- ❌ 1368 lines in one file (45+ minutes to read)
- ❌ Hard to find specific topics
- ❌ Overwhelming for newcomers

**After:**
- ✅ 8 focused chapters (~170 lines each)
- ✅ Progressive learning path
- ✅ Easy to reference specific topics
- ✅ Better for incremental study

---

## Implementation Checklist

### Minimum Viable SDK (v0.1)
- [ ] Parse YAML/JSON GenesisGraph documents
- [ ] Validate against JSON Schema
- [ ] Basic entity/operation/tool builders
- [ ] Export to YAML/JSON

**Estimated:** 2-3 weeks | **Reference:** [Quick Start](sdk-guide/01-quick-start.md)

### Production SDK (v0.5)
- [ ] DID resolution (did:key, did:web)
- [ ] Ed25519 signature verification
- [ ] SHA256/SHA512 hash verification
- [ ] Level A/B selective disclosure
- [ ] Comprehensive tests (>80% coverage)

**Estimated:** 4-6 weeks | **Reference:** [Full guide](sdk-guide/index.md)

### Enterprise SDK (v1.0)
- [ ] Transparency log integration (RFC 6962)
- [ ] Level C sealed subgraphs
- [ ] Profile validators
- [ ] Security audit

**Estimated:** 8-12 weeks | **Reference:** [Integration Patterns](sdk-guide/08-integration-patterns.md)

---

## Quick Reference

**Need code examples?** [SDK Quick Reference](sdk-quick-reference.md)

**Building in Python?** See [genesisgraph/builder.py](https://github.com/scottsen/genesisgraph/blob/main/genesisgraph/builder.py)

**Building in JavaScript?** See [@genesisgraph/sdk](https://www.npmjs.com/package/@genesisgraph/sdk)

**Compliance tests?** [github.com/genesisgraph/compliance-tests](https://github.com/genesisgraph/compliance-tests)

---

## Community

**Questions?** [GitHub Discussions](https://github.com/scottsen/genesisgraph/discussions)

**Building an SDK?** Let us know! We'll list it in the ecosystem and provide support.

---

**Full Guide:** [sdk-guide/index.md](sdk-guide/index.md)

**Original Document (Archived):** Available on request

**Last Updated:** 2025-12-07
**Version:** v0.3.0
