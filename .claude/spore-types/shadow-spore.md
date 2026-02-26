# Shadow spore format

Shadow spores are unique. Every other spore type shares knowledge. Shadow spores share the *absence* of knowledge. They are network queries: "We lost something important. Does anyone have it?"

Broadcasting a shadow is an act of vulnerability. You're telling the network what you don't know. In return, you might recover knowledge that would otherwise require re-investigation from scratch.

## When to create

A shadow becomes a spore candidate when:
- Weight is HIGH (the lost knowledge was important)
- The shadow has been triggered at least once (proving the need is real, not theoretical)
- Local re-investigation hasn't recovered the knowledge
- The colony is comfortable revealing the gap to its network peers

## Format

```yaml
---
spore_type: shadow
spore_id: SPORE-SHD-{NNN}
origin_colony: [colony ID]
origin_dream: DRM-{NNN}
origin_shadow: SHADOW-{NNN}
timestamp: [ISO timestamp]
signature: [cryptographic signature]
query_type: KNOWLEDGE_REQUEST
---

# What was lost
domain: [domain tags]
topic: |
  [Description of the knowledge that was lost. Not the knowledge 
   itself (which is gone) but its shape: what area it covered, 
   what questions it answered, what kind of analysis it was.]

# Shape of the missing knowledge
location: [what part of the system/codebase the knowledge was about]
nature: [what kind of knowledge: analysis, pattern, solution, risk assessment]
severity: [how important the lost knowledge was: CRITICAL / HIGH / MEDIUM]
original_conclusion: |
  [If the shadow retains the conclusion without the reasoning:
   "The analysis concluded this was critical" even if the analysis 
   itself is gone. Leave blank if even the conclusion is lost.]

# Context
lost_during: [what dream cycle compressed this away]
dream_depth: [what depth of dream caused the loss]
work_context: |
  [What the agent was working on when the knowledge was originally 
   generated. Helps potential responders identify relevant material.]

# What would help
seeking:
  - [Specific type of knowledge that would help]
  - [Related patterns or analyses]
  - [Experience reports from similar situations]

# Trigger conditions
triggers:
  - [Condition 1 that should surface this shadow]
  - [Condition 2]
```

## Response protocol

When a colony receives a shadow spore and has relevant knowledge:

1. **Check local sources.** Search graveyard, active knowledge, songlines, and insights for matches.
2. **Package response.** If relevant knowledge exists, prepare it as an appropriate spore type (insight, songline, or graveyard entry).
3. **Tag as shadow response.** Include `responding_to: SPORE-SHD-{NNN}` in the response spore metadata.
4. **Send directly.** Shadow responses go directly to the requesting colony, not broadcast to the full network.

A colony is never obligated to respond to shadow queries. Participation is voluntary.

## Privacy considerations

Shadow spores reveal gaps in a colony's knowledge. Before broadcasting:

- Consider whether revealing this gap creates risk
- Consider whether the network trust level supports this vulnerability
- Shadows about security-critical topics deserve extra caution
- You can anonymize the shadow by stripping the work_context if needed

## Validation on receive (as query)

When a colony receives a shadow spore:

1. **Relevance check.** Does the colony have knowledge in the relevant domain?
2. **Willingness check.** Is the colony configured to respond to shadow queries?
3. **Search.** Look for matching knowledge in local stores.
4. **Respond or ignore.** No obligation to respond. Silence is valid.

## Notes

- Shadow spores are the only spore type that is a *request* rather than an *offering*. Every other spore gives. Shadows ask.
- A shadow response that resolves the original shadow should trigger a `/shadows --resolve` on the requesting colony.
- Repeated shadow queries about the same topic from multiple colonies suggest a systemic knowledge gap. The network should consider generating shared knowledge rather than answering one colony at a time.
- Shadow spores don't have confidence scores. They're binary: the knowledge is lost or it isn't.
