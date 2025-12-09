# claude-rcdd-skills

**Research & Computational Drug Development Multi-Agent System**

A comprehensive skill marketplace and agent framework for drug discovery research using Claude Code.

## Overview

This repository provides:
- **Skills** - Modular knowledge packages for scientific databases, tools, and methodologies (23 skills)
- **Agents** - Specialized AI personas for different aspects of drug discovery (5 agents)
- **Root Coordination** - Root Claude handles all agent coordination via Task tool with file checkpoints

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

### 23 Scientific Skills

Skills are automatically activated based on your query context:

| Category | Skills |
|----------|--------|
| **Literature** | perplexity-search, pubmed-database, literature-review |
| **Databases** | chembl-database, drugbank-database, pubchem-database, hmdb-database, zinc-database |
| **Structural** | pdb-database, uniprot-database |
| **Pathways** | reactome-database, string-database, opentargets-database |
| **Cheminformatics** | rdkit, medchem, biopython |
| **Visualization** | matplotlib, scientific-visualization |
| **Methodology** | scientific-writing, scientific-critical-thinking, scientific-brainstorming, hypothesis-generation |
| **Cognitive (Root-only)** | strategic-thinking |

### 5 Specialized Agents

Access via `@agent-name`:

| Agent | Model | Role |
|-------|-------|------|
| @literature-reviewer | opus | Literature search & synthesis |
| @medicinal-chemist | opus + thinking | Drug design, SAR, cheminformatics, pathway analysis |
| @target-evaluator | sonnet | Target validation, structural biology, sequence analysis |
| @scientific-writer | opus + thinking | Document preparation, figure generation |
| @validator | sonnet | Citation verification, research quality assessment |

> **Note:** Root Claude coordinates all agents. Agents execute tasks and write outputs to files. No agent spawns other agents.

---

## How to Use

Once installed, simply ask your question. Root Claude will:
1. Classify query complexity (DIRECT/QUICK/STANDARD/DEEP)
2. Route to appropriate specialist agents based on keywords
3. Coordinate multi-agent workflows with file checkpoints
4. Return results with validated citations

### Complexity Modes

| Mode | Use Case | What Happens |
|------|----------|--------------|
| **DIRECT** | Simple factual questions | Claude answers directly using skills, no agents |
| **QUICK** | Focused questions | Single agent spawned, output verified |
| **STANDARD** | Multi-step research | Agent chain with checkpoints |
| **DEEP** | Complex investigations | `strategic-thinking` skill loaded first, then full chain |

### Quick Reference: Natural Language Triggers

| You say... | Routes to |
|------------|-----------|
| "What's known about X?" / "Find papers on..." | @literature-reviewer |
| "Analyze this compound" / "Check druglikeness" | @medicinal-chemist |
| "Is X a good target?" / "Druggability of..." | @target-evaluator |
| "Write a report on..." / "Draft a summary" | @literature-reviewer → @scientific-writer → @validator |
| "Check these citations" / "Verify PMIDs" | @validator |
| "Deep dive into..." / "Comprehensive analysis" | DEEP mode (full chain) |

### Direct Agent Access

You can invoke specific agents directly:

```
@scientific-skills:literature-reviewer find recent papers on CRISPR
@scientific-skills:medicinal-chemist assess druglikeness of compound X
@scientific-skills:target-evaluator evaluate BRAF as a drug target
@scientific-skills:scientific-writer draft a methods section
@scientific-skills:validator verify the citations in my document
```

### Agent Chains

Root Claude coordinates mandatory agent chains:

| Task | Chain |
|------|-------|
| Document with references | @literature-reviewer → @scientific-writer → @validator |
| Drug candidate evaluation | @literature-reviewer → @medicinal-chemist |
| Natural product assessment | @literature-reviewer → @medicinal-chemist (with HMDB) |
| Target validation | @target-evaluator → @literature-reviewer |
| Comprehensive discovery | @literature-reviewer → @target-evaluator → @medicinal-chemist → @scientific-writer → @validator |

Each step writes outputs to `.claude/outputs/[date]-[task]/` directories. Root Claude verifies files exist before proceeding to next agent.

---

## Repository Structure

```
claude-rcdd-skills/
├── .claude-plugin/
│   └── marketplace.json          # Plugin manifest for Claude Code
├── .claude/
│   ├── schemas/                  # Inter-agent data formats
│   ├── skill-dependencies.md     # Skill loading order
│   └── outputs/                  # Agent output directories (created at runtime)
├── scientific-skills/             # 23 skill modules
│   ├── perplexity-search/
│   ├── pubmed-database/
│   ├── strategic-thinking/       # Root-only cognitive frameworks
│   ├── rdkit/
│   └── ...
├── agents/                        # 5 agent definitions (auto-discovered by plugin)
│   ├── literature-reviewer.md
│   ├── medicinal-chemist.md
│   ├── target-evaluator.md
│   ├── scientific-writer.md
│   └── validator.md
├── docs/                          # Additional documentation
├── CLAUDE.md                      # Agent routing guide (v1.3.0)
├── README.md                      # This file
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

Claude: [Root Claude coordinates agent chain with checkpoints:
         @literature-reviewer → @medicinal-chemist
         Each agent writes output files, verified before next step]
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
