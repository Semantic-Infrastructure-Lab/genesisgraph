# Chapter 5: Identity & Signing

**Status:** 📝 To be written in v0.4

**Purpose:** DID resolution, cryptographic signatures, and key management

---

## Planned Content

This chapter will cover:

- **DID Resolution**
  - Supported DID methods (did:key, did:web, did:ion, did:ethr)
  - Resolution logic and caching
  - Fallback strategies

- **Signature Generation**
  - Ed25519 signatures
  - Key generation and storage
  - Signature formats

- **Signature Verification**
  - Verifying Ed25519 signatures
  - Public key extraction from DIDs
  - Revocation checking

- **Key Management**
  - Key storage best practices
  - Hardware security modules (HSM)
  - Key rotation strategies

---

## Temporary Reference

Until this chapter is written, see:
- [DID Web Guide](../../user-guide/did-web-guide.md) - DID:web setup
- [Security Guide](../../developer-guide/security.md) - Security best practices
- [Python Identity Module](https://github.com/scottsen/genesisgraph/blob/main/genesisgraph/identity.py) - Reference implementation

---

## Contributing

Want to help write this chapter? See [Contributing Guide](../../developer-guide/contributing.md)

---

**Last Updated:** 2025-12-07
**Target:** v0.4.0
**See:** [SDK Guide Index](index.md) | [← Prev: Selective Disclosure](04-selective-disclosure.md) | [Next: Transparency Logs →](06-transparency-logs.md)
