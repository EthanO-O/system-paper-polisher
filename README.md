# Systems Paper Polisher

A Claude Code skill for polishing and improving computer systems conference papers targeting **OSDI, SOSP, ASPLOS, EuroSys, ATC, NSDI**.

Multi-agent iterative review and improvement with story-driven coherence checking. NOT for writing papers from scratch — for polishing existing drafts.

## Features

- **Story-driven coherence**: Ensures the paper tells one coherent story — system purpose, design logic, and value are clear throughout
- **Multi-agent review**: 6 specialized agents with diverse reviewer personas (senior expert / adjacent-field researcher / busy PC member)
- **Iterative polishing**: Section-by-section → full-paper coherence → targeted iteration
- **Content compression**: Surgical compression to meet page limits
- **Citation safety**: Never generates citations from memory — provides search links for user verification
- **Conference compliance**: Checks formatting, anonymization, page limits against venue requirements

## Commands

| Command | Description |
|---------|-------------|
| `polish` | Full pipeline: polish → compress → check-citations → check-submission |
| `polish-section` | Polish a specific section |
| `polish-paper` | Iterative full-paper polishing |
| `compress` | Compress content to meet page limits |
| `check-citations` | Verify citations, generate verification checklist |
| `check-submission` | Final compliance check against conference requirements |

## Installation

### Claude Code CLI

```bash
claude install-skill /path/to/systems-paper-polisher
```

Or add to your project's `.claude/settings.json`:

```json
{
  "skills": [
    "/path/to/systems-paper-polisher/systems-paper-polisher"
  ]
}
```

### Manual

Copy or symlink the `systems-paper-polisher/` subdirectory (the one containing `SKILL.md`) into your Claude Code skills directory.

## Usage

In Claude Code, simply describe what you want:

```
> polish my paper for OSDI
> polish section 3.2
> compress to 12 pages
> check citations
> check submission for ASPLOS
```

## Agent Team

| Agent | Role |
|-------|------|
| **Story Coherence** | Checks narrative coherence — does the paper tell one unified story? |
| **Style Checker** | Writing clarity, Gopen & Swan principles, terminology consistency (including figure-text alignment) |
| **Reviewer** | 3 personas: senior domain expert, adjacent-field researcher, busy PC member |
| **Experiment Checker** | Claim-evidence alignment, evaluation completeness, citation sufficiency |
| **Improvement** | Synthesizes all feedback, produces revised text (the only agent that writes) |
| **Compressor** | Content compression with prioritized cut suggestions |

## Included Templates

- **USENIX** (OSDI, ATC, NSDI): `usenix2019_v3.sty` + starter `paper.tex`
- **ACM** (SOSP, ASPLOS, EuroSys): `acmart.cls` + sample files
- **fillin.sty**: Placeholder tracking system for missing values and citations

## References

The `references/` directory contains writing guidance adapted for systems papers:

- `story-coherence-guide.md` — How to maintain narrative coherence
- `systems-writing-principles.md` — Levin & Redell, Gopen & Swan, systems-specific conventions
- `section-guides.md` — Per-section writing patterns (abstract, intro, design, eval, etc.)
- `review-checklist.md` — Rejection risk assessment and self-review
- `conference-requirements.md` — Venue-specific submission requirements
- `best-paper-styles.md` — Writing patterns from recent best paper award winners

## Acknowledgments

This skill synthesizes ideas from:
- [systems-paper-writing](https://github.com/) — Systems-specific writing principles and templates
- [Research-Paper-Writing-Skills](https://github.com/) — Section-by-section academic writing guidance
- [academic-research-skills](https://github.com/) — Multi-agent review architecture

## License

MIT
