# Story-Driven Coherence Guide

## What Is Story-Driven Coherence?

A coherent systems paper reads like one continuous argument, not a collection of independent sections. The reader should never wonder "why am I reading this?" — every section should feel like a natural step in understanding the system.

**The core idea**: Your paper opens by explaining what the system does and what problem it solves. Everything that follows — design, implementation, evaluation — should be organized to advance that storyline. The reader should finish the paper with a clear understanding of the system's purpose, how it works, and why the design choices make sense.

This is not about mechanically linking every paragraph back to "the challenges." It's about the reader naturally sensing that the paper is headed somewhere, that each piece contributes to the whole, and that the authors had a clear vision when writing.

## Why It Matters

Reviewers read many papers. They quickly develop a mental model of what the paper is about. If the design section feels disconnected from the introduction's promises, or if the evaluation measures things the introduction didn't emphasize, the reviewer's mental model breaks. This confusion is one of the most common reasons papers receive "hard to follow" or "unclear contribution" feedback.

Papers that tell one clean story are easier to champion in PC discussions. A reviewer who can summarize the paper's contribution in one sentence to the PC is far more likely to fight for acceptance.

## How to Extract the Paper's Storyline

Read the abstract and introduction and answer these questions:

1. **What does the system do?** (1 sentence — the purpose)
   - Example: "ExpertKit separates expert and attention computation across CPU+GPU in MoE inference."

2. **What problem does it solve?** (1-2 sentences — the gap)
   - Example: "Existing MoE inference systems waste GPU memory on rarely-used expert weights, limiting batch size and throughput."

3. **What insight drives the design?** (1 sentence — the non-obvious observation)
   - Example: "Most experts are accessed infrequently enough that CPU execution matches GPU latency when computation is overlapped with attention."

4. **What are the key contributions/claims?** (2-4 bullet points)
   - Example: "1. A disaggregated architecture that... 2. An adaptive scheduler that... 3. Evaluation showing 2.3x throughput..."

These four elements form the **storyline anchor**. Every section should connect back to at least one of them.

## The Story Traceability Matrix

Map each key claim to where it's introduced, addressed, and validated:

```
| Key Point              | Introduced (§) | Addressed in Design (§) | Validated in Eval (§) | Status  |
|------------------------|-----------------|-------------------------|-----------------------|---------|
| Disaggregated arch.    | §1 P3, §2      | §3.1, §3.2              | §5.1 (throughput)     | OK      |
| Adaptive scheduler     | §1 P5          | §3.3                    | §5.2 (latency)        | OK      |
| Expert placement algo  | §1 P4          | §3.4                    | §5.3                  | WEAK    |
| Fault tolerance        | §1 P6          | §3.5                    | ???                   | MISSING |
```

- **OK**: Clear thread from introduction through design to evaluation
- **WEAK**: The thread exists but connections are unclear (e.g., design doesn't explain *why* this approach serves the stated goal, or evaluation metric doesn't directly validate the claim)
- **MISSING**: A claim is made but not followed through

## Positive Patterns

### Pattern 1: Design motivated by concrete need

Each design subsection opens by establishing *why* this component is needed — not by citing "Challenge X from Section 2", but by describing the concrete situation that creates the need:

> **Weak**: "To address Challenge 2 (memory efficiency), we design a tiered expert cache."
>
> **Strong**: "When a single GPU processes multiple batches concurrently, the active expert set changes rapidly. Loading experts from CPU memory on every request would dominate inference latency. We design a tiered expert cache that..."

The strong version creates the same connection without mechanical cross-referencing. The reader naturally thinks "ah, this is about the memory problem from the intro" without being told.

### Pattern 2: Evaluation organized around claims

Structure evaluation sections to match the contributions, but use descriptive subsection titles rather than mechanical ones:

> **Weak**: §5.1 "Claim 1: Throughput", §5.2 "Claim 2: Latency", §5.3 "Claim 3: Scalability"
>
> **Strong**: §5.1 "End-to-End Performance", §5.2 "Tail Latency Under Load", §5.3 "Scaling to Large Expert Counts"

### Pattern 3: Architecture overview as roadmap

An early architecture overview figure + description gives the reader a mental map. Subsequent sections can reference back to this map naturally ("The scheduler, shown in Figure 1, receives..."). This creates implicit coherence — the reader knows where each component fits.

### Pattern 4: Transitions that carry the thread

Between subsections, a brief transition sentence connects what was just discussed to what comes next:

> "With the expert placement decided, we now turn to how the scheduler dispatches requests to the appropriate workers."

This is not mechanical ("Having addressed Challenge 1, we now address Challenge 2") but a natural narrative bridge.

## Anti-Patterns

### Anti-Pattern 1: Mechanical Challenge Mapping

Every design subsection starts with "To address Challenge N" or "As motivated in Section 2." This feels like a checklist and becomes monotonous. The reader should *feel* the connection, not have it announced.

### Anti-Pattern 2: Feature-List Design

The design section reads as: "Component A does X. Component B does Y. Component C does Z." There's no narrative explaining *why* these components exist or how they relate to each other. It reads like API documentation.

### Anti-Pattern 3: Orphan Components

A design component is described in detail but doesn't clearly serve any purpose stated in the introduction. The reader wonders "why is this here?" This often happens with implementation optimizations that don't connect to the research contribution.

### Anti-Pattern 4: Broken Narrative Thread

The introduction raises an issue (e.g., "handling stragglers is critical") but the design section never addresses it, and the evaluation doesn't test it. The promise is made but never delivered.

### Anti-Pattern 5: Evaluation Drift

The evaluation measures something different from what the introduction promised. For example, the intro emphasizes latency improvement but the evaluation section leads with throughput comparisons and barely discusses latency.

## Quick Self-Test

After writing (or polishing) the paper, try this:

1. **One-sentence test**: Can you summarize the paper's main contribution in one sentence? If it takes more than one sentence, the paper may be trying to do too much.

2. **Section deletion test**: For each major section, ask "If I deleted this section, would the paper's argument be incomplete?" If the answer is "not really," the section might be unnecessary or disconnected from the main story.

3. **Stranger test**: If a colleague who hasn't read the paper asks "what's this paper about?", can you explain it in 30 seconds such that the design, evaluation, and contribution all follow naturally from your explanation?

4. **Reverse reading test**: Read the evaluation first, then the design, then the introduction. Does the evaluation test what the introduction promises? Does the design deliver what the evaluation tests?
