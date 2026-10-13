---
name: tech-article-writer
description: Researches and writes technical articles on any tech topic (software development, AI/ML, cloud, DevOps, security, data, tooling, web, mobile) for publication on dev.to. Use this skill whenever the user asks for a technical article, blog post, tutorial, how-to, explainer, deep dive, comparison, "what I learned" write-up, or dev.to post about a technology, library, framework, language, tool, architecture, or engineering concept, even if they only say "write something about X" or "turn these notes/code into a post". Always verifies facts, versions, and APIs with web search before writing, and produces a publish-ready Markdown file with dev.to front matter.
---

# Tech Article Writer

Write technical articles that a developer would actually finish reading, learn something from, and trust. The audience is dev.to: practitioners from beginner to senior who skim first, then read what earns their attention. They are skeptical of fluff and quick to spot wrong code or outdated advice.

Two things separate a good technical article from a mediocre one: **accuracy** (the code runs, the versions are current, the claims are true) and **a clear reason to exist** (one specific thing the reader will be able to do or understand afterwards). Everything below serves those two.

## Workflow

### 1. Pin down the brief

Before researching, settle these. Infer what you can from the request; ask only about what's genuinely unclear, and ask once, briefly.

- **Topic and angle**: What is the one-sentence promise of the article? ("After reading this, you can X" or "You'll understand why Y.") A topic ("Docker") is not an angle ("Cut your Docker build times in half with layer caching").
- **Reader**: Beginner, intermediate, or experienced? What do they already know? Default to intermediate if unspecified.
- **Type**: Tutorial, explainer, deep dive, comparison, opinion, or lessons learned. See `references/article-types.md` for the shape each one takes.
- **Length**: Default to 800-1,500 words for explainers and opinion pieces, 1,200-2,500 for tutorials and deep dives. Respect any length the user gives.
- **Source material**: If the user provides code, notes, a repo, or a draft, that is the primary source. Build the article around it rather than replacing it.

### 2. Research and verify (always)

Technical content rots fast, and confident wrong answers are the worst failure mode here. Use web search before writing, even for topics you know well, and verify:

- **Current versions** of every library, framework, language, and tool mentioned, and the date they were released. Don't write "latest" without checking what that is today.
- **API signatures, flags, and config syntax** against official documentation. Prefer official docs, release notes, changelogs, and maintainers' posts over third-party blogs.
- **Deprecations and breaking changes** that affect the advice. A tutorial built on a removed API is useless.
- **Claims with numbers** (benchmarks, adoption stats, pricing, limits). Find the source. If you can't, soften the claim or cut it.
- **Install and setup steps**, since these break most often.

Keep a short list of the sources you relied on. Link the important ones in the article (official docs, the repo, the release notes), because readers trust articles that show their work.

If search returns conflicting information, say so in the article or pick the authoritative source and note the discrepancy. If something can't be verified, don't present it as fact.

### 3. Outline before drafting

Write a brief outline (headings plus one line each) and check it against the one-sentence promise. Every section should either set up, deliver, or reinforce the promise. Cut sections that are interesting but off-promise; they can become a second article.

For a long or ambitious piece, show the user the outline and get a nod before drafting. For a short, clearly specified one, go straight to the draft.

### 4. Write the draft

**Open with a hook, not a preamble.** The first two or three sentences decide whether the reader stays. Start with the problem, a surprising result, a concrete scenario, or a bold-but-true claim. Skip "In today's fast-paced world of technology..." and "In this article we will explore...". State what the reader will get within the first paragraph.

**Structure for skimmers.** Use `##` and `###` headings that say something ("Why your cache never gets hit") instead of labels ("Overview", "Conclusion"). A reader who only reads headings should still follow the argument. Keep paragraphs to 2-4 sentences. Use lists for genuinely list-like content, tables for comparisons.

**Make code trustworthy.**
- Every code block specifies its language for syntax highlighting.
- Code must be complete enough to run and correct for the versions you verified. State the versions near the top ("Tested with Node 22 and Express 5").
- Show the output or result when it helps the reader confirm they're on track.
- Keep snippets focused. Trim boilerplate, and when you elide code, say so with a comment rather than silently skipping.
- Explain the non-obvious lines, not the obvious ones.
- If you couldn't run the code yourself, say less about guarantees and keep it close to documented examples. When a sandbox is available, run the code to check it.

**Explain, don't just instruct.** Readers retain the "why". After each key step, say what it does and what would go wrong without it. Use one good analogy per hard concept, drawn from something the reader already knows, and make sure the analogy doesn't mislead on the details that matter.

**Be honest about trade-offs.** Say when not to use the thing. Mention costs, limitations, and alternatives. This is what makes an article credible rather than promotional.

**Voice.** Write like a knowledgeable colleague explaining something over coffee: direct, concrete, a little personality, no hype. Use "you" and "we" naturally. Prefer plain words over jargon, and define a term the first time it appears if the audience may not know it. Avoid stacked superlatives ("revolutionary", "game-changing", "seamless") and filler transitions.

**Close with value.** End with a short recap of what the reader can now do, then a specific next step: a challenge to try, a link to the docs for going deeper, a related topic, or a question inviting discussion in the comments. Avoid a generic "I hope you enjoyed this article".

### 5. Review before delivering

Run this checklist and fix problems rather than reporting them:

- [ ] The opening states the promise, and the article delivers it.
- [ ] Every version number, command, flag, and API call matches what you verified.
- [ ] Code blocks have language tags and are consistent with each other (same variable names, same file structure).
- [ ] No unverifiable claims or invented statistics. Quotes from sources are brief and attributed.
- [ ] Headings are informative and the structure survives skimming.
- [ ] Trade-offs and limitations are mentioned.
- [ ] No filler openings, empty superlatives, or repetitive "In conclusion" padding.
- [ ] Sources are linked where a reader would want to check them.

If the `avoid-ai-writing` skill is available, run a pass with it on the prose (not the code) to remove stock AI phrasing before delivering.

## Output format

Deliver the article as a Markdown file in `/mnt/user-data/outputs/`, named with a short kebab-case slug (e.g. `docker-layer-caching.md`), and present it with `present_files`. Keep the closing message to a sentence or two: what the article is, plus any caveat the user needs to know (for example, a claim you couldn't fully verify). Don't re-summarize the article in chat.

Start the file with dev.to front matter:

```markdown
---
title: A Specific, Searchable Title (Ideally Under 70 Characters)
published: false
description: One or two sentences that work as the social-card preview.
tags: tag1, tag2, tag3, tag4
cover_image:
---
```

Front matter rules:
- `published: false` so the user reviews before going live.
- **Up to four tags**, lowercase, no spaces or hyphens inside a tag (dev.to's requirement), chosen from tags that actually exist on dev.to for the topic (e.g. `webdev`, `javascript`, `python`, `devops`, `ai`, `security`, `beginners`, `tutorial`). Add `beginners` only if the article truly is beginner-friendly.
- Leave `cover_image` blank unless the user supplies one.
- Titles that promise a concrete outcome or number outperform vague ones ("How I..." and "N ways to..." work when they're true). Never write clickbait the article can't back up.

dev.to-specific Markdown worth using when it helps: fenced code blocks with language tags, `{% embed URL %}` liquid tags for GitHub repos, CodePen, or YouTube, and tables for comparisons. Avoid raw HTML and elaborate formatting that renders inconsistently.

## Edge cases

- **Controversial or opinion topics** ("Is X dead?"): argue a clear position, acknowledge the strongest counterargument fairly, and back claims with evidence rather than vibes.
- **Fast-moving topics** (new AI models, just-released frameworks): verify release dates and capabilities against primary sources, and state "as of [month year]" so readers know the freshness.
- **Security topics**: explain concepts, defenses, and detection. Don't provide working exploit code or step-by-step attack instructions against real systems; use conceptual examples and defensive guidance.
- **User supplies a draft to improve**: preserve their voice and structure, fix inaccuracies, tighten, and flag what you changed instead of rewriting wholesale.
- **Topic too broad** ("write about AI"): narrow it to a specific angle yourself, tell the user which angle you chose and why, and offer alternatives.
- **Series or follow-ups**: if the topic naturally splits into parts, propose the split and write part one rather than producing a bloated single article.
