# RCDD Examples: Workflow Templates & Worked Scenarios

This document provides both **workflow templates** (step-by-step blueprints) and **worked examples** (concrete outputs showing what results look like).

---

## 📋 Table of Contents

### Part A: Worked Examples (Concrete Outputs)
Quick references showing actual orchestrator responses and outputs.

1. [Quick Inquiry: Vitamin D and Immunity](#quick-inquiry-vitamin-d-and-immunity)
2. [Natural Product Evaluation: Berberine for T2D](#natural-product-evaluation-berberine-for-t2d)
3. [Target Validation: KRAS G12C](#target-validation-kras-g12c)
4. [SAR Analysis: JAK2 Inhibitors](#sar-analysis-jak2-inhibitors)
5. [Pathway Analysis: EGFR Resistance](#pathway-analysis-egfr-resistance)

### Part B: Workflow Templates (Step-by-Step Blueprints)
Detailed procedures for comprehensive drug discovery tasks.

6. [Discovery of Novel EGFR Inhibitors](#workflow-discovery-of-novel-egfr-inhibitors)
7. [Drug Repurposing for Rare Diseases](#workflow-drug-repurposing-for-rare-diseases)
8. [Structure-Based Design of PPI Inhibitors](#workflow-structure-based-design-of-ppi-inhibitors)
9. [Target Identification for Natural Products](#workflow-target-identification-for-natural-products)
10. [Pre-Project Target Assessment](#workflow-pre-project-target-assessment)

---

# Part A: Worked Examples

These examples show **actual outputs** demonstrating orchestrator responses at different complexity levels.

---

## Quick Inquiry: Vitamin D and Immunity

### User Query
> "How does vitamin D affect the immune system?"

### Orchestrator Assessment
```
Query type: Factual inquiry, single topic
Complexity: LOW
Mode: DIRECT
Agents needed: None (self-synthesis)
Target output: ≤600 words, IEEE citations
```

### Response

Vitamin D exerts profound immunomodulatory effects through genomic and non-genomic mechanisms, influencing both innate and adaptive immunity. The discovery that immune cells express the vitamin D receptor (VDR) and the enzyme CYP27B1 for local calcitriol synthesis established vitamin D as an autocrine/paracrine immune regulator [1].

In innate immunity, vitamin D enhances antimicrobial defenses through multiple pathways. Calcitriol induces expression of cathelicidin (LL-37) and β-defensin 2, antimicrobial peptides critical for barrier defense against pathogens [2]. This mechanism underlies the historical use of sunlight and cod liver oil for tuberculosis, later validated when vitamin D was shown to restrict *Mycobacterium tuberculosis* growth in macrophages via cathelicidin induction [3]. Additionally, vitamin D promotes monocyte-to-macrophage differentiation and enhances phagocytic capacity while modulating inflammatory cytokine production [4].

In adaptive immunity, vitamin D generally promotes tolerance and suppresses excessive inflammatory responses. Key effects include:

| Immune Cell | Vitamin D Effect | Molecular Mechanism |
|-------------|------------------|---------------------|
| **Dendritic cells** | Tolerogenic phenotype | ↓ MHC-II, ↓ CD80/86, ↑ IL-10 |
| **T helper cells** | Th1→Th2 shift | ↓ IFN-γ, ↓ IL-17, ↑ IL-4 |
| **Regulatory T cells** | Expansion | ↑ Foxp3+ Treg differentiation |
| **B cells** | ↓ Proliferation | ↓ Plasma cell differentiation |

The molecular basis involves VDR-mediated transcriptional regulation. Upon calcitriol binding, VDR heterodimerizes with RXR and binds vitamin D response elements (VDREs) in target genes including *CAMP* (cathelicidin), *IL10*, and *FOXP3* [5]. Non-genomic effects occur via membrane-associated rapid response steroid-binding protein (MARRS/PDIA3) [6].

Clinical evidence supports immune relevance: meta-analyses demonstrate vitamin D supplementation reduces acute respiratory infection risk by 12% overall and 42% in severely deficient individuals [7]. In autoimmune disease, observational studies link low 25(OH)D with increased risk of multiple sclerosis, type 1 diabetes, and rheumatoid arthritis, though causality from supplementation trials remains under investigation [8].

Optimal immune function appears to require serum 25(OH)D concentrations of 30-50 ng/mL (75-125 nmol/L), above the 20 ng/mL threshold for skeletal health [9].

**References:**

[1] M. Hewison, "Vitamin D and immune function: an overview," *Proc. Nutr. Soc.*, vol. 71, no. 1, pp. 50–61, 2012. PMID: 21849106

[2] P. T. Liu et al., "Toll-like receptor triggering of a vitamin D-mediated human antimicrobial response," *Science*, vol. 311, no. 5768, pp. 1770–1773, 2006. PMID: 16497887

[3] J. H. White, "Vitamin D metabolism and signaling in the immune system," *Rev. Endocr. Metab. Disord.*, vol. 13, no. 1, pp. 21–29, 2012. PMID: 21845365

[4] M. T. Cantorna et al., "Vitamin D and 1,25(OH)2D regulation of T cells," *Nutrients*, vol. 7, no. 4, pp. 3011–3021, 2015. PMID: 25912039

[5] S. Christakos et al., "Vitamin D: metabolism, molecular mechanism of action, and pleiotropic effects," *Physiol. Rev.*, vol. 96, no. 1, pp. 365–408, 2016. PMID: 26681795

[6] I. Nemere et al., "Identification of a membrane receptor for 1,25-dihydroxyvitamin D3," *J. Bone Miner. Res.*, vol. 13, no. 9, pp. 1353–1359, 1998. PMID: 9738506

[7] A. R. Martineau et al., "Vitamin D supplementation to prevent acute respiratory tract infections," *BMJ*, vol. 356, p. i6583, 2017. PMID: 28202713

[8] C. Aranow, "Vitamin D and the immune system," *J. Investig. Med.*, vol. 59, no. 6, pp. 881–886, 2011. PMID: 21527855

[9] M. F. Holick et al., "Evaluation, treatment, and prevention of vitamin D deficiency," *J. Clin. Endocrinol. Metab.*, vol. 96, no. 7, pp. 1911–1930, 2011. PMID: 21646368

---

## Natural Product Evaluation: Berberine for T2D

### User Query
> "Evaluate berberine as a potential treatment for type 2 diabetes"

### Orchestrator Assessment
```
Query type: Natural product evaluation
Complexity: STANDARD
Mode: Full pipeline with NATURAL_COMPOUND assessment
Agents: @literature-reviewer, @medicinal-chemist, @medicinal-chemist
```

### Execution Plan

```
## Plan: Berberine T2D Evaluation
**Date:** 2025-01-15
**Status:** ⏸️ AWAITING APPROVAL
**Complexity:** STANDARD

### Objective
Evaluate berberine for type 2 diabetes treatment potential

### Literature Search Strategy
| Query | Mode | Depth | Assessment |
|-------|------|-------|------------|
| berberine diabetes mechanism | PERPLEXITY | DEEP | NATURAL_COMPOUND |
| berberine AMPK glucose | PUBMED | STANDARD | NATURAL_COMPOUND |
| berberine clinical trial diabetes | PUBMED | STANDARD | NATURAL_COMPOUND |

### Subagent Assignments
| Agent | Task | Output |
|-------|------|--------|
| @literature-reviewer | NATURAL_COMPOUND search | Refs + evidence ratings |
| @medicinal-chemist | HMDB check + SAR | Metabolite status + druglikeness |
| @medicinal-chemist | AMPK pathway context | Pathway map |
| @scientific-writer | Integrated report | Draft document |
| @validator | Verify citations | Validation report |
```

### Key Workflow Steps

**Step 1: HMDB Check (Critical First Step)**
```
Query: berberine
Result: HMDB0003409
Status: ⚠️ FOUND - Plant alkaloid (not endogenous human metabolite)
Class: Isoquinoline alkaloid
Note: Dietary exposure from Berberis species, Coptis chinensis
Plasma concentrations: Low ng/mL after oral dosing (poor bioavailability)
```

**Step 2: Evidence Assessment (NATURAL_COMPOUND Mode)**

| Evidence Type | Available | Quality | Key Findings |
|---------------|-----------|---------|--------------|
| Human RCTs | Yes (14+) | HIGH | HbA1c ↓0.5-0.9%, FBG ↓15-25 mg/dL |
| Animal studies | Yes (50+) | MODERATE-HIGH | db/db mice, ZDF rats consistent |
| Mechanistic | Yes (100+) | HIGH | AMPK activation, multi-target |
| PK studies | Yes | MODERATE | Oral F < 5%, gut-local effects |

**Step 3: Mechanism Summary**

Primary targets (from ChEMBL + literature):
- **AMPK** (AMP-activated protein kinase): Direct activation, IC50 ~10 μM
- **PCSK9**: Inhibits expression, ↓ LDL-C
- **Gut microbiome**: Modulates composition, ↑ SCFA production
- **DPP-4**: Weak inhibition
- **α-glucosidase**: Inhibits, delays glucose absorption

**Step 4: Pathway Context (KEGG/Reactome)**

```
Berberine targets → AMPK activation
    ↓
┌─────────────────────────────────────┐
│ Downstream Effects:                 │
│ • ↑ GLUT4 translocation (muscle)   │
│ • ↓ Hepatic gluconeogenesis        │
│ • ↑ Fatty acid oxidation           │
│ • ↓ Lipogenesis (SREBP1c pathway)  │
└─────────────────────────────────────┘
```

**Step 5: Medicinal Chemistry Assessment**

| Parameter | Value | Assessment |
|-----------|-------|------------|
| MW | 336.4 | ✅ Ro5 compliant |
| LogP | -1.3 (cation) | Quaternary ammonium |
| Oral bioavailability | < 5% | ⚠️ Major limitation |
| Half-life | 5-6 hours | Acceptable |
| Metabolites | Active (dihydroberberine) | Gut reduction |

**Formulation Opportunity Flag:**
```
⚠️ Bioavailability is rate-limiting, not mechanism validity

Strategies in literature:
- Solid lipid nanoparticles: ↑ AUC 3-5x [PMID: 25157968]
- Self-microemulsifying: ↑ AUC 2x [PMID: 28965402]
- Cyclodextrin complexes: ↑ solubility [PMID: 30849366]
- Dihydroberberine prodrug: ↑ absorption [PMID: 18651751]
```

### Final Assessment

| Criterion | Rating | Evidence |
|-----------|--------|----------|
| Mechanism validity | HIGH | Multi-target, AMPK validated |
| Human efficacy | MODERATE-HIGH | RCTs show ~0.5% HbA1c reduction |
| Safety | HIGH | Long traditional use, good tolerability |
| Bioavailability | LOW | < 5%, limits exposure |
| Development potential | MODERATE | Formulation could unlock efficacy |

**Verdict:** Berberine has validated mechanisms and clinical evidence comparable to metformin for glycemic control. Poor bioavailability is the primary limitation but is addressable through formulation. Worth pursuing with advanced delivery systems.

---

## Target Validation: KRAS G12C

### User Query
> "Evaluate KRAS G12C as a drug target for lung cancer"

### Orchestrator Assessment
```
Query type: Target validation
Complexity: STANDARD
Mode: Full pipeline
Agents: @target-evaluator, @target-evaluator, @literature-reviewer
```

### Key Workflow Steps

**Step 1: Open Targets Query**
```
Target: KRAS (ENSG00000133703)
Disease: Lung carcinoma

Tractability:
- Small molecule: Clinical precedence ✅ (sotorasib, adagrasib)
- Antibody: Not applicable (intracellular)
- PROTAC: Emerging

Genetic Evidence:
- Somatic mutations: 25-30% of NSCLC
- G12C specifically: ~13% of NSCLC
- Driver mutation status: Validated oncogene

Safety:
- pLI: 0.99 (highly constrained)
- Essential gene but mutant-selective approach viable
```

**Step 2: Structural Assessment (PDB + AlphaFold)**

| Metric | Value |
|--------|-------|
| PDB structures | 200+ (KRAS family) |
| G12C-specific | 50+ (with covalent inhibitors) |
| Best resolution | 1.1 Å (6OIM with AMG 510) |
| Binding pocket | Switch II pocket, mutant-selective |
| pLDDT | >90 (well-structured) |

**Step 3: Competitive Landscape**

| Drug | Company | Status | Notes |
|------|---------|--------|-------|
| Sotorasib (AMG 510) | Amgen | Approved 2021 | First KRAS inhibitor |
| Adagrasib (MRTX849) | Mirati | Approved 2022 | Longer half-life |
| Divarasib (GDC-6036) | Genentech | Phase III | Brain-penetrant |
| JDQ443 | Novartis | Phase III | Combination focus |

**Step 4: Final Assessment**

| Factor | Assessment | Confidence |
|--------|------------|------------|
| Druggability | ✅ VALIDATED | HIGH |
| Genetic evidence | ✅ STRONG | HIGH |
| Safety approach | ✅ Mutant-selective | HIGH |
| Competitive landscape | ⚠️ CROWDED | - |
| Differentiation needed | YES | - |

**Verdict:** KRAS G12C is a validated, druggable target with approved drugs. New entrants need differentiation: brain penetration, resistance coverage, combinations, or other mutants (G12D, G12V).

---

## SAR Analysis: JAK2 Inhibitors

### User Query
> "Analyze the SAR of these JAK2 inhibitors and suggest improvements"
> [Provides 5 compounds with IC50 data]

### Orchestrator Assessment
```
Query type: SAR analysis
Complexity: STANDARD
Mode: Full pipeline
Agents: @medicinal-chemist, @medicinal-chemist, @literature-reviewer
```

### Workflow Execution

**Step 1: Property Calculation (@medicinal-chemist)**

```python
# Via rdkit skill
# Output: Property table
| Cpd | MW | LogP | TPSA | HBD | HBA | IC50 (nM) |
|-----|-----|------|------|-----|-----|-----------|
| 1 | 478 | 3.2 | 87 | 2 | 7 | 15 |
| 2 | 492 | 3.8 | 87 | 2 | 7 | 8 |
| 3 | 456 | 2.9 | 92 | 3 | 7 | 45 |
| 4 | 510 | 4.1 | 82 | 1 | 7 | 5 |
| 5 | 489 | 3.5 | 95 | 2 | 8 | 22 |
```

**Step 2: Literature SAR Context (@literature-reviewer)**

```
Query: "JAK2 inhibitor SAR pyrimidine hinge"
Mode: PUBMED
Key findings:
- Aminopyrimidine essential for hinge binding [R1]
- N-methylpiperazine improves solubility [R2]
- Fluorine at meta position ↑ potency 3-5x [R3]
```

**Step 3: Structure-Based Insights (PDB)**

```
PDB: 3KRR (JAK2 with tofacitinib analog)
Key interactions:
- Hinge H-bonds: Leu932 backbone
- Gatekeeper: Met929 (small, allows access)
- Solvent-exposed: Piperazine region
```

**Step 4: SAR Analysis (@medicinal-chemist)**

```
Activity Cliff Identified:
Cpd-3 (IC50 = 45 nM) vs Cpd-4 (IC50 = 5 nM)
Difference: Additional HBD in Cpd-3
Interpretation: Extra donor causes desolvation penalty

SAR Map:
- Aminopyrimidine: ESSENTIAL (hinge binding)
- Piperazine N-methyl: BENEFICIAL (↓ IC50 2-3x)
- Meta-F on phenyl: BENEFICIAL (↓ IC50 3x)
- Polar groups solvent-exposed: TOLERATED
- Additional HBD: DETRIMENTAL

Proposed Optimization:
1. Add meta-F to best compound: Predict IC50 ~2 nM
2. Replace piperazine with morpholine: Test selectivity
3. Extend into ribose pocket: Novel vector
```

---

## Pathway Analysis: EGFR Resistance

### User Query
> "Why do patients develop resistance to EGFR inhibitors and what pathways are involved?"

### Orchestrator Assessment
```
Query type: Pathway/mechanism question
Complexity: QUICK-STANDARD
Mode: Pathway-focused with literature
Agents: @medicinal-chemist, @literature-reviewer
```

### Workflow Execution

**Step 1: EGFR Pathway Context (KEGG + Reactome)**

```
EGFR signaling cascade:
EGFR → RAS → RAF → MEK → ERK (proliferation)
EGFR → PI3K → AKT → mTOR (survival)
EGFR → JAK → STAT (transcription)
```

**Step 2: Resistance Mechanisms (Literature + STRING)**

| Mechanism | Frequency | Pathway Involved | Detection |
|-----------|-----------|------------------|-----------|
| T790M mutation | 50-60% | Target modification | Biopsy/ctDNA |
| MET amplification | 5-20% | Bypass via HGF/MET | FISH/NGS |
| HER2 amplification | 10-15% | Bypass via HER2 | FISH/IHC |
| BRAF V600E | 1-2% | RAF activation | NGS |
| PIK3CA mutation | 2-5% | PI3K pathway | NGS |
| SCLC transformation | 5-10% | Lineage switch | Histology |

**Step 3: Pathway Crosstalk Map**

```
                    ┌──────────────────┐
                    │   EGFR blocked   │
                    └────────┬─────────┘
                             │
        ┌────────────────────┼────────────────────┐
        ↓                    ↓                    ↓
   ┌─────────┐         ┌─────────┐         ┌─────────┐
   │   MET   │         │  HER2   │         │  IGF1R  │
   │ bypass  │         │ bypass  │         │ bypass  │
   └────┬────┘         └────┬────┘         └────┬────┘
        │                   │                   │
        └───────────────────┼───────────────────┘
                            ↓
                    ┌───────────────┐
                    │  RAS/PI3K     │
                    │  reactivation │
                    └───────────────┘
```

**Step 4: Therapeutic Implications**

| Resistance Type | Combination Strategy | Examples |
|-----------------|---------------------|----------|
| T790M | 3rd-gen EGFR TKI | Osimertinib |
| MET bypass | EGFR + MET inhibitor | Osimertinib + savolitinib |
| HER2 bypass | EGFR + HER2 inhibitor | Afatinib (dual) |
| PIK3CA | EGFR + PI3K inhibitor | Clinical trials |

---

# Part B: Workflow Templates

Detailed step-by-step blueprints for comprehensive drug discovery tasks.

---

## Workflow: Discovery of Novel EGFR Inhibitors

**Objective**: Identify novel small molecule inhibitors of EGFR with improved properties, potentially overcoming known resistance mutations.

**Skills Used**:
- `chembl-database` - Query bioactivity data for known inhibitors
- `pubchem-database` - Search for compound information and availability
- `rdkit` - Analyze molecular properties and generate analogs
- `medchem` - Predict drug-likeness and ADMET properties
- `pdb-database` - Retrieve predicted protein structures
- `pdb-database` - Experimental structures for docking
- `pubmed-database` & `literature-review` - Resistance mutations and prior art
- `opentargets-database` - Validate targets and find mutation data
- `scientific-visualization` - Create figures and reports

**Workflow Steps**:

```
# Step 1: Query ChEMBL for known EGFR inhibitors with high potency
# - Search for compounds targeting EGFR (CHEMBL203)
# - Filter for high potency (IC50 < 50 nM)
# - Extract SMILES strings and activity data

# Step 2: Analyze structure-activity relationships with RDKit
# - Load compounds into RDKit
# - Calculate key molecular descriptors (MW, LogP, TPSA, HBD, HBA)
# - Generate fingerprints to identify common scaffolds

# Step 3: Identify key resistance mutations
# - Use 'opentargets-database' and literature review
# - Find clinically relevant EGFR mutations (T790M, C797S)

# Step 4: Retrieve EGFR protein structure
# - Download AlphaFold prediction or experimental PDB structure
# - Prepare structure for docking

# Step 5: Generate novel analogs with RDKit
# - Use chemical transformation functions on top scaffolds
# - Filter library for drug-likeness (Lipinski's Rule of Five)

# Step 6: Predict ADMET properties
# - Use 'medchem' and 'rdkit' skills
# - Rank candidates by predicted potency and drug-like properties

# Step 7: Perform virtual screening via molecular docking
# - Dock top 50-100 candidates against wild-type and mutant EGFR
# - Analyze binding poses and energies

# Step 8: Check commercial availability
# - Use 'pubchem-database' to find suppliers

# Step 9: Final literature validation
# - Search for prior publications or patents on top scaffolds

# Step 10: Create comprehensive report
# - Use 'scientific-visualization' for figures
# - Compile methodology, results, and recommendations
```

**Expected Output**: Ranked list of 10-20 novel EGFR inhibitor candidates with predicted activity, favorable ADMET properties, and strong docking scores.

---

## Workflow: Drug Repurposing for Rare Diseases

**Objective**: Identify existing FDA-approved drugs that could be repurposed for treating a rare metabolic disorder.

**Skills Used**:
- `drugbank-database` - Query for approved drugs and their targets
- `opentargets-database` - Find and validate target-disease associations
- `string-database` - Analyze protein-protein interaction networks
- `reactome-database` & `reactome-database` - Perform pathway analysis
- `pubmed-database` & `literature-review` - Find trial data and safety info
- `scientific-visualization` - Create network and pathway diagrams

**Workflow Steps**:

```
# Step 1: Define the disease pathway
# - Query KEGG and Reactome for disease-associated pathways
# - Identify key proteins and enzymes in pathophysiology

# Step 2: Build and analyze PPI network
# - Query STRING database for interaction partners
# - Identify highly connected "hub" proteins as potential targets

# Step 3: Identify druggable targets
# - Query Open Targets for druggability assessment
# - Prioritize targets modulated by existing approved drugs

# Step 4: Find drugs hitting prioritized targets
# - Search DrugBank for approved drugs acting on targets
# - Retrieve mechanism of action and safety information

# Step 5: Investigate drug safety and clinical history
# - Literature review for adverse events and black box warnings
# - Search for past repurposing clinical trials

# Step 6: Perform pathway enrichment analysis
# - Map drug targets back to disease pathways
# - Identify drugs affecting multiple pathway nodes

# Step 7: Final systematic literature review
# - Search for any efficacy data in related conditions

# Step 8: Create comprehensive report
# - Network diagrams, pathway visualizations
# - Prioritized list of repurposing candidates
```

**Expected Output**: Prioritized list of 3-5 FDA-approved drug candidates for repurposing with supporting evidence.

---

## Workflow: Structure-Based Design of PPI Inhibitors

**Objective**: Design small molecule inhibitors of a protein-protein interaction using structure-based methods.

**Skills Used**:
- `pdb-database` - Retrieve co-crystal structures of protein complex
- `pdb-database` - Predicted structures if experimental unavailable
- `uniprot-database` - Protein sequence and domain information
- `chembl-database` - Find known PPI modulators for related targets
- `rdkit` - Fragment-based design and property calculations
- `pubmed-database` - Literature on PPI hot spots
- `scientific-visualization` - Structural figures

**Workflow Steps**:

```
# Step 1: Characterize the protein-protein interaction
# - Retrieve structures from PDB
# - Identify interface residues and hot spots
# - Calculate buried surface area

# Step 2: Analyze hot spot druggability
# - Map key residues contributing to binding energy
# - Assess pocket depth, hydrophobicity, enclosure

# Step 3: Search for existing PPI modulators
# - Query ChEMBL for related PPI targets
# - Identify privileged scaffolds for PPI inhibition

# Step 4: Fragment-based design
# - Generate fragment library targeting hot spots
# - Calculate properties and synthetic accessibility

# Step 5: Virtual screening
# - Dock fragments/compounds to PPI interface
# - Score and rank by predicted binding

# Step 6: Lead optimization
# - Merge fragments, optimize interactions
# - Predict ADMET properties

# Step 7: Create design report
# - Structural visualizations of proposed compounds
# - Synthesis recommendations
```

**Expected Output**: 5-10 designed compounds with predicted binding modes and properties, ready for synthesis.

---

## Workflow: Target Identification for Natural Products

**Objective**: Identify molecular targets of a bioactive natural product with known phenotypic activity but unknown mechanism.

**Skills Used**:
- `hmdb-database` - **CRITICAL**: Check if endogenous metabolite
- `pubchem-database` - Compound information and bioassay data
- `chembl-database` - Search for similar compounds with known targets
- `rdkit` - Structural similarity searches
- `string-database` - Network analysis of candidate targets
- `reactome-database` - Pathway mapping
- `perplexity-search` - Broad literature synthesis
- `scientific-brainstorming` - Creative hypothesis generation

**Workflow Steps**:

```
# Step 1: HMDB metabolite check (ALWAYS FIRST)
# - Query HMDB for compound
# - Determine if endogenous metabolite
# - Note pathways and concentrations if found

# Step 2: Characterize compound structure
# - Retrieve from PubChem or generate SMILES
# - Calculate properties with RDKit

# Step 3: Similarity-based target prediction
# - Search ChEMBL for structurally similar compounds
# - Note their known targets and activities

# Step 4: Bioassay data mining
# - Query PubChem for any existing bioassay results
# - Identify hits against specific targets

# Step 5: Literature synthesis
# - Perplexity search for mechanism studies
# - Compile reported targets and pathways

# Step 6: Network analysis of candidate targets
# - Build interaction network from STRING
# - Identify pathways connecting candidates

# Step 7: Hypothesis generation
# - Use scientific-brainstorming for creative connections
# - Propose testable mechanisms

# Step 8: Validation experiment design
# - Propose biochemical assays to confirm targets
# - Design selectivity panels
```

**Expected Output**: Ranked list of candidate targets with supporting evidence and experimental validation plan.

---

## Workflow: Pre-Project Target Assessment

**Objective**: Comprehensive evaluation of a novel drug target before initiating a discovery program.

**Skills Used**:
- `opentargets-database` - Target-disease associations, tractability, safety
- `uniprot-database` - Protein function and annotations
- `pdb-database` & `pdb-database` - Structural assessment
- `string-database` - Network position and interactions
- `reactome-database` & `reactome-database` - Pathway context
- `chembl-database` - Existing chemical matter
- `drugbank-database` - Approved drugs on target
- `pubmed-database` & `perplexity-search` - Literature evidence
- `scientific-critical-thinking` - Evidence evaluation
- `hypothesis-generation` - Validation experiments
- `native statistical analysis` - Quantitative scoring
- `scientific-visualization` - Report figures
- `scientific-writing` - Final report

**Workflow Steps**:

```
# Step 1: Target identification and basic characterization
# - Resolve gene symbol to Ensembl, UniProt, PDB identifiers
# - Query UniProt for protein function and domains

# Step 2: Genetic evidence assessment
# - Query Open Targets for GWAS, rare variants
# - Evaluate strength of genetic link to disease
# - Apply GRADE-like scoring

# Step 3: Expression and localization analysis
# - Assess tissue-specific expression
# - Determine subcellular localization
# - Identify therapeutic window considerations

# Step 4: Structural druggability assessment
# - Retrieve PDB structures or AlphaFold prediction
# - Analyze binding pockets and druggability
# - Assess pLDDT confidence for AlphaFold regions

# Step 5: Network and pathway analysis
# - Query STRING for interaction partners
# - Map to KEGG and Reactome pathways
# - Assess network centrality and redundancy

# Step 6: Competitive intelligence
# - Search ChEMBL for existing chemical matter
# - Query DrugBank for approved/clinical drugs
# - Literature search for competitor programs

# Step 7: Safety assessment
# - Check genetic constraint (pLI, LOEUF)
# - Review mouse knockout phenotypes
# - Identify known safety liabilities

# Step 8: Knowledge gap identification
# - Use scientific-critical-thinking to identify gaps
# - Propose validation experiments

# Step 9: Quantitative scoring
# - Apply weighted criteria across dimensions
# - Generate overall target attractiveness score

# Step 10: Comprehensive report
# - Executive summary with Go/No-go recommendation
# - Detailed sections on each assessment area
# - Risk analysis and mitigation strategies
```

**Expected Output**: 20-30 page comprehensive target assessment report with quantitative scoring, risk analysis, and clear recommendation for senior leadership review.

---

## Key Takeaways

1. **Match depth to complexity** - Quick questions need 600 words; full evaluations need multi-agent pipelines

2. **HMDB first for natural products** - Always check metabolite status before other analyses

3. **Cross-reference databases** - Use multiple sources for validation (Open Targets + PDB + literature)

4. **Quantitative SAR needs property calculations** - Integrate rdkit + literature + medchem analysis

5. **Pathway analysis needs all three databases** - KEGG + Reactome + STRING for complete picture

6. **Always cite with evidence quality** - Rate evidence levels, especially for natural compounds

7. **Identify formulation opportunities** - Poor bioavailability ≠ invalid mechanism
