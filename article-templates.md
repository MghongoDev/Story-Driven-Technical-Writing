# Article Templates

Choose a template, replace its placeholders, and draft the article. Each skeleton
lists sections in order and describes what to include.

The source series focuses on data work: SQL, PostgreSQL, Power BI, DAX, and
CSV-cleaning pipelines. For another domain, keep the structure and use that field's
terms and examples.

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

[Optional: list deliberate data problems and explain why the examples include them.
Use the same problems in later sections.]

## [Concept family, first member]

[Describe the situation from the setting's point of view. Show the code. Show the
exact output. Explain in one or two sentences. If a wrong version exists, show it
and its error.]

## [Second member]...

[Repeat the section rhythm. Order from simplest to hardest. Where two members are
mirror images, cover the second by contrast with the first.]

## [The hardest one]

[For a concept that uses a chain or self-reference, explain the mechanism in prose
before or after the code, as well as showing it in code.]

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

Use for articles where the work happens in sequence: load, audit, fix,
constrain, load out. This is the "staging table" article shape.

```markdown
# [Project name]: Cleaning and Analyzing [data source]

[Hook: State one data defect and its effect, then give the brief from a named person
("The Hotel Director wants to know..."). Use no more than two paragraphs.]

## The brief in plain words

[Numbered list of the questions the data must answer. Six to eight questions,
grouped by the stakeholder's word for them ("money, busy periods, staff, guest
happiness").]

## The plan

[Show the sequence in a plain-text diagram: raw file → staging (all TEXT) → fixes →
clean table (typed columns and CHECK constraints) → view → analysis. Explain why the
staging table uses TEXT.]

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
     explicitly, and identify the column you will use to test it.
  3. Show the UPDATE with a WHERE clause, and explain why it is there.
  4. Re-run the check. It returns no rows if the fix worked.]

## Step 4: [Move clean rows into a constrained table]

[Show the clean table with typed columns and CHECK constraints. Insert one invalid
row and show the database reject it. Then define the view and business terms the
analysis needs, including what counts as revenue.]

## Step 5: [Answer the [stakeholder]'s questions]

[One subsection per brief question, Q1..Q6. Each shows the query, the grid, and a
one-sentence reading of what the numbers mean. Name what a different metric would
show instead ("Volume and value are different rankings").]

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

Use when the analysis process matters more than the syntax. Organize the article in
chapters rather than steps.

```markdown
# [The data story title, e.g. The [Platform] Data Story]

[One-line summary above any heading: what the project turned into. Then the origin
scene: where the data lives, who asked for it, the brief quoted verbatim, and what
was at stake ("Present on Friday. The CEO will be in the room.")]

## Chapter 1: [Landing the raw data]

[What arrived, how it was staged, why the staging choices were made ("That
everything-is-text decision looks lazy, but it's the opposite.").]

## Chapter 2: [The data problems]

[Group the problems by type. For each, show the SELECT, its output, the fix, and why
you chose that fix over a plain UPDATE.]

## Chapter 3: [The view used for analysis]

[Explain why the presentation layer exists and which values it computes for the
queries below.]

## Chapter 4: [N business questions, N answers]

[Q1..QN, each with a query, output, and a sentence explaining what the result means
for the business ("RT001 alone accounts for roughly a quarter of all route revenue").
Name any confounding factor in the same section.]

## Chapter 5: [Findings for the stakeholder]

[The findings without SQL. Use one sentence per finding, imperative or
declarative ("Protect it.", "price it like one").]

## Work behind the results

[Describe the work behind the results and what it shows. Connect the project to its
setting, such as a shop, airport, or transport service.]
```

---

## Template D: Dashboard / BI build article

Use for a dashboard article that follows a project write-up. Focus on layout, labels,
and DAX.

```markdown
# Building the [System] Dashboard in [tool]

[Hook: Quote the request the dashboard must meet. Because "professional" has no
agreed test, state three criteria, such as matching the database, clear labels, and
finding an answer in under a minute. You can also ask readers to find a specific
mistake on page three.]

## First: how I prepared the data for BI

[Prepare and clean the data in SQL, then import the view. State the grain of the
model. Define the business terms (realised vs lost revenue) in a small table:
Term | Rule | Where it lives.]

## Does the dashboard agree with the database?

[One reconciliation query, its grid, and a table comparing card vs query for each
headline number. State the test passed.]

## The dashboard, page by page

[One subsection per page: list the visuals and what each shows. State what a manager
can learn from each page.]

## The [DAX] behind each metric

[Measure code grouped by page. For each page, a table listing visual → measure, then
the code. Explain the non-obvious ones (DIVIDE's zero handling, REMOVEFILTERS,
HASONEVALUE) in one sentence each.]

## Findings and evidence

[Numbered or bolded findings with exact figures. Each ties back to a query or
measure named above. Findings with confounds get their limits stated in place.]

## How I communicated the findings

[Explain how you presented each finding and why. Describe choices such as showing the
answer before the evidence, using one colour, comparing the spread with the average,
or checking figures against SQL.]

## What I learned from presenting

[5–7 one-line lessons, each concrete ("Define the word before showing the number.")]
## What I would do differently

[Split by priority: "Fix first:...", "Fix next:...", "Do next time:...". Include the
puzzle's answer here, with the diagnostic query that proves it.]

## Repairs and unanswered questions

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
