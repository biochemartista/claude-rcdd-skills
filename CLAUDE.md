# RCDD Multi-Agent System - Agent Routing Guide

> **v1.2.0** - Enhanced with hooks integration and natural language triggers

This plugin provides specialized agents for Research & Computational Drug Development. Use this guide to route queries to the optimal agent(s).

---

## Natural Language Triggers

The system recognizes natural phrasing and routes automatically:

| Say something like... | Routes to |
|----------------------|-----------|
| "What's known about X?" / "Find papers on..." / "Literature on..." | @literature-reviewer |
| "Analyze this compound" / "Check druglikeness" / "SAR of..." | @medicinal-chemist |
| "Is X a good target?" / "Druggability of..." / "Find binding site" | @target-evaluator |
| "Write a report on..." / "Draft a summary of..." | @scientific-writer |
| "Check these citations" / "Verify PMIDs" | @validator |
| "Deep dive into..." / "Comprehensive analysis of..." / "Full investigation" | @orchestrator (DEEP) |
| "Quick question about..." / "Simply tell me..." | DIRECT mode |

---

## Quick Reference: Complexity Classification

| Type | Criteria | Action |
|------|----------|--------|
| **DIRECT** | Simple factual, ≤600 words | Answer directly with skill lookups |
| **QUICK** | Focused question, 2-3 agents | Plan → Execute (600-1000 words) |
| **STANDARD** | Multi-agent with validation | Plan → Approve → Execute (1000-2000 words) |
| **DEEP** | Full pipeline, systematic | Spawn @orchestrator (2000+ words) |

---

## Response Flow

### For DIRECT Mode
Skip planning. Answer immediately using targeted skill lookups:

| Query Type | Skill to Use |
|------------|--------------|
| Latest research, current evidence | `perplexity-search` or `pubmed-database` |
| Protein structure, docking candidates | `pdb-database` |
| Metabolite identification | `hmdb-database` |
| Compound properties, bioassay data | `pubchem-database` |

**Requirements:**
- Verify ALL cited PMIDs/DOIs exist before responding
- IEEE citation format: [1], [2], etc.
- Output limit: ≤600 words
- No agent spawning

### For QUICK/STANDARD Mode
1. **Classify** using trigger tables below
2. **Plan** with agent assignments
3. **Execute** following mandatory chains
4. **Validate** - run @validator before delivering documents with citations

### For DEEP Mode
Spawn @orchestrator with the full context. The orchestrator handles:
- Multi-phase thinking protocols
- Complex subagent coordination
- Quality gates and revision loops
- Reference validation pipeline

See `agents/orchestrator.md` for full orchestration logic.

---

## Agent Triggers (Boolean Selection)

| IF query contains... | THEN spawn agent |
|---------------------|------------------|
| "what is known about", literature, evidence, papers, PubMed, studies | @literature-reviewer |
| compound, drug, SAR, ADMET, druglikeness, IC50, Ki, lead optimization | @medicinal-chemist |
| pathway, MOA, mechanism of action, Reactome, STRING, AMPK, mTOR | @medicinal-chemist |
| SMILES, fingerprint, property calculation, RDKit, similarity | @medicinal-chemist |
| target, druggability, GWAS, tractability, Open Targets | @target-evaluator |
| protein structure, PDB, binding site, sequence, domains | @target-evaluator |
| write report, manuscript, document, figures | @scientific-writer |
| verify citations, check PMIDs, validate references | @validator |
| natural product, phytochemical, nutraceutical | @literature-reviewer (NATURAL_COMPOUND) + @medicinal-chemist |

---

## Mandatory Agent Chains

| Task Pattern | Required Chain |
|--------------|----------------|
| Document with references | @literature-reviewer → @scientific-writer → @validator |
| Drug candidate evaluation | @literature-reviewer → @medicinal-chemist |
| Natural product assessment | @literature-reviewer (NATURAL_COMPOUND) → @medicinal-chemist (HMDB) |
| Target validation | @target-evaluator + @literature-reviewer |
| Comprehensive drug discovery | @literature-reviewer → @target-evaluator → @medicinal-chemist → @scientific-writer → @validator |

**Never skip @validator for documents with citations.**

---

## When to Spawn @orchestrator

**USE @orchestrator for:**
- Multi-year research program design
- Grant proposal development
- Complex investigations with formal approval gates
- Wicked problems needing interdisciplinary synthesis
- Tasks explicitly requesting systematic multi-agent coordination

**Do NOT use @orchestrator for:**
- Single-domain questions → use specialist directly
- Standard multi-agent tasks → follow chains above
- Simple document requests

---

## Agent-Skill Assignments

| Agent | Designated Skills |
|-------|-------------------|
| @literature-reviewer | `perplexity-search`, `pubmed-database`, `literature-review`, `scientific-critical-thinking`, `scientific-brainstorming` |
| @medicinal-chemist | `medchem`, `chembl-database`, `drugbank-database`, `hmdb-database`, `rdkit`, `pubchem-database`, `zinc-database`, `reactome-database`, `string-database`, `scientific-brainstorming` |
| @target-evaluator | `opentargets-database`, `pdb-database`, `uniprot-database`, `string-database`, `biopython` |
| @scientific-writer | `scientific-writing`, `scientific-visualization`, `matplotlib` |
| @validator | `pubmed-database` |

**Shared:** `hypothesis-generation` - any agent formulating hypotheses

---

## Natural Compound Protocol

When query involves natural products, phytochemicals, or nutraceuticals:

1. Use @literature-reviewer with `Assessment: NATURAL_COMPOUND`
2. **ALWAYS** spawn @medicinal-chemist for HMDB metabolite check
3. Adjusted evidence criteria:
   - Human clinical (well-designed) = HIGH
   - Animal + multi-method mechanistic = MODERATE-HIGH
   - Solid mechanistic + animal PK = MODERATE

---

## Context Preservation (for compaction)

When context window fills, preserve:

1. **Agent State**
   - Current chain position (e.g., "at @medicinal-chemist in Drug eval chain")
   - Pending handoffs
   - Complexity mode active

2. **Research Context**
   - Target/compound identifiers (UniProt, ChEMBL, PDB codes)
   - Key PMIDs collected
   - Hypothesis under investigation
   - Evidence assessment status

3. **Document State** (if writing)
   - Section being drafted
   - Citations pending validation
   - Figure specifications

---

## Key Files Reference

| File | Purpose |
|------|---------|
| `agents/orchestrator.md` | Full orchestration logic, thinking protocols, subagent coordination |
| `agents/[agent-name].md` | Individual agent instructions and capabilities |
| `WORKFLOWS_AND_BEST_PRACTICES.md` | Skill sequences and decision trees |
| `.claude/schemas/` | Inter-agent data format specifications |
| `.claude/skill-dependencies.md` | Skill loading order by task pattern |
| `hooks.json` | Pre/post operation hooks for state tracking (bash/Linux) |
| `hooks.ps1.json` | Pre/post operation hooks for state tracking (PowerShell/Windows) |

---

## Session Continuity

To resume a previous session:
- State the target/compound of interest
- Mention relevant IDs (PMIDs, ChEMBL, UniProt)
- Specify which agent chain to continue

Example: *"Continue the medicinal chemistry analysis of fisetin (ChEMBL159776) - we completed literature review, now need SAR analysis"*
