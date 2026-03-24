# GitHub Copilot Instructions for Context Engineering Skills

This repository contains 13 Agent Skills for context engineering — the discipline of curating everything that enters a model's context window (system prompts, tool definitions, retrieved documents, message history, tool outputs) to maximize signal within a limited attention budget.

## Skill Activation

When answering questions or generating code, consult the relevant skill file from the `skills/` directory and apply its guidance. Each skill's full content is in `skills/<skill-name>/SKILL.md`.

| Trigger keywords | Skill to apply |
|-----------------|----------------|
| "understand context", "explain context windows", "design agent architecture", "context budget" | `skills/context-fundamentals/SKILL.md` |
| "diagnose context problems", "fix lost-in-middle", "debug agent failures", "context poisoning" | `skills/context-degradation/SKILL.md` |
| "compress context", "summarize conversation", "reduce token usage", "compaction" | `skills/context-compression/SKILL.md` |
| "optimize context", "reduce token costs", "KV-cache", "observation masking" | `skills/context-optimization/SKILL.md` |
| "design multi-agent system", "supervisor pattern", "swarm architecture", "coordinate agents", "agent handoffs", "sub-agents" | `skills/multi-agent-patterns/SKILL.md` |
| "implement agent memory", "build knowledge graph", "track entities", "Mem0", "Zep" | `skills/memory-systems/SKILL.md` |
| "design agent tools", "MCP tools", "tool consolidation", "tool naming" | `skills/tool-design/SKILL.md` |
| "offload context to files", "dynamic context discovery", "agent scratch pad", "file-based context" | `skills/filesystem-context/SKILL.md` |
| "build background agent", "hosted coding agent", "sandboxed execution", "multiplayer agent" | `skills/hosted-agents/SKILL.md` |
| "evaluate agent performance", "build test framework", "measure quality", "LLM-as-judge" | `skills/evaluation/SKILL.md` |
| "implement LLM-as-judge", "compare model outputs", "evaluation rubrics", "pairwise comparison" | `skills/advanced-evaluation/SKILL.md` |
| "start LLM project", "design batch pipeline", "task-model fit", "pipeline architecture" | `skills/project-development/SKILL.md` |
| "model agent mental states", "BDI architecture", "transform RDF to beliefs", "cognitive agent" | `skills/bdi-mental-states/SKILL.md` |

## Core Principles to Always Apply

1. **Context quality over quantity** — More context is not always better. Attention scarcity and the lost-in-the-middle phenomenon mean that smaller, higher-signal context outperforms larger, noisier context.
2. **Sub-agents isolate context** — Multi-agent architectures exist primarily to manage attention budget and isolate context, not to simulate organizational roles.
3. **Progressive disclosure** — Load only what is needed for the current task. Defer loading detailed information until it is required.
4. **Token-conscious design** — Challenge each piece of context: "Does the model really need this? Does this justify its token cost?"

## Using the Multi-Agent Skill

The `multi-agent-patterns` skill is highlighted separately because it is the most frequently needed skill for production agent systems and the one most users ask about first. It covers orchestrator, peer-to-peer, and hierarchical architectures. Apply it whenever a task exceeds single-context limits or naturally decomposes into parallel subtasks. Read `skills/multi-agent-patterns/SKILL.md` for:

- When to choose each architecture pattern (supervisor vs. swarm vs. hierarchical)
- Context isolation mechanisms (instruction passing, file system coordination, full delegation)
- Consensus and voting protocols that resist sycophantic convergence
- Common failure modes: supervisor bottleneck, error propagation, agent sprawl, telephone game degradation

## Repository Layout

```
skills/                    # 13 skill directories, each with SKILL.md
├── context-fundamentals/
├── context-degradation/
├── context-compression/
├── context-optimization/
├── multi-agent-patterns/
├── memory-systems/
├── tool-design/
├── filesystem-context/
├── hosted-agents/
├── evaluation/
├── advanced-evaluation/
├── project-development/
└── bdi-mental-states/
examples/                  # Complete demonstration projects
docs/                      # Research materials
template/SKILL.md          # Canonical template for new skills
```
