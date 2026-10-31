# PMC-review

An Agent Skill that pre-screens a journal's website and individual manuscripts from the standpoint of PubMed Central (PMC) indexing review.

## What it does

- Checks journal-level policies against the National Library of Medicine (NLM) PMC scope and scientific-quality criteria
- Identifies each manuscript's study design and applies the matching reporting-guideline checklist (ARRIVE, CARE, CONSORT, COREQ, PRISMA, STARD, TREND, or a minimal checklist for other designs)
- Cross-checks findings against rejection patterns derived from real PMC decision letters to 10 journals
- Flags internal contradictions, reference problems (including live DOI verification), and editorial-quality issues
- Gives a qualitative estimate of the likelihood of a successful PMC application
- Produces a prioritized markdown report with manuscript-level and journal-level recommendations

## Structure

```
skills/pmc-review/
├── SKILL.md
└── references/
    ├── application_guideline.md          # NLM/PMC review criteria
    ├── common.md                         # Common rejection reasons
    ├── synthesis.md                      # Frequency analysis + Checklists A–D
    ├── ARRIVE_Guidelines_Checklist.md
    ├── CARE_Guidelines_Checklist.md
    ├── CONSORT-checklist.md
    ├── COREQ_32_Item_Checklist.md
    ├── PRISMA-checklist.md
    ├── STARD-checklist.md
    ├── TREND_Statement_Checklist.md
    └── minimal_checklist_other_designs.md
```

## Installation

- **Any agent (via [skills.sh](https://skills.sh))**:

  ```bash
  npx skills add huhsoleil/PMC-review
  ```

- **Claude Code (manual)**: copy the `skills/pmc-review` folder to `~/.claude/skills/` (personal) or `.claude/skills/` (project).
- **Claude.ai**: zip the `skills/pmc-review` folder and upload it under Settings → Capabilities → Skills.

## Usage

Ask, for example: "Review this journal's website and these three manuscripts for a PMC application," and supply the journal URL and manuscript files.

## Disclaimer

The likelihood estimate is a qualitative judgment based on similarity to known rejected cases, not a validated statistical prediction. The final decision rests with NLM.

## License

This work is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). See [LICENSE](LICENSE).

The reporting-guideline checklists in `skills/pmc-review/references/` (ARRIVE, CARE, CONSORT, COREQ, PRISMA, STARD, TREND) are adapted from their original publications and remain subject to the terms set by their respective authors and publishers. Please cite the original guideline when using them.

## Citation

Huh S. PMC-review: an Agent Skill for pre-screening journals and manuscripts for PubMed Central indexing [software]. 2026. Available from: https://github.com/huhsoleil/PMC-review

## Author

Sun Huh, Hallym University College of Medicine
