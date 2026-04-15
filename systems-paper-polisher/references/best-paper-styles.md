# Best Paper Writing Styles: Patterns from Top Systems Conference Awards

An analysis of common writing patterns in recent (2020-2025) best paper award winners at OSDI, SOSP, ASPLOS, EuroSys, and NSDI. These patterns are not rules — they're observations about what top-quality systems papers tend to have in common.

---

## Pattern 1: The Concrete Opening

Best papers almost never open with a grand, abstract statement ("The rapid growth of cloud computing has..."). Instead, they open with a **specific, concrete scenario** that immediately puts the reader in the problem space.

**Typical structure**:
- Sentence 1: A specific observation or fact that grounds the reader
- Sentences 2-3: Why this matters (with numbers)
- Sentence 4: The tension or challenge this creates

**Example pattern** (synthesized from common structures):
> "Modern language models use Mixture-of-Experts layers with hundreds of experts, but during inference only 2-4 experts are active per token. On a typical GPU server, this means 95% of loaded expert weights sit idle, consuming 48GB of the available 80GB GPU memory — memory that could serve additional requests."

**Why it works**: The reader immediately understands the problem through a concrete picture, not through an abstract claim that could apply to anything.

## Pattern 2: The Gap Statement Is Structural, Not Superficial

Best papers explain *why* existing approaches fail at a **structural** level — not just that they're slow or limited.

**Weak gap** (superficial):
> "Existing systems are slow because they don't optimize for this workload."

**Strong gap** (structural):
> "Existing systems assume a static expert assignment, which worked when models had 8-16 experts. At 128+ experts with dynamic routing, this assumption creates a fundamental mismatch: the memory required to hold all experts exceeds what's available on a single GPU, but pre-partitioning experts across GPUs fragments the routing decisions."

**Why it works**: A structural explanation makes the reader understand that the problem isn't just about better engineering — it requires a new approach.

## Pattern 3: Architecture Figure as the Anchor

Virtually all best papers have a clear, well-labeled architecture figure early in the paper (usually Figure 1 or 2). This figure serves as the reader's mental map for the rest of the paper.

**Characteristics of good architecture figures**:
- Shows all major components and their relationships
- Uses arrows to indicate data flow and control flow (distinguished visually)
- Labels match terminology in the text exactly
- Simple enough to understand in 30 seconds
- Color is used meaningfully, not decoratively (and legible in grayscale)
- Often includes numbered steps showing the flow of a typical operation

**Common tools**: draw.io, TikZ, Inkscape (avoid PowerPoint — it shows)

## Pattern 4: Design Sections Follow Execution Flow

The design section is organized to follow the system's execution flow — how a request/operation moves through the system — rather than being organized by component type.

**Weak organization** (by component type):
> §3.1 Data Structures, §3.2 Algorithms, §3.3 Networking, §3.4 Storage

**Strong organization** (by execution flow):
> §3.1 Request Routing and Scheduling, §3.2 Expert Loading and Caching, §3.3 Computation Pipeline, §3.4 Result Aggregation

**Why it works**: Following execution flow mirrors how readers naturally think about a system. Each section picks up where the previous one left off.

## Pattern 5: Motivation Before Mechanism

Each design subsection in best papers typically opens by establishing *why* this component is needed before explaining *how* it works. The motivation is usually a concrete scenario or observation, not a reference to an abstract challenge.

**Pattern**:
1. Brief scenario or observation that creates the need (2-3 sentences)
2. Why naive approaches don't work (1-2 sentences)
3. The design and how it works (main content)
4. Brief note on advantages or properties (1-2 sentences)

This pattern aligns with the "three elements" framework: motivation → design → advantage.

## Pattern 6: Evaluation Tells a Story

Best paper evaluations don't just present numbers — they guide the reader through a narrative:

1. **Setup** (shared across experiments, described once)
2. **Headline results** first (the best numbers, the main comparison)
3. **Deep dives** that explain *why* the system performs well (or doesn't)
4. **Ablation** showing that each component contributes
5. **Edge cases and limitations** (showing honesty and thoroughness)

Each evaluation subsection has a **one-sentence takeaway** stated at the beginning or end:
> "Figure 5 shows that ExpertKit scales linearly up to 64 GPUs, with throughput increasing by 0.95x per added GPU."

**Why it works**: Reviewers should know what to look for in each figure/table before examining the data.

## Pattern 7: Precise, Grounded Language

Best papers use language that is precise and grounded in specifics. They avoid vague qualifiers and ground every claim in data.

| Pattern in best papers | Pattern in weaker papers |
|------------------------|--------------------------|
| "p99 latency drops from 12ms to 3ms" | "latency improves significantly" |
| "RocksDB 8.0 on ext4" | "a state-of-the-art key-value store" |
| "YCSB-A with Zipfian (θ=0.99)" | "a standard benchmark" |
| "We observe that 73% of experts..." | "Most experts are..." |
| "reduces memory usage by 48GB (60%)" | "significantly reduces memory" |

## Pattern 8: Smooth Transitions

Best papers have smooth transitions between sections that maintain narrative flow without being formulaic.

**Between major sections** — a brief sentence connecting what was just discussed to what comes next:
> "With the scheduling algorithm defined, we now describe how workers execute the assigned computations."

**Between paragraphs** — topic sentences that build on the previous paragraph:
> "While the cache reduces expert loading time, it introduces a new challenge: cache invalidation during model updates."

**Not seen in best papers**:
> "Having addressed Challenge 1, we now turn to Challenge 2." (too mechanical)
> "In this section, we will describe..." (uninformative)

## Pattern 9: Honest Limitations

Best papers discuss limitations proactively — usually in the evaluation section or a dedicated discussion section. This builds reviewer trust and preempts criticism.

**Pattern**:
- Acknowledge specific scenarios where the system performs less well
- Explain *why* (structural reason, not just "future work")
- Distinguish between fundamental limitations and engineering gaps

**Example**:
> "ExpertKit's performance advantage diminishes for models with fewer than 16 experts, where the overhead of CPU-GPU communication outweighs the memory savings. For such models, a conventional GPU-only approach is preferable."

## Pattern 10: Figures That Explain Themselves

Best papers have evaluation figures with captions that tell the reader what to observe:

**Weak caption**: "Figure 5: Throughput comparison."

**Strong caption**: "Figure 5: Throughput under increasing load. ExpertKit sustains linear scaling up to 64 GPUs while the baseline plateaus at 16 GPUs due to memory contention."

The reader should understand the key takeaway from the figure without reading the body text.

---

## Using These Patterns for Polishing

When polishing a paper, use these patterns as reference points:

1. **Introduction**: Does it open concretely (Pattern 1)? Is the gap structural (Pattern 2)?
2. **Architecture**: Is there a clear architecture figure (Pattern 3)?
3. **Design**: Does it follow execution flow (Pattern 4)? Does each subsection motivate before explaining (Pattern 5)?
4. **Evaluation**: Does it tell a story (Pattern 6)? Is the language precise (Pattern 7)?
5. **Throughout**: Are transitions smooth (Pattern 8)? Are limitations discussed honestly (Pattern 9)?
6. **Figures**: Do captions explain what to observe (Pattern 10)?

These are aspirational targets, not requirements. Not every paper will (or should) follow all patterns. Use judgment about what applies to the specific paper being polished.
