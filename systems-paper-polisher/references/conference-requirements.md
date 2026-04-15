# Conference Requirements Matrix

Quick reference for submission requirements at top systems conferences. Verify against the official CFP before submission — requirements may change between years.

---

## Conference Comparison

| | OSDI | SOSP | ATC | ASPLOS | EuroSys | NSDI |
|---|------|------|-----|--------|---------|------|
| **Org** | USENIX | ACM SIGOPS | USENIX | ACM | ACM/EuroSys | USENIX |
| **Pages** | 12 | 12 | 12 | **11** | 12 | 12 |
| **Refs** | Excluded | Excluded | Excluded | Excluded | Excluded | Excluded |
| **Appendix** | Unlimited* | Unlimited* | Unlimited* | Unlimited* | Unlimited* | Unlimited* |
| **Template** | USENIX | ACM sigplan | USENIX | ACM sigplan | ACM sigplan | USENIX |
| **Font** | 10pt, 2-col | 10pt, 2-col | 10pt, 2-col | 10pt, 2-col | 10pt, 2-col | 10pt, 2-col |
| **Blind** | Double | Double | Double | Double | Double | Double |
| **Artifact Eval** | Yes | Yes | Yes | Yes | Yes | Yes |
| **Frequency** | Biennial | Biennial | Annual | ~2x/year | Annual | Annual |

*Appendix is unlimited in length but reviewers are NOT required to read it.

---

## USENIX Conferences (OSDI, ATC, NSDI)

### Template
- Document class: `\documentclass[letterpaper,twocolumn,10pt]{article}`
- Style: `\usepackage{usenix2019_v3}`
- Template source: `templates/USENIX/`

### Page Limit
- **12 pages** for main content
- References do not count toward the page limit
- Unlimited appendix (but reviewers may ignore it)

### Anonymization
- Double-blind: remove author names, affiliations, acknowledgments
- Anonymize self-citations: "Our prior work [X]" → "Prior work [X]"
- Remove identifying information from headers/footers
- `\pagestyle{plain}` or anonymous mode in template

### ArXiv Policy
- Check the specific year's CFP — USENIX venues have varied on ArXiv policies
- Some allow existing ArXiv preprints, some don't
- Generally: do not post a new ArXiv version during the review period

### Camera-Ready
- Add author information
- Include USENIX copyright notice
- Final page limit may differ slightly (check CFP)

---

## ACM SIGOPS (SOSP)

### Template
- Document class: `\documentclass[sigplan,10pt]{acmart}`
- Template source: `templates/ACM/`
- Use anonymous mode: `\documentclass[sigplan,10pt,anonymous]{acmart}`

### Page Limit
- **12 pages** for main content
- References excluded

### Anonymization
- Double-blind
- ACM-specific: remove CCS concepts and keywords in submission (add in camera-ready)
- Remove `\acmDOI`, `\acmISBN`, etc. during review

### Review Process
- Has rebuttal phase — reviewers actively read responses
- Uniform mediocre scores typically don't lead to acceptance
- Highest selectivity among systems venues (~15%)

---

## ASPLOS

### Template
- Document class: `\documentclass[sigplan,10pt]{acmart}` (or `[sigplan,nonacm]`)
- Same ACM template as SOSP

### Page Limit
- **11 pages** (1 page less than most other venues — plan accordingly!)
- References excluded

### Scope
- Spans systems AND architecture — reviewers may have diverse backgrounds
- Hardware-software co-design papers: include simulation methodology details
- Reviewers from architecture side may expect different baseline conventions

---

## EuroSys

### Template
- ACM sigplan format (same as SOSP/ASPLOS)

### Page Limit
- **12 pages**
- References excluded

### Review Process
- Multi-round review with possible major revision decisions
- If given "major revision", this is an opportunity, not a rejection
- High artifact evaluation expectations

---

## Pre-Submission Checklist (All Venues)

### Formatting
- [ ] Correct template (USENIX vs ACM)
- [ ] Within page limit (11 for ASPLOS, 12 for others)
- [ ] Correct font size (10pt) and layout (two-column)
- [ ] Margins correct (do not modify template margins)
- [ ] Figures are vector graphics where possible (PDF/EPS, not PNG)
- [ ] Figures are legible in grayscale (for printing)
- [ ] No overfull hbox warnings (text overflows column)

### Anonymization (Double-Blind)
- [ ] Author names removed
- [ ] Affiliations removed
- [ ] Acknowledgments removed (or anonymized)
- [ ] Self-citations anonymized ("Our prior work" → "Prior work")
- [ ] No identifying URLs (GitHub repos, project pages)
- [ ] No identifying information in PDF metadata
- [ ] Headers/footers don't contain identifying info
- [ ] Supplementary material is also anonymized

### Content
- [ ] No `\fillin` or `\fillcite` placeholders remaining
- [ ] No TODO comments visible
- [ ] All figures have proper captions
- [ ] All tables have proper captions (above the table)
- [ ] All cross-references resolve (`\ref`, `\cite`)
- [ ] Bibliography entries are complete (no missing venues or years)

### Technical
- [ ] Paper compiles without errors
- [ ] Paper compiles without critical warnings (overfull boxes, missing references)
- [ ] PDF is under any file size limit specified by the venue
