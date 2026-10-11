# Story-Driven Technical Writing Reference

A reusable reference for writing technical articles that teach a concept by putting the
reader inside a concrete situation the concept naturally belongs in, then working
through that situation with runnable code and its real output.

It documents how a strong article in this style is built: the narrative frame, the
structure, the treatment of code and output, the voice, the sentence craft, and the
feedback habits that make the writing trustworthy. It is written generically — the
patterns stand on their own and are meant to be picked up by anyone writing technical
content, in any domain.

Read this file first, then use the guides according to what you are doing:

| Document | What it covers |
|---|---|
| [style-reference.md](style-reference.md) | The complete pattern library: narrative framing, article structure, code style, voice, sentence patterns, and the feedback loop. This is the core reference. |
| [article-templates.md](article-templates.md) | Fill-in skeletons for four article shapes (concept tutorial, cleaning/data pipeline, project write-up, dashboard/BI build), plus front-matter and metadata conventions. |
| [quality-checklist.md](quality-checklist.md) | A pre-publish checklist in the order of a real editing pass: narrative, code, clarity, takeaway, and metadata checks. |
| [analysis/analysis-notes.md](analysis/analysis-notes.md) | *(Appendix)* Per-article notes recording how one published 13-article series uses these patterns, plus the cross-article synthesis that produced this reference. |
| [analysis/source-articles.md](analysis/source-articles.md) | *(Appendix)* The 13 source articles of that series, for verification and further study. |

## The core idea in three sentences

A technical concept is introduced by placing it inside a concrete, everyday situation
that the concept belongs in such as a shop, an office, a workshop, a queue. The article then
explains the concept by working through that situation with code that produces output
the reader can check. The situation does the motivating; the output does the proving;
the prose does the explaining in between.

## How to use this reference

1. **Write a new article.** Pick the article shape from
   [article-templates.md](article-templates.md), fill the skeleton, and draft the body.
2. **Check a draft.** Run it through [quality-checklist.md](quality-checklist.md).
3. **Consult the patterns.** Look up a specific question ("how long should the hook
   be?", "how do I introduce a running example?") in
   [style-reference.md](style-reference.md).

Nothing here is license. These are patterns that consistently produce readable,
trustworthy technical writing, not patterns that could replace judgment. When a
template and a good idea conflict, follow the idea and note why it was different.

## Notes for contributors

Corrections welcome. If you write an article using this reference and make choices it
does not cover, add a note to `analysis/analysis-notes.md` under the appropriate
section so the record grows with your work.

---

## Credit

Patterns distilled from [David Mwandairo's public series](https://dev.to/david_mwandairo)
of 13 technical articles on SQL, data analysis, Power BI, and Python. The appendix in
`analysis/` records the per-article evidence behind every claim in this reference.
