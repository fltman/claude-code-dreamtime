# /songlines - Browse and search songlines

## Usage

```
/songlines
/songlines --domain security
/songlines --search "trust boundaries"
/songlines --show SNG-014
```

## What this does

Browse, search, and manage songline artifacts. Songlines are narrative encodings of principle, stories that carry knowledge in a form that transfers across contexts better than rules.

## Workflow

### Default: List songlines

List all songlines in `dreams/artifacts/songlines/`, showing:
- Songline ID (SNG- for originals, INTERP- for interpretations)
- Domain tags
- Transfer rating
- Brief excerpt (first line of narrative)
- Origin (local dream or foreign colony)
- Times interpreted

### --domain {tag}: Filter by domain

Show only songlines tagged with the specified domain. Domains are assigned during dream artifact generation and can include: security, auth, api-design, data-flow, testing, performance, architecture, frontend, backend, infrastructure, devops, and custom tags.

### --search "text": Full-text search

Search across songline narratives, encoded principles, and interpretation notes.

### --show SNG-{NNN}: Display full songline

Show the complete songline: narrative, encoded principles, domain tags, transfer rating, interpretation history, and lineage.

### --heritage SNG-{NNN}: Use as heritage prompt

Package a songline for use as a FLUX heritage prompt. When a timeline inherits this songline, it receives the narrative as part of its founding context. The child timeline doesn't get rules. It gets a story.

## Songline quality indicators

**Transfer rating** (0.0 to 1.0): How well the narrative's principles survive context shifts. Based on interpretation success rate. Above 0.8 is strong. Below 0.5 suggests the songline is too context-specific.

**Interpretation count**: How many times the songline has been re-dreamed for different contexts. Higher count with maintained transfer rating indicates robust knowledge.

**Interpretation success** (0.0 to 1.0): Percentage of interpretations where the encoded principles survived with high fidelity.

## Notes

- Songlines are the most transferable form of dream knowledge. Prefer sharing songlines over raw insights when distributing via SPORE.
- A songline with high transfer rating and many successful interpretations is a strong candidate for heritage prompt use in FLUX crossover events.
- Tension songlines (produced when contradictory songlines are reconciled) hold both principles. They're more complex but often more useful than either source.
