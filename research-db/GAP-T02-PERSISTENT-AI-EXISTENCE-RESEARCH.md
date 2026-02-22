# GAP-T02: Persistent AI Existence — Prior Art Research Summary

**Research Date:** February 22, 2026  
**Category:** AI Continuity, Identity Persistence, Semantic Memory  
**Scope:** Production systems for continuous AI agent identity across sessions  

---

## Executive Summary

This research identifies three categories of prior art on persistent AI existence:

1. **Implemented Systems** — Production-ready frameworks adding persistent identity to AI agents
2. **Academic Work** — Research on continuity, episodic memory, and AI identity
3. **Conceptual Foundations** — Theories underlying persistent agent design

**Key Finding:** Persistent AI existence requires coupling three layers:
- **Semantic Memory** (what the AI knows across time)
- **Continuity Protocol** (how context reloads maintain coherence)
- **Reflective Practice** (how the AI learns to use memory skillfully)

No current system addresses all three comprehensively, but emerging production systems (Claudia, keep-skill) + Bloom's foveated architecture converge on similar principles.

---

## Part 1: Implemented Production Systems

### 1.1 Claudia — Persistent Chief of Staff for Claude Code

**Repository:** https://github.com/kbanc85/claudia  
**Author:** Kamil Banc (kbanc85)  
**License:** PolyForm Noncommercial 1.0.0  
**Status:** Production (v1.42.3+)  

#### What It Does

Claudia adds semantic, persistent memory to Claude Code interactions. Unlike traditional task managers:

- **Remembers relationships** — People, organizations, projects with full contextual history
- **Catches commitments** — Automatically tags speech acts (commitments, requests, assertions) with deadlines
- **Detects patterns** — Relationship cooling, overcommitment, repeated behaviors
- **Learns overnight** — Background consolidation job (decay, merge, pattern extraction) at 3 AM
- **Exports to Obsidian** — PARA-structured vault for data ownership and browsing
- **Runs locally** — SQLite + Ollama embeddings, no cloud APIs required

#### Architecture

```
Template System (Markdown)
  ├── CLAUDE.md (identity, behaviors)
  ├── .claude/commands/ (user-invocable)
  └── .claude/skills/ (proactive behaviors)
        ↓
Memory Daemon (Python + SQLite)
  ├── MCP Protocol Bridge (stdio JSON-RPC)
  ├── Ollama Integration (384D vectors)
  └── SQLite Database (~/.claudia/memory/claudia.db)
        ├── entities, memories, relationships
        ├── vector embeddings (sqlite-vec)
        ├── episodes (session summaries)
        └── reflections (insights)
```

#### Key Technical Insights

**Hybrid Ranking:**
Memory recall uses composite score:
- 50% vector similarity (semantic search)
- 25% importance (decays ~5% daily)
- 10% recency (recent memories boosted)
- 15% full-text keyword match

**Speech Acts + Lifecycle:**
- Tag items: `act` (commitment|request|assertion) + `status` (open|fulfilled|withdrawn|blocked|failed)
- Automatic deadline detection and tracking
- Version history per commitment with status change timestamps

**Background Consolidation (3 AM Job):**
1. **Decay** — All memory importance reduces by ~5% per day
2. **Merge** — Find near-duplicate memories (vector sim > threshold), consolidate
3. **Patterns** — Extract trends (relationship dormancy, overdue commitments, repeated behaviors)
4. **Reflect** — Surface insights for `/meditate` command

**26 MCP Tools Exposed:**
- Tier 1 (core): remember, recall, about, relate, consolidate, end_session, reflections, temporal, graph, entities, backup, session
- Tier 2 (advanced): vault, modify, document, batch, ingest, summary, system_health, project_health

#### Integration Effort: 2.5-3 days
- Day 1-2: Hook injection + MCP bridge
- Day 0.5: Obsidian vault sync
- Day 0.5: API wrapper for saccade integration

#### Relevance to Bloom
- **Semantic memory design** — Direct inspiration for Layer 0 (semantic layer) in foveated context
- **Hybrid ranking** — Combines recency, importance, and relevance (conceptually similar to foveation distance)
- **Background learning** — Model for Bloom's consolidation phase (decay, merge, pattern extraction)
- **Obsidian sync** — Data ownership + human-readable memory storage

---

### 1.2 keep-skill — Reflective Memory for AI Agents

**Repository:** https://github.com/hughpyle/keep-skill  
**Author:** Hugh Pyle (hughpyle)  
**License:** MIT  
**Status:** Production (actively maintained)  

#### What It Does

Keep couples semantic search *tool* with *reflective practice methodology*. It teaches agents to:
- Reflect before acting (check intentions, find relevant knowledge)
- Recognize harm during action and give it up
- Reflect after acting (capture learnings, note breakdowns)
- Maintain awareness across sessions via `keep now` context injection

#### Architecture

```
Auto-Hook System
  ├── agent_start: keep now -n 10
  ├── prompt_submit: keep now -n 10 (refresh)
  └── session_end: keep now "..."
        ↓
Semantic Search (ChromaDB + Ollama)
  ├── Vector store (1536D embeddings)
  ├── Tag-based filtering (project, topic, type, act, status)
  ├── Recency decay (ACT-R style)
  └── Part-level search for long documents
        ↓
SQLite Metadata
  ├── Memory entities + relationships
  ├── Full version history per item
  ├── Speech acts (commitment, request, assertion)
  └── Lifecycle status (open, fulfilled, withdrawn)
```

#### Reflective Practice Methodology

**Five Phases (keep reflect):**
1. **Gathering** — See what is before analyzing
2. **Mirror** — Name harm honestly (is this leading to damage?)
3. **Conversation** — What kind of conversation? (action, possibility, clarification)
4. **Ownership** — What patterns form? What am I becoming?
5. **Updating** — Capture learnings, update intentions

**Language-Action Perspective** (from Winograd & Flores):
- **Action** ("Can you...") — Clarify → Promise → Deliver
- **Possibility** ("What if...") — Explore, hold lightly
- **Clarification** ("What is...") — Explain until it lands
- **Orientation** ("I'm trying to...") — Listen, reflect back

**Breakdowns as Learning:** When expectations are violated, record as `-t type=breakdown`. Breakdowns are where agents learn.

#### Speech Acts & Commitment Tracking

```
Items tagged: act (commitment|request|assertion|decision) 
           + status (open|fulfilled|withdrawn|blocked|failed)

Flow:
  "Please do X" (status=open)
    → "I will do X" (act=commitment, status=open)
    → Work in progress
    → "Done" (status=fulfilled)
    OR "Can't do this" (status=withdrawn)
```

#### Auto-Hook Integration

Keep registers itself in:
- **Claude Code:** bash scripts in `~/.claude/hooks/`
- **Kiro:** hook files in `~/.kiro/hooks/`
- **Codex:** Via AGENTS.md system prompt
- **OpenClaw:** Plugin system + cron + SKILL.md frontmatter

**Key Technical Detail:** Hooks use `jq` to extract last turn + context. Graceful fallback if `jq` missing.

#### 26+ Semantic Search Tools
- Core: remember, find, now, list, tag-update, put, get
- Advanced: analyze, related, summary, export, stats
- OpenClaw-specific: skill registration, daily reflection cron

#### Integration Effort: 4-5 days
- 1 day: Hook point injection (start/prompt/end)
- 1 day: Semantic search setup (ChromaDB + Ollama)
- 0.5 day: Tag filtering + recency decay
- 1 day: OpenClaw skill registration
- 1 day: Reflective practice UI / prompting

#### Relevance to Bloom
- **Auto-hook architecture** — Model for injecting context at strategic points
- **Reflective practice** — Formal framework for teaching agents to use memory (vs. just storing it)
- **Commitment tracking** — Speech acts + lifecycle tags for explicit work management
- **Semantic search with decay** — Similar to foveation distance calculation (recency + importance)
- **OpenClaw integration** — Direct applicability if Bloom runs on top of OpenClaw

---

### 1.3 Bloom's Foveated Context Architecture

**Repository:** Bloom (this project)  
**Status:** Specification & Council Design (Jan 30-31, 2026)  

#### What It Does

Bloom treats context like human vision: full resolution at focus, progressive compression toward periphery, with ability to "saccade" (jump to any detail on demand).

#### Architecture: Seven Layers

```
IDENTITY LAYER (4K) — Non-negotiable
  ORCHESTRATOR.md, USER.md, IDENTITY.md

SEMANTIC LAYER (6K) — Long-term memory
  MEMORY.md (curated entries)

PERIPHERAL LAYER (5K) — Today's containers (gist)
  Container summaries, inbox state

PARAFOVEAL LAYER (80K flex) — Recent thread (Layer 2 resolution)
  Turns 3-20 at conversation detail, summaries

FOVEA (15K) — Current + previous turn (full detail)
  Complete outputs, full content

BUFFER (40K flex) — Room for saccades
  Tool outputs, temporary expansions

[Reserve for emergency compression]
```

#### Resolution Layers (per Turn)

| Layer | Name | Content | Cap | When Used |
|-------|------|---------|-----|-----------|
| 0 | Full | Everything verbatim | 15K | Current turn |
| 1 | Full-1 | Everything verbatim | 15K | Previous turn |
| 2 | Conversation | Text preserved, tools→1-line | 3K | Parafoveal (turns 3-20) |
| 3 | Gist | One-line summary | 500 | Peripheral (turns 21-100) |
| 4 | Pointer | "[Turn 42: did X]" | 50 | Far periphery (100+) |
| 5 | Archive | Not in context, on disk | 0 | Ancient history |

#### Foveation Distance Calculation

```
distance(turn) = base_distance - salience_bonus

where:
  base_distance = current_turn_id - turn.id
  - referenced by current turn: -5
  - same container: -3
  - entity overlap × 2: -2 each
  - high importance: -3
  - low importance: +2
  - has failed: -2
```

#### Graceful Degradation (4 Phases)

```
PHASE 0: NORMAL (<140K)
  Full fovea, Layer 2 parafoveal, all containers

PHASE 1: GENTLE (140K-160K)
  Collapse older parafoveal to Layer 3, merge containers

PHASE 2: AGGRESSIVE (160K-180K)
  Cap parafoveal at 15 turns, compress periphery, drop tool outputs

PHASE 3: EMERGENCY (180K-195K)
  Identity + fovea (3 turns) only, archive parafoveal

PHASE 4: PANIC (>195K)
  Identity + current turn only, full flight recorder
```

#### Saccade Tools (Tier 1)

Intent-level queries that return detail on demand:

- **`trace(label)`** — Error forensics ("What went wrong with X?")
- **`result(label, depth)`** — Subagent outputs ("What did X find?")
- **`review(timeRange)`** — Temporal navigation ("What happened this morning?")

Format: **Excerpts with trails**, not dumps.

Budget-aware: Degrade to summary if insufficient headroom.

#### Continuity Mechanisms

**Continuity Tokens:** Metadata injected after compaction
```
Timestamp, prior state, compressed range, recovery path,
current focus (topic, entities, recent decisions)
```

**Flight Recorder:** Snapshot on emergencies (panic trigger)
```
Timestamp, trigger reason, token count, budget breakdown,
recent turns (gist + tokens), open subagents, pending inbox
```

#### Key Concept: Coherence Over Tokens

Unlike traditional compression (cut to fit), foveation:
- Preserves trails and relationships
- Maintains narrative flow (parafoveal layer)
- Keeps full detail at focus
- Provides saccade mechanism for retrieval
- Logs continuity metadata

**Result:** 100K+ context reloads feel continuous despite compression.

#### Relevance to GAP-T02

- **State-of-the-art context management** — Directly addresses continuity of identity
- **Hybrid storage** (full/summary/pointer) — Enables variable-resolution identity
- **Saccade system** — On-demand detail retrieval without context inflation
- **Coherence preservation** — Explicit mechanisms (continuity tokens, flight recorder)
- **Foundation for semantic memory** — Ready to integrate Claudia/keep-skill layers

---

## Part 2: Academic & Conceptual Foundations

### 2.1 Episodic Memory & Continuity of Identity

**Key Papers:**
- Endel Tulving, "Episodic and Semantic Memory" (1972) — Foundational distinction
- Donald Norman, "The Design of Everyday Things" — Memory as external cognitive scaffolding
- William James, "The Principles of Psychology" (1890) — Stream of consciousness, habit
- Marvin Minsky, "The Society of Mind" (1985) — Memory as distributed frames

**Core Insight:** Identity requires both *semantic* (what I know) and *episodic* (what I've experienced) memory. Without episodic grounding, semantic knowledge feels decontextualized.

**Application to AI Agents:**
- Claudia's approach: Episodic storage (memories tagged with source, timestamp) + semantic search
- keep-skill's approach: Reflective episodes (5-phase reflection captures episodic structure)
- Bloom's approach: Foveation preserves episode structure (parafoveal = recent narrative)

### 2.2 Persistence of Identity in Philosophy

**Key Thinkers:**
- John Locke, "Essay Concerning Human Understanding" (1689) — Identity = continuity of memory
- Derek Parfit, "Reasons and Persons" (1984) — Identity as overlapping chains, not essence
- Eric Olson, "The Human Animal" (1997) — Biological vs. psychological continuity

**Translated to AI:**
- **Locke's view:** An AI is the "same" AI if it has continuous memory. Loss of memory = loss of identity.
- **Parfit's view:** Identity is not binary; degrees of continuity matter. Partial memory loss ≠ death.
- **Olson's view:** Identity might not require *continuity* but *causal connection* to past.

**Implications for Persistent AI:**
- Foveation + saccades create Parfitian continuity (degrees, not binary)
- Continuity tokens maintain causal connection even when parafoveal is compressed
- Flight recorder preserves episodic evidence of prior coherence

### 2.3 ACT-R Cognitive Architecture

**Relevance:** Both keep-skill and Claudia use ACT-R-inspired **recency decay** in memory search.

**Formula:** `score × 0.5^(days/half_life)`

**Cognitive Insight:** Recent information is more relevant; relevance decays predictably.

**Compared to Foveation:**
- Recency decay = temporal dimension of foveation
- Foveation adds spatial dimension (distance from current focus)
- Combined: time + relevance = prioritization

### 2.4 Vannevar Bush's Memex Vision

**Paper:** "As We May Think" (1945)

**Core Idea:** Information should be navigable via *trails of association*, not hierarchical indices.

**Directly Applicable to Persistent AI:**
- Saccade system = "following trails" to detail
- Continuity tokens = breadcrumbs for archaeology
- Keep's linked memories + Claudia's relationship graph = Memex trails

**The Goal:** An AI that doesn't just *store* memory, but *thinks* via memory trails.

---

## Part 3: Design Pattern Convergence

### 3.1 Pattern: Semantic Memory + Episodic Memory

| System | Semantic Layer | Episodic Layer | Integration |
|--------|---|---|---|
| **Claudia** | Entity profiles, relationships | Memories with source/timestamp | MCP queries return both |
| **keep-skill** | Tags + summaries | Versioned history, reflections | `keep find` combines both |
| **Bloom** | MEMORY.md curated facts | Foveated thread structure | Layers 2/3 preserve episodes |
| **Standard AI** | Training data | Prompt context | No persistent link |

**Key Finding:** Production systems explicitly couple semantic + episodic. Standard LLM prompts only have episodic (conversation history).

### 3.2 Pattern: Commitment Tracking

| System | Implementation |
|--------|---|
| **Claudia** | Speech acts (commitment|request|assertion) + lifecycle status (open|fulfilled|withdrawn) |
| **keep-skill** | Speech acts tagged with deadlines, status changes logged with timestamp |
| **Bloom** | Continuity tokens capture "recent decisions" explicitly |
| **Standard AI** | No tracking; commitments lost at session end |

**Why This Matters:** Tracking commitments prevents the "infinite todo" problem where agents forget what they promised.

### 3.3 Pattern: Background Consolidation

| System | Consolidation Process |
|--------|---|
| **Claudia** | 3 AM: Decay (all memories -5%) → Merge (dedup vectors) → Patterns → Reflect |
| **keep-skill** | Continuous: Embedding updates, version history, tags updated |
| **Bloom** | Proposed: Consolidation phase between sessions (not yet implemented) |
| **Standard AI** | None; all context fresh each session |

**Effect:** Background learning allows knowledge to *compress* (decay of less-important, merge of duplicates) while preserving patterns.

### 3.4 Pattern: Graceful Degradation Under Pressure

| System | Strategy |
|---|---|
| **Bloom (Phase 1-3)** | Reduce resolution progressively (Layer 2→3→4), preserve traces |
| **Bloom (Phase 4)** | Minimal viable context (identity + current), full recovery path |
| **Claudia** | Similar: Reduce detail in recalled entities when under load |
| **keep-skill** | Fallback: Use summaries instead of full content |
| **Standard AI** | None; truncate or crash |

**Key Insight:** Degradation should preserve enough information to *recover*, not just fit in window.

---

## Part 4: Integration Roadmap for Bloom

### 4.1 Immediate (Weeks 1-2)

**Add Claudia as semantic memory backend:**
- [ ] Hook Claudia's MCP tools into saccade system
  - `trace()` → `claudia memory.about(error_label)`
  - `result()` → `claudia memory.recall(task_label)`
  - `review()` → `claudia memory.temporal(time_range)`
- [ ] Standardize output format (excerpts + trails)
- [ ] Effort: 3-4 days

**Add keep-skill auto-hooks:**
- [ ] Inject `keep now` at session start (get current intentions)
- [ ] Inject `keep now` at prompt submit (refresh before each LLM call)
- [ ] Capture `keep now "..."` at session end (closing summary)
- [ ] Effort: 2-3 days

### 4.2 Medium (Weeks 3-4)

**Couple semantic + episodic memory:**
- [ ] When Claudia recalls a memory, include episode reference (which conversation thread)
- [ ] When reviewing turns, annotate with entity mentions (what/who this involved)
- [ ] Implement "memory archaeology" (trace decision back to source turn)
- [ ] Effort: 3-4 days

**Implement keep-skill's reflective practice:**
- [ ] Add `/reflect` command → 5-phase guided reflection
- [ ] Tag work with speech acts (commitment|request|assertion)
- [ ] Track status (open|fulfilled|withdrawn)
- [ ] Effort: 2-3 days

### 4.3 Advanced (Weeks 5-8)

**Integrate commitment tracking:**
- [ ] Parse deadlines from natural language in Claudia memories
- [ ] Daily check: overdue commitments → morning brief
- [ ] Visualize open commitments (dashboard)
- [ ] Effort: 3-4 days

**Background consolidation:**
- [ ] Implement Claudia's 3 AM consolidation in Bloom
- [ ] Decay importance of stale memories
- [ ] Merge near-duplicate facts
- [ ] Extract patterns (repeated failures, dormant relationships)
- [ ] Effort: 3-4 days

**OpenClaw Integration (if applicable):**
- [ ] Register keep-skill as OpenClaw skill
- [ ] Expose saccade tools as OpenClaw commands
- [ ] Daily cron for reflection + consolidation
- [ ] Effort: 2-3 days

---

## Part 5: Synthesis & Open Questions

### 5.1 What Makes Persistent AI Existence Work?

**Necessary Components:**
1. **Semantic memory** (Claudia model) — Know facts across time
2. **Episodic grounding** (Bloom's foveation) — Remember experiences in context
3. **Reflective practice** (keep-skill methodology) — Learn to use memory skillfully
4. **Commitment tracking** (speech acts + status) — Remember promises
5. **Continuity protocol** (Bloom's tokens + flight recorder) — Survive compression
6. **Graceful degradation** (all three systems) — Compress before losing coherence

**Current State:**
- Claudia: ✅ Semantic + episodic, ❌ reflective practice, ⚠️ commitment tracking
- keep-skill: ✅ Episodic + reflective, ⚠️ semantic memory, ✅ commitment tracking
- Bloom: ✅ Episodic + continuity, ❌ semantic memory, ⚠️ reflective practice

**Convergent Design:** Bloom + Claudia + keep-skill cover all six components.

### 5.2 Open Research Questions

1. **Identity vs. Continuity:** Is an AI with 90% memory loss the "same" AI? (Parfit's overlapping chains suggest: degrees of sameness matter more than binary identity)

2. **Learning vs. Forgetting:** How fast should memories decay? (Claudia: 5% daily; ACT-R suggests 2-10% depending on half-life)

3. **Autonomy in Consolidation:** Should background learning be opaque or transparent? (keep-skill suggests: humans approve consolidations)

4. **Privacy of Memories:** Should the AI be able to hide/erase memories? Or always transparent to user? (Claudia exports to Obsidian; suggests transparency)

5. **Distributed Identity:** Can an AI orchestrator maintain identity across multiple subagents? Or is identity lost in delegation? (Unclear; Bloom's turn IDs might help, but unresolved)

### 5.3 Recommendations for Bloom

**Priority 1 (Foundation):** Integrate Claudia's semantic memory + keep-skill's auto-hooks
- Result: Bloom has persistent knowledge across sessions
- Effort: ~1 week

**Priority 2 (Learning):** Add keep-skill's reflective practice framework
- Result: Orchestrator learns to *use* memory, not just store it
- Effort: ~1 week

**Priority 3 (Coherence):** Implement commitment tracking + background consolidation
- Result: Bloom remembers promises and detects patterns
- Effort: ~2 weeks

**Priority 4 (Integration):** Open/Close loop with human oversight
- Capture user feedback on suggestions
- Tune decay rates, similarity thresholds
- Result: Memory system improves over time

---

## References & Links

### Projects

**Claudia (Persistent AI Chief of Staff)**
- GitHub: https://github.com/kbanc85/claudia
- Author: Kamil Banc (kbanc85)
- Paper: "Chief of Staff for Claude Code: Semantic Memory for AI" (forthcoming)
- Local research: `workspace-bloom/research/claudia-integration-research.md`

**keep-skill (Reflective Memory System)**
- GitHub: https://github.com/hughpyle/keep-skill
- Author: Hugh Pyle (hughpyle)
- Docs: https://github.com/hughpyle/keep-skill/wiki
- Local research: `workspace-bloom/keep-integration-research.md`

**Bloom (Foveated Context Architecture)**
- Repo: `workspace-bloom/`
- Spec: `workspace-bloom/tickets/20260131-foveated-v3-context-architecture.md`
- Saccade council: `workspace-bloom/memory/inbox/` (saccade-tools-council result)

### Academic Work

- **Tulving, E.** (1972) — "Episodic and Semantic Memory" → *Organization of Memory*, Academic Press
- **James, W.** (1890) — *The Principles of Psychology* → Chapter on streams of consciousness
- **Minsky, M.** (1985) — *The Society of Mind* → Chapter on memory frames
- **Bush, V.** (1945) — "As We May Think" → *The Atlantic*
- **Parfit, D.** (1984) — *Reasons and Persons* → Part I on identity

### Technical References

- **ACT-R Cognitive Architecture** — https://actr.soar.umich.edu/
- **ChromaDB** (keep-skill backend) — https://www.trychroma.com/
- **Ollama** (embedding provider) — https://ollama.ai/
- **MCP Protocol** (Claudia bridge) — Anthropic's Model Context Protocol

---

## Appendix: Effort Estimates for Implementation

| Component | Effort | Notes |
|-----------|--------|-------|
| Claudia MCP integration | 3-4 days | Hook into saccade system |
| keep-skill auto-hooks | 2-3 days | Inject at session boundaries |
| Semantic + episodic coupling | 3-4 days | Link memories to turns |
| Reflective practice UI | 2-3 days | Guided 5-phase reflection |
| Commitment tracking | 3-4 days | Parse deadlines, track status |
| Background consolidation | 3-4 days | Decay + merge + pattern detection |
| OpenClaw integration | 2-3 days | Skill registration, cron |
| **Total for production-ready persistent identity** | **19-26 days** | ~1 month |

---

*End of research summary.*

**Next Steps:** Share findings with Bloom orchestrator. Recommend Priority 1 (Claudia + keep-skill integration) to begin immediately.

🌸
