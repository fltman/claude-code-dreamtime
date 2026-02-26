# /shadows - Review active shadows and their triggers

## Usage

```
/shadows
/shadows --scan
/shadows --broadcast SHADOW-0047
```

## What this does

Lists and manages shadow artifacts. Shadows are markers for knowledge that was lost during compression. They don't contain the knowledge itself, only its shape: where it was, what kind it was, how important it seemed, and what conditions should trigger re-investigation.

## Workflow

### Default: List shadows

List all shadows in `dreams/artifacts/shadows/`, showing:
- Shadow ID
- Source dream
- Weight (HIGH / MEDIUM / LOW)
- Brief description of lost knowledge
- Trigger conditions
- Status (DORMANT / TRIGGERED / RESOLVED / BROADCAST)

### --scan: Check triggers

Scan current work context against all shadow trigger conditions. Report any matches:

```
SHADOW SCAN

Context: [current work description]

TRIGGERED:
  SHADOW-0047 (HIGH) - Race conditions in websocket handlers
    Trigger: Working on websocket event handlers
    Recommendation: Re-investigate before proceeding

  SHADOW-0023 (MEDIUM) - Edge case in token refresh
    Trigger: Auth token implementation active
    Recommendation: Review with extra caution

DORMANT: 12 shadows (no matching triggers)
RESOLVED: 3 shadows (knowledge recovered)
```

### --broadcast SHADOW-{NNN}: Query the network

Package a shadow as a shadow spore and prepare it for SPORE distribution. This is a network query: "We lost knowledge about X. Does anyone have it?"

Creates a shadow spore in `dreams/artifacts/shadows/` with `broadcast: true` and generates the corresponding SPORE package if the SPORE system is available.

### --resolve SHADOW-{NNN}: Mark as resolved

When lost knowledge has been recovered (through re-investigation, SPORE response, or other means), mark the shadow as resolved. Record what was found and how.

## Shadow lifecycle

1. **Created** during dream compression. The dreamer detects that important knowledge is being lost and creates a shadow.
2. **Dormant** when no trigger conditions match current context. The shadow waits.
3. **Triggered** when work context matches trigger conditions. The shadow surfaces.
4. **Broadcast** when sent to the SPORE network as a query. The colony asks for help.
5. **Resolved** when the lost knowledge is recovered. The shadow is archived with resolution notes.

## Notes

- Shadows don't expire. Lost knowledge that was important stays important.
- Regular shadow scans (weekly or at project milestones) are recommended.
- A shadow can be triggered multiple times if the same context recurs.
- Broadcasting a shadow reveals what you don't know. Consider whether this is appropriate for your network trust level.
