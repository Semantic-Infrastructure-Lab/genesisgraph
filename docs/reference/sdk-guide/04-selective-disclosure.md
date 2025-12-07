# Chapter 4: Selective Disclosure

**Status:** 📝 To be written in v0.4

**Purpose:** Implementing A/B/C disclosure levels, Merkle trees, and sealed subgraphs

---

## Planned Content

This chapter will cover:

- **Disclosure Levels**
  - Level A: Full disclosure
  - Level B: Partial disclosure (redacted parameters)
  - Level C: Sealed subgraphs (Merkle commitments)

- **Merkle Tree Implementation**
  - Building Merkle trees
  - Generating inclusion proofs
  - Verification logic

- **Sealed Subgraphs**
  - Creating sealed subgraphs
  - TEE attestation integration
  - Verification without revelation

- **Claim Envelopes**
  - Policy claims without parameter disclosure
  - Claim verification
  - Trust model

---

## Temporary Reference

Until this chapter is written, see:
- [Disclosure Levels Guide](../../user-guide/disclosure-levels.md) - User-facing overview
- [Selective Disclosure Guide](../../user-guide/selective-disclosure.md) - Detailed concepts
- [Python SD-JWT Implementation](https://github.com/scottsen/genesisgraph/blob/main/genesisgraph/credentials/sd_jwt.py) - Reference code

---

## Contributing

Want to help write this chapter? See [Contributing Guide](../../developer-guide/contributing.md)

---

**Last Updated:** 2025-12-07
**Target:** v0.4.0
**See:** [SDK Guide Index](index.md) | [← Prev: Validation](03-validation.md) | [Next: Identity & Signing →](05-identity-signing.md)
