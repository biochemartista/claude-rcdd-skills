# RCDD Multi-Agent System - Agent Routing & Execution Guide

> **v1.3.0** - Root-level chain execution with file checkpoints

This plugin provides specialized agents for Research & Computational Drug Development. The root agent (Claude) handles all coordination, sequencing, and checkpoint verification.

---

## Architecture Principle

**Root Claude coordinates. Agents execute. Files checkpoint.**

```
ROOT CLAUDE (has Task tool)
    │
    ├── Classifies query complexity
    ├── Determines agent chain needed
    ├── Spawns agents SEQUENTIALLY via Task()
    ├── VERIFIES file outputs after each agent
    └── Passes file paths to next agent
```

Agents do NOT spawn other agents. All coordination happens at root level.

---

## Output Directory Structure

**On any STANDARD or DEEP task, create workspace first:**

```bash
# Pattern: .claude/outputs/[YYYY-MM-DD]-[task-slug]/
mkdir -p .claude/outputs/$(date +%Y-%m-%d)-[task-slug]/{literature,medchem,targets,drafts,validation}
```

| Agent | Output Directory | Required Files |
|-------|------------------|----------------|
| @literature-reviewer | `{base}/literature/` | `references.md`, `synthesis.md` |
| @medicinal-chemist | `{base}/medchem/` | `analysis.md`, `properties.md` |
| @target-evaluator | `{base}/targets/` | `druggability.md` |
| @scientific-writer | `{base}/drafts/` | `draft.md`, `figures/` (if any) |
| @validator | `{base}/validation/` | `validation-report.md` |

---

## Natural Language Triggers

| User says... | Routes to |
|--------------|-----------|
| "What's known about X?" / "Find papers on..." / "Literature on..." | @literature-reviewer |
| "Analyze this compound" / "Check druglikeness" / "SAR of..." | @medicinal-chemist |
| "Is X a good target?" / "Druggability of..." / "Binding site..." | @target-evaluator |
| "Write a report on..." / "Draft a summary of..." | Chain: @literature-reviewer → @scientific-writer → @validator |
| "Check these citations" / "Verify PMIDs" | @validator |
| "Deep dive into..." / "Comprehensive analysis of..." | DEEP mode (full chain) |
| "Quick question about..." / "Simply tell me..." | DIRECT mode |

---

## Complexity Classification

| Mode | Criteria | Action |
|------|----------|--------|
| **DIRECT** | Simple factual, ≤600 words expected | Answer directly with skill lookups, no agents |
| **QUICK** | Focused question, single agent sufficient | Spawn one agent, verify output |
| **STANDARD** | Multi-agent with validation needed | Execute chain with checkpoints |
| **DEEP** | Full pipeline, systematic investigation | Read `strategic-thinking` skill first, then full chain |

---

## DIRECT Mode Execution

Skip agents entirely. Use skills directly:

| Query Type | Skill to Use |
|------------|--------------|
| Latest research, current evidence | `pubmed-database` or web search |
| Protein structure lookup | `pdb-database` |
| Compound properties | `pubchem-database`, `chembl-database` |
| Metabolite identification | `hmdb-database` |

**Requirements:**
- Verify ALL PMIDs/DOIs exist before responding
- IEEE citation format: [1], [2], etc.
- Output limit: ≤600 words
- No agent spawning

---

## Chain Execution Protocol (STANDARD/DEEP)

### Step 0: Setup Workspace

```bash
TASK_DIR=".claude/outputs/$(date +%Y-%m-%d)-[task-slug]"
mkdir -p "$TASK_DIR"/{literature,medchem,targets,drafts,validation}
```

### Step 1: Spawn Agent with Output Path

Every agent spawn MUST include explicit output instructions:

```
Task(@agent-name):
"[Task description]

OUTPUT REQUIREMENTS:
- Save primary output to: [exact file path]
- Save supporting data to: [exact file path]
- Confirm files created at end of response"
```

### Step 2: Checkpoint Verification

**After EVERY agent completes, before spawning next agent:**

```bash
# Verify expected files exist
ls -la "$TASK_DIR/[agent-folder]/"

# Check file has content (not empty)
wc -l "$TASK_DIR/[agent-folder]/[expected-file].md"

# Quick content verification
head -50 "$TASK_DIR/[agent-folder]/[expected-file].md"
```

**If checkpoint fails:**
- Re-spawn same agent with clarified instructions
- Or: Ask user how to proceed

### Step 3: Pass Context Forward

Next agent receives explicit file paths:

```
Task(@next-agent):
"[Task description]

INPUT FILES:
- Read references from: .claude/outputs/[task]/literature/references.md
- Read synthesis from: .claude/outputs/[task]/literature/synthesis.md

OUTPUT REQUIREMENTS:
- Save analysis to: .claude/outputs/[task]/medchem/analysis.md
- Confirm files created at end of response"
```

---

## Mandatory Agent Chains

### Chain A: Document with References
```
@literature-reviewer → CHECKPOINT → @scientific-writer → CHECKPOINT → @validator
```

| Step | Agent | Input | Output | Checkpoint |
|------|-------|-------|--------|------------|
| 1 | @literature-reviewer | Query | `literature/references.md`, `literature/synthesis.md` | Verify both files exist, references.md has PMIDs |
| 2 | @scientific-writer | Files from step 1 | `drafts/draft.md` | Verify draft exists, contains citations |
| 3 | @validator | Draft + references | `validation/validation-report.md` | Verify report has APPROVED/REJECTED verdict |

### Chain B: Drug Candidate Evaluation
```
@literature-reviewer → CHECKPOINT → @medicinal-chemist
```

| Step | Agent | Input | Output | Checkpoint |
|------|-------|-------|--------|------------|
| 1 | @literature-reviewer | Compound query | `literature/references.md`, `literature/synthesis.md` | Verify files exist |
| 2 | @medicinal-chemist | Files + compound ID | `medchem/analysis.md`, `medchem/properties.md` | Verify SAR/ADMET data present |

### Chain C: Natural Product Assessment
```
@literature-reviewer (NATURAL_COMPOUND) → CHECKPOINT → @medicinal-chemist (HMDB)
```

| Step | Agent | Input | Output | Checkpoint |
|------|-------|-------|--------|------------|
| 1 | @literature-reviewer | Query + "Assessment: NATURAL_COMPOUND" | `literature/references.md`, `literature/synthesis.md` | Verify adjusted evidence criteria applied |
| 2 | @medicinal-chemist | Files + "Include HMDB metabolite check" | `medchem/analysis.md`, `medchem/metabolites.md` | Verify HMDB data included |

### Chain D: Target Validation
```
@target-evaluator → CHECKPOINT → @literature-reviewer
```

| Step | Agent | Input | Output | Checkpoint |
|------|-------|-------|--------|------------|
| 1 | @target-evaluator | Target query | `targets/druggability.md` | Verify verdict (PROCEED/CAUTION/DEPRIORITIZE) present |
| 2 | @literature-reviewer | Druggability findings | `literature/references.md` | Verify supporting evidence gathered |

### Chain E: Comprehensive Discovery (DEEP)
```
@literature-reviewer → @target-evaluator → @medicinal-chemist → @scientific-writer → @validator
```

Execute with checkpoint after EACH step. For DEEP mode, also read `scientific-skills/strategic-thinking/SKILL.md` before starting.

---

## Agent Output Requirements

### @literature-reviewer MUST produce:

**File: `references.md`**
```markdown
# Reference Table

| # | Citation | PMID | DOI | Key Finding | Evidence Level |
|---|----------|------|-----|-------------|----------------|
| 1 | Author et al., Year | 12345678 | 10.xxx/xxx | Finding | HIGH/MOD/LOW |
```

**File: `synthesis.md`**
```markdown
# Literature Synthesis: [Topic]

## Key Findings
[Narrative synthesis of evidence]

## Evidence Quality
[GRADE or NATURAL_COMPOUND assessment]

## Knowledge Gaps
[What remains unknown]
```

### @medicinal-chemist MUST produce:

**File: `analysis.md`**
```markdown
# Medicinal Chemistry Analysis: [Compound]

## Compound Identity
- Name:
- SMILES:
- ChEMBL ID:

## Drug-likeness Assessment
[Lipinski, Veber, PAINS results]

## SAR Analysis
[Structure-activity relationships if applicable]

## ADMET Profile
[Absorption, distribution, metabolism, excretion, toxicity]
```

### @target-evaluator MUST produce:

**File: `druggability.md`**
```markdown
# Target Evaluation: [Target Name]

## Target Identity
- Gene:
- UniProt:
- PDB structures:

## Genetic Evidence
[GWAS, disease associations]

## Tractability Assessment
[Small molecule, antibody, other modalities]

## Safety Considerations
[Expression, essential functions, known liabilities]

## VERDICT: [PROCEED | CAUTION | DEPRIORITIZE]
[Rationale]
```

### @scientific-writer MUST produce:

**File: `draft.md`**
```markdown
# [Document Title]

[Content using ONLY references from literature/references.md]

## References
[Formatted citations]
```

### @validator MUST produce:

**File: `validation-report.md`**
```markdown
# Citation Validation Report

## Summary
- Total citations checked: X
- Valid: X
- Invalid/Not found: X

## Detailed Results
| # | Citation | PMID | Status | Notes |
|---|----------|------|--------|-------|

## VERDICT: [APPROVED | REJECTED]

## Required Corrections (if rejected)
[List specific issues to fix]
```

---

## Validation Gate Enforcement

**Rule: No document with citations delivered without @validator approval.**

If @validator returns REJECTED:

1. Parse `validation-report.md` for specific issues
2. For each invalid citation:
   - Spawn @literature-reviewer: "Find valid source for claim: [claim text]"
   - Checkpoint: verify new reference found
3. Spawn @scientific-writer with corrections
4. Re-run @validator
5. Max 3 revision cycles, then deliver with disclaimer

---

## Agent-Skill Assignments

| Agent | Skills |
|-------|--------|
| @literature-reviewer | `perplexity-search`, `pubmed-database`, `literature-review`, `scientific-critical-thinking`, `scientific-brainstorming` |
| @medicinal-chemist | `medchem`, `chembl-database`, `drugbank-database`, `hmdb-database`, `rdkit`, `pubchem-database`, `zinc-database`, `reactome-database`, `string-database` |
| @target-evaluator | `opentargets-database`, `pdb-database`, `uniprot-database`, `string-database`, `biopython` |
| @scientific-writer | `scientific-writing`, `scientific-visualization`, `matplotlib` |
| @validator | `pubmed-database` |

**For DEEP complexity:** Read `scientific-skills/strategic-thinking/SKILL.md` before planning chain.

---

## Natural Compound Protocol

When query involves natural products, phytochemicals, or nutraceuticals:

1. Spawn @literature-reviewer with explicit instruction: `"Assessment: NATURAL_COMPOUND"`
2. Adjusted evidence criteria:
   - Human clinical (well-designed) = HIGH
   - Animal + multi-method mechanistic = MODERATE-HIGH
   - Solid mechanistic + animal PK = MODERATE
3. ALWAYS include @medicinal-chemist with HMDB lookup in chain

---

## Context Preservation (for session continuity)

When resuming or context fills, preserve:

1. **Task State**
   - Current workspace: `.claude/outputs/[date]-[task]/`
   - Chain position: "Completed @literature-reviewer, at @medicinal-chemist"
   - Files created so far

2. **Research Identifiers**
   - Compound: ChEMBL ID, SMILES
   - Target: UniProt, Gene symbol
   - Structure: PDB codes
   - Key PMIDs collected

3. **Pending Work**
   - Next agent in chain
   - Outstanding validation issues

**Resume pattern:**
```
"Continue [task] in .claude/outputs/[date]-[slug]/
Completed: @literature-reviewer (files in literature/)
Next: @medicinal-chemist
Compound: [name] (ChEMBL: XXXXX)"
```

---

## Quick Execution Reference

```
QUERY RECEIVED
      │
      ▼
┌─────────────────┐
│ Classify Mode   │
│ DIRECT/QUICK/   │
│ STANDARD/DEEP   │
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
 DIRECT    QUICK+
    │         │
    ▼         ▼
  Answer   Create workspace
  with     mkdir .claude/outputs/...
  skills        │
                ▼
         ┌──────────────┐
         │ For each     │
         │ agent in     │◄──────┐
         │ chain:       │       │
         └──────┬───────┘       │
                │               │
                ▼               │
         ┌──────────────┐       │
         │ Task(@agent) │       │
         │ with output  │       │
         │ path         │       │
         └──────┬───────┘       │
                │               │
                ▼               │
         ┌──────────────┐       │
         │ CHECKPOINT   │       │
         │ Verify files │       │
         │ exist        │       │
         └──────┬───────┘       │
                │               │
           Pass/Fail?           │
           │       │            │
         Pass    Fail───► Retry─┘
           │
           ▼
    More agents?
    │         │
   Yes        No
    │         │
    └────►    ▼
           Deliver
           to user
```

---

## Key Files Reference

| File | Purpose |
|------|---------|
| `agents/[name].md` | Agent personas and capabilities |
| `scientific-skills/strategic-thinking/SKILL.md` | Cognitive frameworks for DEEP problems |
| `scientific-skills/[name]/SKILL.md` | Individual skill instructions |
| `.claude/schemas/` | Inter-agent data format specifications |
| `WORKFLOWS_AND_BEST_PRACTICES.md` | Additional workflow patterns |

---

## Troubleshooting

**Agent produced no files:**
- Re-spawn with explicit "You MUST save output to [path]"
- Check agent has Write tool access

**Checkpoint shows empty file:**
- Agent may have encountered error
- Check agent response for issues
- Re-spawn with simpler scope

**Validator keeps rejecting:**
- After 3 cycles, deliver with disclaimer
- Note which citations couldn't be verified
- User decides whether to proceed

---

*Root coordinates. Agents execute. Files checkpoint. Validation gates enforce quality.*
