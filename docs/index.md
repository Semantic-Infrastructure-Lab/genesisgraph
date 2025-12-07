# GenesisGraph Documentation

**An open standard for cryptographically proving how things were made.**

GenesisGraph enables verifiable provenance across AI pipelines, manufacturing, scientific research, healthcare, and supply chains—solving the "certification vs IP protection" dilemma through selective disclosure.

## Why GenesisGraph?

Traditional documentation can be edited. GenesisGraph provides:

✅ **Cryptographic Proof** - Hashes, signatures, timestamps prevent tampering
✅ **Selective Disclosure** - Prove compliance without revealing trade secrets
✅ **Machine Verification** - Auditors validate automatically
✅ **Universal Format** - Works across tools, organizations, industries
✅ **Progressive Trust** - Start simple, add cryptography when needed

## Core Innovation: A/B/C Disclosure Levels

| Level | What You Share | Use When |
|-------|---------------|----------|
| **A: Full** | All details visible | Internal audits, open research |
| **B: Partial** | Policy claims visible, parameters hidden | Regulatory compliance |
| **C: Sealed** | Merkle commitments + TEE | High-value IP, supply chains |

**Example:** Prove ISO 9001 compliance without revealing manufacturing toolpaths, or AI safety compliance without exposing proprietary prompts.

**Learn more:** [Disclosure Levels Guide](user-guide/disclosure-levels.md)  

## Quick Links — Organized by Incremental Reveal

<div class="grid cards" markdown>

-   :material-clock-fast:{ .lg .middle } __Layer 1: Getting Started__

    ---

    5-minute tutorial and understand the A/B/C disclosure model

    [:octicons-arrow-right-24: Quickstart](getting-started/quickstart.md)
    [:octicons-arrow-right-24: Disclosure Levels](user-guide/disclosure-levels.md)

-   :material-book-open-variant:{ .lg .middle } __Layer 2: User Guide__

    ---

    Learn features, see examples, and find answers

    [:octicons-arrow-right-24: User Guide](user-guide/overview.md)
    [:octicons-arrow-right-24: Use Cases](use-cases.md)
    [:octicons-arrow-right-24: FAQ](faq.md)

-   :material-code-braces:{ .lg .middle } __Layer 3: Technical Depth__

    ---

    Architecture, specifications, and SDK reference

    [:octicons-arrow-right-24: Architecture](developer-guide/architecture.md)
    [:octicons-arrow-right-24: Main Spec](specifications/main-spec.md)
    [:octicons-arrow-right-24: SDK Reference](reference/sdk-quick-reference.md)

-   :material-strategy:{ .lg .middle } __Layer 4: Strategic Context__

    ---

    Vision, roadmap, and planning for decision-makers

    [:octicons-arrow-right-24: Vision](strategic/vision.md)
    [:octicons-arrow-right-24: Roadmap](strategic/roadmap.md)
    [:octicons-arrow-right-24: Critical Gaps](strategic/critical-gaps.md)

</div>

## The Innovation: Selective Disclosure

GenesisGraph solves the **"certification vs IP protection" dilemma** with three disclosure levels:

| Level | Description | Use When |
|-------|-------------|----------|
| **Level A: Full Disclosure** | All details visible | Internal audits, research collaboration |
| **Level B: Partial Envelope** | Policy claims visible, parameters hidden | Regulatory compliance |
| **Level C: Sealed Subgraph** | Merkle commitments + TEE attestations | High-value IP, supply chains |

This enables proving **ISO 9001 compliance without revealing manufacturing toolpaths**, or **AI safety compliance without exposing proprietary prompts**.

## Installation

=== "Python"

    ```bash
    pip install genesisgraph
    ```

=== "JavaScript/TypeScript"

    ```bash
    npm install @genesisgraph/sdk
    ```

=== "CLI Tool"

    ```bash
    pip install genesisgraph[cli]
    gg --version
    ```

## Simple Example

```python
from genesisgraph import GenesisGraph, Entity, Operation, Tool

# Create a document
gg = GenesisGraph(spec_version="0.1.0")

# Add entities
input_data = Entity(id="data", type="Dataset", version="1", file="./data.csv")
gg.add_entity(input_data)

# Add operations
transform = Operation(
    id="process",
    type="transformation",
    inputs=["data"],
    outputs=["result"]
)
gg.add_operation(transform)

# Export
gg.save_yaml("workflow.gg.yaml")
```

Validate:

```bash
gg validate workflow.gg.yaml
# ✓ Validation PASSED
```

## Use Cases by Industry

<div class="grid cards" markdown>

-   :material-robot:{ .lg .middle } __AI Pipelines__

    ---

    Prove how AI models generated outputs, with selective disclosure of prompts

    [:octicons-arrow-right-24: See AI Examples](use-cases.md#ai-pipelines)

-   :material-cube-outline:{ .lg .middle } __Manufacturing__

    ---

    ISO 9001 compliance with sealed CAM toolpaths

    [:octicons-arrow-right-24: See Manufacturing](use-cases.md#manufacturing)

-   :material-flask:{ .lg .middle } __Scientific Research__

    ---

    Reproducible research with full parameter disclosure

    [:octicons-arrow-right-24: See Research](use-cases.md#scientific-research)

</div>

**See the complete [Use Cases & Integration Guide](use-cases.md) for code examples and integration patterns.**

## Community & Support

- **GitHub**: [github.com/scottsen/genesisgraph](https://github.com/scottsen/genesisgraph)
- **Issues**: [Report bugs](https://github.com/scottsen/genesisgraph/issues)
- **Discussions**: [Community forum](https://github.com/scottsen/genesisgraph/discussions)

## Next Steps

1. **New users**: Start with the [Quickstart Guide](getting-started/quickstart.md)
2. **Developers**: Read the [Architecture Documentation](developer-guide/architecture.md)
3. **Enterprise**: Review [Security Considerations](developer-guide/security.md)
4. **Researchers**: See the [Main Specification](specifications/main-spec.md)

---

**Current Version:** v0.3.0  
**License:** Apache 2.0 (code), CC-BY 4.0 (specification)
