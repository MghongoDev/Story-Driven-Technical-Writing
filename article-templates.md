# Article Templates

Fill-in skeletons for the four article shapes in this style. Copy one, replace the
bracketed placeholders, and draft the body. Each template lists the sections in
order, with a note on each section's job and typical length.

Per the source series this reference came from, the templates are data-domain-shaped —
SQL, PostgreSQL, Power BI, DAX, and CSV-cleaning pipelines are the native examples.
If you write for a different technical domain, keep the section rhythm and generalize
the tool names; do not drop the domain specifics in favor of abstraction. A
cleaning-pipeline article in another field still has a Stage 1 and a Step 5; only the
vocabulary moves.

---

## Template A: Concept tutorial (the SQL/language explainer)

Use for: teaching one family of tools (joins, window functions, subqueries, loops,
NULL handling, operators). This is the default shape.

```markdown
# [Concept]: [A vivid subtitle that names the setting]

[Hook, 1–2 paragraphs, no heading.]
[Describe the place and the people: a studio on paper, a co-op, a record shop, a
conductor, a ranger. State the problem the place has. End on the sentence that names
the concept as the answer, e.g. "That is what a JOIN is."]

[Short orientation block, untitled or one sentence:]
["We'll use [named fictional business] as the running example. Every query below
shows the output you'd see in [tool]."]

## The setup

[Minimum data or code to make the examples runnable: CREATE TABLE/INSERT or variable
definitions. If a dataset was introduced in an earlier article, link to it ("See the
tables used for this article here") and show only what is new.]

[Optional but signature: declare the data's deliberate imperfections in a short
paragraph. Name each crack in one sentence. Say why they are there ("Real databases
have rows like this."). These become the material for later sections.]

## [Concept family, first member]

[Describe the situation from the setting's point of view. Show the code. Show the
exact output. Explain in one or two sentences. If a wrong version exists, show it
and its error.]

## [Second member]...

[Repeat the section rhythm. Order from simplest to hardest. Where two members are
mirror images, cover the second by contrast with the first.]

## [The hardest one]

[The concept that needs a chain or a self-reference. Walk the reader through the
mechanism step by step, in prose, before or after the code — not instead of it.]

## A recap table (if the article covered a family)

You need to...                                  | Use
-----------------------------------------------|-----
[A situation]                                   | [Tool 1]
[A situation]                                   | [Tool 2]

## Try It Yourself

[2–5 challenges. First: change the code so it exercises a new case and predict the
output. Middle: extend it to a related problem. Last: apply the concept to a real
situation from your own week, or invite the reader to share in the comments.]
```

Notes:
- The title format "[Concept]: [setting]" is the default.
- Front matter paragraph before first heading stays 2–4 sentences.
- The engine-difference parenthesis appears the first time a family member hits it,
  in place, never collected in a table.

---

## Template B: Cleaning pipeline walkthrough (the sequential fix-it)

Use for: articles where the work genuinely happens in sequence — load, audit, fix,
constrain, load out. This is the "staging table" article shape.

```markdown
# [Project name]: Cleaning and Analyzing [data source]

[Hook: one real defect stated as a fact, the absurdity it causes, and the brief from
a named person ("The Hotel Director wants to know..."). Two paragraphs max.]

## The brief in plain words

[Numbered list of the questions the data must answer. Six to eight questions,
grouped by the stakeholder's word for them ("money, busy periods, staff, guest
happiness").]

## The plan: [short analogy for the progression]

[A flow diagram in plain text: raw file → staging (all TEXT) → fixes one defect at a
time → clean table (real types plus CHECK constraints) → view → the analyses. State
why staging is all TEXT in one sentence.]

## Step 1: [Get the data in without losing a row]

[The staging CREATE TABLE. The row count after load. The first sanity-check SELECT
plus its grid. State the convention once here: "The output under each query is what
came back, laid out the way [tool] shows it."]

## Step 2: [Audit the damage before touching anything]

[One UNION ALL query that counts every defect category and names each. Present the
grid. Say what the counts tell you ("Fourteen kinds of damage"). Distinguish a
missing value (a gap) from a wrong value (a defect).]

## Step 3: [Fix the data, one defect at a time]

[Subsections named for the damage, e.g. 3.1 Duplicate bookings, 3.2 Guest names.
Each follows the same loop:
  1. Show the defect (a SELECT with its grid).
  2. State the rule you will apply, and why, in one sentence. Name any guess
     explicitly ("That is an assumption, and I say so here so a reader can overrule
     it.") and the witness column that will confirm or kill it.
  3. Show the UPDATE (with a WHERE clause — say why).
  4. Re-run the check. It returns the proof ("All 285 agree, so both guessed rules
     survived the test.").]

## Step 4: [Move the clean rows into a table that says no]

[The clean table with real types and CHECK constraints. Deliberately insert one bad
row and show the database refuse it. Then the view that prepares the columns the
analysis needs. State the business definitions here (what counts as revenue).]

## Step 5: [Answer the [stakeholder]'s questions]

[One subsection per brief question, Q1..Q6. Each shows the query, the grid, and a
one-sentence reading of what the numbers mean — including one line that names what a
different metric would say instead ("Volume and value are different rankings").]

## What the [stakeholder] gets

[A short paragraph that answers the brief in plain nouns and exact figures. Then the
questions the data raised but cannot answer, listed as questions for the business.]

## Pitfalls I hit, so you can skip them

[4–5 one-line lessons, each arising from something that actually happened above.]

## Try it yourself

[Load the file, predict the audit count, extend an analysis the brief didn't ask
for. End with an invitation to correct you in the comments.]
```

---

## Template C: Project write-up / data story (narrative first)

Use for: telling the story of an end-to-end analysis, when the journey (not the
syntax) is the point. Chapters, not steps.

```markdown
# [The data story title, e.g. The [Platform] Data Story]

[One-line summary above any heading: what the project turned into. Then the origin
scene: where the data lives, who asked for it, the brief quoted verbatim, and what
was at stake ("Present on Friday. The CEO will be in the room.")]

## Chapter 1: [Landing the raw data]

[What arrived, how it was staged, why the staging choices were made ("That
everything-is-text decision looks lazy, but it's the opposite.").]

## Chapter 2: [The damage inventory — make it vivid]

[Title the problems, e.g. "Twenty-Three Ways a Spreadsheet Can Lie to You."
Subsections per defect family, each with the SELECT, the output, the fix. Add one
sentence per fix explaining why that instrument rather than a plain UPDATE.]

## Chapter 3: [The view that everything else stands on]

[The presentation layer. Why it exists, what it computes once so the queries below
don't repeat it.]

## Chapter 4: [N business questions, N answers]

[Q1..QN, each with query, output, and the sentence that turns the number into a
boardroom statement ("RT001 alone accounts for roughly a quarter of all route
revenue"). Where a number has a confound, name it in the same section.]

## Chapter 5: [What the [boss] actually needs to hear]

[The findings with all SQL stripped away. One sentence per finding, imperative or
declarative ("Protect it.", "price it like one").]

## The part that doesn't show up in a query

[One to two paragraphs on the unglamorous work that made the answers possible, and
the principle it proves. End with a line that reframes the project inside its real
world — a shop counter, a boarding gate, a transport stage.]
```

---

## Template D: Dashboard / BI build article

Use for: the build-log that follows a project write-up, when the artifact is a
dashboard and the interesting decisions are about shape, labels, and DAX.

```markdown
# Building the [System] Dashboard in [tool]

[Hook: the instruction the artifact must satisfy, quoted verbatim, and the fact that
"professional" is not testable — so state YOUR three tests here (e.g. numbers tie to
the database; labels say what they mean; a busy manager gets an answer in under a
minute). Tell the reader there is a deliberate mistake to find ("I'll also set you a
puzzle. Page three contains a mistake that sits in plain sight.").]

## First: how I prepared the data for BI

[A dashboard does not clean data. Import the view, not the table. State the grain of
the model. Define the business terms (realised vs lost revenue) in a small table:
Term | Rule | Where it lives.]

## Does the dashboard agree with the database?

[One reconciliation query, its grid, and a table comparing card vs query for each
headline number. State the test passed.]

## The dashboard, page by page

[One subsection per page: which visuals, what each carries, and one honest sentence
about what a reader glancing from across a table gets.]

## The [DAX] behind each metric

[Measure code grouped by page. For each page, a table listing visual → measure, then
the code. Explain the non-obvious ones (DIVIDE's zero handling, REMOVEFILTERS,
HASONEVALUE) in one sentence each.]

## Key insights

[Numbered or bolded findings with exact figures. Each ties back to a query or
measure named above. Findings with confounds get their limits stated in place.]

## How I communicated the findings

[The choices that made it land: answer before evidence, one colour, spread beside
the average, risk stated as a question, numbers checked against SQL first. One
paragraph each.]

## What I learned from presenting

[5–7 one-line lessons, each concrete ("Define the word before showing the number.")]
## What I would do differently

[Split by priority: "Fix first:...", "Fix next:...", "Do next time:...". Include the
puzzle's answer here, with the diagnostic query that proves it.]

## What comes next

[The repair list in one sentence, then the question the data raised that the data
cannot answer, and where that answer lives.]
```

---

## Front matter and metadata

Conventions distilled from the style (these match dev.to front matter, adapt as
needed for your platform):

```yaml
title: "[Concept]: [Setting-based subtitle]"
published: true
tags: [language or tool, database/tool tag, tutorial, and either a topic tag or basics]
```

Rules:

- **Tags:** 4 per article. One primary tag naming the exact topic (e.g. `sqlnullvalues`,
  `windowfunctions`, `forloops`), one for the technology (`postgres`, `dax`, `python`),
  one `tutorial` or `dataanalysis`, one for the series stage (`basics`,
  `showdev`, `project`).
- **Series primers:** When an article builds on an earlier one, it links back in the
  setup section, not in the intro: "See the tables used for this article here."
- **Repository links:** Real-data articles state in the setup block ("Note: To access
  the files I used in this project, check out this Github repository") once, early.
- **Runnability claims:** State the engine and version in the first code section
  ("I ran every query below, in order, against the real file on PostgreSQL 16",
  "Each snippet was run on Python 3.12").
