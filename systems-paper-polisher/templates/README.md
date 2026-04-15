# LaTeX Templates

Conference-specific LaTeX templates for systems paper submission.

```
templates/
├── USENIX/           # For OSDI, ATC, NSDI
│   ├── paper.tex     # Starter document
│   ├── paper.bib     # Sample bibliography
│   ├── usenix2019_v3.sty
│   └── usenix.sty
├── ACM/              # For SOSP, ASPLOS, EuroSys
│   ├── sample-sosp.tex
│   ├── sample-asplos.tex
│   ├── sample-sigconf.tex
│   ├── acmart.cls
│   ├── ACM-Reference-Format.bst
│   └── [supporting files]
└── utils/
    └── fillin.sty    # Placeholder tracking system
```

## Quick Start

```bash
# USENIX venues (OSDI, ATC, NSDI)
cp templates/USENIX/* your-paper-dir/

# ACM venues (SOSP, ASPLOS, EuroSys)
cp templates/ACM/* your-paper-dir/

# Always copy the placeholder utility
cp templates/utils/fillin.sty your-paper-dir/
```

## The `fillin.sty` Placeholder System

Add `\usepackage{fillin}` to your preamble to use tracked placeholders:

- `\fillin[description]` — Red marker for missing values
- `\fillcite[description]` — Blue marker for missing citations
- `\fillnum` — Quick numeric placeholder
- `\printfillinlistifany` — Before submission: shows outstanding items or "All completed!"

Remove `\usepackage{fillin}` from the final camera-ready version.
