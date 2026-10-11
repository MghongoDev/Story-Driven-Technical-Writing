# Analysis Notes: The 13 Source Articles

These notes describe the structure, examples, code, and voice of each article. The
synthesis at the end compares patterns across the series.

---

## 1. DDL and DML: how a database designs a room and remembers who escaped it

- **Frame:** A two-person escape room studio runs on paper until someone asks a
  question the paper cannot answer. DDL builds the containers; DML fills them.
- **Approach:** The written-vs-execution order table appears as a side-by-side
  comparison; the article demonstrates it with ONE query and walks the pipeline in
  prose. An acrostic ("Fried Wings Give Heartburn So Order Lightly") is offered as a
  "SQL Hack" for the execution order. ALTER is shown with a GUI "Table Structure
  panel" output rather than a row grid, because that is what a GUI would actually
  show.
- **Code style:** Small CREATE/INSERT/UPDATE/DELETE sequence, each with its status
  line; then a four-table join as the payoff.
- **Ending:** "Try rebuilding this Vault of Whispers schema yourself..." This is a
  build challenge, not a quiz.

## 2. SQL Joins Explained: A Beekeeping Co-op in Six Queries

- **Frame:** An urban beekeeping co-op with deliberately broken data. "The gaps are
  where the learning happens."
- **Approach:** The six join types are each covered in one section with an
  identical rhythm. The dataset's three cracks (an orphaned keeper, an orphaned hive,
  an orphaned harvest) are named up front, and each join's result is then read against
  them. CROSS JOIN is framed by a real scheduling need, not by combinatorics.
- **Code style:** Three tiny tables, five rows each. A third table ("harvests") is
  introduced late, with a note that production tables often go unqueried.
- **Ending:** A decision table ("You want... / Use"), then "Try It Yourself".

## 3. Subqueries and CTEs: Asking a Question Inside a Question

- **Frame:** The article returns to the co-op from the joins article and adds a
  keeper, extending the mentorship lineage to three generations for the recursive CTE.
- **Approach:** Links back to the earlier dataset ("See the tables used for
  this article here") rather than repeating it. The article shows a nested-subquery
  version, explains its duplication ("duplicated word for word"), then presents a CTE.
  It explains how the recursive CTE runs before examining the code. The NOT IN + NULL
  trap appears in its section, along with NOT EXISTS as a safer option.
- **Historical note:** A version-sensitive parenthetical ("PostgreSQL 12 and later
  will inline a non-recursive CTE...") gives real advice rather than a doc link.

## 4. SQL Functions: The Toolbox Hiding Inside Every SELECT

- **Frame:** The co-op again, plus one messy free-text notes column added via
  UPDATEs, so the string functions have something honest to clean.
- **Approach:** Functions are classified by behavior (scalar, aggregate, or
  window) before category (string, date, or number). This avoids a common beginner
  mistake. A `LENGTH`-before-`TRIM` example shows how nesting order changes the answer.
- **Code style:** Nested scalar functions in one expression (`LOWER(REPLACE(...))`,
  `ROUND(AVG(...))`) with the nesting read aloud in prose.

## 5. Window Functions: Seeing the Group Without Losing the Row

- **Frame:** The co-op once more; the harvests table is expanded to eight rows so
  windows have enough history to show ranking and frame behavior. Hive 999's orphan status is retained
  deliberately: "A window function doesn't care whether a row has a valid foreign key
  anywhere else."
- **Approach:** The article explains the parts before naming the functions:
  PARTITION BY decides the groups, ORDER BY inside OVER() decides the sequence, and
  the frame decides which neighbors count. Each ranking function's difference is
  staged only when a tie actually exists in the data. The moving-average frame clause
  is taught through a real smoothing trade-off (smoothness vs responsiveness).
- **Short:** At about six minutes, this is one of the two shortest articles in the
  series.

## 6. Handling NULL Values in SQL

- **Frame:** A record shop ("The Vinyl Vault") where sleeves lack price stickers,
  years, and condition grades. "It means 'we don't know.'"
- **Approach:** The `WHERE list_price = NULL` trap returns an empty result instead
  of an error: "The query runs, the shop owner sees an empty result set, and walks
  away thinking every record has a price." The article compares `COUNT(*)` and
  `COUNT(column)` using five rows and two non-NULL values, then explains how missing
  values affect an average. It pairs `NULLIF` with division by zero and recommends
  `COALESCE` for portability ("required in a small shop").
- **Close:** The article says `NULL` is not a data-quality failure. It represents
  information the shop did not record, such as a record's year or price.

## 7. The SafariConnect Data Story

- **Frame:** A project brief from a fictional Operations Director. The article uses
  chapters rather than steps.
- **Approach:** The article explains why it uses an all-text staging table: it keeps
  a messy import from failing on the first row. It also describes its WHERE-clause
  practice ("I keep the WHERE clause on each update so the Updated Rows count tells
  me how many rows I really touched"). The closing paragraph says, "Matatus and buses
  move millions of Kenyans every day. Somewhere
  behind the app... there is a table like this one, quietly deciding whether the
  person running the company can trust their own numbers."
- **Code style:** Longest article in the SQL set (17 min read). Sections frequently
  mix a full cleaning fix with the analysis query it enables.

## 8. Building the SafariConnect Dashboard

- **Frame:** The next day of the same project: "Wednesday's job was simple to state
  and hard to do: turn a PostgreSQL schema full of correct answers into something a
  CEO could read in ten seconds."
- **Approach:** The article explains choices a CEO might question: the grain
  of the view, dates pulled in SQL rather than Power Query ("Anything I can verify
  with a query, I verify with a query"), indexes justified as user experience, one
  view instead of five imports. The "What I'd Build Differently Next Time" section
  names five defects in the finished dashboard, in plain language, with the diagnosis
  (mislabeled legend, unresolved (Blank), cut-off labels, single palette, no map).
- **Code style:** Full DAX for every visual, each measure explained in one sentence.
- **Voice:** The article's self-critique is specific and unedited. It shows how the
  series handles mistakes in public.

## 9. Cleaning and Analyzing Tembo Hotel's Bookings

- **Frame:** "One guest at Tembo Hotel & Suites checked out three days before
  checking in. The spreadsheet says so." Absurdity first, method second.
- **Approach:** An ASCII flow diagram comes before the code. One `UNION ALL`
  query counts each defect, and the article reruns the check after each fix. Guesses
  are stated as guesses and tested against a witness column (`nights_stayed`). The
  article also inserts a bad row to show a `CHECK` constraint rejecting it. "Pitfalls
  I hit, so you can skip them" closes with one-line lessons.
- **Length:** At 27 minutes, this is the series' longest article. It repeats the
  defect check and repair sequence nine times.

## 10. Building the Tembo Hotel Dashboard in Power BI

- **Frame:** Opens with a brief to make the dashboard look professional and use
  Power BI for the visuals. It then sets three criteria and poses a puzzle about a
  mistake on page three, which it answers in section 7.
- **Approach:** A reconciliation table (Dashboard vs SQL vs Match) comes before
  discussion of visuals. Measure tables ("Visual → Title → Axis → Measure") come
  before the code. The repair list is ordered by priority ("Fix first / Fix next / Do
  next time"). An "unused measures" section records DAX measures not used on the
  dashboard. "Small samples
  call for plain language. Nineteen months and 285 bookings can show a pattern. They
  cannot prove one. I try to write 'suggests' where I would like to write 'shows'."
- **Voice:** The article uses first person to explain its decisions and mistakes.

## 11. Python Basics in the Matatu Context

- **Frame:** A conductor counts heads, knows the fare, makes change from a KSh 500
  note, and decides by feel when the vehicle is full. "Listen to what he tracks:
  a number plate, a seat count, a fuel bill and a yes or no... That is text, a whole
  number, a decimal number and a true-or-false answer."
- **Approach:** Corrects the "variable is a box" teaching inline ("The picture
  fails quickly, so use this one") and offers the sticky-note model instead. Errors
  are treated as content: the NameError traceback gets a reading lesson ("Read the
  error from the bottom"). Three complete runnable scripts close the article, each
  with two runs shown.
- **Code style:** Terminal transcripts with the `$ python fact.py` line above each
  block; two runs per script (success and failure).

## 12. Python Operators and Conditionals at the Airport Check-in Desk

- **Frame:** One passenger, one bag, one scale, two seconds. Every operator is
  introduced as something the desk does.
- **Approach:** The article defines truthiness before `and`/`or` return-value behavior
  is explored; the `city == "Lisbon" or "Porto"` bug gets a full section ("The bug
  nearly every beginner writes once") and its fix shows why it passed testing. A
  broken if/elif order produces a `-60 dollar` fee, proving order carries information.
  The same script runs with four variable configurations, shown in four transcript
  blocks, to trace branch behavior.
- **Code style:** The article recommends whole-number arithmetic when the quantities
  allow it.

## 13. Python Loops at the Nairobi Animal Orphanage

- **Frame:** A ranger with a clipboard, a sore back, and dozens of identical checks.
- **Approach:** The article connects loop anatomy to a fence patrol. Each
  letter in the checkpoint code (`"IIIBII"`) marks a state, illustrating how a loop
  works. It names the behavior in "When the mood is S, continue jumps back to the
  top" only after showing the example. A summary table ("Which loop do I
  pick?") appears within the article. It closes with an
  eight-script combination ("Morning round at the orphanage: all four at once") that
  uses all four loop tools together, then a line-by-line trace.
- **Code style:** Fictional-data disclaimer + the "Note: 'Python' in this article has
  been used to denote the programming language, not the snake." The dry clarification
  takes one line.

---

## Cross-article synthesis

The comparisons below identify patterns shared across the series.

### Repeated section structure

Each article uses a similar sequence:

1. **Pose** a specific problem and name the person who needs it solved.
2. **Show** the code that answers it.
3. **Show** the output exactly as the reader's tool would print it.
4. **Explain** the mechanism in one or two sentences.
5. **Address** a relevant error, wrong version, or confounding factor.

### What varies per article type

| Type | Frame | Ending | Length |
|---|---|---|---|
| Concept tutorial | Fictional business with named characters | Try It Yourself challenges | 6–12 min |
| Cleaning pipeline | A real-format brief and a csv | Pitfalls I hit | 17–27 min |
| Project write-up | A real project's background | Findings and limits | 9–17 min |
| Dashboard build | The brief, such as "make it professional" | Repairs and open questions | 9–17 min |

### Shared principles

- Use the setting to explain the concept instead of introducing it in isolation.
- The datasets are small and include problems that later examples address.
- Each article shows output in the format produced by the tool.
- The writing is direct and informed.
- Each article avoids filler and gets to the point.
- Every article gives readers enough context to run its examples, even when it links
  to earlier articles in the series.

### Patterns across the series

- **Reuse settings.** The beekeeping co-op spans three SQL articles,
  gaining one column or one character each time, so each new article has fresh
  material without the reader re-learning a schema.
- **Refer back when useful.** The Hive 999 example refers to the orphaned `hive_id`
  from the joins article. This cross-reference gives readers useful context.
- **Choose data problems that fit the topic.** The dataset's flaws are chosen per
  article to be the material that article's concepts act on (orphaned keys for joins,
  padded strings for TRIM, ambiguous dates for TO_DATE, unreadable ratings for
  between-1-and-5).
- **Pair analysis with dashboards.** The analysis article answers questions; the
  dashboard article presents those answers and reviews its own defects.
- **Show decisions and mistakes.** The reconciliation test, repair list, and comments
  invitation make the author's choices open to review.
