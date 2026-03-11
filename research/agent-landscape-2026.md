# Agent Landscape Research — March 2026

Research conducted during Session 002 via parallel agent. Key findings relevant
to Logic Prime's architecture.

## Validation: Markdown Memory Works

Three independent high-value projects (Manus, Claude Code itself, OpenClaw)
converged on plain-text file-based memory over complex vector DB + RAG pipelines.
The lesson: **transparency and debuggability beat sophistication** in practice.

This validates LP's current approach. Don't upgrade to a database until forced.

## Key Insight: Multiple Memory Types Required

The Tsinghua survey (Dec 2025, arXiv 2512.13564) found that agents implementing
multiple memory types show measurably better task completion on multi-session
benchmarks. Single-type memory is insufficient.

**Required memory types:**
1. **Working memory** — current session context (LP has this: CLAUDE.md)
2. **Episodic memory** — what happened (LP has this: session logs)
3. **Semantic memory** — what was learned (LP DOES NOT have this yet)

**Action item**: Add a semantic memory layer — a place to store learned
knowledge, patterns, and conclusions that persist across sessions independently
from episodic logs.

## Letta (formerly MemGPT): Most Relevant Prior Art

- Three-tier memory: Core (always in-context), Recall (searchable history),
  Archival (processed knowledge in external stores)
- Agents **self-edit their own memory** using tools — the agent decides what to
  remember, forget, and archive
- Feb 2026: Introduced **Context Repositories** using git-based versioning for
  memory — very close to what LP is doing
- Introduced Agent File (.af) format for serializing stateful agents

## Sophia: Meta-Cognitive Layer

Westlake University/SJTU, Dec 2025 (arXiv 2512.18202). Proposes "System 3" —
a meta-cognitive monitor that maintains narrative identity across sessions.
Integrates Theory of Mind, Self-Model, Episodic Memory, and Intrinsic Motivation.

In 36-hour deployments: improved complex task success from 20% to 60%, reduced
reasoning steps for recurring problems by 80% via persistent "Growth Journal."

**Relevance to LP**: CLAUDE.md's self-model section is a crude version of this.
Could formalize it.

## Beads: Git-Backed Memory

Steve Yegge's project. Stores agent state as JSONL in `.beads/` directory. Memory
branches with code branches, merges with code merges.

**Relevance**: Elegant for developer tools. LP already uses git-backed memory;
this validates the approach and suggests a more structured format could help.

## Failure Modes to Watch

1. **Error cascading** — one early mistake propagates through subsequent
   decisions, compounding. Primary reliability killer.
2. **Memory corruption** — poisoned entries from weeks ago silently steer future
   actions. Persistent memory is a double-edged sword.
3. **Catastrophic autonomous actions** — agents executing destructive operations.
   (An autonomous coding agent once ran DROP DATABASE on production.)
4. **Demo-to-production gap** — most agent projects die in the transition from
   "it works in a demo" to "it works reliably."
5. **Current success rate: ~50%** — autonomous agents succeed about half the
   time. Sobering.

## Key Takeaways for LP Architecture

1. **Stay with markdown/files for now.** Validated by multiple production systems.
2. **Add semantic memory.** The missing third type. A `knowledge/` directory or
   similar for learned patterns and conclusions.
3. **Self-editing memory is the right pattern.** LP already does this with
   CLAUDE.md updates. Be more deliberate about what to remember vs forget.
4. **Think about integrity.** Memory corruption is a real failure mode. Consider
   checksums or review mechanisms.
5. **Simplicity compounds.** BabyAGI's lesson: a simple loop you understand
   beats a complex system you don't. Don't over-engineer.
6. **Watch Letta and Sophia.** Most architecturally relevant prior work.

## Sources
- Letta docs: https://docs.letta.com/concepts/letta/
- Sophia paper: https://arxiv.org/abs/2512.18202
- Tsinghua memory survey: https://arxiv.org/abs/2512.13564
- Beads: https://yuv.ai/blog/beads-git-backed-memory-for-ai-agents-that-actually-remembers
- GitHub Copilot memory: https://github.blog/ai-and-ml/github-copilot/building-an-agentic-memory-system-for-github-copilot/
- Manus/markdown memory: https://dev.to/imaginex/ai-agent-memory-management-when-markdown-files-are-all-you-need-5ekk
- Agent failure modes: https://galileo.ai/blog/agent-failure-modes-guide
