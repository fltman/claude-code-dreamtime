# /orient - Wake from dream and integrate artifacts

## Usage

```
/orient
/orient --dream DRM-003
```

## What this does

Runs the post-dream orientation protocol. The agent takes stock of what the dream produced, checks for active triggers, calibrates confidence, and resumes work with transformed knowledge.

## Workflow

1. **Inventory.** List all artifacts from the most recent dream (or specified dream):
   - Insights: count and brief summary of each
   - Warnings: count and severity
   - Songlines: count and domain tags
   - Shadows: count and trigger conditions

2. **Continuity check.** Assess whether the current task still makes sense given what the dream revealed. Possible outcomes:
   - CONTINUE: Task is valid, proceed with adjusted understanding
   - REVISE: Task is valid but approach needs revision based on dream insights
   - PAUSE: Dream revealed something that requires attention before continuing
   - ABORT: Dream revealed something that invalidates the current task

3. **Shadow scan.** Check all active shadows against current work context. For each shadow with triggered conditions:
   - Surface the shadow
   - Recommend action (re-investigate, query SPORE network, proceed with caution)
   - Flag in current work state

4. **Confidence calibration.** Review confidence levels across active domains:
   - Where has confidence increased? (insights consolidated understanding)
   - Where has confidence decreased? (shadows mark uncertain ground)
   - Where is confidence unchanged?

5. **SPORE assessment.** Check whether any artifacts should be shared with the network:
   - Insights with high confidence and broad applicability: suggest as insight spore
   - Songlines with high transfer rating: suggest as songline spore
   - Shadows seeking lost knowledge: suggest as shadow spore (network query)

6. **Log to Ledger.** If METAMORPHOSIS Ledger is active, record:
   - Dream cycle completed (ID, depth, intention)
   - Artifacts produced (count by type)
   - Confidence changes
   - Shadow triggers activated
   - Continuity assessment

7. **Resume.** Present summary and return to waking work.

## Output format

```
ORIENT COMPLETE

Dream: DRM-{NNN} (depth {N}, {intention_type})

Artifacts produced:
  Insights: {N} ({brief list})
  Warnings: {N} ({severity summary})
  Songlines: {N} ({domain tags})
  Shadows: {N} ({trigger summary})

Continuity: {CONTINUE|REVISE|PAUSE|ABORT}
  {explanation}

Active shadow triggers: {N}
  {list if any}

Confidence shifts:
  {domain}: {UP|DOWN|STABLE} ({reason})

SPORE candidates: {N}
  {list if any}

Resuming work.
```

## Parameters

`--dream DRM-{NNN}` - Orient on a specific dream. Default: most recent dream in history.

`--skip-spore` - Skip SPORE assessment. Use when working offline or in a colony without network peers.

## Notes

- Orient should run after every dream. Skipping orient risks dream amnesia (ignoring artifacts) or dream paralysis (being unable to act).
- Orient can be run multiple times on the same dream. Useful when new context activates previously dormant shadows.
- If orient reveals PAUSE or ABORT, present findings to the user before proceeding.
