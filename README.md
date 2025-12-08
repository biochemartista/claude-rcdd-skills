# claude-rcdd-skills

**Research & Computational Drug Development Multi-Agent System**

A comprehensive skill marketplace and agent framework for drug discovery research using Claude Code.

## Overview

This repository provides:
- **Skills** - Modular knowledge packages for scientific databases, tools, and methodologies (22 skills)
- **Agents** - Specialized AI personas for different aspects of drug discovery (6 agents)
- **Orchestration** - A master orchestrator that coordinates the entire system

## Installation

### Method 1: Install from GitHub (Recommended)

```bash
# In Claude Code, add the marketplace
/plugin marketplace add biochemartista/claude-rcdd-skills

# Install the plugin
/plugin install scientific-skills@claude-rcdd-skills

# Verify installation
/plugin list
```

**For Private Repository:** Make sure you have GitHub authentication configured in Claude Code.

### Method 2: Local Development

For testing or development without pushing to GitHub:

```bash
# Add local marketplace
/plugin marketplace add D:/GITHUB/claude-rcdd-skills

# Install plugin
/plugin install scientific-skills@claude-rcdd-skills
```

### Method 3: Auto-Install for Projects

Add to your project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "rcdd-skills": {
      "source": {
        "source": "github",
        "repo": "biochemartista/claude-rcdd-skills"
      }
    }
  },
  "enabledPlugins": ["scientific-skills@rcdd-skills"]
}
```

When you open the project in Claude Code, it automatically installs the marketplace and plugin.

See [CLAUDE_CODE_INSTALL.md](CLAUDE_CODE_INSTALL.md) for detailed installation instructions and troubleshooting.

---

## What's Included

### 22 Scientific Skills

Skills are automatically activated based on your query context:

| Category | Skills |
|----------|--------|
| **Literature** | perplexity-search, pubmed-database, literature-review |
| **Databases** | chembl-database, drugbank-database, pubchem-database, hmdb-database, zinc-database |
| **Structural** | pdb-database, uniprot-database |
| **Pathways** | reactome-database, string-database, opentargets-database |
| **Cheminformatics** | rdkit, medchem, biopython |
| **Visualization** | matplotlib |
| **Methodology** | scientific-writing, scientific-critical-thinking, scientific-brainstorming, scientific-visualization, hypothesis-generation |

### 6 Specialized Agents

Access via `@agent-name`:

| Agent | Model | Role |
|-------|-------|------|
| **@orchestrator** | opus + thinking | Chief Scientific Architect |
| @literature-reviewer | opus | Literature search & synthesis |
| @medicinal-chemist | opus + thinking | Drug design, SAR, cheminformatics, pathway analysis |
| @target-evaluator | sonnet | Target validation, structural biology, sequence analysis |
| @scientific-writer | opus + thinking | Document preparation, figure generation |
| @validator | sonnet | Citation verification, research quality assessment |

---

## How to Use

Once installed, invoke the **orchestrator agent** to automatically route your query to the appropriate specialist agent(s):

```
@scientific-skills:orchestrator [your query]
```

The orchestrator will:
1. Classify query complexity (DIRECT/QUICK/STANDARD/DEEP)
2. Route to appropriate specialist agents based on keywords
3. Coordinate multi-agent workflows when needed
4. Return results with validated citations

**For simple inquiries**, the orchestrator can answer directly using:
- `perplexity-search` - AI-powered web search with reasoning
- `pubmed-database` - PubMed literature access
- `pubchem-database` - Compound lookup

**For complex research**, it delegates to specialist agents who use their full skill sets.

### Quick Reference: Common Queries

| Query Type | Example Command |
|------------|----------------|
| **Literature search** | `@scientific-skills:orchestrator find literature on AMPK pathway activation` |
| **Compound evaluation** | `@scientific-skills:orchestrator evaluate maslinic acid as a drug candidate` |
| **Target assessment** | `@scientific-skills:orchestrator is BRAF a good drug target?` |
| **SAR analysis** | `@scientific-skills:orchestrator analyze SAR for these SMILES: [compounds]` |
| **Mechanism of action** | `@scientific-skills:orchestrator what is the MOA of metformin?` |
| **Simple questions** | `@scientific-skills:orchestrator does vitamin C affect immunity?` |
| **Document writing** | `@scientific-skills:orchestrator write a review on honokiol for cancer` |

### Direct Agent Access (Advanced)

You can also invoke specific agents directly when you know exactly which specialist you need:

```
@scientific-skills:literature-reviewer find recent papers on CRISPR
@scientific-skills:medicinal-chemist assess druglikeness of compound X
@scientific-skills:medicinal-chemist calculate properties for this SMILES
@scientific-skills:target-evaluator evaluate BRAF as a drug target
```

### Automatic Agent Routing

The orchestrator uses keyword triggers to route queries:

| Keywords | Routed To |
|----------|-----------|
| "literature", "papers", "studies", "what is known" | @literature-reviewer |
| "compound", "SAR", "ADMET", "druglikeness", "IC50" | @medicinal-chemist |
| "pathway", "MOA", "Reactome", "STRING", "AMPK", "mTOR" | @medicinal-chemist |
| "SMILES", "fingerprint", "RDKit", "properties" | @medicinal-chemist |
| "target", "druggability", "GWAS", "Open Targets" | @target-evaluator |
| "structure", "PDB", "binding site", "sequence" | @target-evaluator |
| "write report", "manuscript", "document", "figures" | @scientific-writer |

> **Note:** The orchestrator handles multi-agent workflows automatically. For example, "evaluate compound X" will route through literature-reviewer → medicinal-chemist. The @medicinal-chemist agent now handles property calculations, pathway context, and cheminformatics internally.

---

## Repository Structure

```
claude-rcdd-skills/
├── .claude-plugin/
│   └── marketplace.json          # Plugin manifest for Claude Code
├── scientific-skills/             # 22 skill modules
│   ├── perplexity-search/
│   ├── pubmed-database/
│   ├── rdkit/
│   └── ...
├── agents/                        # 6 agent definitions (auto-discovered by plugin)
│   ├── literature-reviewer.md
│   ├── medicinal-chemist.md
│   ├── orchestrator.md
│   ├── target-evaluator.md
│   ├── scientific-writer.md
│   └── validator.md
├── docs/                          # Additional documentation
├── CLAUDE.md                      # Project context for main orchestrator
├── README.md                      # This file
├── CLAUDE_CODE_INSTALL.md         # Detailed installation guide
├── WORKFLOWS_AND_BEST_PRACTICES.md # Usage workflows
└── LICENSE.md                     # MIT License
```

---

## Usage Examples

### Quick Query (Skills activate automatically)

Skills load automatically based on your question context:

```
You: Find recent papers on CRISPR gene editing for cancer

Claude: [Automatically uses pubmed-database and perplexity-search skills]
```

### Using Specific Agents

```
You: @literature-reviewer conduct a systematic review of honokiol for prostate cancer

Claude: [Literature reviewer agent coordinates with relevant skills]
```

### Multi-Agent Research

```
You: Evaluate maslinic acid as a drug candidate

Claude: [Main orchestrator coordinates multiple agents:
         @literature-reviewer → @medicinal-chemist → @target-evaluator
         Each uses appropriate skills automatically]
```

### Direct Mode (Simple Questions)

```
You: Does vitamin C affect the immune system?

Claude: [Provides concise ~600 word response with citations,
         skills used behind the scenes]
```

---

## Customization

### Adding New Skills

1. Create folder in `scientific-skills/`:
   ```
   scientific-skills/my-new-skill/
   ├── SKILL.md
   └── references/
   ```

2. Add to `.claude-plugin/marketplace.json`:
   ```json
   "skills": [
     "./scientific-skills/my-new-skill",
     ...
   ]
   ```

3. Update and reinstall:
   ```bash
   /plugin marketplace update claude-rcdd-skills
   /plugin install scientific-skills@claude-rcdd-skills --force
   ```

### Adding New Agents

Agents in the `agents/` folder are **automatically discovered** when the plugin is installed. They appear as plugin agents namespaced under the plugin name (e.g., `scientific-skills:agent-name`).

1. Create file in `agents/`:
   ```markdown
   ---
   name: my-agent
   description: What this agent does
   model: sonnet
   tools:
     - Read
     - Write
     - WebSearch
     - scientific-skills/relevant-skill  # Add any required skills
   ---
   
   # My Agent
   
   ## Role
   ...
   ```

2. Agents are automatically discovered from `agents/` - no registration in `marketplace.json` needed
   
3. Reinstall the plugin to load the new agent:
   ```bash
   /plugin install scientific-skills@claude-rcdd-skills --force
   ```

---

## Updating

```bash
# Update marketplace
/plugin marketplace update claude-rcdd-skills

# Reinstall plugin with latest changes
/plugin install scientific-skills@claude-rcdd-skills --force
```

---

## Requirements

- Claude Code v2.0.12 or higher
- For GitHub installation: GitHub authentication configured
- For local installation: Access to local file system

---

## Documentation

- **[CLAUDE_CODE_INSTALL.md](CLAUDE_CODE_INSTALL.md)** - Detailed installation guide
- **[WORKFLOWS_AND_BEST_PRACTICES.md](WORKFLOWS_AND_BEST_PRACTICES.md)** - Common workflows and usage patterns
- **[LICENSE.md](LICENSE.md)** - MIT License

---

## Contributing

1. Fork the repository
2. Create feature branch
3. Add/modify skills or agents
4. Test locally with `/plugin marketplace add ./path/to/fork`
5. Submit pull request

---

## Support

- **GitHub Issues:** https://github.com/biochemartista/claude-rcdd-skills/issues
- **Email:** antonio.lelas@gmail.com

---

## License

MIT License - See [LICENSE.md](LICENSE.md) for details

---

## Acknowledgments

Forked and adapted from the excellent [claude-scientific-skills](https://github.com/K-DenseInc/claude-scientific-skills) by K-Dense Inc, with focus on drug discovery and computational chemistry workflows.
