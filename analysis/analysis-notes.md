# Analysis Notes: The 13 Source Articles

Notes taken while reading each article, recording its narrative frame, structure,
code style, and distinctive moves. Read together, they show the shared method and
where each article type diverges. Per-article notes first, cross-article synthesis
last.

---

## 1. DDL and DML: how a database designs a room and remembers who escaped it

- **Frame:** A two-person escape room studio runs on paper until someone asks a
  question the paper cannot answer. DDL builds the containers; DML fills them.
- **Signature moves:** The written-vs-execution order table appears as a side-by-side
  comparison; the article demonstrates it with ONE query and walks the pipeline in
  prose. An acrostic ("Fried Wings Give Heartburn So Order Lightly") is offered as a
  "SQL Hack" for the execution order. ALTER is shown with a GUI "Table Structure
  panel" output rather than a row grid, because that is what a GUI would actually
  show.
- **Code style:** Small CREATE/INSERT/UPDATE/DELETE sequence, each with its status
  line; then a four-table join as the payoff.
- **Ending:** "Try rebuilding this Vault of Whispers schema yourself..." — a build
  challenge, not a quiz.

## 2. SQL Joins Explained: A Beekeeping Co-op in Six Queries

- **Frame:** An urban beekeeping co-op with deliberately broken data. "The gaps are
  where the learning happens."
- **Signature moves:** The six join types are each covered in one section with an
  identical rhythm. The dataset's three cracks (an orphaned keeper, an orphaned hive,
  an orphaned harvest) are named up front, and each join's result is then read against
  them. CROSS JOIN is framed by a real scheduling need, not by combinatorics.
- **Code style:** Three tiny tables, five rows each; a third table ("harvests") is
  introduced late — with the wry note that plenty of production tables go unqueried.
- **Ending:** A decision table ("You want... / Use"), then "Try It Yourself".

## 3. Subqueries and CTEs: Asking a Question Inside a Question

- **Frame:** Same co-op as the joins article, with one new keeper added so the
  mentorship lineage runs three generations deep — seeded for the recursive CTE.
- **Signature moves:** Links back to the earlier dataset ("See the tables used for
  this article here") instead of re-printing it. A nested-subquery version is shown
  first, its duplication named honestly ("duplicated word for word"), and the CTE
  version follows as the fix. The recursive CTE gets a full prose walk of the engine's
  passes before the code is dissected. The NOT IN + NULL trap is flagged inside the
  section, with NOT EXISTS named as the safer habit.
- **Historical note:** A version-sensitive parenthetical ("PostgreSQL 12 and later
  will inline a non-recursive CTE...") gives real advice rather than a doc link.

## 4. SQL Functions: The Toolbox Hiding Inside Every SELECT

- **Frame:** The co-op again, plus one messy free-text notes column added via
  UPDATEs, so the string functions have something honest to clean.
- **Signature moves:** Functions are classified by *behavior* (scalar / aggregate /
  window) before by category (string / date / number) — a taxonomy mistake beginners
  actually make. "The order you nest functions in changes the answer, not just the
  syntax" is shown with a LENGTH-before-TRIM concrete example.
- **Code style:** Nested scalar functions in one expression (`LOWER(REPLACE(...))`,
  `ROUND(AVG(...))`) with the nesting read aloud in prose.

## 5. Window Functions: Seeing the Group Without Losing the Row

- **Frame:** The co-op once more; the harvests table is expanded to eight rows so
  windows have enough history to be interesting. Hive 999's orphan status is retained
  deliberately: "A window function doesn't care whether a row has a valid foreign key
  anywhere else."
- **Signature moves:** The anatomy is decomposed before the functions are named:
  PARTITION BY decides the groups, ORDER BY inside OVER() decides the sequence, and
  the frame decides which neighbors count. Each ranking function's difference is
  staged only when a tie actually exists in the data. The moving-average frame clause
  is taught through a real smoothing trade-off (smoothness vs responsiveness).
- **Short:** At ~6 minutes' reading, this is one of the two shortest in the series —
  proof the style doesn't demand length.

## 6. Handling NULL Values in SQL

- **Frame:** A record shop ("The Vinyl Vault") where sleeves lack price stickers,
  years, and condition grades. "It means 'we don't know.'"
- **Signature moves:** The `WHERE list_price = NULL` trap is demonstrated as a silent
  wrong answer, not an error: "The query runs, the shop owner sees an empty result
  set, and walks away thinking every record has a price." COUNT(*) vs COUNT(column)
  is staged as the five-vs-two mistake an average can hide. The NULLIF/division-by-zero
  pairing is the tool-introduction payoff. Engine portability is a first-class
  argument for COALESCE ("required in a small shop").
- **Close:** "NULL isn't a data-quality failure to panic over... It's a fact about the
  world — a record whose year nobody wrote down, a price nobody set yet..." — the
  reframing ending.

## 7. The SafariConnect Data Story

- **Frame:** A real-format project brief, quoted verbatim from a fictional-but-
  plausible Operations Director. The article is organized in chapters, not steps.
- **Signature moves:** The staging-table-is-all-TEXT decision is defended as
  deliberate ("It's the one rule that keeps a messy import from crashing on line
  one"). WHERE-clause discipline is shown as a habit ("I keep the WHERE clause on each
  update so the Updated Rows count tells me how many rows I really touched"). The
  closer reframes: "Matatus and buses move millions of Kenyans every day. Somewhere
  behind the app... there is a table like this one, quietly deciding whether the
  person running the company can trust their own numbers."
- **Code style:** Longest article in the SQL set (17 min read). Sections frequently
  mix a full cleaning fix with the analysis query it enables.

## 8. Building the SafariConnect Dashboard

- **Frame:** The next day of the same project: "Wednesday's job was simple to state
  and hard to do: turn a PostgreSQL schema full of correct answers into something a
  CEO could read in ten seconds."
- **Signature moves:** Everything a CEO might question gets a named "why": the grain
  of the view, dates pulled in SQL rather than Power Query ("Anything I can verify
  with a query, I verify with a query"), indexes justified as user experience, one
  view instead of five imports. The "What I'd Build Differently Next Time" section
  names five defects in the finished dashboard, in plain language, with the diagnosis
  (mislabeled legend, unresolved (Blank), cut-off labels, single palette, no map).
- **Code style:** Full DAX for every visual, each measure explained in one sentence.
- **Voice:** The self-critique is specific and unedited — this article is the series'
  clearest demonstration of public accountability.

## 9. Cleaning and Analyzing Tembo Hotel's Bookings

- **Frame:** "One guest at Tembo Hotel & Suites checked out three days before
  checking in. The spreadsheet says so." Absurdity first, method second.
- **Signature moves:** An ASCII flow diagram of the pipeline before any code. The
  audit-query pattern (one UNION ALL query that counts every defect at once) and the
  "re-run the check, expect zero rows" loop after every fix. Guesses are named as
  guesses, with a witness column (`nights_stayed`) that confirms or kills them — this
  is the article's methodological core. CHECK constraints demonstrated by deliberately
  inserting a bad row and showing the database refuse it. "Pitfalls I hit, so you can
  skip them" closes the article in one-line lessons.
- **Rhythm:** The longest article in the series (27 min read) because the
  defect-fix-prove loop repeats nine times; the repetition is the point.

## 10. Building the Tembo Hotel Dashboard in Power BI

- **Frame:** Opens on the brief's shortest instruction ("Make it look professional —
  use Power BI for the visuals"), then states three tests that make "professional"
  checkable. Sets a genuine puzzle ("Page three of the dashboard contains a mistake
  that sits in plain sight") the pays off in section 7.
- **Signature moves:** A reconciliation table (Dashboard vs SQL vs Match) before any
  visual discussion. Measure tables ("Visual → Title → Axis → Measure") before the
  code. A "Fix first / Fix next / Do next time" priority ordering for the repair list.
  An "unused measures" section turning leftover DAX into future value. "Small samples
  call for plain language. Nineteen months and 285 bookings can show a pattern. They
  cannot prove one. I try to write 'suggests' where I would like to write 'shows'."
- **Voice:** First-person throughout, and the "I" is operational: where a choice was
  deliberate, the article says so; where something slipped, it says that too.

## 11. Python Basics in the Matatu Context

- **Frame:** A conductor counts heads, knows the fare, makes change from a KSh 500
  note, and decides by feel when the vehicle is full — "Listen to what he tracks:
  a number plate, a seat count, a fuel bill and a yes or no... That is text, a whole
  number, a decimal number and a true-or-false answer."
- **Signature moves:** Corrects the "variable is a box" teaching inline ("The picture
  fails quickly, so use this one") and offers the sticky-note model instead. Errors
  are treated as content: the NameError traceback gets a reading lesson ("Read the
  error from the bottom"). Three complete runnable scripts close the article, each
  with two runs shown.
- **Code style:** Terminal transcripts with the `$ python fact.py` line above each
  block; two runs per script (success and failure).

## 12. Python Operators and Conditionals at the Airport Check-in Desk

- **Frame:** One passenger, one bag, one scale, two seconds. Every operator is
  introduced as something the desk does.
- **Signature moves:** Truthiness is defined before `and`/`or` return-value behavior
  is explored; the `city == "Lisbon" or "Porto"` bug gets a full section ("The bug
  nearly every beginner writes once") and its fix shows why it passed testing. A
  broken if/elif order produces a `-60 dollar` fee, proving order carries information.
  Four identical scripts run with four different variable configurations — four
  transcript blocks in a row — to trace branch behavior.
- **Code style:** Whole-gram arithmetic is a stated habit ("a habit worth copying
  whenever the quantities allow it"), floated as content.

## 13. Python Loops at the Nairobi Animal Orphanage

- **Frame:** A ranger with a clipboard, a sore back, and dozens of identical checks.
- **Signature moves:** Straight from loop anatomy to fence patrol: a string of
  checkpoint codes (`"IIIBII"`) where letters are states — a compact way to animate a
  loop. "When the mood is S, continue jumps back to the top" — the abstract behavior
  named only after the concrete example shows it. A summary table ("Which loop do I
  pick?") is woven into the body, not bolted on at the end. The article closes with an
  eight-script combination ("Morning round at the orphanage: all four at once") that
  uses all four loop tools together, then a line-by-line trace.
- **Code style:** Fictional-data disclaimer + the "Note: 'Python' in this article has
  been used to denote the programming language, not the snake." — dry humor, one
  line, gone.

---

## Cross-article synthesis

This is the summary of what all 13 articles do together.

### The core loop

Every article runs the same engine at the section level:

1. **Pose** the situation as a real problem with a named person who wants something.
2. **Show** the code that answers it.
3. **Show** the output exactly as the reader's tool would print it.
4. **Explain** the mechanism in one or two sentences.
5. **Name** the trap, the wrong version, or the confound, in the same breath.

### What varies per article type

| Type | Frame | Ending | Length |
|---|---|---|---|
| Concept tutorial | Fictional business with named characters | Try It Yourself challenges | 6–12 min |
| Cleaning pipeline | A real-format brief and a csv | Pitfalls I hit | 17–27 min |
| Project write-up | The origin scene of a real project | A reframing closer | 9–17 min |
| Dashboard build | The impossible brief ("professional") | Repair list and what's next | 9–17 min |

### What never varies

- The setting carries the concept; the concept is never taught in the abstract.
- The data is small enough to hold in your head, and imperfect on purpose.
- Output is always shown, always honest, always in the tool's own shape.
- The voice is a competent colleague at a neighbouring desk, not a lecturer.
- Every article respects the reader's time: no filler paragraphs, no throat-clearing.
- Every article is self-contained in its head even when it links to a series — a
  reader landing on the middle article can still run everything in it.

### Series-level design worth copying

- **World-building across articles.** The beekeeping co-op spans three SQL articles,
  gaining one column or one character each time, so each new article has fresh
  material without the reader re-learning a schema.
- **Callback as continuity.** "Hive 999 is still the orphaned hive_id from the joins
  article" — cross-references are functional, never decorative.
- **Deliberate imperfection as curriculum.** The dataset's flaws are chosen per
  article to be the material that article's concepts act on (orphaned keys for joins,
  padded strings for TRIM, ambiguous dates for TO_DATE, unreadable ratings for
  between-1-and-5).
- **Projects come in pairs.** The analysis article does the thinking; the dashboard
  article does the communication; and the dashboard article grades itself.
- **Style as accountability.** The voice is opinionated and the opinions are checked
  in public (the reconciliation test, the "Fix first" list, the comments invitation).
  The persona is credible because its failures are visible.
