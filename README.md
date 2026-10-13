# Story-driven technical writing reference

Use this reference to write technical articles around practical examples. Explain a concept with runnable code and show output readers can check.

The guides cover example choice, article structure, code, output, voice, sentence style, and reader feedback. Adapt them to your subject and audience.

## The documents

Read this file first, then use each file for the task it fits:

| Document | Use it to |
|---|---|
| [style-reference.md](style-reference.md) | Look up guidance on examples, structure, code, voice, and sentence style. |
| [article-templates.md](article-templates.md) | Start a concept tutorial, data-cleaning guide, project write-up, or dashboard article. |
| [quality-checklist.md](quality-checklist.md) | Review an article before publishing. |
| [analysis/analysis-notes.md](analysis/analysis-notes.md) | See how the patterns appear in the 13 source articles. |
| [analysis/source-articles.md](analysis/source-articles.md) | Open the source articles. |
| [skills-guide.md](skills-guide.md) | Use the three installed agent skills to draft, correct, and publish a technical article. |

## Write a new article

1. Choose the article shape in [article-templates.md](article-templates.md): concept tutorial, cleaning pipeline walkthrough, project write-up, or dashboard build.
2. Fill the skeleton. The template lists the sections in order and says what each one holds.
3. Draft the body against [style-reference.md](style-reference.md).

## Review a draft

Run the draft through [quality-checklist.md](quality-checklist.md). It checks the narrative first, then the code, then voice and metadata. The last prose section is the Orwell pass, the same correction step the skills guide runs on your draft.

## Look up a pattern

Bring the question you have, such as "how long should the hook be?" or "how do I introduce a running example?", to [style-reference.md](style-reference.md). If you want to see a pattern at work rather than read about it, the analysis notes point each guideline to its examples in the source series.

## The core idea

Start with an everyday situation that needs the concept, such as a shop, office, or workshop. Use runnable code to address the problem and show output readers can check. Explain how the code works.

## Patterns, not rules

This guide offers patterns, not rules. Use them to support your judgment, not replace it. When a template and a good idea conflict, follow the idea and note why.

## Writing with the skills

Three agent skills are installed with this reference: `tech-article-writer` drafts the article, and `apply-orwell`, followed by `avoid-ai-writing`, corrects the prose. [skills-guide.md](skills-guide.md) shows how to run the three of them on your own article, from the first draft to the publish check.

## Notes for contributors

Send corrections or add a note to `analysis/analysis-notes.md` when you make a choice this reference does not cover.

## Credit

This reference draws on [David Mwandairo's public series](https://dev.to/david_mwandairo) of 13 articles about SQL, data analysis, Power BI, and Python. The `analysis/` appendix links each guideline to examples from the series.
