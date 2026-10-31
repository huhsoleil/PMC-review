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
pmc-review/
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

- **Claude Code**: copy the `pmc-review` folder to `~/.claude/skills/` (personal) or `.claude/skills/` (project).
- **Claude.ai**: zip the `pmc-review` folder and upload it under Settings → Capabilities → Skills.

## Usage

Ask, for example: "Review this journal's website and these three manuscripts for a PMC application," and supply the journal URL and manuscript files.

## Disclaimer

The likelihood estimate is a qualitative judgment based on similarity to known rejected cases, not a validated statistical prediction. The final decision rests with NLM.

## Author

Sun Huh, Hallym University College of Medicine
