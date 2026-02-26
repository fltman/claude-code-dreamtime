# /interpret - Interpret a foreign songline for local context

## Usage

```
/interpret SNG-014
/interpret SNG-014 --context "ETL pipeline for healthcare data"
/interpret --reconcile SNG-014 SNG-027
```

## What this does

Invokes the dream interpreter agent to translate a songline into local context. The interpreter re-dreams the narrative, preserving encoded principles while adapting metaphors to fit the local domain.

## Workflow

### Standard interpretation

1. **Load songline.** Read the specified songline from `dreams/artifacts/songlines/` or from a received SPORE package.

2. **Determine local context.** Use `--context` if provided. Otherwise, infer from current project state, active FLUX evolution, or recent work.

3. **Invoke interpreter.** Call the interpreter agent (`--agents interpreter`) with the songline and local context.

4. **Review interpretation.** The interpreter produces:
   - Extracted principles (what the narrative encodes, independent of metaphor)
   - Local mapping (how each concept maps to local domain)
   - Re-dreamed narrative (new story in local terms)
   - Adapted principles (how the principles apply here)
   - Fidelity score (how well principles survived translation)
   - Adaptation score (how native the new narrative feels)

5. **Save.** Write interpretation to `dreams/artifacts/songlines/INTERP-{NNN}.yaml`.

6. **Update source.** Increment the source songline's interpretation count and update its transfer rating based on fidelity.

### --reconcile: Reconcile contradictory songlines

When two songlines encode opposing principles, the interpreter produces a tension songline that holds both. Neither is wrong. The tension itself is the knowledge.

1. **Load both songlines.**
2. **Extract principles from each.**
3. **Identify the contradiction.** What specifically conflicts?
4. **Compose tension narrative.** A story that contains both principles in productive relationship.
5. **Map contexts.** When does principle A apply? When does principle B apply? When does the tension itself matter?
6. **Save as tension songline.** Marked with `type: tension` and references to both sources.

## Parameters

`SNG-{NNN}` - The songline to interpret. Required.

`--context "text"` - Explicit local context. If omitted, inferred from current state.

`--reconcile SNG-A SNG-B` - Reconcile two contradictory songlines into a tension songline.

`--dry-run` - Show the interpretation without saving.

## Notes

- Interpretation is not translation. The interpreter re-dreams the knowledge. The new narrative should feel native, not imported.
- Low fidelity scores (below 0.6) suggest the songline's knowledge may not transfer to this context. Consider whether the principles genuinely apply or whether you're forcing a fit.
- Tension songlines are some of the most valuable artifacts. Don't avoid contradictions. Hold them.
