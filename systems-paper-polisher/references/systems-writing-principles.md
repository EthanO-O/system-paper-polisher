# Systems Paper Writing Principles

A consolidated guide to writing clear, precise, and compelling systems papers. Draws from Levin & Redell (1997), Roscoe (ETH), Gopen & Swan (1990), and established systems community conventions.

---

## 1. The Key Insight Principle (Levin & Redell)

Every systems paper should be organizable around **one key insight** — a single, non-obvious observation that enables the solution. If you can't state it in one sentence, either the insight isn't clear or the paper is trying to do too much.

The three pillars:

| Pillar | Question | Evidence Required |
|--------|----------|-------------------|
| The Problem | Is it real and measured? | Quantitative study showing the problem exists in practice |
| The Insight | Is it non-obvious? | A reviewer should be able to paraphrase it to a colleague |
| The Conviction | Does the evaluation convince? | End-to-end experiments on realistic workloads |

**Self-test**: Can you complete this sentence? "The key insight of this paper is that _____, which enables _____ and results in _____."

---

## 2. Gopen & Swan's Reader Expectation Principles

These seven principles are grounded in how readers process English prose. Following them makes your writing effortlessly clear.

### 2.1 Subject-Verb Proximity

Keep the grammatical subject close to its main verb. Long interruptions force the reader to hold context in working memory.

> **Weak**: "The scheduler, which maintains a priority queue of pending requests sorted by expected expert locality and factors in current GPU memory utilization as well as network bandwidth availability, dispatches the request."
>
> **Strong**: "The scheduler dispatches the request based on expected expert locality, current GPU memory utilization, and network bandwidth."

### 2.2 Stress Position

Readers expect the most important information at the **end** of a sentence. Place your emphasis there.

> **Weak**: "A 2.3x throughput improvement is achieved by our disaggregated architecture."
>
> **Strong**: "Our disaggregated architecture achieves a 2.3x throughput improvement."

### 2.3 Topic Position

The **beginning** of a sentence should provide context — connecting to what's already known. The end delivers new information.

> **Context first**: "Because expert weights are sparse, we store them in CPU memory rather than GPU memory."
> (Reader knows: expert weights are sparse → learns: stored in CPU memory)

### 2.4 Old Before New

Each sentence should begin with familiar information and end with the new point. This creates a natural chain of understanding.

> "Requests arrive at the controller. **The controller** assigns each request to a worker based on expert affinity. **Each worker** maintains a local cache of frequently-used experts."

Each sentence starts by referencing something the previous sentence introduced.

### 2.5 One Paragraph, One Message

Every paragraph should make exactly **one point**. State it in the first sentence (the topic sentence). The remaining sentences develop, support, or elaborate that point.

**Test**: After writing a paragraph, can you summarize its point in one sentence? If not, it probably makes multiple points and should be split.

### 2.6 Action in the Verb

Put the action in the verb, not in a nominalized noun.

> **Weak**: "We perform an analysis of the scheduling overhead."
> **Strong**: "We analyze the scheduling overhead."
>
> **Weak**: "The implementation of the cache requires..."
> **Strong**: "Implementing the cache requires..."

### 2.7 Sentence Flow

Each sentence should connect to the previous one through a clear relation:
- **Cause/consequence**: "Because...", "Therefore...", "As a result..."
- **Contrast**: "However...", "In contrast...", "Unlike..."
- **Refinement**: "Specifically...", "In particular...", "More precisely..."
- **Example**: "For instance...", "Consider...", "In our experiments..."

If the relation between two consecutive sentences isn't clear, the flow is broken.

---

## 3. Systems-Specific Style Conventions

### 3.1 Precision in Metrics

Systems papers demand quantitative precision. Vague language suggests the author doesn't know their own numbers.

| Weak | Strong |
|------|--------|
| "Performance improves significantly" | "Throughput increases by 2.3x on YCSB-A" |
| "Low latency" | "p99 latency of 1.2ms under 10K QPS" |
| "Modest overhead" | "4.7% CPU overhead and 12MB memory overhead" |
| "Scales well" | "Throughput scales linearly from 1 to 64 nodes" |

### 3.2 Latency Reporting

Mean latency is almost never sufficient in systems papers. Tail latency matters because it affects real user experience — a single slow request can block an entire user-facing operation.

**Always report**: p50, p99, p999 (or at minimum p50 and p99)
**Also show**: CDF plots for latency distributions, throughput-latency curves

### 3.3 Named Baselines

Name every system you compare against, with version numbers.

> **Weak**: "Compared to prior work, our system is faster."
> **Strong**: "Compared to RocksDB 8.0 and LevelDB 1.23, ExpertKit achieves..."

### 3.4 Named Workloads

Specify workloads precisely.

> **Weak**: "We evaluate on a realistic workload."
> **Strong**: "We evaluate on YCSB-A (50% read, 50% update) with 1KB values and Zipfian key distribution (θ=0.99)."

### 3.5 Hardware Specification

Fully specify the evaluation hardware:
- CPU: model, core count, clock speed
- Memory: capacity, type (DDR4/DDR5), speed
- Storage: model, type (SSD/HDD), interface (NVMe/SATA)
- Network: bandwidth, technology (RDMA/TCP)
- OS: distribution and kernel version

### 3.6 Words to Avoid

| Avoid | Use Instead |
|-------|-------------|
| "novel" (overused) | Just describe what's new — the reader will judge novelty |
| "utilize" | "use" |
| "leverage" | "use" or "exploit" or describe the specific benefit |
| "synergistic" | Describe the specific interaction |
| "holistic" | Describe what's included |
| "facilitate" | "enable" or "allow" or describe the specific mechanism |
| "paradigm" | "approach" or "model" (unless genuinely appropriate) |

### 3.7 Formatting Conventions

- No rhetorical questions in the body text. "How can we solve this?" → "To solve this, we..."
- No contractions. "don't" → "do not", "can't" → "cannot"
- Expand abbreviations on first use. "We use Remote Direct Memory Access (RDMA) for..."
- Use `\paragraph{Heading.}` (run-in headings) for fine-grained structure instead of deep `\subsubsubsection` nesting
- Prefer flowing prose with transition words over inline (1), (2), (3) lists in the introduction

### 3.8 AI Writing Anti-Patterns

These are common problems when AI assists with academic writing. They make prose feel machine-generated and are easy to spot by experienced reviewers. Check and fix these aggressively.

**Punctuation and connectors**:

- **Avoid em dashes**. Express parenthetical content using subordinate clauses or commas instead. Em dashes feel informal and are overused by AI.
  > Weak: "The scheduler — which handles all routing — dispatches requests."
  > Strong: "The scheduler, which handles all routing, dispatches requests."

- **Avoid mid-sentence explanatory colons**. A colon used to "explain" what came before ("X: Y elaborates on X") is informal in systems papers. Restructure as a subordinate clause or split into two sentences. Colons are acceptable only for introducing formal lists or definitions.
  > Weak: "This creates a problem: the cache cannot hold all experts."
  > Strong: "This creates a problem because the cache cannot hold all experts."

- **Avoid informal clause connectors**. Words like "so", "but", "plus", and "also" used as conjunctions between independent clauses read as conversational. Use "therefore", "thus", "however", "whereas", or restructure as subordinate clauses.

- **Avoid semicolons in body prose**. In running text, replace semicolons with sentence breaks. Semicolons are acceptable only inside enumeration lists ("first, X; second, Y; third, Z").

**Sentence structure**:

- **Avoid dense nested relative clauses**. "The X that makes A effective also identifies B" embeds two claims in one clause. Split into two sentences.

- **Avoid runs of consecutive short sentences**. Three or more one-clause sentences in a row read as a bullet list in disguise. Consolidate with compound sentences. Reserve standalone short sentences for deliberate emphasis, used sparingly.

- **Avoid comma-heavy, over-interrupted sentences**. When a main clause is broken by multiple parenthetical insertions, the sentence becomes hard to parse. Symptoms: three or more comma-delimited interruptions between subject and verb. Fix: extract parenthetical content into separate sentences, or move contrastive asides to the start.

**Framing and word choice**:

- **Avoid defensive "not X but Y" framing**. "Our contribution is not X itself but Y" reads as apologetic and concedes primacy to prior work. Instead, state the contribution positively: "SystemName extends X by treating Y as the elastic unit."

- **Avoid engineering-level language in design sections**. Describe *what* the system does and *why*, not implementation-level details like specific API calls, parameter defaults, or code patterns. Save those for the implementation section.

- **Avoid uncommon or informal words** that sound technical but may be unfamiliar or imprecise:

  | Avoid (in prose) | Prefer |
  |-------------------|--------|
  | "tractable" | "manageable" or restructure |
  | "steers" | "directs" |
  | "monotonically" | "steadily" or state the direction |
  | "amortized" (loosely) | "average" or "distributed across" |
  | "aforementioned" | "this" or restate the noun |

---

## 4. Placeholder System

When a value is unknown during drafting, use explicit placeholders rather than guessing:

- `\fillin[description]` — for missing values/claims (renders as red [N:?])
- `\fillcite[description]` — for missing citations (renders as blue [cite])
- `\fillnum` — for quick numeric placeholders

Before submission: run `\printfillinlistifany` to verify all placeholders are resolved.

The `fillin.sty` package is available in `templates/utils/fillin.sty`.

---

## 5. Time Allocation

Spend roughly equal time on:
1. **Abstract + Introduction + Motivation** — These determine first impression
2. **Figures** (architecture + evaluation) — Reviewers look at figures before reading
3. **Design + Implementation** — The technical core
4. **Evaluation + Everything else** — The validation

Many authors under-invest in the introduction and over-invest in the design section. The introduction sets up the entire paper — if it doesn't work, the design section won't save it.

---

## 6. The Levin & Redell Self-Review Checklist

Before considering the paper "done," check:

- [ ] Can I state the key insight in one sentence?
- [ ] Is the problem motivated with quantitative evidence (not just assertions)?
- [ ] Does the introduction make a reader *want* to keep reading?
- [ ] Is every contribution claim backed by a specific experiment?
- [ ] Are all baselines named with versions and fairly configured?
- [ ] Does the architecture figure clearly convey the system's structure?
- [ ] Is terminology consistent throughout?
- [ ] Have I acknowledged limitations honestly?
- [ ] Are all citations verified (not generated from memory)?
- [ ] Are all `\fillin` placeholders resolved?
