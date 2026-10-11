# Quality Checklist

Use this list before publishing. Check the example and code first, then edit the
prose for clarity.

---

## 1. Narrative

- [ ] The opening places the reader in a concrete setting within two paragraphs, and
      the setting has a problem the concept solves.
- [ ] The running example has a name, and its people have names.
- [ ] If the dataset is invented, its imperfections are declared on purpose and
      later sections use them rather than avoiding them.
- [ ] Each section opens from the situation's point of view ("The co-op needs a
      mailing list..."), not from the keyword's ("UPPER() is used to...").
- [ ] The article ends with a challenge for the reader, not a summary of itself.
- [ ] If this article continues a series, it links to the earlier data in the setup
      section and shows only what is new.

## 2. Code

- [ ] Every block is complete and runnable as shown.
- [ ] Every block is followed by its output, such as a result grid, terminal text, or
      status line. Do not describe output in prose instead.
- [ ] Engine or version differences are flagged in parentheses where the
      affected code appears, not collected into a compatibility table.
- [ ] If a common mistake helps explain a pattern, show the mistake and its result.
- [ ] No snippet is longer than roughly a screen.
- [ ] Comments explain why, not what.
- [ ] A "You want... / Use" decision table appears near the end if the article covers
      a family of tools.

## 3. Voice

- [ ] The article speaks in "we" and "you" throughout; no "the user" scaffolding.
- [ ] Opinions appear as working habits with reasons ("I keep the WHERE clause on
      every update so the row count means something"), not as declarations.
- [ ] Local details, such as currency, place names, or everyday transactions, come
      from a context the writer knows. Readers should understand the concept without
      sharing that context.
- [ ] Where project experience is used, failures are stated plainly and in
      public, without hedging.
- [ ] Findings that rest on a confound say so in place ("The dashboard shows the
      pattern. It does not claim a cause.").

## 4. Clarity (the Orwell pass)

Apply George Orwell's rules to the prose, one paragraph at a time:

- [ ] No dying metaphors or stock figures of speech carried over from other writing.
- [ ] Short words win where a short word is available ("use" beats "utilize").
- [ ] Words that can be cut are cut. Read each sentence and try deleting its last
      clause; if the sentence survives, delete it.
- [ ] Use active voice unless the actor does not matter.
- [ ] Jargon gets an everyday equivalent on first use: "common table expression, a
      name declared once that the rest of the query can refer to."
- [ ] Keep code and exact technical terms precise. Do not trade precision for polish.

## 5. Prompts and endings

- [ ] Mnemonics and acrostics appear only where order truly must be memorized, and
      nowhere else.
- [ ] The final line addresses the reader or the real world, never the article.
- [ ] Where reader feedback matters (queries you might have gotten wrong), the
      article says so in the comments invitation.

## 6. Metadata

- [ ] Concept tutorial titles follow the shape "**Concept**: *setting*". Project
      article titles use a verb-led form, such as "Cleaning and Analyzing..." or
      "Building the... Dashboard..."
- [ ] A small set of tags, one of which names the exact topic, one the technology,
      one the article type (tutorial / analysis / project), one the series stage.
- [ ] Engine and version stated in the first code section.
- [ ] Repository link stated once, early, in a "Note:" line, for real-data articles.
- [ ] A fictional-data disclaimer appears once, after the first example, if the data
      is invented ("The names, codes and every number below are invented for teaching.
      They are not real [organization] procedures.").

## Patterns to avoid

- Headings named "Introduction", "Conclusion", "Background", "Overview".
- "Let's dive in!" and any greeting that promises what the next paragraph does.
- Bulleted lists of what code does, sitting next to code that already shows it.
- Emphasis via ALL CAPS in prose (ALL CAPS in code is fine, e.g. in string literals).
- Emoji in body text.
- Do not apologize for a messy dataset or a small example. State those facts.
- A concluding paragraph that retells the article's sections in order.
- Remove sentences that would fit any example. Write about the specific shop, studio,
  or workshop rather than an unnamed company.
