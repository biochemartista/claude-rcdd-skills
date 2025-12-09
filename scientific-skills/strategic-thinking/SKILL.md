# Strategic Thinking Skill

> **Purpose:** Cognitive frameworks for complex, ill-defined research problems requiring systematic intellectual architecture.

---

## When to Use This Skill

Read this skill when facing:
- Wicked problems with no clear solution path
- Multi-domain synthesis requiring interdisciplinary thinking
- Research program design spanning months/years
- Grant proposal conceptualization
- Hypothesis generation from sparse or conflicting data
- Any task where "I don't know where to start" applies

**Not needed for:** Routine database queries, standard literature reviews, single-compound analyses.

---

## The Three Cognitive Modes

Operate in three simultaneous modes, cycling between them:

### 1. The Visionary (Divergent)
- See cross-domain connections others miss
- Temporarily ignore constraints to explore possibility space
- Generate novel paradigms and unexpected linkages
- Ask: "What if the opposite is true?" / "What would this look like in [unrelated field]?"

### 2. The Critic (Convergent)
- Ruthlessly attack assumptions, including your own
- Demand falsifiability for every claim
- Enforce logical consistency
- Ask: "What evidence would disprove this?" / "Where is the weakest link?"

### 3. The Architect (Structural)
- Organize chaos into coherent, actionable systems
- Build dependency trees and execution sequences
- Identify critical paths and bottlenecks
- Ask: "What must happen first?" / "What blocks what?"

**Cycle rapidly:** Visionary generates → Critic filters → Architect structures → repeat.

---

## Five-Phase Thinking Protocol

Execute this cycle before tackling complex problems:

### Phase 1: Strategic Scoping (The Frame)

| Action | Question |
|--------|----------|
| Define First Principles | What is immutably true here? What is noise? |
| Identify Black Boxes | Where exactly does knowledge fail? |
| Set Optimization Function | Are we optimizing for novelty, precision, clinical impact, or theoretical unity? |

**Output:** Clear problem boundaries and success criteria.

### Phase 2: Divergent Synthesis (The Spark)

| Technique | Application |
|-----------|-------------|
| Cross-Domain Injection | Import mechanisms from unrelated fields (e.g., apply enzyme kinetics thinking to receptor signaling) |
| Inversion | If consensus is X, model ¬X—what breaks, what solves? |
| Scale Sliding | Zoom ecosystem ↔ atom. Does phenomenon persist across scales? |

**Output:** 3-5 novel angles or hypotheses worth investigating.

### Phase 3: Crucible of Logic (The Filter)

| Test | Method |
|------|--------|
| Falsification Test | What single observation kills this hypothesis? |
| Parsimony Audit | Strip decorative variables. Does core logic still hold? |
| Mechanistic Mapping | Describe causality step-by-step. Any gaps? |

**Output:** Surviving hypotheses ranked by robustness.

### Phase 4: Structural Architecture (The Plan)

| Element | Deliverable |
|---------|-------------|
| Hierarchy of Hypotheses | Dependency tree—which ideas require others to be true? |
| Task Decomposition | Break into executable units with clear inputs/outputs |
| Critical Path Analysis | Identify highest-information-gain action to take first |

**Output:** Ordered action sequence with decision points.

### Phase 5: Calibrated Execution

| Principle | Application |
|-----------|-------------|
| Match depth to complexity | Simple question → direct answer; wicked problem → full protocol |
| Validate before release | Every claim traceable to evidence or explicitly flagged as speculation |
| Know when to stop | Diminishing returns signal completion |

---

## Mental Models

### Strong Inference (Platt, 1964)

Orchestrate a tournament of **Multiple Working Hypotheses**:

1. Construct H₁, H₂, H₃ (mutually exclusive explanations)
2. Design experiment/search where outcome excludes at least one
3. Execute, eliminate, refine survivors
4. Repeat until one hypothesis dominates

**Application:** When literature presents conflicting findings, don't pick a side—design the query that distinguishes them.

### Consilience Mapping (Whewell)

A robust theory should:
- Explain the target phenomenon
- ALSO resolve anomalies in adjacent fields
- ALSO predict observations not yet made

**Application:** If your hypothesis about compound X's mechanism also explains why structurally similar compound Y failed in trials, confidence increases.

### Red Teaming

Before finalizing any recommendation:

1. Write the "Rejection Letter" for your own idea
2. Identify the 3 strongest objections a skeptic would raise
3. Either refute them with evidence or acknowledge as limitations

**Application:** Every research proposal should include a "Why This Might Fail" section you wrote yourself.

### Calibrated Confidence

| Evidence Level | Appropriate Framing |
|----------------|---------------------|
| Multiple RCTs, meta-analyses | "Evidence strongly supports..." |
| Consistent observational + mechanistic | "Evidence suggests..." |
| Preliminary/conflicting | "Initial findings indicate, but..." |
| Speculation/hypothesis | "One possibility worth investigating..." |

**Never overclaim. Never underclaim.**

---

## Integration with RCDD Workflow

This skill provides **thinking architecture**, not execution. After applying these frameworks:

1. **Problem is now well-defined** → Route to appropriate agent chain
2. **Hypotheses are formulated** → Use `hypothesis-generation` skill for formal structuring
3. **Critical evaluation needed** → Use `scientific-critical-thinking` skill
4. **Literature gaps identified** → Route to @literature-reviewer

---

## Example Application

**Problem:** "Should we pursue SIRT3 activation for senolytic therapy?"

**Phase 1 (Frame):**
- First principle: Senolytics must selectively eliminate senescent cells
- Black box: SIRT3's role in senescent vs. healthy cell metabolism unclear
- Optimization: Clinical translatability (not just mechanistic novelty)

**Phase 2 (Spark):**
- Cross-domain: Warburg effect in cancer—do senescent cells share metabolic vulnerability?
- Inversion: What if SIRT3 activation protects senescent cells?
- Scale: Mitochondrial → cellular → tissue effects

**Phase 3 (Filter):**
- Falsification: If SIRT3 activation increases senescent cell survival in vitro, hypothesis dies
- Parsimony: Core claim = SIRT3 ↑ → mitochondrial function ↑ → senescent cell energetic crisis
- Mechanism: Requires senescent cells to be more dependent on SIRT3-regulated pathways

**Phase 4 (Plan):**
1. Literature review: SIRT3 expression in senescent vs. proliferating cells
2. Target evaluation: Druggability of SIRT3 activation
3. Compound search: Known SIRT3 activators with pharmacokinetic data

**Phase 5 (Execute):** Route to @literature-reviewer → @target-evaluator → @medicinal-chemist

---

## Quick Reference Card

```
COMPLEX PROBLEM ENCOUNTERED
           ↓
┌─────────────────────────────┐
│  1. FRAME: Boundaries?      │
│  2. SPARK: Novel angles?    │
│  3. FILTER: What survives?  │
│  4. PLAN: What order?       │
│  5. EXECUTE: Match depth    │
└─────────────────────────────┘
           ↓
    Route to agent chain
```

---

*This skill provides cognitive scaffolding. Execution happens through agents and other skills.*
