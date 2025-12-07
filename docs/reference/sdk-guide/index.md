# SDK Development Guide

**Purpose:** Complete reference for building GenesisGraph SDK libraries

**Version:** v0.3.0
**Audience:** SDK developers implementing GenesisGraph in new languages

---

## Quick Navigation

**New to GenesisGraph?** Start with [Getting Started](../../getting-started/quickstart.md)

**Building an SDK?** Follow this guide sequentially

**Need quick reference?** See [SDK Quick Reference](../sdk-quick-reference.md)

---

## Guide Structure

This guide is organized progressively from basics to advanced features:

### Part 1: Fundamentals

1. [**Quick Start**](01-quick-start.md)
   *30-minute overview: data model, validation, examples*
   **Start here** if you're new to SDK development

2. [**Core Data Model**](02-data-model.md)
   *Entities, Operations, Tools, Attestations - the four pillars*
   **Essential** for all SDK implementations

3. [**Validation & Schema**](03-validation.md)
   *Schema validation, error handling, validation results*
   **Required** for spec compliance

### Part 2: Advanced Features

4. [**Selective Disclosure**](04-selective-disclosure.md)
   *A/B/C disclosure levels, Merkle trees, sealed subgraphs*
   **Core innovation** - critical for regulated use cases

5. [**Identity & Signing**](05-identity-signing.md)
   *DID resolution, cryptographic signatures, key management*
   **Security critical** - implements trust model

6. [**Transparency Logs**](06-transparency-logs.md)
   *RFC 6962 integration, inclusion proofs, Rekor/Trillian*
   **Auditability** - enables public verification

### Part 3: Ecosystem Integration

7. [**Profiles & Extensions**](07-profiles.md)
   *Industry-specific validators (AI, CAM, FDA, ISO 9001)*
   **Domain customization** - adapts to specific industries

8. [**Integration Patterns**](08-integration-patterns.md)
   *CI/CD, API wrappers, tool plugins, common architectures*
   **Real-world deployment** - practical integration strategies

---

## SDK Implementation Checklist

### Minimum Viable SDK (v0.1)

- [ ] Parse YAML/JSON GenesisGraph documents
- [ ] Validate against JSON Schema
- [ ] Basic entity/operation/tool builders
- [ ] Export to YAML/JSON
- [ ] CLI wrapper (optional)

**Estimated effort:** 2-3 weeks
**Reference:** Python SDK core (genesisgraph/builder.py, validator.py)

### Production SDK (v0.5)

- [ ] DID resolution (did:key, did:web minimum)
- [ ] Ed25519 signature generation/verification
- [ ] SHA256/SHA512 hash verification
- [ ] Level A/B selective disclosure
- [ ] Comprehensive test suite (>80% coverage)

**Estimated effort:** 4-6 weeks
**Reference:** Python SDK (full feature set)

### Enterprise SDK (v1.0)

- [ ] Transparency log integration (RFC 6962)
- [ ] Level C sealed subgraphs (Merkle trees)
- [ ] BBS+ signatures (optional)
- [ ] Profile validators (AI Basic, CAM, etc.)
- [ ] Performance optimizations
- [ ] Security audit

**Estimated effort:** 8-12 weeks
**Reference:** Python SDK v1.0 (future)

---

## Language-Specific Considerations

### Python
**Reference Implementation:** [github.com/scottsen/genesisgraph](https://github.com/scottsen/genesisgraph)
- Use `pydantic` for data validation
- `cryptography` library for signatures
- `jsonschema` for schema validation
- See [Python SDK source](https://github.com/scottsen/genesisgraph/tree/main/genesisgraph)

### JavaScript/TypeScript
**Implementation:** [@genesisgraph/sdk](https://www.npmjs.com/package/@genesisgraph/sdk)
- Use `zod` or `joi` for validation
- `tweetnacl` or `@noble/ed25519` for signatures
- `ajv` for schema validation
- See [TypeScript SDK](https://github.com/genesisgraph/genesisgraph-ts)

### Rust
**Status:** Planned (community contribution welcome)
- Use `serde` for serialization
- `ed25519-dalek` for signatures
- `jsonschema` crate for validation

### Go
**Status:** Planned (community contribution welcome)
- Use `encoding/json` for serialization
- `golang.org/x/crypto/ed25519` for signatures
- `gojsonschema` for validation

---

## Testing Your SDK

### Compliance Test Suite

We provide a **cross-language compliance test suite** with golden test files:

```bash
# Clone the test suite
git clone https://github.com/genesisgraph/compliance-tests

# Run against your SDK
./run-tests.sh --sdk=your-sdk-name
```

**Test Coverage:**
- 50+ valid GenesisGraph documents (must parse successfully)
- 30+ invalid documents (must reject with specific errors)
- 20+ cryptographic test vectors (signatures, hashes)
- 10+ selective disclosure scenarios

### Minimum Passing Criteria

Your SDK must:
1. ✅ Parse all valid examples in `examples/`
2. ✅ Reject all invalid examples in `compliance-tests/invalid/`
3. ✅ Verify all signatures in `compliance-tests/crypto/`
4. ✅ Match expected validation errors (error codes + messages)

---

## Community & Support

**Questions?** [GitHub Discussions](https://github.com/scottsen/genesisgraph/discussions)

**Found a bug in the spec?** [Report an issue](https://github.com/scottsen/genesisgraph/issues)

**Building an SDK?** Let us know! We'll:
- List it in the official ecosystem
- Provide technical support
- Help with testing and validation

---

## Related Documentation

- [Main Specification](../../specifications/main-spec.md) - Normative spec (MUST read)
- [SDK Quick Reference](../sdk-quick-reference.md) - Code patterns cheat sheet
- [Implementation Summary](../implementation-summary.md) - Feature matrix
- [Security Considerations](../../developer-guide/security.md) - Security best practices

---

**Next Step:** Read [Quick Start](01-quick-start.md) to begin SDK development

**Last Updated:** 2025-12-07
**Spec Version:** v0.3.0
