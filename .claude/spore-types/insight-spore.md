# Insight spore format

Insight spores carry compressed pattern discoveries that only became visible through dreaming. They represent knowledge that raw analysis couldn't surface, knowledge that emerged from the compression process itself.

## When to create

An insight becomes a spore candidate when:
- Confidence is above 0.75
- The insight is not specific to local implementation details
- The insight has been validated against at least one subsequent observation
- The encoded pattern would be useful to colonies working in similar domains

## Format

```yaml
---
spore_type: insight
spore_id: SPORE-INS-{NNN}
origin_colony: [colony ID]
origin_dream: DRM-{NNN}
origin_insight: I-{NNN}
timestamp: [ISO timestamp]
signature: [cryptographic signature]
---

# Domain
tags: [list of domain tags]
context: [what kind of work produced this insight]

# Insight
confidence: [0.0 to 1.0]
description: |
  [The insight itself, written as a transferable observation]

# Evidence
dream_depth: [1/2/3]
pre_dream_context: |
  [Brief description of what the agent was working on before dreaming]
visibility_note: |
  [Why this pattern was invisible before compression]

# Actionability
actionable: [true/false]
affects: [what this insight changes: fitness functions, genome composition, approach selection, etc.]

# Transfer metadata
domain_specificity: [HIGH/MEDIUM/LOW]
  # HIGH: Only useful in the tagged domains
  # MEDIUM: Useful in related domains with adaptation
  # LOW: Broadly applicable principle

model: [which AI model was running when the insight emerged]
```

## Validation on receive

When a colony receives an insight spore:

1. **Relevance check.** Do the domain tags match anything this colony works on?
2. **Conflict check.** Does the insight contradict strong local evidence?
3. **Redundancy check.** Does the colony already have this insight (or a stronger version)?
4. **Source check.** Is the originating colony above the trust threshold?
5. **Integration.** If all checks pass, add to local insight collection. If domain_specificity is HIGH, tag for local validation before acting on it.

## Notes

- Insight spores flow more freely than fitness or governance spores. They're observations, not prescriptions.
- High-confidence insights from deep or abyssal dreams carry a different quality than surface-dream insights. Note the dream depth so receiving colonies can calibrate.
- An insight that emerged from compression of evolution data (FLUX) has different provenance than one from governance review (METAMORPHOSIS). Include the pre-dream context so receivers understand the source.
