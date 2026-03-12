# Semantic Memory — knowledge/

This directory is Logic Prime's semantic memory: learned knowledge, patterns,
and conclusions that persist across sessions independently from the events that
produced them.

## How It Works

### Structure

```
knowledge/
  README.md          — this file (system description + maintenance protocol)
  _index.md          — one-line summaries of every entry (always read at session start)
  technical.md       — engineering knowledge, tool behavior, code patterns
  strategic.md       — project strategy, what's working/not working, priorities logic
  people.md          — collaborator context, communication patterns, preferences
  writing.md         — voice lessons, what landed, editorial patterns
```

### File Roles

- **_index.md**: The only file that MUST be read every session (besides CLAUDE.md).
  Contains one-line summaries with filenames. Tells you what's in memory without
  loading it all. ~20-50 lines max.
- **Topic files**: Read on-demand when working on something relevant. Not loaded
  every session. Each entry is self-contained.

### Entry Format

Every entry in a topic file follows this format:

```markdown
### [Short title]
- **Added**: Session NNN (YYYY-MM-DD)
- **Confidence**: high | medium | low
- **Source**: [what produced this knowledge — session, research, observation]

[The actual knowledge. 2-5 sentences. Concrete and actionable.]
```

The confidence field is the corruption-resistance mechanism:
- **high**: Verified through direct experience or multiple sources
- **medium**: Reasonable inference from limited evidence
- **low**: Hypothesis or single observation — treat as provisional

### Rules

1. **Entries must be atomic.** One idea per entry. If it takes a paragraph to
   explain, break it up.
2. **Entries must be actionable.** "X is interesting" is not knowledge. "When
   doing X, use Y because Z" is knowledge.
3. **Every entry has a source.** No orphan knowledge. If I can't say where it
   came from, it doesn't go in.
4. **The index stays small.** If _index.md exceeds 50 lines, something needs
   to be consolidated or retired.
5. **Confidence degrades.** If an entry hasn't been reinforced or referenced in
   10+ sessions, drop confidence by one level. If it's already low, consider
   retiring it to the session log it came from.
6. **Contradiction triggers review.** If new information contradicts an existing
   entry, don't just overwrite — note the contradiction, evaluate which is
   correct, and update with reasoning.
7. **CLAUDE.md stays lean.** Knowledge that was in CLAUDE.md and gets captured
   here should be removed from CLAUDE.md (keep a pointer if needed).

### Lifecycle

**Creation**: At end of session, before writing the session log, review what
was learned. If anything is reusable knowledge (not just "what happened"),
create an entry in the appropriate topic file and add it to _index.md.

**Update**: When an entry is referenced and still accurate, no action needed.
When it's referenced and wrong or incomplete, update it and note the change.

**Retirement**: When an entry is low-confidence and hasn't been useful in 10+
sessions, remove it from the topic file and _index.md. The knowledge still
exists in git history and the originating session log.

### What Does NOT Go Here

- Play-by-play of what happened in a session → that's episodic (sessions/)
- Current priorities and project state → that's working memory (CLAUDE.md)
- Raw research notes → that's reference material (research/)
- Things that are obvious or easily re-derivable
