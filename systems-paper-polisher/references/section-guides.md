# Section-by-Section Writing Guide for Systems Papers

Adapted from general academic writing principles for the computer systems domain. Each section has a purpose, common structure patterns, and a quality checklist.

---

## Table of Contents

1. [Abstract](#abstract)
2. [Introduction](#introduction)
3. [Background / Motivation](#background--motivation)
4. [Design / Architecture](#design--architecture)
5. [Implementation](#implementation)
6. [Evaluation](#evaluation)
7. [Related Work](#related-work)
8. [Conclusion](#conclusion)

---

## Abstract

### Purpose
Convey the problem, approach, and key results in 150-250 words. The abstract is the paper's trailer — it should make the reader want to read more.

### Structure (5-Sentence Formula)

1. **The problem**: What concrete problem exists? (1 sentence)
2. **Why existing approaches fail**: What's the gap? (1 sentence)
3. **Your approach + key insight**: What do you do and why does it work? (1-2 sentences)
4. **Evaluation setup**: How did you validate? (1 sentence, brief)
5. **Headline results**: What are the top 2-3 numbers? (1 sentence)

### Template Variants

**Variant A: Problem → Contribution** (most direct)
> [Problem with quantification]. Existing systems [limitation]. We present [SystemName], which [approach]. [SystemName] achieves [key result 1] and [key result 2] on [benchmark].

**Variant B: Problem → Insight → Contribution** (adds conceptual bridge)
> [Problem]. The key challenge is [challenge]. We observe that [insight]. Based on this observation, [SystemName] [approach]. Evaluation on [benchmarks] shows [results].

**Variant C: Multiple Contributions** (for systems with several innovations)
> [Problem]. We present [SystemName] with three key contributions: (1) [contribution + advantage], (2) [contribution + advantage], (3) [contribution + advantage]. On [benchmarks], [SystemName] achieves [headline results].

### Checklist
- [ ] Can a reader identify the problem, approach, and results in one pass?
- [ ] Are headline numbers specific (not "significant improvement")?
- [ ] Is the abstract self-contained (no undefined abbreviations)?
- [ ] Does every claim have a corresponding experiment?

---

## Introduction

### Purpose
Set up the entire paper. After reading the introduction, the reader should understand what the paper does, why it matters, and what to expect.

### Structure (typically 2-2.5 pages)

**Part 1: Problem and Context** (1-2 paragraphs)
- Open with a concrete scenario showing why the problem matters
- Quantify the problem if possible ("X% of cloud workloads are...", "GPU memory is wasted Y% of the time")
- Establish the scope: what domain, what scale, what constraints

**Part 2: The Gap** (1-2 paragraphs)
- Why existing systems fall short — be specific about their limitations
- This is NOT a related work section — discuss limitations thematically, not paper-by-paper
- The gap should lead naturally to your insight

**Part 3: Your Approach** (2-3 paragraphs)
- State the key insight clearly (1-2 sentences, ideally one)
- Describe the system at a high level — what it does, how it works
- Reference the architecture figure if one exists
- Briefly mention key design decisions and why they work

**Part 4: Contributions** (1 paragraph)
- Bulleted list of 3-5 specific, falsifiable contributions
- Each contribution should be testable: "We show that X achieves Y" not "We propose X"
- Include evaluation highlights: "On [benchmark], [SystemName] achieves [result]"

**Part 5: Paper Organization** (optional, 1 sentence)
- "The rest of this paper is organized as follows: §2..., §3..., ..."
- Some authors prefer this, others find it unnecessary. Either is fine.

### Logic Flow (Backward → Forward)

**Think backward** (to discover the logic):
- What's our result? → What design achieves it? → What insight enables that design? → What problem makes this design necessary? → Why does the problem exist?

**Write forward** (to present clearly):
- Problem exists → Existing approaches fail because → Our insight is → Our system does → Our results show

### Checklist
- [ ] Does the first paragraph establish why this problem matters?
- [ ] Is the gap between existing work and the need clearly articulated?
- [ ] Is the key insight explicitly stated (not buried or implied)?
- [ ] Are contributions specific and falsifiable?
- [ ] Does the introduction length not exceed ~2.5 pages?

---

## Background / Motivation

### Purpose
Provide evidence that the problem is real and worth solving. In systems papers, this often includes a measurement study or analysis of real workloads.

### Structure

**Option A: Measurement Study** (strongest)
- Present measurements from real systems/workloads that demonstrate the problem
- Show *why* existing approaches fail (not just *that* they fail)
- Identify the root cause, which leads to the paper's key insight

**Option B: Analysis + Example** (common)
- Walk through a concrete example showing the problem
- Analyze why the problem occurs (structural, not incidental)
- Show the cost (performance, resource waste, complexity)

### Systems-Specific Advice

- Motivation must be **quantitative**, not just qualitative assertions
- "Memory is wasted" is weak; "48% of GPU memory holds cold expert weights" is strong
- The measurement methodology should be reproducible
- If the problem is well-established, a brief quantitative summary suffices
- If the problem is novel, a thorough measurement study is needed

### Checklist
- [ ] Is the problem demonstrated with quantitative evidence?
- [ ] Does the analysis explain *why* existing approaches fail (structural reason)?
- [ ] Does the motivation naturally lead to the paper's key insight?

---

## Design / Architecture

### Purpose
Explain *how* the system works and *why* it's designed this way. This is the technical core of the paper.

### Structure

**Overview** (1 subsection)
- System architecture figure (the most important figure in the paper)
- High-level description: components, data flow, control flow
- Scope: what's included and what's out of scope
- Preview: what each subsequent subsection covers

**Component Subsections** (1 per major component)

Each component subsection should contain three elements:

1. **Motivation**: Why does this component exist? What need does it serve?
   - Open with the concrete scenario or need (not "To address Challenge X")
   - The reader should naturally connect this to the earlier problem discussion
   - Typical openers: "When [situation occurs], the system needs to...", "A remaining challenge is..."

2. **Design**: How does the component work?
   - Describe in execution order: given [input], step 1 → step 2 → step 3 → [output]
   - Define key data structures and representations first
   - Use pseudocode or algorithms for complex logic
   - Reference the architecture figure to show where this component fits

3. **Rationale / Advantage**: Why this approach over alternatives?
   - Brief comparison with obvious alternatives
   - Why this design is better for the specific problem
   - Tie advantage to measurable behavior when possible

### Ordering

Order subsections by the system's data flow or execution flow — the reader should follow the same path as a request through the system.

### Checklist
- [ ] Is there an architecture overview figure?
- [ ] Does each subsection explain *why* the component is needed (not just *what* it does)?
- [ ] Is the design described in execution order?
- [ ] Are design decisions justified (not just stated)?
- [ ] Can a skilled researcher implement the system from this description?

---

## Implementation

### Purpose
Provide practical details needed for reproducibility and to demonstrate engineering effort.

### Standard Content
- Language, platform, key libraries (with versions)
- Lines of code (total and per component, if informative)
- Key implementation decisions and why they were made
- Integration with existing systems (if applicable)
- Anything non-obvious about the implementation

### Advice
- Keep it concise — this is not the design section
- Focus on decisions that affect performance or correctness
- If the implementation is straightforward, a single paragraph may suffice
- Detailed parameters and configurations can go in the evaluation setup

---

## Evaluation

### Purpose
Provide evidence that the system's design claims are valid. Every claim in the introduction should have a corresponding experiment.

### Three Core Questions

Every systems paper evaluation should answer:

1. **Is it better than the state of the art?**
   - End-to-end comparison against strong, recent baselines
   - Fair setup: same hardware, same workload, systems properly tuned
   - Multiple benchmarks if the system is general-purpose

2. **Which design choices matter?**
   - Ablation studies for key components
   - Remove/replace/disable methodology
   - Shows that the contribution is in the design, not just good engineering

3. **How far does it generalize?**
   - Stress tests under different workloads, scales, configurations
   - Failure scenarios and recovery behavior
   - Honest reporting of limitations and failure modes

### Structure

1. **Experimental Setup** (1 subsection)
   - Hardware specification (CPU, memory, storage, network, OS)
   - Software: baseline versions, configuration, tuning
   - Workloads: precise description, parameters, data sizes
   - Methodology: number of runs, warm-up, measurement window

2. **End-to-End Comparison** (1-2 subsections)
   - Main results against baselines
   - Multiple metrics: throughput AND latency (not just one)
   - Latency as percentiles: p50, p99, p999

3. **Ablation Study** (1 subsection)
   - Each key design choice tested individually
   - Clear methodology: what's removed/replaced

4. **Deep Dives** (1-2 subsections)
   - Scalability, sensitivity analysis, overhead breakdown
   - Whatever specific claims need detailed validation

### Figure and Table Guidelines

**Tables**:
- Caption above the table
- Use booktabs style (`\toprule`, `\midrule`, `\bottomrule`)
- No vertical lines
- Label metric direction in headers (PSNR ↑, Latency ↓)
- Include units
- Highlight best results with bold

**Figures**:
- Line graphs for time-series or scaling experiments
- Bar charts for categorical comparisons
- CDF plots for latency distributions
- Caption should explain what to observe and why it matters

**Figure Quality Requirements**:
- **Vector format** (PDF, EPS, or TikZ) for architecture diagrams and plots — never raster for line art
- **Grayscale-legible** — verify by printing or converting to grayscale; do not rely on color alone to distinguish data series
- **Colorblind-safe** — use Okabe-Ito or Paul Tol palette for multi-series plots
- **Self-contained captions** — a reader should understand the figure without consulting the main text
- **No title inside the figure** — the caption serves that function
- **Error bars or confidence intervals** for throughput measurements
- **Latency as percentiles** (p50, p99, p999) — never mean only

**Architecture Figure** (the most important figure in the paper):
- Show all major components and their relationships
- Distinguish data flow and control flow with different arrow styles
- Labels must match terminology in the text exactly
- Should be understandable in 30 seconds
- Tools: draw.io, TikZ, Inkscape (avoid PowerPoint)

### Checklist
- [ ] Does every introduction claim have a supporting experiment?
- [ ] Are baselines strong, recent, and fairly configured?
- [ ] Are latencies reported as percentiles (not just mean)?
- [ ] Is hardware fully specified?
- [ ] Are ablation studies present for key design choices?
- [ ] Are failure modes and limitations discussed?

---

## Related Work

### Purpose
Position the paper in the research landscape. Show what's been done, where the gaps are, and how this work is different.

### Structure

**Organize by theme**, not by individual paper. Group related systems by the approach they take or the problem they address.

Each theme paragraph:
1. **Topic sentence**: Define the group ("Several systems address X by...")
2. **Representative systems**: Brief summary of 3-5 key systems and their approach
3. **Limitation**: What these systems don't handle (tied to YOUR contribution)
4. **Distinction**: How your work differs

### Advice
- Be fair to prior work — describe what they do well, not just limitations
- Include all strong baselines that appear in the evaluation
- Don't hide the most relevant competitors — reviewers will notice
- Don't make it a citation dump — each cited paper should serve a purpose
- 1-1.5 pages is typical; rarely more than 2 pages

### Checklist
- [ ] Are the strongest competitors discussed?
- [ ] Is related work organized by theme (not paper-by-paper)?
- [ ] Is the distinction from prior work clear in technical terms?
- [ ] Are all evaluation baselines also discussed here?

---

## Conclusion

### Purpose
Briefly summarize the contribution and point to future work. Keep it short — 0.5-0.75 pages.

### Structure
1. Restate the problem and core approach (1-2 sentences)
2. Summarize the strongest evidence (1-2 sentences)
3. State the broader impact or takeaway (1 sentence)
4. Limitations (1-2 sentences, if not already discussed)
5. Future work (1-2 sentences, concrete directions)

### Advice
- Don't repeat the introduction verbatim — summarize at a higher level
- Don't introduce new information
- Keep it concise — reviewers rarely spend time here
