# Article types

Pick the type that matches the promise, then follow its shape. Types can blend (a tutorial with a short "why this works" section), but the dominant type decides the structure.

## Contents
- Tutorial / how-to
- Explainer
- Deep dive
- Comparison
- Opinion / argument
- Lessons learned / case study

---

## Tutorial / how-to

**Promise:** "After reading this, you can build/do X."

**Shape:**
1. Hook: the problem or the end result (a screenshot, output, or one-line demo).
2. What you'll build, prerequisites, and tested versions.
3. Steps in order, each with: what we're doing, the code, what to expect, and why.
4. Run it / verify it works.
5. Common errors and fixes (the real ones you hit or found in docs and issues).
6. Where to go next.

**Watch for:** Skipped setup steps, missing imports, steps that only work on one OS without saying so. Number the steps. Provide a link to a complete repo or a final full listing of the code for anything longer than a couple of files.

## Explainer

**Promise:** "You'll understand what X is and how it works."

**Shape:**
1. Hook: the confusion or misconception the concept clears up.
2. The simplest accurate version in a paragraph.
3. A concrete example before the abstractions.
4. How it works underneath, layered from simple to detailed.
5. When to use it and when not to.
6. Summary and further reading.

**Watch for:** Analogies that break under inspection. Say where an analogy stops being accurate.

## Deep dive

**Promise:** "You'll understand the internals or behavior of X well enough to reason about it or debug it."

**Shape:**
1. Hook: a puzzling behavior, performance mystery, or bug that motivates digging.
2. Background the reader needs (brief).
3. Investigation or walkthrough, with evidence: source code excerpts, profiler output, benchmarks, traces.
4. Findings and what they mean in practice.
5. Practical takeaways.

**Watch for:** Benchmarks without methodology (hardware, versions, sample size). Source code claims should link to the exact file and version.

## Comparison

**Promise:** "You'll be able to choose between X and Y for your situation."

**Shape:**
1. Hook: the decision the reader is facing.
2. Criteria that matter (state them up front).
3. Side-by-side on each criterion, with a summary table.
4. Recommendations by scenario ("Pick X if..., pick Y if...").
5. Caveats: what you didn't test, biases, what may change.

**Watch for:** Unfair comparisons (tuned vs. untuned), stale feature matrices, and not disclosing your own preference or affiliation.

## Opinion / argument

**Promise:** "Here's a position worth considering, and why."

**Shape:**
1. Hook: the claim, stated clearly and early.
2. Why it matters now.
3. Evidence and reasoning, strongest point first.
4. The best counterargument, addressed fairly.
5. What the reader should do differently, if they agree.

**Watch for:** Straw men, unsupported absolutes ("always", "never"), and claims that depend on unstated context.

## Lessons learned / case study

**Promise:** "Here's what happened and what you can take from it."

**Shape:**
1. Hook: the outcome or the failure.
2. Context: the system, constraints, and goal.
3. What we tried, in order, including what didn't work and why.
4. The result, with numbers where possible.
5. Lessons, stated generally enough to transfer.

**Watch for:** Sharing confidential or proprietary details. Use only information the user supplied or is clearly free to share. Keep the narrative honest about mistakes; that's what makes these valuable.
