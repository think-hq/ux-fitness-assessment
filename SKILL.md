---
name: ux-fitness-assessment
description: Use when reviewing whether a UI is the right paradigm for its task and data, when a page works but feels like the wrong shape, when assessing if an interaction pattern matches the user's mental model, or when evaluating UX fitness at page-level or atomic-component level
---

# UX Fitness Assessment

## Overview

**Assess whether a UI is the ideal paradigm for the task, then score how well it executes that paradigm.**

Most UX problems aren't poor execution — they're the wrong UI type entirely. A beautifully polished table displaying graph data is still the wrong UI. This skill catches paradigm mismatches first, then evaluates execution quality.

**Not for:** Accessibility audits, visual/aesthetic assessment, performance, or design system compliance.

## When to Use

- After a UI is designed or implemented, as a fitness check
- When reviewing whether an existing page is the right *shape* for its task
- When something feels off but you can't articulate why
- When comparing alternative UI approaches for a feature

## Theoretical Foundations

Each dimension maps to established UX research:

| Theory | Author | Principle | Applies To |
|--------|--------|-----------|------------|
| Gulf of Execution/Evaluation | Norman (1988) | UI must match user's mental model of cause→effect | Paradigm Fit |
| Direct Manipulation | Shneiderman (1983) | Objects should behave like real-world counterparts | Paradigm Fit |
| Natural Mapping | Norman (1988) | Controls spatially/conceptually map to effects | Paradigm Fit |
| Hick's Law | Hick (1952) | Decision time = log₂(n+1); more choices = slower | Cognitive Load |
| Miller's Law | Miller (1956) | Working memory holds 7±2 chunks | Cognitive Load |
| Recognition over Recall | Nielsen (1994) | Show options, don't require memory | Information Scent |
| Fitts's Law | Fitts (1954) | Time to target = f(distance/size) | Interaction Cost |
| Feedback Principle | Norman (1988) | Every action needs visible, immediate feedback | Feedback Loop |

**Core premise (Norman's Gulf model):** UX fitness = how small the gulf between user intent and UI action (execution) + how small the gulf between system state and user perception (evaluation).

---

## The Formula

```
UX Fitness = Paradigm Cap × (Execution Score / 10) × 100%
```

| Component | How Calculated |
|-----------|---------------|
| Paradigm Cap | 1.0 (match), 0.75 (defensible), 0.40 (mismatch) |
| Execution Score | Weighted sum of 6 dimensions (each scored 1-10) |
| Normalisation | Divide by 10 to convert 1-10 scale to 0-1 range |

**If paradigm fit fails, execution score is capped.** You cannot polish a table into being the right choice when the data is a graph.

---

## Stage 1: Paradigm Fit

### Process

1. **Identify the task(s)** — What must the user accomplish?
2. **Classify the data nature** — What shape is the underlying data?
3. **If compound data:** identify the dominant nature (see Compound Data Rule)
4. **Name the user's mental model** — How does the user think about this?
5. **Check paradigm match** — Does the chosen UI align with data nature + mental model?

### Paradigm Classification Table

| Data/Task Nature | Ideal Paradigm(s) | Wrong Choice Signals |
|-----------------|-------------------|---------------------|
| Relationships between entities | Node graph, network diagram | Flat table, nested lists |
| Sequential steps with progress | Wizard, stepper, timeline | Single long form, tabs |
| Hierarchical data (parent-child) | Tree view, nested nav, accordion | Flat list, breadcrumbs alone |
| Comparison across items | Table, matrix, side-by-side | Cards, carousel |
| Spatial/geographic data | Map, floor plan | Address list, table with coords |
| Temporal progression | Timeline, gantt, calendar | Table sorted by date |
| Filtering a large set | Faceted search, filter panel | Single dropdown, paginated list only |
| Status monitoring (live) | Dashboard, live indicators, gauges | Log output, table with manual refresh |
| Composition/assembly | Drag-and-drop builder, canvas | Form with textarea |
| Navigation of known structure | Sidebar nav, tabs, breadcrumbs | Search-only, flat links |
| Unstructured exploration | Search, infinite scroll, recommendations | Fixed categories only |
| Configuration with dependencies | Conditional form, rule builder | Flat settings page ignoring deps |

### Compound Data Rule

When a page has **mixed data natures** (e.g., project page = hierarchical + temporal + relational):

1. **Identify dominant nature** — which nature is most critical to the user's primary task?
2. **Primary paradigm** must serve the dominant nature
3. **Secondary natures** can be served by supporting views/panels
4. **Compound paradigms** exist for common combinations:

| Combination | Compound Paradigm |
|-------------|-------------------|
| Hierarchical + Temporal | Work breakdown timeline (tree + gantt) |
| Spatial + Filtering | Map with filter panel |
| Relational + Hierarchical | Graph with collapsible clusters |
| Temporal + Status | Timeline with status indicators |
| Comparison + Filtering | Filterable comparison matrix |

**If no compound paradigm exists:** primary paradigm wins, secondary natures get supporting views (panels, drawers, toggleable views).

### Defensible Criteria

A ⚠️ Defensible verdict applies when the paradigm is suboptimal BUT one or more valid constraints exist:

| Constraint | Example | Why It's Valid |
|------------|---------|----------------|
| Technical limitation | No graph library; team can't maintain one | Shipping > perfection if gap is small |
| Data volume | Tree view breaks at 10,000+ nodes | Paradigm physically can't render the data |
| User expertise | Power users explicitly prefer tables for speed | Expert mental model differs from novice |
| Progressive disclosure | Simple view first, complex view on demand | Both paradigms present, simple as default |
| Platform constraint | Mobile viewport can't fit a gantt chart | Hardware limits the paradigm |
| Transition cost | Users trained on current paradigm for years | Switching cost exceeds UX gain |

**Defensible is NOT valid when:**
- "We didn't think of it" (ignorance ≠ constraint)
- "It was easier to build" (developer convenience ≠ user need)
- "The library we already use does tables" (sunk cost)

### Paradigm Fit Verdict

| Verdict | Meaning | Score Cap |
|---------|---------|-----------|
| ✅ **Match** | Paradigm aligns with data nature and mental model | No cap (1.0) |
| ⚠️ **Defensible** | Suboptimal but reasonable given stated constraints | Cap at 75% (0.75) |
| ❌ **Mismatch** | Wrong paradigm entirely | Cap at 40% (0.40) |

**When flagging a mismatch, always name:**
1. What paradigm *should* be used
2. Why the current one fails the user's mental model (reference Norman's Gulf)
3. What the user is forced to do mentally to compensate

---

## Stage 2: Execution Quality

### Task Frequency Modifier

Before scoring, classify task frequency — this shifts weight priorities:

| Frequency | User Profile | Weight Shift |
|-----------|-------------|--------------|
| **High** (daily+) | Practised user | +5% to Interaction Cost, −5% from Cognitive Load |
| **Medium** (weekly) | Familiar user | No shift (use default weights) |
| **Low** (monthly or less) | Occasional user | +5% to Information Scent, −5% from Interaction Cost |

**Rationale:** Frequent users have internalised the UI (Hick's Law: practiced choices are faster). Rare users need more guidance (Recognition over Recall). Adjust weights accordingly.

### Dimensions (6 total)

Score each 1-10, apply weights:

| Dimension | Default Weight | What to Assess | Grounded In |
|-----------|---------------|----------------|-------------|
| Task alignment | 25% | Does every element serve the user's goal? | Gulf of Execution |
| Cognitive load | 25% | Can user accomplish goal without stopping to think? | Hick's Law, Miller's Law |
| Information scent | 20% | Can user tell where they are, what to do, what things mean? | Recognition over Recall |
| Interaction cost | 15% | Minimum actions to complete task? | Fitts's Law |
| Error prevention | 10% | Does UI structurally prevent mistakes? | Norman's Constraints |
| Feedback loop | 5% | Does user know what happened after every action? | Gulf of Evaluation |

### Scoring Guide

| Score | Meaning |
|-------|---------|
| 9-10 | Ideal — hard to improve |
| 7-8 | Good — minor friction |
| 5-6 | Adequate — noticeable friction, workarounds needed |
| 3-4 | Poor — user regularly confused or stuck |
| 1-2 | Broken — task completion requires external help |

### Final Score Calculation

```
Execution Score = (task_alignment × 0.25) + (cognitive_load × 0.25) + 
                  (info_scent × 0.20) + (interaction_cost × 0.15) + 
                  (error_prevention × 0.10) + (feedback_loop × 0.05)

Final UX Fit = (Execution Score / 10) × Paradigm Cap × 100%
```

**Worked example:** Paradigm is ⚠️ Defensible (cap 0.75). Scores: 8, 7, 8, 6, 7, 8.
```
Execution = (8×0.25) + (7×0.25) + (8×0.20) + (6×0.15) + (7×0.10) + (8×0.05)
          = 2.0 + 1.75 + 1.6 + 0.9 + 0.7 + 0.4 = 7.35
Final     = (7.35 / 10) × 0.75 × 100% = 55.1%
```

---

## Multi-Task Pages

When a page serves multiple tasks (e.g., dashboard = monitoring + drill-down + configuration):

1. **List all tasks** the page serves
2. **Assign frequency weight** to each task (how often does user do this here?)
3. **Run full assessment per task** (paradigm fit + execution)
4. **Aggregate:**

```
Page UX Fit = Σ (task_frequency_weight × task_fit_score)
```

| Task | Frequency Weight | UX Fit | Weighted |
|------|-----------------|--------|----------|
| Monitor status | 60% | 85% | 51% |
| Drill into alert | 30% | 70% | 21% |
| Change threshold | 10% | 40% | 4% |
| **Page Total** | | | **76%** |

**Rule:** If the highest-frequency task has a paradigm mismatch, the page fails regardless of aggregate score.

---

## Assessment Levels

Apply at three levels:

| Level | Scope | Question |
|-------|-------|----------|
| **System** | Whole product/flow | Is the overall interaction model right for this domain? |
| **Page** | Single screen | Is this page the right paradigm for its goal? |
| **Atomic** | Individual widget/component | Does this element earn its place and use the right pattern? |

A page can pass at page-level but have atomic failures (e.g., right layout, wrong date picker type).

---

## How to Run the Assessment

1. **State the user's goal(s)** — one sentence per task
2. **Classify task frequency** — high/medium/low
3. **Classify data nature** from paradigm table (identify dominant if compound)
4. **Check paradigm fit** — match, defensible, or mismatch?
5. **If mismatch:** stop, name the correct paradigm, explain gulf
6. **If match/defensible:** apply frequency modifier to weights, score 6 dimensions
7. **Calculate final score** with explicit normalisation
8. **For multi-task pages:** aggregate per-task scores
9. **Report findings** with evidence for each rating

### Output Format

```
## UX Fitness Assessment: [Page/Component Name]

**User Goal(s):** [one sentence per task, with frequency weight]
**Data Nature:** [classification — note if compound, state dominant]
**Task Frequency:** High | Medium | Low

### Stage 1: Paradigm Fit
**Chosen Paradigm:** [what was built]
**Ideal Paradigm:** [what should exist]
**Verdict:** ✅ Match | ⚠️ Defensible (constraint: X) | ❌ Mismatch
**Reasoning:** [why — reference mental model gap]

### Stage 2: Execution Quality (weights adjusted for frequency)
| Dimension | Score | Evidence |
|-----------|-------|----------|
| Task alignment | /10 | ... |
| Cognitive load | /10 | ... |
| Information scent | /10 | ... |
| Interaction cost | /10 | ... |
| Error prevention | /10 | ... |
| Feedback loop | /10 | ... |

**Execution Score:** X/10
**Final UX Fit:** X% (calculation shown)

### Recommendations
1. [Highest impact change]
2. [Next priority]
```

---

## Common Mistakes

| Mistake | Why It Happens | Reality |
|---------|---------------|---------|
| Skipping Stage 1 | UI "works" so jump to polishing | Working ≠ right paradigm |
| Accepting table as default | Tables are easy to build | Tables suit comparison, not all data |
| Confusing pretty with fit | Good styling feels like good UX | A polished wrong paradigm is still wrong |
| Ignoring mental model | Evaluating UI in isolation | Users bring expectations from real-world metaphors (Norman) |
| Scoring without evidence | "Feels like a 7" | Every score needs specific observable evidence |
| Only assessing happy path | Feature works when used correctly | Assess what happens when user is lost or wrong |
| Ignoring task frequency | Treating all tasks equally | Primary task dominance trumps edge-case polish |
| Calling mismatch "defensible" without constraint | Don't want to flag a big problem | Defensible requires a named, valid constraint |
| Skipping feedback dimension | "User can see it changed" | Visible ≠ understood; feedback must confirm intent was met |
