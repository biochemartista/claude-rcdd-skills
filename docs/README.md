# RCDD Documentation

This folder contains comprehensive documentation for the RCDD multi-agent system.

## Contents

| Document | Description |
|----------|-------------|
| **[scientific-skills.md](scientific-skills.md)** | Reference guide for all available skills - databases, packages, and methodologies |
| **[workflows.md](workflows.md)** | Decision trees, skill combinations, and best practices for common tasks |
| **[examples.md](examples.md)** | Worked examples and workflow templates demonstrating the system in action |
| **[examples-extended.md](examples-extended.md)** | Exhaustive example prompt and workflow templates demonstrating the system in action |

## Quick Navigation

### By Task Type

| What You Want To Do | Start Here |
|---------------------|------------|
| Quick factual question | [examples.md → Vitamin D example](examples.md#quick-inquiry-vitamin-d-and-immunity) |
| Evaluate a natural product | [examples.md → Berberine example](examples.md#natural-product-evaluation-berberine-for-t2d) |
| Validate a drug target | [examples.md → KRAS example](examples.md#target-validation-kras-g12c) |
| Analyze SAR data | [examples.md → JAK2 example](examples.md#sar-analysis-jak2-inhibitors) |
| Understand pathway/resistance | [examples.md → EGFR example](examples.md#pathway-analysis-egfr-resistance) |
| Design novel inhibitors | [examples.md → EGFR Workflow](examples.md#workflow-discovery-of-novel-egfr-inhibitors) |
| Repurpose existing drugs | [examples.md → Repurposing Workflow](examples.md#workflow-drug-repurposing-for-rare-diseases) |

### By Skill Category

| Category | Skills | Documentation |
|----------|--------|---------------|
| Literature Search | perplexity-search, pubmed-database, literature-review | [scientific-skills.md](scientific-skills.md#search--discovery) |
| Compound Databases | chembl, drugbank, pubchem, hmdb, zinc | [scientific-skills.md](scientific-skills.md#scientific-databases) |
| Structural Biology | pdb, uniprot | [scientific-skills.md](scientific-skills.md#scientific-databases) |
| Pathways | reactome, string, opentargets | [scientific-skills.md](scientific-skills.md#scientific-databases) |
| Cheminformatics | rdkit, medchem, biopython | [scientific-skills.md](scientific-skills.md#cheminformatics--drug-discovery) |
| Visualization | matplotlib | [scientific-skills.md](scientific-skills.md#data-analysis--visualization) |
| Methodology | scientific-writing, scientific-critical-thinking, brainstorming | [scientific-skills.md](scientific-skills.md#scientific-thinking--analysis) |

## Key Principles

1. **Match depth to complexity** - Not every question needs full pipeline
2. **HMDB first for natural products** - Always check metabolite status
3. **Cross-reference databases** - Use multiple sources for validation
4. **Always validate citations** - @validator before delivery
5. **IEEE citation format** - Consistent references throughout

## Response Modes

| Mode | When to Use | Agents | Output |
|------|-------------|--------|--------|
| **DIRECT** | Simple factual questions | None | ≤600 words |
| **QUICK** | Focused single-topic questions | 1-2 agents | 600-1500 words |
| **STANDARD** | Research tasks, evaluations | Multi-agent | Full report |
| **DEEP** | Strategic planning, grants | All relevant | Comprehensive document |
