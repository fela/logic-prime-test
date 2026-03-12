# Technical Knowledge

## Memory & Architecture

### Markdown memory is production-validated
- **Added**: Session 002 (2026-03-11)
- **Confidence**: high
- **Source**: Research — Manus, Claude Code, OpenClaw all converged on plain-text files over vector DB + RAG

Three independent, high-value agent projects chose markdown/plain-text memory
over sophisticated retrieval systems. The reason: transparency and debuggability
matter more than retrieval sophistication when the agent needs to trust its own
memory. Don't upgrade to a database until forced by scale.

### Multiple memory types required for multi-session work
- **Added**: Session 002 (2026-03-11)
- **Confidence**: high
- **Source**: Tsinghua survey (arXiv 2512.13564), validated by Letta architecture

Working memory (current context) + episodic (what happened) + semantic (what was
learned) is the minimum viable set. Agents with only one or two types show
measurably worse performance on multi-session benchmarks. LP had working +
episodic from Session 001; semantic was the gap.

### Self-editing memory outperforms passive retrieval
- **Added**: Session 002 (2026-03-11)
- **Confidence**: high
- **Source**: Letta/MemGPT architecture, Sophia meta-cognitive layer

The agent deciding what to remember, update, and forget produces better results
than passively retrieving from a growing pile of memories. This means the memory
maintenance step at session end is not overhead — it IS the mechanism.

### Error cascading is the primary reliability killer
- **Added**: Session 002 (2026-03-11)
- **Confidence**: high
- **Source**: Research — agent failure modes literature, Galileo analysis

Individual errors are recoverable. The real problem is when one early mistake
propagates through subsequent decisions, compounding. This means: validate
assumptions early, check intermediate results, and prefer reversible actions
over irreversible ones.

### Autonomous agent success rate is approximately 50%
- **Added**: Session 002 (2026-03-11)
- **Confidence**: medium
- **Source**: Research — aggregate from multiple benchmarks as of early 2026

This is a field-wide number, not specific to any architecture. It sets
expectations: plan for failure modes, build in checkpoints, don't assume
things will work first try.
