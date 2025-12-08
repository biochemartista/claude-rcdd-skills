# RCDD Skills: Workflows & Best Practices

## Overview

This guide provides practical workflows showing how skills combine for common drug discovery tasks. Each workflow includes decision points, skill sequences, and real examples.

---

## Quick Reference: Skill Categories

| Category | Skills | Primary Use |
|----------|--------|-------------|
| **Search** | perplexity-search, pubmed-database | Finding literature |
| **Compound Data** | chembl-database, drugbank-database, pubchem-database, hmdb-database | Bioactivity, properties |
| **Structural** | pdb-database, pdb-database, uniprot-database | Protein structures |
| **Pathways** | reactome-database, reactome-database, string-database, opentargets-database | Biological context |
| **Cheminformatics** | rdkit, medchem | Molecular analysis |
| **Methodology** | scientific-writing, scientific-critical-thinking, scientific-brainstorming | Process & output |

---

## Workflow 1: Quick Literature Inquiry

**Scenario:** User asks a focused scientific question requiring brief, cited answer.

**Example:** "Does curcumin have anti-inflammatory activity?"

### Decision Tree

```
Is question simple & factual?
    │
    ├─ YES → DIRECT Mode (no agent delegation)
    │         └─ Orchestrator synthesizes directly
    │         └─ Optional: Quick PubMed verification
    │         └─ Output: ≤600 words with IEEE citations
    │
    └─ NO → Escalate to QUICK/STANDARD mode
```

### Skill Sequence

```
1. [Optional] pubmed-database
   └─ Quick search: "curcumin anti-inflammatory"
   └─ Retrieve 3-5 key PMIDs for citation

2. Orchestrator synthesis
   └─ Combine knowledge + retrieved citations
   └─ Format as flowing prose with [1], [2] references
```

### Best Practices

- **Don't over-engineer simple questions** - DIRECT mode exists for a reason
- **Cite foundational + recent work** - Mix seminal papers with current findings
- **Include molecular targets** - Name 3-5 key proteins/pathways
- **State evidence quality** - "Meta-analyses show..." vs "Preliminary data suggests..."

### Example Output Structure

```
[Opening: Direct answer to question]
[Body: 2-3 mechanisms with molecular targets]
[Key proteins: Table or inline list]
[Clinical relevance: Human data if available]
[References: IEEE format, 5-10 citations]
```

---

## Workflow 2: Compound Mechanism Investigation

**Scenario:** User wants to understand how a compound works at molecular level.

**Example:** "What is the mechanism of action of metformin?"

### Decision Tree

```
Is compound well-known (approved drug)?
    │
    ├─ YES → Start with drugbank-database
    │         └─ Get established mechanisms
    │         └─ Then literature for recent discoveries
    │
    └─ NO (natural product/novel) → Start with literature
              └─ perplexity-search (broad)
              └─ Then chembl-database for bioactivity
```

### Skill Sequence (Approved Drug)

```
1. drugbank-database
   └─ Query: compound name
   └─ Extract: targets, pathways, pharmacology
   └─ Output: Established mechanism summary

2. chembl-database
   └─ Query: compound for bioactivity data
   └─ Extract: IC50/EC50 values, target selectivity
   └─ Output: Quantitative activity profile

3. reactome-database OR reactome-database
   └─ Query: primary target gene
   └─ Extract: pathway context
   └─ Output: Systems-level understanding

4. pubmed-database OR perplexity-search
   └─ Query: "[compound] mechanism recent"
   └─ Extract: Novel mechanisms, controversies
   └─ Output: Current research frontier
```

### Skill Sequence (Natural Product)

```
1. hmdb-database (CRITICAL FIRST STEP)
   └─ Query: compound name
   └─ Check: Is it endogenous metabolite?
   └─ Output: Metabolite status + pathways if found

2. perplexity-search
   └─ Mode: NATURAL_COMPOUND assessment
   └─ Query: "[compound] mechanism molecular target"
   └─ Output: Literature synthesis + evidence quality

3. chembl-database
   └─ Query: compound bioactivity
   └─ Output: Known targets + IC50 data

4. pubchem-database
   └─ Query: compound properties
   └─ Output: Structure, properties, bioassay results
```

### Best Practices

- **Always check HMDB for natural products** - Critical for identifying metabolite status
- **Distinguish primary vs secondary targets** - Note selectivity
- **Include quantitative data** - IC50, Ki, EC50 values with conditions
- **Note species differences** - Human vs rodent data

---

## Workflow 3: Target Validation Assessment

**Scenario:** Evaluate whether a gene/protein is a viable drug target.

**Example:** "Is PCSK9 a good target for cardiovascular disease?"

### Skill Sequence

```
1. opentargets-database (PRIMARY)
   └─ Query: gene symbol
   └─ Extract: 
      • Tractability (small molecule, antibody, etc.)
      • Genetic evidence (GWAS, rare variants)
      • Safety signals (constraint scores, phenotypes)
      • Known drugs (clinical precedence)
   └─ Output: Druggability scorecard

2. uniprot-database
   └─ Query: gene symbol → UniProt AC
   └─ Extract:
      • Protein function
      • Domain architecture
      • Subcellular localization
      • Isoforms
   └─ Output: Protein profile

3. pdb-database + pdb-database
   └─ Query: UniProt AC
   └─ Extract:
      • Experimental structures (count, resolution)
      • Ligand-bound structures
      • AlphaFold pLDDT scores
      • Binding site druggability
   └─ Output: Structural readiness assessment

4. string-database
   └─ Query: gene symbol
   └─ Extract:
      • Interaction partners
      • Pathway enrichment
      • Functional context
   └─ Output: Network position

5. perplexity-search OR pubmed-database
   └─ Query: "[target] [disease] drug development"
   └─ Extract: Competitive landscape, clinical progress
   └─ Output: Development status
```

### Decision Matrix

| Factor | Green Flag | Yellow Flag | Red Flag |
|--------|------------|-------------|----------|
| Tractability | Clinical precedence | Predicted tractable | Unknown |
| Genetics | Strong GWAS + rare variants | GWAS only | No genetic link |
| Safety | pLI < 0.5, no severe phenotypes | pLI 0.5-0.9 | pLI > 0.9, lethal KO |
| Structure | High-res ligand-bound | AlphaFold high pLDDT | No structure |
| Expression | Tissue-restricted | Moderate breadth | Ubiquitous |

### Best Practices

- **Start with Open Targets** - Most comprehensive single source
- **Cross-validate genetic evidence** - GWAS + rare variants = strong
- **Check structural druggability** - Pocket existence matters
- **Assess competitive landscape** - Crowded targets need differentiation

---

## Workflow 4: Natural Product Drug Candidate Evaluation

**Scenario:** Comprehensive assessment of natural compound for drug development.

**Example:** "Evaluate honokiol as a potential anticancer agent"

### Skill Sequence

```
1. hmdb-database (ALWAYS FIRST)
   └─ Query: "honokiol"
   └─ Critical check: Endogenous metabolite?
   └─ Output: Metabolite status, pathways, concentrations

2. pubchem-database
   └─ Query: compound name → CID
   └─ Extract: Structure, SMILES, properties, synonyms
   └─ Output: Chemical identity confirmed

3. rdkit (via @medicinal-chemist)
   └─ Input: SMILES
   └─ Calculate: MW, LogP, TPSA, HBD, HBA, Ro5
   └─ Output: Druglikeness profile

4. perplexity-search
   └─ Mode: NATURAL_COMPOUND
   └─ Depth: DEEP
   └─ Queries:
      • "honokiol mechanism anticancer molecular"
      • "honokiol pharmacokinetics bioavailability"
      • "honokiol clinical trials human"
   └─ Output: Literature synthesis + evidence quality ratings

5. chembl-database
   └─ Query: compound bioactivity
   └─ Extract: All targets, IC50 values, selectivity
   └─ Output: Target profile + potency data

6. reactome-database + reactome-database
   └─ Query: Primary targets identified
   └─ Extract: Pathway context, crosstalk
   └─ Output: Systems-level mechanism map

7. medchem (via @medicinal-chemist)
   └─ Input: All above data
   └─ Analyze: SAR, ADMET, liabilities, optimization potential
   └─ Output: Medicinal chemistry assessment
```

### Natural Compound Evidence Criteria

| Level | Criteria | Example |
|-------|----------|---------|
| HIGH | Human clinical data, well-designed | Phase II RCT with PK |
| MODERATE-HIGH | Animal efficacy + multi-method mechanistic | Xenograft + WB + RNA-seq |
| MODERATE | Solid mechanistic, animal PK | Multiple cell lines, mouse PK |
| LOW-MODERATE | Single method, sound methodology | One assay type, good controls |
| LOW | Preliminary in vitro, concerns | Single study, no controls |

### Best Practices

- **HMDB first, always** - Metabolite status changes everything
- **Assess bioavailability early** - Often the limiting factor
- **Weight mechanistic rigor** - Multi-method validation = higher confidence
- **Identify formulation opportunities** - Poor bioavailability ≠ mechanism invalid
- **Consider dietary exposure** - Baseline intake affects dosing strategy

---

## Workflow 5: SAR Analysis & Lead Optimization

**Scenario:** Analyze structure-activity relationships and propose optimizations.

**Example:** "Analyze SAR of kinase inhibitor series and suggest improvements"

### Skill Sequence

```
1. rdkit (via @medicinal-chemist)
   └─ Input: Compound SMILES list + activity data
   └─ Calculate: Properties for all compounds
   └─ Generate: Fingerprints, similarity matrix
   └─ Output: Property table, chemical space visualization

2. chembl-database
   └─ Query: Target + similar scaffolds
   └─ Extract: Published SAR, activity cliffs
   └─ Output: Literature SAR context

3. pubmed-database OR perplexity-search
   └─ Query: "[target] SAR structure-activity [scaffold]"
   └─ Extract: Published optimization strategies
   └─ Output: Reference SAR from literature

4. pdb-database
   └─ Query: Target with ligands bound
   └─ Extract: Binding mode, key interactions
   └─ Output: Structure-based design insights

5. medchem (via @medicinal-chemist)
   └─ Input: All above + activity data
   └─ Analyze:
      • Activity cliffs identification
      • Pharmacophore mapping
      • ADMET liability assessment
      • Optimization proposals
   └─ Output: SAR report + prioritized modifications

6. rdkit (via @medicinal-chemist)
   └─ Input: Proposed analog SMILES
   └─ Calculate: Predicted properties
   └─ Output: Property predictions for proposals
```

### SAR Analysis Checklist

- [ ] Core scaffold identified
- [ ] Key pharmacophoric features mapped
- [ ] Activity cliffs documented
- [ ] Potency vs selectivity trade-offs noted
- [ ] ADMET liabilities flagged
- [ ] Metabolic soft spots identified
- [ ] Synthetic accessibility considered
- [ ] Patent landscape checked

### Best Practices

- **Map the pharmacophore first** - Essential vs tolerated features
- **Identify activity cliffs** - Small changes, big effects
- **Balance potency with properties** - Don't optimize into a corner
- **Consider metabolic stability early** - Blocks soft spots proactively
- **Check synthetic feasibility** - Beautiful molecules need to be makeable

---

## Workflow 6: Literature Review for Report/Grant

**Scenario:** Comprehensive literature review for formal document.

**Example:** "Literature review on PROTAC technology for grant proposal"

### Skill Sequence

```
1. perplexity-search (BROAD SYNTHESIS)
   └─ Depth: DEEP
   └─ Queries:
      • "PROTAC protein degradation technology overview"
      • "PROTAC clinical trials progress 2023 2024"
      • "PROTAC advantages limitations challenges"
   └─ Output: Broad landscape synthesis

2. pubmed-database (SYSTEMATIC)
   └─ Query with MeSH: "Proteolysis Targeting Chimera"[MeSH] 
   └─ Filters: Review, last 5 years
   └─ Output: Key reviews for background

3. pubmed-database (PRIMARY LITERATURE)
   └─ Query: "PROTAC" AND "clinical trial"
   └─ Filters: Clinical Trial, last 3 years
   └─ Output: Clinical development data

4. scientific-critical-thinking
   └─ Apply: GRADE framework to evidence
   └─ Assess: Study quality, bias, gaps
   └─ Output: Evidence quality ratings

5. scientific-writing (via @scientific-writer)
   └─ Input: Reference table + synthesis
   └─ Constraint: ONLY cite from provided refs
   └─ Output: Draft literature review

6. validator (MANDATORY)
   └─ Input: Draft document
   └─ Check: All PMIDs real, claims supported
   └─ Output: Validation report
```

### Literature Search Strategy Matrix

| Question Type | Primary Tool | Secondary Tool | Rationale |
|---------------|--------------|----------------|-----------|
| "What is known about X" | perplexity-search | pubmed-database | Broad synthesis needed |
| Specific mechanism | pubmed-database | perplexity-search | MeSH terms effective |
| Recent developments | perplexity-search | - | Preprints, non-indexed |
| Clinical evidence | pubmed-database | - | Structured trial data |
| Controversial topic | perplexity-search | pubmed-database | Reasoning weighs sources |
| Systematic review | pubmed-database | perplexity-search | Reproducible methodology |

### Best Practices

- **Start broad, then focus** - Perplexity for landscape, PubMed for specifics
- **Verify all citations** - Never deliver without @validator
- **Assess evidence quality** - Not all papers are equal
- **Identify gaps explicitly** - What ISN'T known matters for grants
- **Balance recency with foundations** - Cite seminal + recent work

---

## Workflow 7: Pathway Analysis for Target Context

**Scenario:** Understand biological context of a target for drug discovery.

**Example:** "What pathways does EGFR participate in and what are implications for drug resistance?"

### Skill Sequence

```
1. uniprot-database
   └─ Query: "EGFR" → UniProt AC (P00533)
   └─ Extract: Function, GO terms, domains
   └─ Output: Protein identity + annotations

2. reactome-database
   └─ Query: hsa:1956 (EGFR KEGG ID)
   └─ kegg_link: Find all pathways
   └─ kegg_get: Retrieve pathway details
   └─ Output: KEGG pathway memberships

3. reactome-database
   └─ Query: UniProt P00533
   └─ Extract: Participating pathways, reactions
   └─ Output: Reactome pathway context

4. string-database
   └─ Query: EGFR, organism 9606
   └─ Extract: Top interaction partners
   └─ Enrichment: Pathway enrichment analysis
   └─ Output: Network context + functional clustering

5. opentargets-database
   └─ Query: ENSG00000146648 (EGFR)
   └─ Extract: Disease associations, genetic evidence
   └─ Output: Disease relevance

6. perplexity-search
   └─ Query: "EGFR resistance mechanisms pathway crosstalk"
   └─ Output: Literature on resistance + bypass pathways
```

### Pathway Integration Checklist

- [ ] All three pathway databases queried (KEGG, Reactome, STRING)
- [ ] Consensus pathways identified
- [ ] Crosstalk pathways mapped
- [ ] Feedback loops noted
- [ ] Resistance mechanisms reviewed
- [ ] Combination targets identified

### Best Practices

- **Use all three pathway databases** - Different curation, complementary
- **Map crosstalk explicitly** - Where pathways connect matters
- **Consider feedback loops** - Predict resistance mechanisms
- **Identify combination opportunities** - Bypass pathways = combination targets
- **Note tissue context** - Pathway activity varies by tissue

---

## Skill Combination Quick Reference

### For Compound Questions

| Question | Skill Combination |
|----------|-------------------|
| "What is X?" (identity) | pubchem → rdkit |
| "Is X a metabolite?" | hmdb (first!) |
| "What does X target?" | chembl → drugbank |
| "What are X's properties?" | rdkit → pubchem |
| "How does X work?" | chembl → kegg/reactome → literature |

### For Target Questions

| Question | Skill Combination |
|----------|-------------------|
| "Is X druggable?" | opentargets → pdb → alphafold |
| "What pathways involve X?" | kegg → reactome → string |
| "Is X safe to target?" | opentargets (safety) → literature |
| "What's X's structure?" | pdb → alphafold → uniprot |
| "What interacts with X?" | string → literature |

### For Literature Questions

| Question | Skill Combination |
|----------|-------------------|
| Broad overview | perplexity-search |
| Specific data | pubmed-database |
| Clinical evidence | pubmed-database (filters) |
| Verify citation | pubmed-database → web fetch |
| Evidence quality | scientific-critical-thinking |

---

## Anti-Patterns: What NOT to Do

### ❌ Don't Skip HMDB for Natural Products
```
WRONG: Query chembl → rdkit → literature
RIGHT: Query hmdb FIRST → then chembl → rdkit → literature
```

### ❌ Don't Deliver Without Validation
```
WRONG: @scientific-writer → deliver to user
RIGHT: @scientific-writer → @validator → deliver
```

### ❌ Don't Use Full Pipeline for Simple Questions
```
WRONG: "What is aspirin?" → create plan → multi-agent → report
RIGHT: "What is aspirin?" → DIRECT mode → 400 word answer
```

### ❌ Don't Rely on Single Database
```
WRONG: Query KEGG only for pathway analysis
RIGHT: Query KEGG + Reactome + STRING, find consensus
```

### ❌ Don't Fabricate Citations
```
WRONG: [Citation needed] → make up plausible PMID
RIGHT: [Citation needed] → flag gap → request from @literature-reviewer
```

---

## Skill Loading Protocol

Before using any skill, agents MUST:

```
1. READ the SKILL.md file
   └─ Contains: API details, parameters, examples, references

2. CHECK references/ folder if exists
   └─ Contains: Supporting documentation, lookup tables

3. FOLLOW the skill's specified workflow
   └─ Don't improvise - skills encode best practices

4. REPORT per skill's output format
   └─ Standardized output enables downstream integration
```

### Example Skill Loading

```markdown
## Before querying ChEMBL:

1. Read: scientific-skills/chembl-database/SKILL.md
2. Note: API endpoints, query parameters, output format
3. Check: references/target_types.md for classification
4. Execute: Query per skill instructions
5. Output: Format per skill specification
```

---

## Summary: When to Use What

| Situation | Start With | Then Add |
|-----------|------------|----------|
| Quick factual question | DIRECT synthesis | Optional PubMed verify |
| Compound mechanism | drugbank/chembl | kegg/reactome, literature |
| Natural product | **hmdb** (always first) | chembl, literature, rdkit |
| Target validation | opentargets | pdb, uniprot, string |
| SAR analysis | rdkit, chembl | pdb, medchem skill |
| Literature review | perplexity (broad) | pubmed (specific) |
| Pathway context | kegg + reactome + string | opentargets, literature |
| Document writing | scientific-writing | validator |

The key principle: **Match skill complexity to task complexity.** Not every question needs every database.
