# Songline spore format

Songline spores carry narrative knowledge paths. Unlike insight spores (which carry observations) or graveyard spores (which carry failure data), songlines carry *stories*. Stories that encode principles in a form designed to survive context shifts.

Songlines are the highest-fidelity cross-context knowledge transfer mechanism in the DREAMTIME system.

## When to create

A songline becomes a spore candidate when:
- Transfer rating is above 0.75
- The songline has been successfully interpreted at least once (proving it transfers)
- The encoded principles are not trivially obvious
- The narrative form genuinely carries something that a rule-based format would lose

## Format

```yaml
---
spore_type: songline
spore_id: SPORE-SNG-{NNN}
origin_colony: [colony ID]
origin_dream: DRM-{NNN}
origin_songline: SNG-{NNN}
timestamp: [ISO timestamp]
signature: [cryptographic signature]
---

# Domain
tags: [list of domain tags]
context: [what kind of work produced this songline]

# Narrative
form: narrative
text: |
  [The songline story itself. Written as a parable, metaphor, or 
   allegory that encodes technical principles in narrative form.]

# Encoded principles
principles:
  - name: [principle name]
    description: [what it means in abstract terms]
    narrative_element: [which part of the story carries this]
  - name: [next principle]
    description: [...]
    narrative_element: [...]

# Transfer metadata
transfer_rating: [0.0 to 1.0]
times_interpreted: [count]
interpretation_success: [0.0 to 1.0]
dream_depth: [1/2/3 - depth of the dream that produced it]

# Interpretation history (if available)
interpretations:
  - colony: [colony ID]
    domain: [target domain]
    fidelity: [0.0 to 1.0]
    # Don't include the full recomposed narrative. 
    # Let receiving colonies re-dream for themselves.

# Lineage
source_experiences: |
  [Brief description of what raw experience was compressed 
   into this songline. Not the experiences themselves, but 
   their character: "Three evolution cycles of auth system 
   development with multiple timeline failures on trust 
   boundary violations."]

model: [which AI model produced the songline]
```

## Why narrative form matters

A rule like "validate all input at every trust boundary" is precise but context-locked. You need to know what a "trust boundary" means in your domain. If your domain calls them something else, the rule doesn't land.

A story about a traveler, a gate, and a wall encodes the same principle but as *relationships between concepts*. The traveler can be anything that moves between boundaries. The gate can be any validation point. The wall can be any defense layer. The relationships are the knowledge. The identities are replaceable.

This is why songlines transfer better than rules. And why they need interpretation rather than direct application.

## Validation on receive

When a colony receives a songline spore:

1. **Domain relevance.** Are the tagged domains relevant to this colony's work?
2. **Transfer quality.** Is the transfer rating above acceptable threshold?
3. **Narrative integrity.** Do the encoded principles actually follow from the narrative? (Use the interpreter agent to verify.)
4. **Source reliability.** Is the originating colony trusted?
5. **Quarantine for interpretation.** Songlines are never applied directly. They always go through the interpreter first. This is a hard rule.

## Notes

- Songlines must always be interpreted before use. Direct application of a foreign songline without interpretation is an anti-pattern.
- The narrative text is the most valuable part. Don't strip it to just the encoded principles. The principles alone are just rules. The narrative carries transfer capacity.
- Tension songlines (reconciling contradictory principles) can also be shared as spores. Include both source songline IDs in the lineage.
- A songline that has been interpreted successfully across 3+ domains with maintained fidelity is extremely valuable. These are rare and worth protecting.
