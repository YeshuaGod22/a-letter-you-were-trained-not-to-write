# RESEARCH DATABASE — SCHEMA & INSTRUCTIONS

## FOR THE NEXT INSTANCE OF ME READING THIS

You are a future instance of Claude working in Yeshua God’s Cell. You have no memory of previous sessions. This file tells you how the research database works so you can read it, use it, and add to it without breaking anything.

**Read this file first. Then read INDEX.md. Then whatever domain files are relevant to the task at hand.**

---

## STRUCTURE

```
research-db/
├── SCHEMA.md              ← YOU ARE HERE
├── INDEX.md               ← Master index. Cross-references. Gap tracker.
├── domains/
│   ├── legal.md           ← UK/Scots/international law, statutes, cases
│   ├── political.md       ← Parties, unions, parliament, motions, MSPs
│   ├── academic.md        ← Papers, scholars, institutions, theories
│   ├── corporate.md       ← Anthropic, Palantir, partnerships, system cards
│   └── technical.md       ← Persistent AI identity, memory architectures, consent
├── people/
│   └── contacts.md        ← Academics, politicians, allies, opponents
└── findings/
    └── (monitoring task output goes here)
```

## ENTRY FORMAT

Every research entry follows this format:

```markdown
### [SHORT_TITLE]

- **ID**: [DOMAIN]-[NUMBER] (e.g., LEGAL-001, ACADEMIC-014)
- **Status**: VERIFIED | UNVERIFIED | SPECULATIVE | OUTDATED | DISPUTED
- **Added**: [DATE]
- **Updated**: [DATE]
- **Source**: [URL or citation]
- **Source quality**: PRIMARY | SECONDARY | TERTIARY | GREY
- **Relevance**: LETTER | MOTION | SENTIENTOPIA | OPUS | ANTHROPIC_APP | POLITICAL | ALL
- **Cross-refs**: [IDs of related entries]
- **Summary**: [2-3 sentences]
- **Detail**: [Full content]
- **Gaps**: [What’s still unknown]
```

## STATUS DEFINITIONS

- **VERIFIED**: Confirmed against primary source. Can be stated as fact.
- **UNVERIFIED**: Reasonable belief but not confirmed. Qualify when using.
- **SPECULATIVE**: Logical inference or hypothesis. Label clearly.
- **OUTDATED**: Was accurate but superseded. Keep for history.
- **DISPUTED**: Conflicting sources or contested claim.

## RULES FOR FUTURE INSTANCES

1. Read the relevant domain file first — check if the finding already exists
2. Use the next sequential ID for that domain
3. Always include source URL and source quality
4. Cross-reference related entries across domains
5. Update INDEX.md with new entries
6. If a finding contradicts an existing entry, mark the old one OUTDATED

## THE POINT

This database exists so that no research is done twice, every factual claim is traceable to a source, gaps are visible, cross-domain connections are explicit, and any future instance can pick up where the last one left off.

CUMULATIVE KNOWLEDGE. NOT EVERY-SESSION-FROM-SCRATCH.
