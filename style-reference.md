# Style Reference: Writing Technical Articles

This reference explains how to write story-driven technical articles. Each section
describes a technique, shows an example, and explains when to use it. The sections
cover setting, structure, code, voice, and sentence style.

Choose a setting that fits the concept, and show code the reader can run there.

*(The examples below show each pattern in context. They are invented unless noted.)*

---

## Layer 1: The narrative frame

### 1.1 Anchor the concept in a concrete everyday setting

Open with a place the reader can picture. Choose a setting where the concept solves
an existing problem, rather than adding a setting for decoration.

Examples:

- A database-concept article → a small business drowning in paper records until
  someone asks a question the paper cannot answer.
- A joins-concept article → a co-op or team where records live in two lists that
  don't line up perfectly.
- A loops-concept article → a worker with a clipboard of dozens of identical checks.
- A conditionals-concept article → one person at a counter making a two-second
  decision from a few numbers.

Choose a setting that fits the concept. Do not add details just to make the example
quirky.

**How to do it:**

1. Name the place and the people in it (a ranger, a front desk, a keeper, a clerk).
2. State the problem the place has before naming any technology.
3. Only then introduce the concept as what handles the problem.

### 1.2 Introduce one invented, named world per article (and reuse it across articles)

Fictional businesses, teams, or workplaces get names, and their people get real-sounding
names:

- A business, team, or workplace with a plausible name for its setting, such as a
  studio room, a person in a co-op, or a shop label.

Keep the same setting across an article series. Add a character or dataset column
when a later article needs one, so readers can build on what they already know.

Give the sample data a few deliberate problems that the article can address:

> "This data has three problems. One person never registered. One record points to an
> ID that does not exist. One entry refers to something that was never created. These
> rows let us see how each query handles missing or invalid data."

Name data problems before using them in examples. Then show how each concept handles
one, such as an outer join keeping an unmatched row or `COALESCE` supplying fallback
text.

### 1.3 Teach by asking the question the concept answers

Open sections with a specific question, not a textbook topic label:

- "Which product has the worst average turnaround time across all three sites?"
- "Which orders are still worth restocking?"
- "When are we busiest, and where should the next person go?"

Where a question exists, the article shows it first and the code second.

### 1.4 State why the concept matters

Open or close with a one-line claim about why the concept exists:

- "A join is not a special feature reserved for experts. It is the answer to a
  problem every relational system creates on purpose: your data lives in more than
  one place, and a single query rarely cares about the boundaries."
- "A subquery is a value dropped exactly where you need it. A CTE is a name declared
  once, that the rest of the query can refer to as often as it likes."
- "A NULL is not zero, not an empty string, not 'we checked and there's nothing
  there.' It means 'we don't know.'"

Each sentence states the concept and gives the article its main claim.

### 1.5 Close with a challenge, not a summary

Nearly every article ends with a "Try It Yourself" section of 2–5 concrete challenges:

- "Try rebuilding this schema yourself, add a related table, and see what else your
  queries can answer once the structure is in place."
- "Take the text column and write a query that extracts just the first word..."
- "Move the failing case to the last position. How many rows get processed now?"

End by asking readers to extend, change, or test the code. When relevant, invite them
to share what they tried in the comments.

---

## Layer 2: Structure

### 2.1 The shared skeleton

Every article follows the same order:

1. **Hook:** the situation, including the problem and the setting
2. **Orientation:** one untitled sentence or short block introducing the running
   example and the tool whose output will be shown
3. **The setup:** the running scenario and any data or code it needs
4. **Concept body:** sections, one per idea, moving from simplest to hardest
5. **A decision table:** "You want... / Use", usually just before the end
6. **Try It Yourself:** 2–5 challenges (see 1.5)

### 2.2 One section, one idea

Keep sections at one heading level. Each follows the same sequence:

1. **Describe** the situation from the setting's point of view.
2. **Show** the code (one query or script, short and complete).
3. **Show** the exact output (a result grid, a terminal print, or a tool status
   line).
4. **Explain** in one or two sentences: what changed, and why this tool was the
   right one.

For a difficult concept, compare the correct code with a common mistake:

> "Write the filter against the alias defined in the SELECT list and the engine
> rejects it: at the point the filter executes, that column doesn't exist yet."

### 2.3 Group related ideas

Group related ideas by purpose, such as the places a subquery can sit, join types,
loop tools, or `NULL`-handling functions. Explain them from simple to complex, and
compare similar tools.

### 2.4 Add a decision table for related tools

When an article covers related tools, such as joins, `NULL` functions, or ranking
functions, add a two-column "Which one should I use?" table before the closing
challenge.

### 2.5 Explain difficult concepts in order

When introducing a difficult concept, such as a recursive query or validation
constraint, explain it through an example:

> "The recursive query starts with the anchor row, then adds rows linked to it. It
> repeats until no new rows match. Here, that takes three passes."

Put warnings about specific risks, such as floating-point storage, `NULL`-sensitive
filters, or division by zero, in the sections that explain them.

### 2.6 Keep the example consistent across tutorials

Avoid pausing to explain the dataset as a separate feature. Keep details consistent
between articles, such as the co-op's mentor lineage or the studio's third room.
Refer back to a specific detail only when it helps explain the current concept.

---

## Layer 3: Code

### 3.1 Short, complete, and runnable

No snippet is more than a screen long. Each block is a complete statement or a
complete script with any needed variable definitions, so the reader can run it as
shown. Imports, setup statements, and sample data definitions are shown when the
output depends on them.

### 3.2 Every block of code is followed by its output

The article shows what the terminal prints, what the result grid holds, or what the
tool messages:

> "Query OK, 2 rows affected (0.02 sec)"

Output is shown as an inline grid or a result table, with headers, exactly as the
database client, notebook, or terminal would render it. State the convention once,
early:

> "I ran every query below, in order, against the real data on [engine and version].
> The output under each query is what came back, laid out the way [tool] shows it."

> "Each snippet was run on [language version], and each output block shows what the
> terminal printed."

When a command returns no rows, say so plainly. Do not invent output.

### 3.3 Comments explain why, not how

Comments are rare and short. When present, they mark intent or an instruction to the
reader:

```sql
-- Staging table with every column as text, so a stray letter in a
-- numeric column can't abort the load
```

```python
# Everything in whole units, so the arithmetic stays clean
```

### 3.4 Show incorrect examples beside the correct version

When a common mistake illustrates a concept, show the code and its result:

```python
city = "Oslo"
if city == "Lisbon" or "Porto":  # truthy second operand, so always true
```

```sql
-- wrong: filtering on an aggregate in the wrong clause
Error: Invalid use of group function
```

Show the incorrect version as part of the example, then explain what it does.
Sometimes it passes ordinary tests ("The regular case still gets the right answer,
which is how this bug survives testing"). That is why examples should test edge cases,
not just the expected path.

### 3.5 Engine differences are flagged at the moment they matter

One clause, in parentheses, right next to the code:

> "(MySQL doesn't support `||` for concatenation by default; use `CONCAT()` there
> instead.)"

> "One caution: [this engine] doesn't support [this clause] directly. You emulate it
> with [alternative]."

> "MIN(...ctid) needs [version] or newer. On older versions, use ROW_NUMBER() in a
> CTE."

Keep the main text focused on one engine. Add alternate syntax in a short
parenthetical when it matters.

### 3.6 Show output in the tool's format

When the output shape matters, show a table with the headers and rows as the tool
renders them. When a command returns nothing, say so plainly. Choose a markdown table
or plain grid to fit the result, keep the format consistent, and never claim output
you didn't produce.

---

## Layer 4: Voice

### 4.1 Second person: "we" and "you", never "the user"

Use "we" and "you" to address the reader directly:

- "We'll build a small database for a fictional business called [name]..."
- "Say the shop raises the price by KSh 20..." is a thought experiment addressed to
  the reader.
- "Notice that the sale price is NULL here..." points to a detail; it is an
  instruction, not a fact.

Explain choices with reasons: "COALESCE works for a single fallback." "I keep the
project in its own schema."

### 4.2 Write as a practitioner, not to promote yourself

When the article carries real project experience, the voice is a working analyst
reporting what happened, not a hero telling a story:

> "The brief was blunt: 'I need you to clean this data... The CEO will be in the
> room.' No pressure."

> "I do not trust a dashboard until its totals match a query I wrote by hand."

Self-critique is normal and public. Articles that end a project list, by name, what
was built wrong and how to fix it next time, without hedging or softening. Full
sentences replace jargon everywhere.

### 4.3 Use details from the writer's own setting

Use details from the writer's own context, such as currency, place names, everyday
transactions, foods, businesses, and languages. Readers should understand the
concepts even if they do not know the setting.

For a fictional setting, choose plausible names. Readers should follow the example
without sharing that setting. Name the specific shop, studio, or market instead of an
unnamed company.

### 4.4 Show reactions through details

Use specific events to show a reaction. For example:

> "There it is: 5.0 kg of honey logged against a hive that doesn't exist... In a real
> co-op this is exactly the kind of row a data-quality check should flag..."

> "That gap between a correct query and a convincing dashboard is where this part of
> the project actually lived."

> "One partner saw them occupy the same whiteboard... That kind of insight bends how
> you sequence a lesson."

A closing line can connect the example to a broader point:

> "[Public transport] moves millions of Kenyans every day. Somewhere behind the app,
> the mobile-payment prompt, and the seat-selection screen, there is a table like this
> one, quietly deciding whether the person running the company can trust their own
> numbers."

---

## Layer 5: Sentence craft

### 5.1 Use short, direct sentences

Vary short declarative sentences with longer analytical ones. Split sentences that
carry separate points. Use numbers and units where they add precision ("290 rows, 23
defect categories, 283 after cleaning, KES 62,400.00").

### 5.2 Use colons to introduce explanations

Use a colon to introduce an explanation:

> "Counting starts at zero, so `sacco[0]` is the first letter, and `sacco[:9]` means
> 'everything before position 9.'"

> "Some joins throw unmatched rows away. Others keep them and fill the missing
> columns with NULL."

### 5.3 Keep each sentence focused

Give long sentences one main point:

- One concept per sentence.
- Put code output in a block, not in prose.
- Repetition is allowed, but always with a new purpose ("Notice", "Again", "This
  time..."), never to pad length.

### 5.4 Use parentheses for brief technical notes

Parentheses hold engine differences, small technical footnotes, and wry asides:

> "Four columns here have gaps: a missing year, a missing grade, a missing price, and
> a missing quantity (each gap tells a different story)."

### 5.5 Use metaphors briefly

Keep each metaphor to one sentence, then explain the idea literally:

- "A variable is a sticky note with a name on it."
- "One builds the containers. The other fills and changes what's inside them."
- "Confusing them is where most beginner mistakes come from."

Avoid extended allegories. Return to the data after the example.

### 5.6 Phrases that guide the reader

- "Notice that..." points to a detail in a code block.
- "Here is the..." / "Here's the..." introduces a code block or output.
- "The pattern is..." connects related examples.
- "That's because..." / "That is why..." links a result to its cause.
- Invented-data disclosures appear once, after the first example, not before it.
- Endings that address the reader in second person with a challenge.

A mnemonic, acrostic, or rhyme appears only where something has a fixed order worth
memorizing, never as filler:

> "SQL Hack: An acrostic I use to remember the SQL execution order is 'Fried Wings
> Give Heartburn So Order Lightly.'" (From, Where, Group by, Having, Select, Order
> by, Limit)

---

## Layer 6: Reader feedback

### 6.1 Answer common questions

Address known questions in the section where they arise. For example:

> "The brief was blunt about Thursday: ten minutes, live dashboard... That last part
> changes how you prepare more than anything else."

> "This is the one that separates a careful analyst from a hopeful one."

### 6.2 State what the data cannot show

State each finding's limits. Name any confounding factors:

> "The data cannot show whether payment type affects cancellations. The same two
> colleagues handle both. Check the staff records before changing the deposit policy."

> "The dashboard shows a pattern, not its cause."

Describe the result the data supports, and separate it from possible causes.

### 6.3 Accept critique in public

When reporting on a project, compare the result with stated tests. List any failures
in priority order ("Fix first:...", "Fix next:...", "Do next time:...").

### 6.4 Invite disagreement

Articles that claim a result end with a version of the same line:

> "If you spot an error in the cleaning rule or know a better way to write the query,
> leave a comment."

---

## What not to do (anti-patterns)

Avoid these patterns in narrative articles:

- No section titled "Introduction," "Conclusion," "Background," or "Overview."
- Use numbered steps only when order matters, as in a data-cleaning pipeline or build
  log.
- No bullet-point summaries of what code does, next to code that already shows it.
- No stock-API references ("Let's dive in!" or "In this guide, we will explore...").
- No code longer than a screen, and no half-shown fragments.
- No `print()` output replaced with prose such as "This will print the number."
- No jargon invented for the article; technical terms stay exact (NULL the keyword,
  "common table expression" spelled out once at first use).
- No "in conclusion" restatement of everything the article said.
- No apology for a dataset's imperfections; they are a feature, declared on purpose.
- Choose details that tie the example to a specific place rather than writing only
  about an unnamed company.
