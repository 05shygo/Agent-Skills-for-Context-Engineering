# Agent Skills for Context Engineering

A comprehensive, open collection of Agent Skills focused on context engineering principles for building production-grade AI agent systems. These skills teach the art and science of curating context to maximize agent effectiveness across any agent platform.

## What is Context Engineering?

Context engineering is the discipline of managing the language model's context window. Unlike prompt engineering, which focuses on crafting effective instructions, context engineering addresses the holistic curation of all information that enters the model's limited attention budget: system prompts, tool definitions, retrieved documents, message history, and tool outputs.

The fundamental challenge is that context windows are constrained not by raw token capacity but by attention mechanics. As context length increases, models exhibit predictable degradation patterns: the "lost-in-the-middle" phenomenon, U-shaped attention curves, and attention scarcity. Effective context engineering means finding the smallest possible set of high-signal tokens that maximize the likelihood of desired outcomes.

## Recognition

This repository is cited in academic research as foundational work on static skill architecture:

> "While static skills are well-recognized [Anthropic, 2025b; Muratcan Koylan, 2025], MCE is among the first to dynamically evolve them, bridging manual skill engineering and autonomous self-improvement."

— [Meta Context Engineering via Agentic Skill Evolution](https://arxiv.org/pdf/2601.21557), Peking University State Key Laboratory of General Artificial Intelligence (2026)

## Skills Overview

### Foundational Skills

These skills establish the foundational understanding required for all subsequent context engineering work.

| Skill | Description |
|-------|-------------|
| [context-fundamentals](skills/context-fundamentals/) | Understand what context is, why it matters, and the anatomy of context in agent systems |
| [context-degradation](skills/context-degradation/) | Recognize patterns of context failure: lost-in-middle, poisoning, distraction, and clash |
| [context-compression](skills/context-compression/) | Design and evaluate compression strategies for long-running sessions |

### Architectural Skills

These skills cover the patterns and structures for building effective agent systems.

| Skill | Description |
|-------|-------------|
| [multi-agent-patterns](skills/multi-agent-patterns/) | Master orchestrator, peer-to-peer, and hierarchical multi-agent architectures |
| [memory-systems](skills/memory-systems/) | Design short-term, long-term, and graph-based memory architectures |
| [tool-design](skills/tool-design/) | Build tools that agents can use effectively |
| [filesystem-context](skills/filesystem-context/) | Use filesystems for dynamic context discovery, tool output offloading, and plan persistence |
| [hosted-agents](skills/hosted-agents/) | **NEW** Build background coding agents with sandboxed VMs, pre-built images, multiplayer support, and multi-client interfaces |

### Operational Skills

These skills address the ongoing operation and optimization of agent systems.

| Skill | Description |
|-------|-------------|
| [context-optimization](skills/context-optimization/) | Apply compaction, masking, and caching strategies |
| [evaluation](skills/evaluation/) | Build evaluation frameworks for agent systems |
| [advanced-evaluation](skills/advanced-evaluation/) | Master LLM-as-a-Judge techniques: direct scoring, pairwise comparison, rubric generation, and bias mitigation |

### Development Methodology

These skills cover the meta-level practices for building LLM-powered projects.

| Skill | Description |
|-------|-------------|
| [project-development](skills/project-development/) | Design and build LLM projects from ideation through deployment, including task-model fit analysis, pipeline architecture, and structured output design |

### Cognitive Architecture Skills

These skills cover formal cognitive modeling for rational agent systems.

| Skill | Description |
|-------|-------------|
| [bdi-mental-states](skills/bdi-mental-states/) | **NEW** Transform external RDF context into agent mental states (beliefs, desires, intentions) using formal BDI ontology patterns for deliberative reasoning and explainability |

## Skill Reference Guide

Detailed descriptions of every skill — what it covers, when to use it, and example trigger phrases for Copilot / Claude.

### context-fundamentals

**What it covers:** The anatomy of a context window (system prompts, tool definitions, retrieved documents, message history, tool outputs), how attention mechanics work, the U-shaped attention curve, "lost in the middle" recall degradation, and the four principles of context assembly: informativity, position-aware placement, progressive disclosure, and iterative curation.

**When to use:**
- Designing a new agent system from scratch
- Onboarding a team to context engineering concepts
- Debugging unexpected agent behavior that might relate to what's in context
- Reviewing context-related architectural decisions

**Example triggers:** "understand context windows", "explain attention budget", "design agent architecture", "why does my agent ignore instructions in the middle?"

---

### context-degradation

**What it covers:** Five concrete degradation patterns — lost-in-middle, context poisoning, distraction, confusion, and clash — with measurable detection signals and specific mitigation strategies for each. Provides actionable thresholds (e.g., middle-context recall drops 10–40% for contexts over 4K tokens).

**When to use:**
- Agent performance degrades unexpectedly during long conversations
- Debugging incorrect or contradictory agent outputs
- Designing systems that must handle large contexts reliably
- Investigating cases where provided information is ignored

**Example triggers:** "diagnose context problems", "fix lost-in-middle", "why does my agent hallucinate when I give it a long document?", "context poisoning"

---

### context-compression

**What it covers:** Three production strategies — anchored iterative summarization, opaque compression, and regenerative full summary — with trade-offs for each. Targets the correct optimization metric: *tokens per task* (not tokens per request). Covers when to trigger compression and what structure to preserve.

**When to use:**
- Agent sessions exceed context window limits
- Code bases or documents exceed context windows
- Designing conversation summarization strategies
- Debugging "forgetting" of file edits or previous decisions

**Example triggers:** "compress context", "summarize conversation history", "reduce token usage", "my agent keeps forgetting what files it modified"

---

### context-optimization

**What it covers:** Four optimization techniques in priority order — KV-cache optimization, observation masking, compaction, and context partitioning. Explains that tool outputs consume 80%+ of tokens in typical agent trajectories and shows how to reclaim that space. Covers when to trigger compaction (>70% utilization) and how to partition work across sub-agents.

**When to use:**
- Reducing token costs in production
- Hitting context limits during long agent runs
- Optimizing latency for large conversations
- Building production systems at scale

**Example triggers:** "optimize context", "reduce token costs", "implement KV-cache", "my API costs are too high"

---

### multi-agent-patterns

**What it covers:** Three primary architecture patterns — supervisor/orchestrator, peer-to-peer/swarm, and hierarchical — with guidance on when each is appropriate. Covers context isolation mechanics, consensus protocols that resist sycophancy, handoff design, and common failure modes (supervisor bottleneck, error propagation, agent sprawl, telephone-game degradation).

**When to use:**
- A single agent's context window can't hold all task-relevant information
- Tasks decompose naturally into parallel or independent subtasks
- Building systems with multiple specialized components
- Coordinating agents across different domains or tool sets

**Example triggers:** "design multi-agent system", "implement supervisor pattern", "swarm architecture", "coordinate agents", "sub-agents"

---

### memory-systems

**What it covers:** The memory spectrum from volatile context to persistent storage. Covers production frameworks (Mem0, Zep/Graphiti, Letta, LangMem, Cognee), temporal knowledge graphs, vector stores, entity memory, and benchmark results from LoCoMo and LongMemEval. Provides a decision framework for choosing the right persistence layer.

**When to use:**
- Building agents that must retain knowledge across sessions
- Choosing between memory frameworks
- Implementing entity consistency across conversations
- Designing memory architectures that scale

**Example triggers:** "implement agent memory", "persist state across sessions", "build knowledge graph for agents", "track entities over time", "choose a memory framework"

---

### tool-design

**What it covers:** The contract principle — every tool description must unambiguously answer what it does, when to use it, and what it returns. Covers the consolidation principle (eliminate tools with overlapping purpose), tool naming conventions, parameter design, error surface minimization, and the 2–3× token inflation cost of verbose tool schemas.

**When to use:**
- Creating new tools for an agent system
- Debugging tool selection errors or misuse
- Optimizing an existing tool set
- Standardizing tool conventions across a codebase

**Example triggers:** "design agent tools", "reduce tool complexity", "implement MCP tools", "my agent picks the wrong tool"

---

### filesystem-context

**What it covers:** The filesystem as the primary overflow layer for agent context. Covers four context failure modes (missing, under-retrieved, over-retrieved, buried) and the filesystem remedy for each. Explains dynamic context discovery vs. static inclusion, scratch pad patterns, just-in-time loading, and sub-agent coordination through shared files.

**When to use:**
- Tool outputs bloating the context window
- Agents needing to persist state across long trajectories
- Sub-agents sharing information without direct message passing
- Tasks requiring more context than fits in one window

**Example triggers:** "offload context to files", "dynamic context discovery", "agent scratch pad", "file-based context", "agents sharing state"

---

### hosted-agents

**What it covers:** Remote sandboxed execution infrastructure — image registry patterns for sub-second startup, multiplayer session design with shared state, multi-client interface patterns (Slack, web, Chrome extension), Modal sandbox integration, and self-spawning agent architectures. Covers the three-layer architecture: sandbox, API, client.

**When to use:**
- Building background coding agents that run independently of user devices
- Designing sandboxed execution environments
- Implementing multi-user agent sessions
- Scaling agent infrastructure beyond a local machine

**Example triggers:** "build background agent", "hosted coding agent", "sandboxed execution", "multiplayer agent", "Modal sandboxes"

---

### evaluation

**What it covers:** How to evaluate agent systems differently from traditional software — focusing on outcomes rather than execution paths, multi-dimensional rubrics, LLM-as-judge deployment at scale, quality gates, and regression detection. Includes the "95% finding" on performance drivers and guidance for production continuous evaluation.

**When to use:**
- Testing agent performance systematically
- Validating that context engineering choices achieve intended effects
- Building quality gates for agent pipelines
- Comparing different agent configurations

**Example triggers:** "evaluate agent performance", "build test framework", "measure agent quality", "LLM-as-judge", "catch regressions"

---

### advanced-evaluation

**What it covers:** Production-grade LLM-as-judge techniques — direct scoring, pairwise comparison, rubric generation, and bias mitigation (position bias, length bias, verbosity bias). Covers evaluation taxonomy selection, correlation with human judgments, position-swap protocols, and the EvaluatorAgent pattern for combining all techniques.

**When to use:**
- Building automated evaluation pipelines
- Comparing multiple model responses to select the best
- Establishing consistent quality standards
- Debugging inconsistent evaluation results

**Example triggers:** "implement LLM-as-judge", "compare model outputs", "evaluation rubrics", "pairwise comparison", "mitigate position bias"

---

### project-development

**What it covers:** Task-model fit analysis (proceed/stop decision tables), pipeline architecture design, batch processing patterns, cost estimation, structured output design, and agent-assisted development methodology. Covers how to evaluate whether a task is suited for LLMs vs. traditional code before writing anything.

**When to use:**
- Starting a new project that might benefit from LLM processing
- Evaluating task-model fit before committing to implementation
- Designing a batch processing pipeline with structured outputs
- Choosing between single-agent and multi-agent approaches

**Example triggers:** "start LLM project", "design batch pipeline", "task-model fit", "should I use an LLM for this?", "pipeline architecture"

---

### bdi-mental-states

**What it covers:** Formal BDI (Belief-Desire-Intention) cognitive architecture for agents — transforming RDF/external context into structured mental states, the endurant/perdurant ontological separation, bidirectional motivational chains, and integration with BDI frameworks (SEMAS, JADE, JADEX). Enables traceable, explainable agent reasoning.

**When to use:**
- Modeling rational agent behavior with explainable reasoning chains
- Processing external RDF context into structured beliefs
- Implementing neuro-symbolic AI or Logic Augmented Generation
- Coordinating mental states across multi-agent platforms

**Example triggers:** "model agent mental states", "BDI architecture", "transform RDF to beliefs", "build cognitive agent", "explainable agent reasoning"

---

## Design Philosophy

### Progressive Disclosure

Each skill is structured for efficient context use. At startup, agents load only skill names and descriptions. Full content loads only when a skill is activated for relevant tasks.

### Platform Agnosticism

These skills focus on transferable principles rather than vendor-specific implementations. The patterns work across Claude Code, Cursor, and any agent platform that supports skills or allows custom instructions.

### Conceptual Foundation with Practical Examples

Scripts and examples demonstrate concepts using Python pseudocode that works across environments without requiring specific dependency installations.

## Usage

### Usage with Claude Code

This repository is a **Claude Code Plugin Marketplace** containing context engineering skills that Claude automatically discovers and activates based on your task context.

### Installation

**Step 1: Add the Marketplace**

Run this command in Claude Code to register this repository as a plugin source:

```
/plugin marketplace add muratcankoylan/Agent-Skills-for-Context-Engineering
```

**Step 2: Install the Plugin**

Option A - Browse and install:
1. Select `Browse and install plugins`
2. Select `context-engineering-marketplace`
3. Select `context-engineering`
4. Select `Install now`

Option B - Direct install via command:

```
/plugin install context-engineering@context-engineering-marketplace
```

This installs all 13 skills in a single plugin. Skills are activated automatically based on your task context.

### Skill Triggers

| Skill | Triggers On |
|-------|-------------|
| `context-fundamentals` | "understand context", "explain context windows", "design agent architecture" |
| `context-degradation` | "diagnose context problems", "fix lost-in-middle", "debug agent failures" |
| `context-compression` | "compress context", "summarize conversation", "reduce token usage" |
| `context-optimization` | "optimize context", "reduce token costs", "implement KV-cache" |
| `multi-agent-patterns` | "design multi-agent system", "implement supervisor pattern" |
| `memory-systems` | "implement agent memory", "build knowledge graph", "track entities" |
| `tool-design` | "design agent tools", "reduce tool complexity", "implement MCP tools" |
| `filesystem-context` | "offload context to files", "dynamic context discovery", "agent scratch pad", "file-based context" |
| `hosted-agents` | "build background agent", "create hosted coding agent", "sandboxed execution", "multiplayer agent", "Modal sandboxes" |
| `evaluation` | "evaluate agent performance", "build test framework", "measure quality" |
| `advanced-evaluation` | "implement LLM-as-judge", "compare model outputs", "mitigate bias" |
| `project-development` | "start LLM project", "design batch pipeline", "evaluate task-model fit" |
| `bdi-mental-states` | "model agent mental states", "implement BDI architecture", "transform RDF to beliefs", "build cognitive agent" |

<img width="1014" height="894" alt="Screenshot 2025-12-26 at 12 34 47 PM" src="https://github.com/user-attachments/assets/f79aaf03-fd2d-4c71-a630-7027adeb9bfe" />

### For GitHub Copilot

This repository ships a `.github/copilot-instructions.md` file that GitHub Copilot reads automatically in any repository that references or includes it. The file maps every skill to its trigger keywords and applies the four core context engineering principles in every Copilot response.

**Option A — Use the skills in this repository directly (VS Code)**

1. Clone this repository to **any directory** you prefer, for example:
   ```bash
   # macOS / Linux  (substitute your fork URL if you've forked the repo)
   git clone https://github.com/muratcankoylan/Agent-Skills-for-Context-Engineering.git ~/agent-skills

   # Windows (PowerShell)
   git clone https://github.com/muratcankoylan/Agent-Skills-for-Context-Engineering.git $HOME\agent-skills
   ```
2. Open that cloned folder **as your VS Code workspace root** (`File → Open Folder…` and select the cloned directory).
3. GitHub Copilot automatically reads `.github/copilot-instructions.md` from the workspace root and will apply the relevant skill (`skills/<skill-name>/SKILL.md`) whenever you ask context engineering questions in Copilot Chat.

> **Key point:** The directory you choose doesn't matter — what matters is that the repository root (the folder that contains `.github/copilot-instructions.md`) is opened as your VS Code workspace. Do **not** open a subdirectory inside the clone, or Copilot won't find the instructions file.

**Using GitHub Copilot in the VS Code integrated terminal**

Once you have opened the repository folder in VS Code as described above, any Copilot interaction in the integrated terminal (e.g., `@terminal` or inline suggestions) also benefits from the loaded instructions, because VS Code shares the workspace context with the terminal session.

**Option B — GitHub Copilot CLI (`gh copilot`)**

The standalone `gh copilot` CLI tool (`gh copilot suggest` / `gh copilot explain`) does **not** automatically read `copilot-instructions.md`. To get skill-guided responses in `gh copilot`:

1. Run `gh copilot suggest` or `gh copilot explain` as normal.
2. Prefix your prompt with the relevant skill keyword from the [Skill Triggers](#skill-triggers) table (e.g., *"design multi-agent system: ..."*) — Copilot will incorporate the concept even without the file.
3. For richer guidance, paste the contents of the relevant `skills/<skill-name>/SKILL.md` file directly into your prompt.

**Option C — Copy the instructions into your own project**

```bash
mkdir -p .github
curl -o .github/copilot-instructions.md \
  https://raw.githubusercontent.com/muratcankoylan/Agent-Skills-for-Context-Engineering/main/.github/copilot-instructions.md
```

Then copy the skills you need:

```bash
mkdir -p skills/multi-agent-patterns
curl -o skills/multi-agent-patterns/SKILL.md \
  https://raw.githubusercontent.com/muratcankoylan/Agent-Skills-for-Context-Engineering/main/skills/multi-agent-patterns/SKILL.md
```

Copilot will read both files and apply multi-agent pattern guidance when you ask about agent coordination, supervisor architectures, or swarm patterns.

### For Cursor (Open Plugins)

This repository is listed on the [Cursor Plugin Directory](https://cursor.directory/plugins/context-engineering).

The `.plugin/plugin.json` manifest follows the [Open Plugins](https://open-plugins.com) standard, so the repo also works with any conformant agent tool (Codex, GitHub Copilot, etc.).

### Using Individual Skills

To use a single skill without installing the full plugin, copy its `SKILL.md` directly into your project's `.claude/skills/` directory:

```bash
# Example: add just the context-fundamentals skill
mkdir -p .claude/skills
curl -o .claude/skills/context-fundamentals.md \
  https://raw.githubusercontent.com/muratcankoylan/Agent-Skills-for-Context-Engineering/main/skills/context-fundamentals/SKILL.md
```

Available skills: `context-fundamentals`, `context-degradation`, `context-compression`, `context-optimization`, `multi-agent-patterns`, `memory-systems`, `tool-design`, `filesystem-context`, `hosted-agents`, `evaluation`, `advanced-evaluation`, `project-development`, `bdi-mental-states`

### For Custom Implementations

Extract the principles and patterns from any skill and implement them in your agent framework. The skills are deliberately platform-agnostic.

## Examples

The [examples](examples/) folder contains complete system designs that demonstrate how multiple skills work together in practice.

| Example | Description | Skills Applied |
|---------|-------------|----------------|
| [digital-brain-skill](examples/digital-brain-skill/) | **NEW** Personal operating system for founders and creators. Complete Claude Code skill with 6 modules, 4 automation scripts | context-fundamentals, context-optimization, memory-systems, tool-design, multi-agent-patterns, evaluation, project-development |
| [x-to-book-system](examples/x-to-book-system/) | Multi-agent system that monitors X accounts and generates daily synthesized books | multi-agent-patterns, memory-systems, context-optimization, tool-design, evaluation |
| [llm-as-judge-skills](examples/llm-as-judge-skills/) | Production-ready LLM evaluation tools with TypeScript implementation, 19 passing tests | advanced-evaluation, tool-design, context-fundamentals, evaluation |
| [book-sft-pipeline](examples/book-sft-pipeline/) | Train models to write in any author's style. Includes Gertrude Stein case study with 70% human score on Pangram, $2 total cost | project-development, context-compression, multi-agent-patterns, evaluation |

Each example includes:
- Complete PRD with architecture decisions
- Skills mapping showing which concepts informed each decision
- Implementation guidance

### Digital Brain Skill Example

The [digital-brain-skill](examples/digital-brain-skill/) example is a complete personal operating system demonstrating comprehensive skills application:

- **Progressive Disclosure**: 3-level loading (SKILL.md → MODULE.md → data files)
- **Module Isolation**: 6 independent modules (identity, content, knowledge, network, operations, agents)
- **Append-Only Memory**: JSONL files with schema-first lines for agent-friendly parsing
- **Automation Scripts**: 4 consolidated tools (weekly_review, content_ideas, stale_contacts, idea_to_draft)

Includes detailed traceability in [HOW-SKILLS-BUILT-THIS.md](examples/digital-brain-skill/HOW-SKILLS-BUILT-THIS.md) mapping every architectural decision to specific skill principles.

### LLM-as-Judge Skills Example

The [llm-as-judge-skills](examples/llm-as-judge-skills/) example is a complete TypeScript implementation demonstrating:

- **Direct Scoring**: Evaluate responses against weighted criteria with rubric support
- **Pairwise Comparison**: Compare responses with position bias mitigation
- **Rubric Generation**: Create domain-specific evaluation standards
- **EvaluatorAgent**: High-level agent combining all evaluation capabilities

### Book SFT Pipeline Example

The [book-sft-pipeline](examples/book-sft-pipeline/) example demonstrates training small models (8B) to write in any author's style:

- **Intelligent Segmentation**: Two-tier chunking with overlap for maximum training examples
- **Prompt Diversity**: 15+ templates to prevent memorization and force style learning
- **Tinker Integration**: Complete LoRA training workflow with $2 total cost
- **Validation Methodology**: Modern scenario testing proves style transfer vs content memorization

Integrates with context engineering skills: project-development, context-compression, multi-agent-patterns, evaluation.

## Star History
<img width="3664" height="2648" alt="star-history-2026317" src="https://github.com/user-attachments/assets/0fe53d8d-7fdd-45be-9c28-057881b23b44" />

## Structure

Each skill follows the Agent Skills specification:

```
skill-name/
├── SKILL.md              # Required: instructions + metadata
├── scripts/              # Optional: executable code demonstrating concepts
└── references/           # Optional: additional documentation and resources
```

See the [template](template/) folder for the canonical skill structure.

## Contributing

This repository follows the Agent Skills open development model. Contributions are welcome from the broader ecosystem. When contributing:

1. Follow the skill template structure
2. Provide clear, actionable instructions
3. Include working examples where appropriate
4. Document trade-offs and potential issues
5. Keep SKILL.md under 500 lines for optimal performance

Feel free to contact [Muratcan Koylan](https://x.com/koylanai) for collaboration opportunities or any inquiries.

## License

MIT License - see LICENSE file for details.

## References

The principles in these skills are derived from research and production experience at leading AI labs and framework developers. Each skill includes references to the underlying research and case studies that inform its recommendations.
