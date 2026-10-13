# Skills guide

Three agent skills are installed here, and together they cover the work of writing a technical article: `tech-article-writer` drafts it, `apply-orwell` tightens the prose, and `avoid-ai-writing` catches the patterns that make text sound machine-written. This guide shows how to run them in order on your own article.

## Where the skills live

The skills are installed in `.agents/skills/`, the layout agent tools load by name:

| Skill | File |
|---|---|
| apply-orwell | `.agents/skills/apply-orwell/SKILL.md` |
| avoid-ai-writing | `.agents/skills/avoid-ai-writing/SKILL.md` |
| tech-article-writer | `.agents/skills/tech-article-writer/SKILL.md` (with `references/article-types.md`) |

The packaged archives stay in `skills/*.skill` as the source copies. Reinstall by unzipping them again:

```bash
mkdir -p .agents/skills && for f in skills/*.skill; do unzip -o "$f" -d .agents/skills/; done
```

## What each skill does in an article

| Skill | Role in the article |
|---|---|
| tech-article-writer | Runs the whole drafting workflow: pin down the topic and angle, research and verify every claim with web search, pick an article type from `references/article-types.md`, and produce a publish-ready Markdown file with dev.to front matter. |
| apply-orwell | The first correction pass. Reads the draft paragraph by paragraph against Orwell's six rules: cut stale figures of speech, use the short word, cut the survivable word, prefer the active voice, use the everyday word over the jargon word. Code and exact technical terms are exempt. |
| avoid-ai-writing | The second correction pass, which apply-orwell's standing rule calls for. Audits the draft for machine-written patterns: flagged vocabulary, em-dash splices, hedged stacks, uniform sentence length, manufactured emphasis. Rewrites the flagged spans. |

## The writing sequence

1. **Draft with tech-article-writer.** Give it the topic, the reader, the length, and any source material such as code, notes, or a repo. It settles the brief, verifies facts and versions with web search, chooses the article type, and drafts against the type's shape. The drafter can lean on this reference while it works: the article shapes in [article-templates.md](article-templates.md) match `references/article-types.md`, and the sentence patterns in [style-reference.md](style-reference.md) describe how a good example reads.
2. **Correct with apply-orwell.** Apply the six rules to the prose, one paragraph at a time. Cut words where the sentence survives without them, and swap long or borrowed words for short, plain ones. Leave code, quoted text, and exact technical terms alone.
3. **Audit with avoid-ai-writing.** Ask for a rewrite pass over the draft. Fix the flagged words and constructions, and vary the sentence and paragraph length the pass reports. Run a second pass only if you asked for one; one rewrite and one corrective pass usually clear the flags.
4. **Check before publishing.** Run the finished article through [quality-checklist.md](quality-checklist.md). Its narrative, code, voice, and metadata sections cover what the two correction passes do not, and its section 4 is the same Orwell pass on paper.
