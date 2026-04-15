---
name: systems-paper-polisher
description: Polish and improve existing computer systems conference papers for OSDI, SOSP, ASPLOS, EuroSys, ATC, NSDI. Use when the user wants to polish a draft, improve writing quality, compress to page limits, verify citations, or run pre-submission checks. Supports both full-paper iterative polishing and targeted section-level editing. Features multi-agent review with diverse reviewer personas and story-driven coherence checking. NOT for writing papers from scratch — use systems-paper-writing for that.
version: 1.0.0
tags: [Paper Polishing, Systems, OSDI, SOSP, ASPLOS, EuroSys, ATC, NSDI, Editing, Review, LaTeX]
---

# Systems Paper Polisher

Polish existing computer systems conference papers through multi-agent iterative review and improvement. The goal is to help authors present their systems work clearly and compellingly — making the system's purpose, design logic, and value easy for readers to follow.

## Core Philosophy

A good systems paper tells one coherent story: what problem the system solves, why existing approaches fall short, what insight drives the design, and how the evaluation validates the claims. Every section should naturally advance this story. The reader should finish the paper understanding not just *what* the system does, but *why* each design decision makes sense in the context of the problem.

This skill helps ensure that coherence while improving writing clarity and addressing reviewer concerns — without changing the technical content itself.

### What This Skill Does and Does Not Do

**Does**: Improve presentation, strengthen narrative coherence, check claim-evidence alignment, suggest structural reorganization, verify citations, compress to page limits, check submission compliance.

**Does not**: Change system design, fabricate experimental results, generate citations from memory, or write new technical content. When something is missing (a number, a citation, an experiment), it marks a placeholder for the author to fill.

---

## Commands

### Implicit Prerequisite: Conference Info

Every command begins by establishing the target conference (if not already known in the session):
1. Ask which conference the paper targets (OSDI, SOSP, ASPLOS, EuroSys, ATC, NSDI, or other)
2. Load requirements from `references/conference-requirements.md`
3. If the user provides a CFP link, fetch and parse specific requirements
4. Conference info persists for the session — no repeated questions

### Full Pipeline

**`polish`** — "润色论文" / "polish my paper" / "完整润色流程"

Runs the complete polishing pipeline in sequence:
```
1. polish-paper      → Iterative full-paper polishing
2. compress         → Compress to target page count (if needed)
3. check-citations  → Generate citation verification checklist
4. check-submission → Final compliance check against conference requirements
```

At startup, ask the user their preferred pacing:
- **Interactive** (default): Pause between stages for user confirmation
- **Continuous**: Auto-advance, only pause when user input is needed

### Sub-Commands

Each sub-command can be invoked independently.

#### `polish-section` — "润色 section 3.2" / "improve the introduction"

Polish a specific section through the full review→improve cycle. Read `agents/` for agent details.

**Flow**:
1. Read the target section + read intro/motivation to extract the paper's storyline
2. **Phase 1** — Launch 4 review agents in parallel (see Agent Team below)
3. Present consolidated feedback to the user
4. **Phase 2** — Run improvement-agent to produce revised text
5. User reviews. If "iterate", loop back to Phase 1 with revised text

#### `polish-paper` — "润色全文" / "polish the full paper"

Full-paper iterative polishing. Read `references/story-coherence-guide.md` for the coherence framework.

**Flow**:
```
Phase 0: INTAKE
  Read entire paper + target conference
  Extract storyline from intro/motivation (what the system does, what problem
    it solves, core insight) → confirm with user
  Build initial Story Traceability Matrix
  (Optional) Search for related excellent papers as style reference

Round 1: Section-by-section polish
  Order: intro → design subsections → eval → abstract → related work → conclusion
  Each section: Phase 1 (parallel review) → Phase 2 (improve) → user approval

Round 2: Full-paper coherence pass
  Focus: cross-section consistency, terminology uniformity, redundancy,
    abstract/intro alignment with actual content
  Phase 1 → Phase 2 → user approval

Round 3+: Targeted iteration (optional)
  Re-polish sections flagged in Round 2
  Stop when: no CRITICAL/MAJOR issues remain OR user says "done"
```

After completion, suggest: "Consider running `compress`, `check-citations`, and `check-submission` next."

#### `compress` — "压缩到12页" / "compress to 12 pages" / "cut 1 page"

Compress paper content to meet page limits. Read `agents/compressor-agent.md` for details.

**Flow**:
1. Analyze current paper length vs target
2. Identify compression opportunities by priority (see compressor-agent)
3. Present prioritized cut list with estimated savings
4. User selects which cuts to apply
5. Produce revised text
6. Optionally re-check style on compressed sections

#### `check-citations` — "检查引用" / "verify references"

Verify citation integrity and generate a checklist for user verification.

**Flow**:
1. Extract all `\cite{}` references and their BibTeX entries
2. For each citation, attempt verification via DBLP/Semantic Scholar API
3. Flag suspicious entries (mismatched year, venue, or authors; DOI not resolving)
4. For any suggested new citations from review agents, include search links
5. Generate `citation-checklist.md` with verification status

**Output format** (`citation-checklist.md`):
```markdown
# Citation Verification Checklist

## Existing Citations
- [x] [smith2023raft] Smith et al., "Raft Consensus", OSDI 2023 — Verified via DBLP
- [ ] [jones2022fast] Jones et al., "Fast Paxos" — DOI not found, please verify

## Suggested Citations (from review)
- [ ] Need: work on disaggregated memory for comparison
  - Search: [DBLP](https://dblp.org/search?q=disaggregated+memory) | [Scholar](https://scholar.google.com/scholar?q=disaggregated+memory)
- [ ] Need: recent NVM storage system baseline
  - Search: [DBLP](https://dblp.org/search?q=NVM+storage+system) | [Scholar](https://scholar.google.com/scholar?q=NVM+storage+system)
```

#### `check-submission` — "最终检查" / "投稿检查" / "submission check"

Final compliance check against conference requirements.

**Checks**:
- Page count within limit (12 pages for most, 11 for ASPLOS)
- Correct template (USENIX vs ACM)
- Anonymous submission mode enabled (no author names, no self-identifying references)
- ArXiv policy compliance (if applicable)
- Reference formatting
- Figure format (vector graphics preferred)
- Required sections present (e.g., ethics statement, data availability)
- No `\fillin` / `\fillcite` placeholders remaining

---

## Agent Team

Six agents organized in three phases. Each agent has a focused, non-overlapping concern. Full agent specifications are in `agents/`. Read only the agents needed for the current task.

### Phase 0: Intake (no agent — orchestrator logic)

Extract the paper's storyline and build the Story Traceability Matrix. See `references/story-coherence-guide.md` for the matrix format and extraction method.

### Phase 1: Parallel Review (4 agents, independent)

| Agent | File | Focus |
|-------|------|-------|
| Story Coherence | `agents/story-coherence-agent.md` | Does the paper tell one coherent story? Does each design section naturally connect to the stated problem? |
| Style Checker | `agents/style-checker-agent.md` | Writing clarity, paragraph structure, terminology consistency, systems-specific style |
| Reviewer | `agents/reviewer-agent.md` | Adversarial review from 3 diverse personas (senior expert, adjacent-field researcher, busy PC member) |
| Experiment Checker | `agents/experiment-checker-agent.md` | Claim-evidence alignment, experiment completeness, citation sufficiency |

Each agent produces a structured issue list with severity tags: **CRITICAL** / **MAJOR** / **MINOR**.

### Phase 2: Synthesis + Improvement (1 agent)

| Agent | File | Focus |
|-------|------|-------|
| Improvement | `agents/improvement-agent.md` | Collect all review opinions, produce revised text with tracked changes |

### Standalone (invoked by `compress`)

| Agent | File | Focus |
|-------|------|-------|
| Compressor | `agents/compressor-agent.md` | Content compression to meet page limits |

---

## Citation Safety

AI-generated citations have a ~40% error rate. This skill treats citation integrity as a hard constraint.

**Rules**:
- Never generate BibTeX entries from memory — search programmatically or mark as placeholder
- When suggesting citations, provide search links (DBLP, Semantic Scholar, Google Scholar) instead of BibTeX
- Use `\fillcite[description]` for missing citations in the LaTeX source
- The `check-citations` command generates a verification checklist for the user to manually verify

**Why this matters**: A single fabricated citation can result in desk rejection. It's better to leave a `\fillcite` placeholder than to risk a hallucinated reference. The author is always the final authority on citations.

---

## Reference Files

Load only what's needed for the current task:

| File | When to Read |
|------|-------------|
| `references/story-coherence-guide.md` | During Phase 0 intake and story-coherence-agent work |
| `references/systems-writing-principles.md` | During style-checker-agent and improvement-agent work |
| `references/section-guides.md` | When polishing a specific section type (intro, design, eval, etc.) |
| `references/review-checklist.md` | During reviewer-agent work |
| `references/conference-requirements.md` | During check-submission and intake |
| `references/best-paper-styles.md` | During style-checker-agent and improvement-agent work, or when user asks about writing style |

---

## Writing Principles (Quick Reference)

These principles are expanded in `references/systems-writing-principles.md`. Key points for quick access:

1. **One story, one paper**: The paper should be organizable around a single key insight
2. **Show, don't tell**: Let the design naturally demonstrate how it addresses the problem — don't pepper the text with "we solve challenge X"
3. **Precise language**: "p99 latency drops from 12ms to 3ms" not "performance improves significantly"
4. **One paragraph, one point**: First sentence states the paragraph's message
5. **Old before new**: Each sentence builds on what the reader already knows
6. **Measure everything**: Motivation needs quantitative evidence, not just assertions
7. **Name your baselines**: "RocksDB 8.0" not "prior work"; "Linux 6.1 CFS" not "the default scheduler"
8. **Never fabricate**: Use `\fillin` / `\fillcite` placeholders for missing values and citations
