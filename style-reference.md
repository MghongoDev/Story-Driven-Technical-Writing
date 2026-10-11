# Style Reference: The Complete Pattern Library

This document distills how a strong story-driven technical article is built. Each
pattern names what it does, shows at least one illustrative example of the shape it
takes, and gives guidance on when to use it. Patterns are grouped by layer: narrative
frame, structure, code, voice, and sentence craft.

The guiding principle across all layers: **a technical article should read like a story
about a place, and the code should be something the reader could run in that place.**

*(The illustrative snippets below are examples of the shape a pattern takes — invented
where needed, so they are not tied to any specific published article.)*

---

## Layer 1: The narrative frame

### 1.1 Anchor the concept in a concrete everyday setting

Every strong article of this kind opens by placing the concept inside a place the
reader can picture. The setting is chosen *because* the concept is the natural answer
to a problem the setting already has — not for decoration.

Examples of the shape (changing the domain swaps the setting, not the principle):

- A database-concept article → a small business drowning in paper records until
  someone asks a question the paper cannot answer.
- A joins-concept article → a co-op or team where records live in two lists that
  don't line up perfectly.
- A loops-concept article → a worker with a clipboard of dozens of identical checks.
- A conditionals-concept article → one person at a counter making a two-second
  decision from a few numbers.

The rule is not "be quirky." The rule is: pick a setting where the concept is the
natural answer to a problem the setting already has.

**How to do it:**

1. Name the place and the people in it (a ranger, a front desk, a keeper, a clerk).
2. State the problem the place has before naming any technology.
3. Only then introduce the concept as what handles the problem.

### 1.2 Introduce one invented, named world per article (and reuse it across articles)

Fictional businesses, teams, or workplaces get names, and their people get real-sounding
names:

- A business, team, or workplace with a name that could plausibly exist in its
  setting (a room name in a studio, a person in a co-op, a label in a shop) — anything
  the domain fits.

Once established, a world is reused across a series: add one character or one column
to keep the data fresh, so the reader doesn't re-learn a new dataset each time.

The running example should be darker than a textbook's. Give the dataset deliberate
imperfections that the article later uses:

> "Notice three deliberate cracks in this data. One person never registered anything.
> One record points to an ID that doesn't exist. One entry refers to something that
> was never created. Real datasets have rows like this. A good demonstration should
> too."

This is a signature move. The imperfections are declared up front, then become the
material the concepts act on: an outer join keeps the row nobody matched, a coalesce
cleans the missing text.

### 1.3 Teach by asking the question the concept answers

Sections open with a genuine business question, not a textbook topic label:

- "Which product has the worst average turnaround time across all three sites?"
- "Which orders are stillworth restocking?"
- "When are we busiest, and where should the next person go?"

Where a question exists, the article shows it first and the code second.

### 1.4 Frame the bigger idea, not just the syntax

Articles open and close with one-line claims about why the concept exists:

- "A join is not a special feature reserved for experts. It is the answer to a
  problem every relational system creates on purpose: your data lives in more than
  one place, and a single query rarely cares about the boundaries."
- "A subquery is a value dropped exactly where you need it. A CTE is a name declared
  once, that the rest of the query can refer to as often as it likes."
- "A NULL is not zero, not an empty string, not 'we checked and there's nothing
  there.' It means 'we don't know.'"

These sentences do double duty: they are the clearest possible summary of the concept,
and they act as the article's thesis statement.

### 1.5 Close with a challenge, not a summary

Nearly every article ends with a "Try It Yourself" section of 2–5 concrete challenges:

- "Try rebuilding this schema yourself, add a related table, and see what else your
  queries can answer once the structure is in place."
- "Take the text column and write a query that extracts just the first word..."
- "Move the failing case to the last position. How many rows get processed now?"

The choreography: end with an invitation to extend, change, or break the code. Where
it fits, an explicit invitation to share the result in the comments. The difficulty
curve is real — it ends with a nudge to apply the concept to the reader's own week.

---

## Layer 2: Structure

### 2.1 The shared skeleton

Every article follows the same order:

1. **Hook:** the concrete situation (the problem, the setting, and the stakes)
2. **Orientation:** one untitled or one-sentence block introducing the running
   example and the tool whose output will be shown
3. **The setup:** the running scenario and any data or code it needs
4. **Concept body:** sections, one per idea, moving from simplest to hardest
5. **A decision table:** "You want... / Use", usually just before the end
6. **Try It Yourself:** 2–5 challenges (see 1.5)

### 2.2 One section = one idea, with a repeating rhythm

Sections are never subsections of subsections. Each follows the same dance:

1. **Describe** the situation from the setting's point of view.
2. **Show** the code (one query or script, short and complete).
3. **Show** the exact output (a result grid, a terminal print, or a tool status
   line).
4. **Explain** in one or two sentences: what changed, and why this tool was the
   right one.

The deepest sections add a small comparison — what the code would produce if you
wrote it wrong instead:

> "Write the filter against the alias defined in the SELECT list and the engine
> rejects it: at the point the filter executes, that column doesn't exist yet."

### 2.3 Recurrence groups ideas by kind, not by keyword

Strong articles group ideas into families that share a shape, then cover each family
once: the three places a subquery can sit, the six join types, the loop's four tools,
the handful of NULL-handling functions. Within a family, order runs from simple to
complex, and mirror-image members are taught by contrast with each other.

### 2.4 The mixed structure: narrative, then one lookup section, then the why

When a concept article covers a family of tools (joins, NULL functions, ranking
functions), it ends with a "which one should I use" decision table before the closing
challenge. The table is plain, two columns, no qualifiers, no footnotes.

### 2.5 Difficulty arrives silently

Where the article introduces a heavy concept (ranking functions, recursive queries,
self-referencing logic, validation constraints), it is not flagged with warnings.
Instead, the narrative walks through it as if it were a natural next step:

> "The recursive half then runs repeatedly: first it finds anyone connected to the
> anchor row, then it runs again on those new rows, then it runs once more, finds
> nobody new, and stops. Three generations, discovered without knowing in advance how
> many there would be."

A targeted warning, where a concept has a real trap (floating-point storage,
NULL-sensitive filters, division by zero), lives inside the section that needs it —
not as a generic advisory at the top of the page.

### 2.6 Quiet encyclopedism: the world exists independently of this tutorial

No article stops to caption its own dataset. The studio has a whiteboard problem and a
third room; the co-op has a mentor lineage three generations deep. This gives the world
internal continuity the article can call back to later ("the orphaned row from the
joins article is still here, with no matching parent"). The callback is always
functional: it reintroduces a piece of the data by name, never to pad length.

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

Where a command returns no rows, say so in the same visual language ("A brand-new
table has no rows to show, so the tool confirms the command ran and moves on") rather
than inventing output that isn't there.

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

### 3.4 Counter-examples are shown alongside the correct version

When a pattern has a natural wrong version, the article shows it and lets the reader
watch it fail:

```python
city = "Oslo"
if city == "Lisbon" or "Porto":  # truthy second operand, so always true
```

```sql
-- wrong: filtering on an aggregate in the wrong clause
Error: Invalid use of group function
```

The wrong version is not a caption; it is part of the story. Sometimes the wrong
version survives real-world testing ("The regular case still gets the right answer,
which is how this bug survives testing"), which teaches why edge-case testing matters
more than the happy path alone.

### 3.5 Engine differences are flagged at the moment they matter

One clause, in parentheses, right next to the code:

> "(MySQL doesn't support `||` for concatenation by default; use `CONCAT()` there
> instead.)"

> "One caution: [this engine] doesn't support [this clause] directly. You emulate it
> with [alternative]."

> "MIN(...ctid) needs [version] or newer. On older versions, use ROW_NUMBER() in a
> CTE."

The pattern: the main text stays in one engine; the parenthetical names the alternate
syntax; no version tables at the end.

### 3.6 Output imagery is deliberate

Where the article needs to prove the output shape, it shows a data table with
headers and rows exactly as the tool would render. Where a command returns nothing,
say so plainly, in the tool's own voice. Use whichever format — markdown table or
plain grid — reads better for that particular result; don't switch shape without a
reason, and never claim output you didn't produce.

---

## Layer 4: Voice

### 4.1 Second person: "we" and "you", never "the user"

The article speaks from inside the situation:

- "We'll build a small database for a fictional business called [name]..."
- "Say the shop raises the price by KSh 20..." — a thought experiment addressed to
  the reader.
- "Notice that the sale price is NULL here..." — notice, an instruction, not a fact.

The narrator is present and opinionated. Lessons from hard cases are stated as
habits: "This is where veteran analysts look first." "This is why COALESCE is the
portable choice for a single fallback." "I keep the project in its own schema."

### 4.2 First-person practitioner, not first-person celebrity

When the article carries real project experience, the voice is a working analyst
reporting what happened, not a hero telling a story:

> "The brief was blunt: 'I need you to clean this data... The CEO will be in the
> room.' No pressure."

> "I do not trust a dashboard until its totals match a query I wrote by hand."

Self-critique is normal and public. Articles that end a project list, by name, what
was built wrong and how to fix it next time, without hedging or softening. Full
sentences replace jargon everywhere.

### 4.3 Local texture, not local theme

Anchor concepts in *local texture from the writer's own context* — currency, place
names, everyday transactions, foods, businesses, and languages the writer actually
knows. This texture earns specificity without exoticizing: the concepts still read as
universal, and the setting earns its details. A reader from another place still
understands every concept; they just see a place the writer knows rather than a
generic "somewhere."

Where the setting is fictional, the names should be plausible for the place, but the
teaching stays generic in the sense that it never depends on the reader sharing the
locale — only on recognizing it. Specificity is the point: a strong article is
*about* its shop, its studio, its market, never about "a company".

### 4.4 Emotional beats arrive as small déjà-vus, not declarations

The emotional peaks are concrete, small, and earned late:

> "There it is: 5.0 kg of honey logged against a hive that doesn't exist... In a real
> co-op this is exactly the kind of row a data-quality check should flag..."

> "That gap between a correct query and a convincing dashboard is where this part of
> the project actually lived."

> "One partner saw them occupy the same whiteboard... That kind of insight bends how
> you sequence a lesson."

A closing line that reframes the article inside a larger truth is common:

> "[Public transport] moves millions of Kenyans every day. Somewhere behind the app,
> the mobile-payment prompt, and the seat-selection screen, there is a table like this
> one, quietly deciding whether the person running the company can trust their own
> numbers."

---

## Layer 5: Sentence craft

### 5.1 Short declaratives carry the signal

The prose alternates six-to-twelve-word declarative sentences with longer analytical
ones. Compound sentences stay rare. Where a fact has two clauses, they usually get
two sentences. Small numbers and units carry precision, and exact figures appear in
prose where they matter ("290 rows, 23 defect categories, 283 after cleaning, KES
62,400.00").

### 5.2 The colon–pause–payoff rhythm

A statement is followed by a colon, then its explanation:

> "Counting starts at zero, so `sacco[0]` is the first letter, and `sacco[:9]` means
> 'everything before position 9.'"

> "Some joins throw unmatched rows away. Others keep them and fill the missing
> columns with NULL."

This is the most repeated shape in the style: state the idea, then stop, then explain
why, so the reader meets each claim as an idea before it becomes an argument.

### 5.3 Word count is an explicit cost

Long sentences each carry one new thing:

- One concept per sentence.
- Code output stays out of prose; it lives in a block.
- Repetition is allowed, but always with a new purpose ("Notice", "Again", "This
  time..."), never to pad length.

### 5.4 Em-dashes and parentheses do the bookkeeping

Parentheses hold engine differences, small technical footnotes, and wry asides:

> "Four columns here have gaps: a missing year, a missing grade, a missing price, and
> a missing quantity (each gap tells a different story)."

### 5.5 Metaphors are concrete and die fast

The article uses a metaphor for one sentence, then returns to the literal:

- "A variable is a sticky note with a name on it."
- "One builds the containers. The other fills and changes what's inside them."
- "Confusing them is where most beginner mistakes come from."

They never spawn a world of their own (no extended allegory); once their job is done,
the article returns to the actual data.

### 5.6 Small repeated mechanical gambits

- "Notice that..." — pointing at a specific detail in a block.
- "Here is the..." / "Here's the..." — introducing a block or output.
- "The pattern is..." — generalizing two or three instances.
- "That's because..." / "That is why..." — closing a looped explanation.
- Invented-data disclosures appear once, after the first example, not before it.
- Endings that address the reader in second person with a challenge.

A mnemonic, acrostic, or rhyme appears only where something has a fixed order worth
memorizing, never as filler:

> "SQL Hack: An acrostic I use to remember the SQL execution order is 'Fried Wings
> Give Heartburn So Order Lightly.'" (From, Where, Group by, Having, Select, Order
> by, Limit)

---

## Layer 6: The feedback loop

### 6.1 Answer the reader's unspoken objection

When a concept has a known confusion, the article names it and resolves it inside the
section that raises it. Two shapes:

> "The brief was blunt about Thursday: ten minutes, live dashboard... That last part
> changes how you prepare more than anything else."

> "This is the one that separates a careful analyst from a hopeful one."

### 6.2 Admit what the data cannot say

Findings are presented with their limits attached. A confound is named, not hidden:

> "The data can't separate the two causes. It may be that the payment type makes a
> difference, or that the two colleagues who log reservations with this payment type
> also handle the cancellations. Either way, it points at the fix: ask for a deposit
> up front, and check how cancellations get recorded."

> "The dashboard shows the pattern. It does not claim a cause."

The word "shows" is preferred over "proves"; the pattern repeats wherever findings
rest on a confounded variable.

### 6.3 Accept critique in public

Articles that end a build grade their own work against a stated test. Failures are
listed in plain language, in priority order ("Fix first:...", "Fix next:...",
"Do next time:..."). No failures are excused, and no defect is hidden.

### 6.4 Invite disagreement

Articles that claim a result end with a version of the same line:

> "If you spot a cleaning rule I got wrong, or a better way to write any query here,
> tell me in the comments. I'd like to know."

---

## What not to do (anti-patterns)

These are the habits a story-driven article avoids, by omission:

- No section titled "Introduction," "Conclusion," "Background," or "Overview."
- No numbered "Step 1: Do X" in narrative articles — except where the work is
  genuinely sequential (a data-cleaning pipeline, a build log), where steps carry
  real order and the labels earn their place.
- No bullet-point summaries of what code does, next to code that already shows it.
- No stock-API references ("Let's dive in!" or "In this guide, we will explore...").
- No code longer than a screen, and no half-shown fragments.
- No `print()` output replaced with prose such as "This will print the number."
- No jargon invented for the article; technical terms stay exact (NULL the keyword,
  "common table expression" spelled out once at first use).
- No "in conclusion" restatement of everything the article said.
- No apology for a dataset's imperfections; they are a feature, declared on purpose.
- No setting so generic it could be swapped for any other without the article
  noticing. Specificity is the test: the article is *about* its place, not about
  "a company."
