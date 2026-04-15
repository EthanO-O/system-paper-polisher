# Review Checklist and Rejection Risk Assessment

Use this checklist to simulate what reviewers will look for. Address high-risk items before submission.

---

## Five Rejection Dimensions

Most rejections trace back to one or more of these dimensions. For each, review the signals and pre-emption strategies.

### 1. Insufficient Contribution

**Signals reviewers look for**:
- The technique is well-explored in prior work
- The improvement is predictable from combining known techniques
- The contribution is primarily engineering, not research insight
- The problem targeted is too narrow or too easy

**Pre-emption**:
- Clearly articulate the non-obvious insight
- If the approach seems incremental, explain why the combination is challenging or why prior attempts failed
- Show that the problem is harder than it appears (measurement study helps)

### 2. Unclear Writing

**Signals**:
- Method not reproducible from the description
- Key design motivation missing (reader doesn't know *why* this component exists)
- Terms used inconsistently
- No architecture figure or figure is incomprehensible

**Pre-emption**:
- Architecture figure as early as possible
- One paragraph = one point, topic sentence first
- Consistent terminology throughout
- Have someone unfamiliar with the work read Sections 1-3

### 3. Weak Empirical Results

**Signals**:
- Marginal improvement over baselines (within noise)
- Only one metric shown (throughput without latency, or vice versa)
- Only mean latency, no percentiles
- Only microbenchmarks, no end-to-end evaluation

**Pre-emption**:
- Show multiple metrics, especially throughput AND latency
- Report p50, p99, p999 for latency
- Include end-to-end evaluation on realistic workloads
- Show where the system wins AND where it doesn't

### 4. Incomplete Evaluation

**Signals**:
- Missing ablation studies for key design choices
- Weak baselines or unfair configurations
- Missing scalability experiments (if scalability is claimed)
- Missing important workload scenarios
- Hardware setup not specified

**Pre-emption**:
- Build a claim-experiment matrix (every claim needs an experiment)
- Include ablation for each key design decision
- Use strong, recent baselines with documented configurations
- Fully specify hardware and software setup

### 5. Questionable Design Soundness

**Signals**:
- Unrealistic assumptions (e.g., requires global knowledge, zero-failure environment)
- No discussion of failure handling or edge cases
- Benefits don't clearly outweigh added complexity
- Design has obvious scalability bottleneck not addressed

**Pre-emption**:
- Discuss failure handling and limitations honestly
- Include stress tests and failure recovery experiments
- If the design has known limitations, acknowledge them before reviewers point them out

---

## Systems-Specific Reviewer Heuristics

Experienced systems reviewers apply these implicit tests:

### The "Would I Deploy This?" Test
Does this system solve a real problem well enough that a practitioner would consider using it? Systems that are purely academic exercises without practical grounding face skepticism.

### The "What's the Catch?" Test
Reviewers actively look for hidden limitations. If the paper doesn't acknowledge tradeoffs, reviewers will find them and be less charitable. Honest discussion of limitations builds trust.

### The "What Baseline Would I Compare Against?" Test
If there's an obvious baseline that's missing, it raises red flags. Ask yourself: "If I were reviewing this, what system would I immediately want to see compared?"

### The "Could This Be a Workshop Paper?" Test
Is the contribution substantial enough for a top venue? If the core idea could be fully described in 4 pages, it might be better suited for a workshop.

---

## Pre-Submission Self-Review

Answer each question with specific evidence from the paper:

### Content
- [ ] Can I state the key insight in one sentence?
- [ ] Is the problem motivated with quantitative evidence?
- [ ] Does the introduction make the reader want to keep reading?
- [ ] Is every contribution claim backed by a specific experiment?
- [ ] Are limitations honestly acknowledged?

### Evaluation
- [ ] Are all baselines named with version numbers?
- [ ] Are baselines fairly configured? (documented configurations)
- [ ] Are latencies reported as percentiles (p50, p99, p999)?
- [ ] Are workloads precisely described?
- [ ] Is hardware fully specified?
- [ ] Are ablation studies present for key design choices?
- [ ] Do results include both good and bad scenarios?

### Writing
- [ ] Is there an architecture figure?
- [ ] Is terminology consistent throughout?
- [ ] Does each paragraph make one point?
- [ ] Are figures and tables self-explanatory with good captions?
- [ ] Are transitions between sections smooth?

### Technical Integrity
- [ ] Are all numbers measured (not estimated or fabricated)?
- [ ] Are all citations verified (not generated from memory)?
- [ ] Are all `\fillin` / `\fillcite` placeholders resolved?
- [ ] Is the paper anonymous (for double-blind venues)?

---

## Rebuttal Preparation

If the paper goes through a review process with rebuttal:

### When to rebut
- Factual errors in reviews ("the paper doesn't compare against X" when it does)
- Misunderstandings that can be clarified with evidence
- Minor experiments that can be run during the rebuttal period

### When NOT to rebut
- All reviewers gave low scores — the problem is fundamental
- The criticism is about the research direction, not execution
- You would need to redesign the system to address the concern

### Rebuttal format
- Brief thanks (1 sentence)
- Address each concern with specific evidence
- If you can run a new experiment, include the results
- Stay factual, not emotional
- Keep it concise — reviewers have limited time for rebuttals
