# Quality Checklist

Run a draft through this list before publishing. The order matches a real editing
pass: read for the story first, then check the code, then cut the prose. Every item
describes what a strong story-driven article does (or avoids) — phrased so it works
for any writer and any domain.

---

## 1. Narrative

- [ ] The opening places the reader in a concrete setting within two paragraphs, and
      the setting has a problem the concept genuinely solves.
- [ ] The running example has a name, and its people have names.
- [ ] If the dataset is invented, its imperfections are declared on purpose — and
      later sections use them rather than avoiding them.
- [ ] Each section opens from the situation's point of view ("The co-op needs a
      mailing list..."), not from the keyword's ("UPPER() is used to...").
- [ ] The article ends with a challenge for the reader, not a summary of itself.
- [ ] If this article continues a series, it links to the earlier data in the setup
      section and shows only what is new.

## 2. Code

- [ ] Every block is complete and runnable as shown.
- [ ] Every block is followed by its real output — grid, terminal text, or status
      line — never a prose description of the output.
- [ ] Engine or version differences are flagged in a parenthesis at the moment the
      affected code appears, not collected into a compatibility table.
- [ ] Where a pattern has a natural wrong version, the wrong version is shown and its
      failure is shown too (error message, wrong number, or silent surprise).
- [ ] No snippet is longer than roughly a screen.
- [ ] Comments explain why, not what.
- [ ] A "You want... / Use" decision table appears near the end if the article covers
      a family of tools.

## 3. Voice

- [ ] The article speaks in "we" and "you" throughout; no "the user" scaffolding.
- [ ] Opinions appear as working habits with reasons ("I keep the WHERE clause on
      every update so the row count means something"), not as declarations.
- [ ] Local texture (currency, place names, everyday transactions) appears naturally
      from a context the writer actually knows, and the concepts still read as
      universal — never exoticized, never dependent on the reader sharing the locale.
- [ ] Where real project experience is used, failures are stated plainly and in
      public, without hedging.
- [ ] Findings that rest on a confound say so in place ("The dashboard shows the
      pattern. It does not claim a cause.").

## 4. Clarity (the Orwell pass)

Apply George Orwell's rules to the prose, one paragraph at a time:

- [ ] No dying metaphors or stock figures of speech carried over from other writing.
- [ ] Short words win where a short word is available ("use" beats "utilize").
- [ ] Words that can be cut are cut. Read each sentence and try deleting its last
      clause; if the sentence survives, delete it.
- [ ] Passive constructions are converted to active unless the actor genuinely
      doesn't matter.
- [ ] Jargon gets an everyday equivalent on first use: "common table expression, a
      name declared once that the rest of the query can refer to."
- [ ] Code and exact technical terms are exempt — never trade precision for polish.

## 5. Prompts and endings

- [ ] Mnemonics and acrostics appear only where order truly must be memorized, and
      nowhere else.
- [ ] The final line addresses the reader or the real world, never the article.
- [ ] Where reader feedback matters (queries you might have gotten wrong), the
      article says so in the comments invitation.

## 6. Metadata

- [ ] Title follows the shape "**Concept**: *setting*" for concept tutorials — or a
      verb-led form ("Cleaning and Analyzing...", "Building the... Dashboard...") for
      project articles.
- [ ] A small set of tags, one of which names the exact topic, one the technology,
      one the article type (tutorial / analysis / project), one the series stage.
- [ ] Engine and version stated in the first code section.
- [ ] Repository link stated once, early, in a "Note:" line, for real-data articles.
- [ ] A fictional-data disclaimer appears once, after the first example, if the data
      is invented ("The names, codes and every number below are invented for teaching.
      They are not real [organization] procedures.").

## Anti-patterns (delete these from a draft on sight)

- Headings named "Introduction", "Conclusion", "Background", "Overview".
- "Let's dive in!" and any greeting that promises what the next paragraph does.
- Bulleted lists of what code does, sitting next to code that already shows it.
- Emphasis via ALL CAPS in prose (ALL CAPS in code is fine, e.g. in string literals).
- Emoji in body text.
- Apologies for the dataset being messy or the example being small — declare them
  instead.
- A concluding paragraph that retells the article's sections in order.
- Any sentence that would survive unchanged if the running example were swapped for
  a different one. Specificity is the test: the article should be *about* its shop,
  its studio, its workshop — not about "a company".
