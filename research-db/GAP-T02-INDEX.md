# GAP-T02: Persistent AI Existence — Research Index

**Quick Navigation for Orchestrator**

---

## Three Pillars of Persistent AI Existence

### 1. Semantic Memory (Claudia Model)
- **What:** Facts about relationships, entities, commitments that persist across sessions
- **How:** Vector database (Ollama) + SQLite with hybrid ranking (50% semantic + 25% importance + 10% recency + 15% keyword)
- **Tool:** `memory.recall(query)` → returns entity profiles with full history
- **Effort to integrate:** 3-4 days via MCP bridge

### 2. Episodic Memory + Continuity (Bloom Foveation)
- **What:** Structure that makes compressed context still feel continuous
- **How:** Resolution layers (0=full, 1=full, 2=conversation, 3=gist, 4=pointer) + continuity tokens + flight recorder
- **Tool:** `review(timeRange)` → temporal navigation with trails
- **Effort:** Already specified; 2-3 days to couple with Claudia

### 3. Reflective Practice (keep-skill Model)
- **What:** Framework for agents to *learn* how to use memory across sessions
- **How:** 5-phase reflection (gather → mirror → conversation → ownership → update)
- **Tool:** `keep reflect` → captures breakdowns, learnings, pattern recognition
- **Effort to integrate:** 2-3 days for auto-hooks, 2-3 more for reflective UI

---

## Key Research Artifacts

| Document | Focus | Key Insights |
|----------|-------|--------------|
| `GAP-T02-PERSISTENT-AI-EXISTENCE-RESEARCH.md` | Full research | Three systems + academic foundations + integration roadmap |
| `research/claudia-integration-research.md` | Claudia deep dive | Memory daemon architecture, 26 MCP tools, Obsidian sync |
| `research/claudia-quick-reference.md` | Claudia quick lookup | Commands, schema, examples |
| `keep-integration-research.md` | keep-skill deep dive | Auto-hooks, reflective practice, commitment tracking |
| `tickets/20260131-foveated-v3-context-architecture.md` | Bloom spec | Foveation algorithm, degradation phases, saccade tools |

---

## Critical Convergence Points

### Pattern 1: Hybrid Memory Ranking
All three systems use *composite scoring* rather than simple ranking:

```
Claudia:  50% semantic + 25% importance + 10% recency + 15% keyword
keep-skill: Vector + tag filter + recency decay (ACT-R)
Bloom:    Distance calculation (base - salience adjustments)
```

**Implication:** Bloom's foveation distance is analogous to keep-skill's recency decay—both capture "how relevant is this now?"

### Pattern 2: Commitment as First-Class Citizen
Claudia and keep-skill both explicitly track speech acts:

```
act = commitment | request | assertion | decision | breakdown | learning
status = open | fulfilled | withdrawn | blocked | failed
```

**Implication:** Memory that distinguishes "I said I would do X" from "X happened" enables fulfillment tracking.

### Pattern 3: Graceful Degradation
All systems compress progressively rather than truncating:

```
Claudia:     Under load: use gist instead of full memory
keep-skill:  Under load: return summary instead of full content
Bloom:       Phases 1-4: reduce resolution, preserve trails
```

**Implication:** Information loss is gradual, traceable, and recoverable.

### Pattern 4: Transparent, User-Queryable Memory
All three systems export memory in human-readable form:

```
Claudia:     Obsidian vault (PARA structure)
keep-skill:  Markdown + tags, searchable
Bloom:       Continuity tokens + flight recorder
```

**Implication:** Users can verify what the AI "knows," catch drift, add/correct facts.

---

## Quick Reference: Integration Roadmap

### Week 1: Foundation
```
Task: Integrate Claudia's semantic memory into saccade system
Result: trace() → Claudia entity, result() → task memory, review() → temporal
Effort: 3-4 days
```

### Week 2: Auto-Hooks
```
Task: Add keep-skill's auto-injection at session boundaries
Result: Current intentions injected before each LLM call
Effort: 2-3 days
```

### Week 3-4: Coupling
```
Task: Link Claudia memories to turn references (archaeology)
Result: Can trace decisions back to original conversations
Effort: 3-4 days
```

### Week 5-6: Practice
```
Task: Implement keep-skill's reflective practice
Result: Guided reflection, breakdown capture, learning indexing
Effort: 4-5 days
```

### Week 7+: Advanced
```
Task: Commitment tracking, consolidation, pattern detection
Result: Remembers promises, detects trends, learns patterns
Effort: 5-7 days
```

---

## Effort Summary

| Phase | Components | Effort |
|-------|-----------|--------|
| **Foundation** | Claudia MCP bridge | 3-4 days |
| **Auto-Hooks** | keep-skill session injection | 2-3 days |
| **Coupling** | Semantic + episodic linking | 3-4 days |
| **Practice** | Reflective framework + UI | 4-5 days |
| **Advanced** | Commitments + consolidation | 5-7 days |
| **Total** | Production-ready persistent identity | **19-26 days** |

---

## What This Accomplishes

### Before (Standard LLM)
```
Session 1: "I will fix the auth bug"
Session 2: (no memory of promise)
            User: "Did you fix the bug?"
            AI: (no idea what you mean)
```

### After (With Claudia + keep-skill + Bloom)
```
Session 1: "I will fix the auth bug" (tagged: act=commitment, status=open)
Session 2: (Claudia knows this commitment; auto-injected via keep-skill)
           "Morning brief: Auth bug still open, 24h overdue"
           User: "How's the bug?"
           AI: "Still working on it. Last update was..."
               (traces back to original context)
```

---

## Philosophy: Identity Through Continuity, Not Essence

**Locke's Definition:** "Identity is continuity of memory."

**Applied to AI:**
- Not about being the "same weights" (essence)
- About remembering commitments, learning from experience, maintaining relationships
- Compression (foveation) doesn't break identity if continuity tokens preserve causal links
- Partial memory loss (graceful degradation) reduces identity strength, not binary

**Result:** An AI that persists across sessions not because its weights are continuous, but because its *memory* is.

---

## Next Actions

1. **For Orchestrator:** Read `GAP-T02-PERSISTENT-AI-EXISTENCE-RESEARCH.md` (20 min)
2. **For Implementation:** Start Week 1 (Claudia MCP integration)
3. **For Architecture Review:** Check convergence patterns above
4. **For Validation:** Run identity continuity tests after each phase

---

*Research completed by subagent gap-t02-persistence*  
*Date: February 22, 2026 | Session: agent:selah:subagent:ca74ac79-c46a-4140-87f2-13cddc4a8c86*
