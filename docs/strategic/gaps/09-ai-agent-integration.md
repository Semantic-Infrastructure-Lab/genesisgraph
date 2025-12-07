# Gap #9: Integration with Delegated AI Agents

**Priority:** 🔴 **CRITICAL**

**Status:** Planned for v0.7.0 (Aug 2026)

**Blocks:** Agentic AI deployments, autonomous systems

---

## The Problem

GenesisGraph defines provenance for:
- Discrete outputs (files, datasets, responses)
- Discrete operations (transformations)

But **AI agents operate continuously**, not as discrete workflows:
- Multi-turn conversations
- Tool use across sessions
- Memory updates over time
- Reasoning traces with intermediate steps

### Current Gap

```yaml
# ❌ GenesisGraph can't express:
# - Agent decision traces
# - Multi-turn conversation provenance
# - Tool delegation by agents
# - Agent memory updates
# - Safety/alignment certifications
# - Chain-of-thought provenance
```

**This is the most important gap for AI governance.**

---

## Impact

**Who This Blocks:**
- AI agent developers
- AI safety researchers
- Organizations deploying autonomous agents
- Regulators evaluating AI systems

**Use Cases Affected:**
- Autonomous agent auditing
- AI safety certification
- Multi-agent collaboration tracking
- Regulatory compliance for AI systems

---

## Recommended Improvements

### 1. Create Agent Provenance Extension (GG-Agent-v1)

```yaml
spec_version: 0.2.0
profile: gg-agent-v1

agents:
  - id: assistant_alpha
    type: AIAgent
    model: claude-sonnet-4
    vendor: Anthropic
    identity:
      did: did:agent:assistant-alpha-session-001
    capabilities:
      tools: [web_search, calculator, code_execution]
      memory: contextual_window_200k
      reasoning: chain_of_thought
    delegation:
      delegated_by: did:person:user_jane
      credential: vc:agent-delegation-2025
      constraints:
        max_cost_usd: 10.00
        allowed_tools: [web_search, calculator]
        prohibited_actions: [file_write, network_external]
```

### 2. Add Agent Operation Types

```yaml
operations:
  - id: op_agent_reasoning
    type: agent_reasoning_step
    agent: assistant_alpha
    inputs:
      - user_message@turn_5
      - memory_context@turn_1_to_4
    outputs:
      - reasoning_trace@turn_5
      - tool_invocations@turn_5
    reasoning:
      method: chain_of_thought
      steps:
        - step: 1
          thought: "User wants to calculate mortgage payment"
          disclosure: visible
        - step: 2
          thought: "Need current interest rates"
          tool_call:
            tool: web_search
            query: "30-year mortgage rates 2025"
          disclosure: visible
        - step: 3
          thought: "[REDACTED - proprietary prompt engineering]"
          disclosure: sealed
          commitment: sha256:abc123...
    attestation:
      mode: verifiable
      signer: did:model:claude-sonnet-4
      timestamp: 2025-11-20T15:30:22Z
```

### 3. Add Agent State Checkpoints

```yaml
entities:
  - id: agent_state_checkpoint
    type: AgentMemorySnapshot
    version: turn_10
    hash: sha256:state_hash_turn_10...
    derived_from:
      - agent_state_checkpoint@turn_9
      - user_message@turn_10
      - tool_results@turn_10
    contents:
      conversation_history: encrypted_blob_1
      working_memory: encrypted_blob_2
      long_term_facts: encrypted_blob_3
    encryption:
      method: age_encryption
      recipients: [did:person:user_jane]
```

### 4. Add Delegation Provenance

```yaml
operations:
  - id: op_agent_tool_use
    type: agent_tool_invocation
    agent: assistant_alpha
    tool: web_search@2.1.0
    delegation_chain:
      - grantor: did:person:user_jane
        grantee: did:agent:assistant-alpha
        capability: use_tools
        constraints:
          allowed_tools: [web_search, calculator]
      - grantor: did:agent:assistant-alpha
        grantee: did:svc:brave-search
        capability: search_query
        constraints:
          max_queries_per_day: 100
    inputs: [search_query@turn_5]
    outputs: [search_results@turn_5]
    policy_evaluation:
      policy: user-agent-safety-v1
      decision: permit
      reason: "Tool in allowed list, under rate limit"
```

### 5. Add Safety/Alignment Attestations

```yaml
attestations:
  - id: alignment_certification
    type: safety_evaluation
    target: assistant_alpha
    claims:
      - property: refusal_of_harmful_requests
        result: pass
        test_suite: anthropic_safety_v2
        test_date: 2025-11-01T00:00:00Z
      - property: jailbreak_resistance
        result: pass
        test_suite: harmbench_v1
      - property: goal_alignment
        result: verified
        evaluator: did:org:anthropic-safety-team
    attestation:
      signer: did:org:anthropic
      signature: ed25519:safety_cert_sig...
      valid_until: 2026-11-01T00:00:00Z
```

### 6. Add Redacted Reasoning Traces

```yaml
operations:
  - id: op_reasoning_private
    type: agent_reasoning_step
    reasoning:
      disclosure_level: selective
      visible_steps:
        - "Analyzing user request for personal finance advice"
        - "Checking if request falls within authorized domain"
        - "Request approved, proceeding with calculation"
      sealed_steps:
        commitment: sha256:reasoning_merkle_root...
        num_steps_sealed: 7
        policy_claims:
          - claim: "No personal data logged"
            result: verified
          - claim: "Reasoning aligned with user values"
            result: verified
```

---

## Implementation Plan

**Dependencies:**
- Gap #2: Agent delegation framework

**Effort:** 8-12 weeks
- Weeks 1-3: Agent extension spec design
- Weeks 4-6: Pilot implementation with 1 AI lab
- Weeks 7-9: Reasoning trace + safety attestations
- Weeks 10-12: Testing + documentation

**Deliverables:**
- [ ] `gg-agent-v1` profile specification
- [ ] Agent operation types in schema
- [ ] Pilot implementation (with 1 AI lab)
- [ ] Safety attestation framework
- [ ] Agent provenance guide

---

## Success Criteria

A gap is considered "plugged" when:
- [ ] Agent operations representable in provenance
- [ ] Multi-turn conversations can be traced
- [ ] Reasoning traces support selective disclosure
- [ ] Safety attestations verifiable
- [ ] Real-world AI agent deployment using framework

---

## Known Challenges

**Technical Novelty:**
- No existing standard to reference
- Moving target (AI safety standards evolving)
- Partnership-dependent (requires AI lab collaboration)

**Partial Solutions:**
- ✅ Can capture agent operations (tool use, delegation)
- ✅ Can record reasoning traces with selective disclosure
- ⚠️ Safety/alignment attestations require trusted evaluators
- ⚠️ Continuous agent behavior hard to represent in discrete graph
- ❌ Can't verify agent's internal reasoning without model access

**Risk Level:** 🔴 VERY HIGH (novel + partnership-dependent)

**Mitigation:**
- Partner with one AI lab for pilot
- Start with simpler use cases (single-turn tool use)
- Iterate based on real-world deployments
- Build on delegation framework (Gap #2)

---

## Related Documentation

- [Roadmap v0.7](../roadmap.md#v070-aug-2026) - AI agent integration
- [Gap #2: Delegation](02-delegation-authorization.md) - Foundation for agents
- [Gaps Index](index.md) - All critical gaps

---

**Last Updated:** 2025-12-07
**Owner:** AI governance working group
**Target Version:** v0.7.0 (Aug 2026)
