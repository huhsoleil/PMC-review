---
name: pmc-review
description: Pre-screens a journal's website and individual manuscripts from the standpoint of PubMed Central (PMC) indexing review — checks journal policies, matches each manuscript against the applicable reporting-guideline checklist, flags internal contradictions and reference problems (including live DOI verification), estimates the likelihood of a successful PMC application, and produces a prioritized markdown report with improvement recommendations. Use when the user asks for a PMC application review, PMC indexing self-check, journal pre-application audit, or manuscript screening against PMC/reporting-guideline standards.
---

# PMC Application Pre-Review

## Purpose

Simulate, as closely as possible, how a PMC/NLM scientific-quality reviewer and a medical-librarian consultant would evaluate (1) a journal's website/policies and (2) an individual manuscript, using the National Library of Medicine's own stated criteria and an empirical analysis of real rejection letters. The goal is to surface exactly the kinds of problems that have caused real journals to be rejected, before the journal submits or resubmits its PMC application.

## Reference materials (`references/`)

Read the relevant reference file(s) before writing any part of the report — do not rely on general knowledge of these guidelines from training, since the exact wording and item numbering in these files is what the report must cite.

| File | Purpose |
| --- | --- |
| `references/application_guideline.md` | Official NLM/PMC scope and scientific-quality review criteria (verbatim) |
| `references/common.md` | Common rejection reasons, grouped into: (1) Policy, (2) Lack of scientific quality, (3) Editing and publishing |
| `references/synthesis.md` | Frequency analysis of rejection reasons across 10 real journals, plus Checklists A (submission stage), B (peer-review stage), C (editorial stage), and D (journal-level, annual) |
| `references/ARRIVE_Guidelines_Checklist.md` | Animal research (in vivo experiments) |
| `references/CARE_Guidelines_Checklist.md` | Case reports |
| `references/CONSORT-checklist.md` | Randomized controlled trials |
| `references/COREQ_32_Item_Checklist.md` | Qualitative research |
| `references/PRISMA-checklist.md` | Systematic reviews / meta-analyses |
| `references/STARD-checklist.md` | Diagnostic accuracy studies |
| `references/TREND_Statement_Checklist.md` | Non-randomized behavioral/public-health interventions |
| `references/minimal_checklist_other_designs.md` | Minimum checklist for manuscripts matching none of the seven designs above (narrative reviews, data descriptors, protocols) plus common minimum items |

## Inputs

Ask for whatever of the following the user has not already supplied:

1. The journal's website URL (optional but recommended — enables the journal-level check in Part A).
2. One or more manuscript files (required for Part B). Accept the formats the user provides (docx, pdf, markdown, etc.) and read them fully rather than sampling.

If only a manuscript is provided, skip Part A and note in the report that the journal-level check was not performed. If only a website is provided, skip Part B accordingly.

## Procedure

### Part A — Journal website review (journal level)

Using Checklist D from `synthesis.md` and the "Journal policies" considerations in `application_guideline.md`, review the journal's website and check:

- Are aims and scope, the peer-review process, conflict-of-interest policy, and research-ethics policy explicitly published and current?
- Does the editorial board listing give full names, institutional affiliations, and areas of expertise? Is there real diversity across editors and authors?
- Is there a stated policy for handling manuscripts authored by editors/board members (independent handling editor, disclosure)? Is the proportion of board-authored articles reasonable?
- Does the mix of article types (original research vs. reviews, case reports, etc.) match the journal's stated aims?
- Is the publication schedule met, and is the volume sufficient to demonstrate sustainability?
- Are article-processing charges (APCs), if any, disclosed?
- Does the "Instructions for Authors" page reference ICMJE Recommendations and the COPE/DOAJ/WAME/OASPA Principles of Transparency and Best Practice in Scholarly Publishing?
- Are there mechanical defects on the site itself (broken links, missing pages, outdated information)?

### Part B — Manuscript review (article level)

For each manuscript, work through these eight steps in order:

1. **Identify the study design.** Determine whether the manuscript is a randomized controlled trial, systematic review/meta-analysis, case report, qualitative study, diagnostic accuracy study, animal study, or non-randomized behavioral/public-health intervention, and select the matching checklist from the table above. A manuscript can match more than one (e.g., a systematic review of diagnostic accuracy studies may draw on both PRISMA and STARD). If none of the seven applies, use `references/minimal_checklist_other_designs.md`, selecting the sub-section (narrative review / data descriptor / protocol) that fits, plus its common minimum items.
2. **Check every item of the selected checklist(s)** against the manuscript, noting for each item whether it is reported, partially reported, or missing, with a pointer to where it should appear (section/paragraph) if missing.
3. **Cross-check against PMC's known rejection patterns**, applying every item in `common.md`'s three categories and in `synthesis.md` Checklists A, B, and C. Prioritize the two most frequent failure categories from the synthesis (methods insufficient for reproducibility; weak/unjustified study design), since these appeared in 8 of 9 analyzed rejections.
4. **Check internal consistency.** Compare statements across sections for contradictions: e.g., "prospective" in the text vs. "retrospective" in the ethics-approval statement; mismatched sample sizes, dates, or numeric values between the abstract, body text, and tables; conclusions that go beyond what the stated aim and results support. Use `synthesis.md` section 2.6 as the model for this kind of check.
5. **Check citation-to-claim fit.** For each substantive claim in the manuscript, confirm a citation is present, that the cited source actually supports the claim, that the reference list is not overly dependent on theses/grey literature, and that a sufficient share of citations are recent peer-reviewed sources (Checklist A7–A9, B9).
6. **Check reference formatting and verify DOIs live.** First check bibliographic formatting mechanically (author names, year, journal name, volume/issue, pages, consistent style). Then, for each reference that has (or should have) a DOI, query the Crossref REST API (`https://api.crossref.org/works/{doi}`) or resolve the DOI to confirm: (a) the DOI actually resolves/exists, and (b) the metadata returned (authors, year, title, journal) matches what is cited in the manuscript's reference list. Flag any DOI that does not resolve, or whose metadata disagrees with the manuscript's citation, as a reference error. If no network access is available in the working environment, perform the formatting check only and state explicitly in the report that live DOI verification could not be performed due to network restrictions — do not silently skip this step.
7. **Check tables and figures** for duplication of data already stated in the text, missing or uninformative legends/annotations, and any table/figure cited in the text that does not actually show the data being referenced (Checklist C2–C4).
8. **Check editorial quality**: grammar, typos, logical flow, and abbreviations that are defined but used only once (`common.md`, "Editing and Publishing").

## Output: the report

Always save the finished report as a markdown (`.md`) file (never chat text alone), and give the user a short summary in the conversation. Match the manuscript's own language for direct quotes, but write the report itself in formal academic English unless the user has asked for another language. Use tables liberally; keep prose in sentence case.

Structure the report as follows:

1. **Executive summary — prioritized issues.** List the 3–5 most consequential problems first, ordered by how often that category of problem appears in the `synthesis.md` frequency table (i.e., problems in the top-ranked categories — reproducibility of methods, justification of study design — come first if present).
2. **Estimated likelihood of a successful PMC application.** Using the frequency table in `synthesis.md` as a baseline (e.g., methods reproducibility failed in 8/9 rejected journals; weak study-design justification in 8/9; editorial/language quality in 7/9), compare how many of these high-frequency failure categories this journal/manuscript currently exhibits, and express the result as a qualitative band — "low (roughly <20%)", "moderate (roughly 20–50%)", or "high (roughly >50%)" — never a precise statistical probability. Explicitly state that this is a qualitative estimate based on similarity to known rejected cases, not a validated statistical prediction, and list exactly which findings drove the estimate.
3. **Part A results** (journal-level), if performed.
4. **Part B results** (manuscript-level), with subsections B-1 through B-8 mirroring the eight steps above, each as a findings table (item / status / evidence or location / recommendation).
5. **Improvement recommendations**, split into two tiers:
   - *Manuscript-level*: changes the authors/editors can make to this specific manuscript, separated into quick fixes (wording, formatting, citation fixes) and structural fixes (study design justification, reproducibility of methods).
   - *Journal-level*: policy and process changes the journal itself should adopt, drawn from `synthesis.md` section 3 (editorial policy and governance, strengthening peer review, pre-acceptance editorial gate) — e.g., adopting a structured review form, mandating reporting-guideline checklists at submission, setting a ceiling on board-authored content, adding a mechanical reference/DOI verification step before acceptance.
6. **Checklists and sources used** — list which guideline checklist(s) were applied and cite the specific reference file and section/item numbers relied on throughout the report, so every finding is traceable back to `references/`.

## Notes

- Treat every finding as traceable: cite the specific checklist item number or the section of `application_guideline.md` / `synthesis.md` / `common.md` that supports it, rather than general impressions.
- When evidence is ambiguous (e.g., a checklist item might be addressed in a supplementary file not provided), say so explicitly rather than guessing, and ask the user for the missing material if it materially affects the assessment.
- Do not soften the likelihood estimate or the rejection-risk findings; the value of this skill is in surfacing exactly the problems that have caused real rejections.
