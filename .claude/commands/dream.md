# /dream - Enter dream state

## Usage

```
/dream
/dream --depth 2
/dream --depth 3 --intention "Find why alpha outperforms beta on edge cases"
```

## What this does

Initiates a deliberate dream cycle. The agent pauses waking work, sets a compression intention, chooses dream depth, and enters a consolidation state.

## Workflow

1. **Assess readiness.** Check for dream readiness signals:
   - Contradictory accumulation (conflicting observations without resolution)
   - Repetition detection (re-deriving earlier conclusions)
   - Coherence decay (losing consistency across topics)
   - Exploration saturation (broad coverage, needs depth)
   - Context pressure (above 70% utilization)
   
   If no signals are present, warn the user that dreaming may be premature and ask for confirmation.

2. **Set intention.** Ask the user or determine from context:
   - What should this dream focus on?
   - Intention type: CONSOLIDATION, COMPARATIVE, ABSTRACTION, ANOMALY, or INTEGRATION
   
   If `--intention` flag is provided, use that. Otherwise, propose an intention based on current work state.

3. **Choose depth.** 
   - Surface (depth 1): Preserve structure, compress examples. Token reduction ~40%.
   - Deep (depth 2): Compress structure into principles. Token reduction ~75%.
   - Abyssal (depth 3): Compress everything into weighted tendencies. Token reduction ~95%.
   
   If `--depth` flag is provided, use that. Otherwise, recommend based on context.

4. **Create dream state file.** Write to `dreams/active/DRM-{NNN}.yaml` with pre-dream state, compression priorities, and empty artifact lists.

5. **Execute compression.** Invoke the dreamer agent (`--agents dreamer`) to:
   - Review all current context according to intention
   - Identify what to retain at high fidelity vs. release
   - Generate artifacts: insights, warnings, songlines, shadows
   - Write artifacts to `dreams/artifacts/{type}/`
   - Update dream state file with artifact references

6. **Present results.** Show the user what the dream produced:
   - Artifact count by type
   - Key insights in brief
   - Any active warnings
   - Shadows created (knowledge lost)
   - Recommendation for next step (orient, or continue dreaming deeper)

7. **Transition.** Move dream state file to `dreams/history/`. Suggest `/orient` to integrate artifacts.

## Parameters

`--depth [1|2|3]` - Dream depth. 1=surface, 2=deep, 3=abyssal. Default: 1.

`--intention "text"` - Free text dream intention. If not provided, dreamer agent will propose one.

`--type [consolidation|comparative|abstraction|anomaly|integration]` - Intention type. If not provided, inferred from intention text.

`--force` - Skip readiness check. Dream even if no signals are present.

## Examples

```
/dream
  > Assesses readiness, proposes intention and depth, guides through dream cycle.

/dream --depth 2 --intention "What do all the failed timelines have in common?"
  > Deep dream focused on cross-cutting failure patterns.

/dream --depth 3
  > Abyssal dream. Maximum compression. Only intuitions survive.
```

## Notes

- Only one dream can be active at a time. Check `dreams/active/` first.
- Dreaming takes the agent offline temporarily. Nothing external happens during the dream.
- After dreaming, always suggest `/orient` to integrate artifacts.
- If FLUX evolution is running, dreaming pauses evolution until orient completes.
