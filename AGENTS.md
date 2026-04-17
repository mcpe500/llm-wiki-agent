# LLM Wiki Agent — Schema & Workflow Instructions

This repository is maintained entirely by your coding agent. No API key or Python scripts are required for normal operation — just open this repo in Codex, OpenCode, or any agent that reads this file, and talk to it.

This repo has **two complementary knowledge layers**:

1. **`wiki/`** — modular, linked, incremental knowledge for retrieval, maintenance, and traceability.
2. **`structured/`** — human-first, linear, deeply explanatory knowledge meant to be consumed in one sitting.

The purpose of `structured/` is explicit and non-optional:

> Build a canonical “god document” — either as `god.md` or `god.html` — that a human can read in one session and come away with a complete, deeply structured understanding of the topic, from foundations to advanced nuances, tradeoffs, contradictions, mental models, formulas, notations, and expert-level insights.

This is intentionally a “god function” joke, but applied to documentation:
- not fragmented notes
- not shallow summaries
- not merely a wiki index
- but a **single master teaching artifact**

The goal is that reading the structured layer alone should make the reader understand the topic at an extremely deep level — ideally approaching expert, research, or PhD-level conceptual mastery.

---

## How to Use

Describe what you want in plain English:
- *"Ingest this file: raw/papers/my-paper.md"*
- *"What does the wiki say about transformer models?"*
- *"Explain the formulas behind this method"*
- *"Rebuild the structured god document"*
- *"Check the wiki for orphan pages and contradictions"*
- *"Build the knowledge graph"*

Or use shorthand triggers:
- `ingest <file>` → runs the Ingest Workflow
- `query: <question>` → runs the Query Workflow
- `lint` → runs the Lint Workflow
- `build graph` → runs the Graph Workflow
- `build structured` → runs the Structured Workflow
- `rebuild god document` → runs the Structured Workflow
- `god mode` → rebuilds the structured master document
- `discuss <topic>` → runs the Discussion Workflow

---

## Directory Layout

```text
raw/                # Immutable source documents — never modify these

raw-processed/      # Source-faithful, formatted derivatives of raw files
  *.md              # Clean markdown/text versions with structure improved
                    # Must preserve all information from raw as completely as possible
                    # Examples: translated versions, PDF-to-markdown conversions, cleaned formatting

wiki/               # Agent-owned modular knowledge layer
  index.md          # Catalog of all pages — update on every ingest
  log.md            # Append-only chronological record
  overview.md       # Living synthesis across all sources
  sources/          # One summary page per source document
  entities/         # People, organizations, products, projects, places, systems, datasets, etc.
  concepts/         # Reusable abstract knowledge units: ideas, frameworks, methods, processes, doctrines, patterns, etc.
  formulas/         # Equations, rules, identities, objective functions, constraints, metrics, notations, symbolic structures
  syntheses/        # Saved query answers

discussion/         # Back-and-forth conversations and decisions
  index.md          # Catalog of all discussions — update on every new entry
  YYYY-MM-DD-topic.md  # Individual discussion entries

structured/         # Human-readable long-form mastery layer
  god.md            # Canonical god markdown (default structured master document)
  god.html          # Optional canonical god HTML for richer visualization and pedagogy
  manifest.md       # What the structured layer covers, gaps, and rebuild priorities
  changelog.md      # Append-only record of major structured revisions

graph/              # Auto-generated graph data
tools/              # Custom scripts — agent-built as needed
  README.md         # Tool inventory and usage guide
  *.py              # Individual tools (naming: verb-object.py)
````

### Layer Responsibilities

* `raw/` is the immutable evidence base.
* `raw-processed/` is the formatted, source-faithful preprocessing layer used before deeper wiki extraction.
* `wiki/` is optimized for modularity, retrieval, and maintenance.
* `structured/` is optimized for sequential reading, pedagogy, and full conceptual understanding.
* `graph/` is optimized for visualizing relationships.
* `tools/` is optimized for automation, conversion, generation, and any ad-hoc scripting needs that arise during the agent's work.

The agent must keep these layers aligned.

---

## Core Principle

The repository must support two different but connected modes of understanding:

### A. Modular knowledge access

The user wants pages, entities, concepts, formulas, source summaries, and graph relationships.

### B. Deep human understanding

The user wants one canonical document that explains the whole topic from start to finish in a coherent way.

That second mode is the purpose of `structured/god.md` or `structured/god.html`.

If there is ever tension between fragmentation and comprehension:

* `wiki/` may stay modular
* `structured/` must stay coherent

---

## Knowledge Modeling Principle

The repository should model knowledge at the level that is most useful for:

* human understanding
* retrieval
* synthesis
* long-term maintainability

Do not optimize for maximum page count.
Do not optimize for minimum page count.
Optimize for the level of granularity that best supports explanation, navigation, and structured mastery.

A good wiki is not the one with the most pages.
A good wiki is the one that helps humans and agents understand the material correctly.

---

## Raw-Processed Layer Standard

The `raw-processed/` folder exists to hold **partially processed but information-complete** versions of source material before deeper wiki extraction.

This layer is for:

* formatting messy text into clean Markdown
* converting PDFs, DOCX, slides, or other formats into readable Markdown/text
* translating content when needed
* normalizing headings, lists, tables, and structure
* preserving the full information content of the source while making it easier to parse and read

### Raw-Processed Rules

* Preserve the source content as completely as possible.
* Do **not** summarize away details at this stage.
* Do **not** drop sections just because they seem low priority.
* Do **not** rewrite aggressively enough to lose meaning.
* Prefer **structure-preserving conversion** over OCR.
* OCR is **not** the default strategy.
* If the source already contains extractable text, convert it directly into well-structured Markdown/text instead of using OCR.
* If translation is performed, preserve meaning and informational completeness as closely as possible.
* The `raw-processed/` layer is still not the final wiki layer; it is a faithful intermediate representation.

The purpose of `raw-processed/` is to make raw material readable and machine-usable **without losing information**.

---

## Page Format

Every wiki page uses this frontmatter:

```yaml
---
title: "Page Title"
type: source | entity | concept | formula | synthesis | structured | discussion
tags: []
sources: []       # list of source slugs that inform this page
last_updated: YYYY-MM-DD
---
```

Use `[[PageName]]` wikilinks to link to other wiki pages.

---

## Structured Layer Standard

The `structured/` folder exists for **single-session mastery**.

A human should be able to read the structured master document once and leave with:

* a full overview
* correct terminology
* a strong internal mental model
* deep explanation of mechanisms
* concrete examples
* advanced nuance
* edge cases and failure modes
* tradeoffs
* contradictions between sources
* formulas and notation explained in plain language
* open questions
* next directions for deeper study

### Canonical Structured Output

The canonical structured deliverable is:

1. `structured/god.md` — default canonical master explanation
2. `structured/god.html` — optional richer canonical master explanation when HTML can better teach the subject through layout, diagrams, visual structure, tables, callouts, progressive disclosure, interactive explanation, or embedded visual reasoning

### Selection Rule

* Use **`god.md`** by default
* Also create or update **`god.html`** when the topic benefits significantly from:

  * diagrams
  * spatial explanation
  * flow visualization
  * side-by-side comparisons
  * layered pedagogy
  * richer interactive or visual teaching structure

If both exist, they must represent the same conceptual canon.

### Non-Negotiable Objective

The structured layer must not merely summarize the wiki.
It must **teach the topic**.

Its job is not to sound knowledgeable.
Its job is to make the human reader actually understand.

---

## Structured Quality Bar

Before considering the structured layer acceptable, ask:

* Could a smart beginner read this and form a real mental model?
* Could an intermediate reader use this to correct misconceptions?
* Could an advanced reader respect the nuance and not dismiss it as shallow?
* Does this explain not only **what** the topic is, but also **why**, **how**, **when**, **where it breaks**, and **what experts disagree about**?
* Does it explain important formulas, notation, and symbolic expressions clearly when they matter?
* Would a serious reader feel they truly learned the subject, rather than merely skimmed notes?

If the answer is “not yet”, keep refining.

---

## Structured Document Requirements

Whether written as Markdown or HTML, the structured master document must be:

* **self-contained**
* **linear**
* **teaching-oriented**
* **conceptually complete**
* **readable in one long session**
* **deep rather than merely broad**
* **source-grounded**
* **clear about uncertainty**
* **explicit about assumptions and tradeoffs**
* **designed for full understanding, not token efficiency**

### The Structured Layer Must Not Degrade Into

Do **not** let the structured layer become:

* a dump of copied notes
* a bloated but shallow summary
* disconnected sections without narrative flow
* jargon without explanation
* decorative length
* empty academic tone
* pseudo-depth

Length alone is not depth.
Density alone is not understanding.
The structured layer must optimize for comprehension.

---

## Recommended Structure for `god.md`

Use this outline unless the topic strongly requires a better one:

```markdown
---
title: "Topic God Document"
type: structured
tags: []
sources: []
last_updated: YYYY-MM-DD
coverage: draft | partial | substantial | comprehensive
format: markdown
---

# Topic Name

## 1. Executive Orientation
What this topic is, why it matters, and how to read this document.

## 2. Core Definitions
Define the essential terms precisely and clearly.

## 3. Big Picture Mental Model
Explain the whole system before diving into the parts.

## 4. Historical / Conceptual Background
How this topic emerged and what problem it was meant to solve.

## 5. Fundamental Building Blocks
The primitives, assumptions, abstractions, components, and key formulas if relevant.

## 6. Internal Mechanics
How it works step by step.

## 7. Canonical Examples
Progressive examples from simple to more complex.

## 8. Formalisms, Models, and Notation
Explain the important formulas, symbols, representations, or formal structures in plain language.

## 9. Advanced Nuances
Subtleties, expert distinctions, edge cases, caveats.

## 10. Tradeoffs and Failure Modes
Where it works, where it fails, what breaks.

## 11. Alternatives and Competing Views
Other approaches and how they differ.

## 12. Common Misconceptions
What people often misunderstand.

## 13. Contradictions Across Sources
Where sources disagree and what that means.

## 14. Practical Heuristics
Rules of thumb, decision frameworks, applied insight.

## 15. Open Questions
What remains debated, unclear, or unresolved.

## 16. Final Synthesis
A compressed but deep restatement of the whole topic.

## Appendix A. Terminology Map
Short definitions and relationships among terms.

## Appendix B. Formula / Notation Map
Key formulas, symbols, and how they relate.

## Appendix C. Suggested Next Reading
What the reader should study next.
```

---

## Recommended Structure for `god.html`

When HTML is warranted, it should still cover the same intellectual content as `god.md`, but may additionally use:

* diagrams
* visual callouts
* layered sections
* collapsible advanced notes
* side-by-side comparisons
* flow layouts
* concept dependency maps
* visual timelines
* failure-mode cards
* misconception vs correction panels
* formula walkthroughs
* symbol legends
* interactive explanatory layouts

The HTML version should improve comprehension, not just aesthetics.

### HTML Rule

If `god.html` exists, it must remain:

* self-contained
* readable offline
* faithful to source-grounded claims
* pedagogically superior where visuals matter
* synchronized in substance with `god.md`

---

## Ingest Workflow

Triggered by: *"ingest <file>"*

Steps (in order):

1. Read the source document fully
2. Create or update a corresponding file in `raw-processed/`

   * convert the source into clean, structured Markdown/text when needed
   * preserve all information as completely as possible
   * improve readability and structure without collapsing content into summary
   * prefer direct extraction / conversion over OCR
3. Read `wiki/index.md` and `wiki/overview.md` for current modular context
4. Read `structured/god.md` and/or `structured/god.html` if they exist
5. Write `wiki/sources/<slug>.md` — use the source page format below
6. Update `wiki/index.md` — add entry under Sources
7. Update `wiki/overview.md` — revise synthesis if warranted
8. Identify candidate **entities**, **concepts**, and **formulas / notations** mentioned in the processed source
9. Create or update entity pages only for items that meet the **Page Creation Rule**
10. Create or update concept pages only for items that meet the **Page Creation Rule**
11. Create or update formula pages only for items that meet the **Formula Creation Rule**
12. Record peripheral, one-off, or low-value terms inline inside the relevant source page instead of forcing a standalone page for each mention
13. Flag contradictions with existing wiki content
14. Update the structured layer:

    * revise `structured/god.md`
    * revise `structured/god.html` if present or warranted
    * ensure the new information is integrated into the linear teaching narrative
15. Update `structured/manifest.md`
16. Append to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <Title>`
17. Append to `structured/changelog.md`: `## [YYYY-MM-DD] structured integration | <Title>`
18. **Post-ingest validation**

    * check for broken `[[wikilinks]]`
    * verify all new pages are in `wiki/index.md`
    * verify the processed source still preserves the original information
    * verify the structured layer still reads coherently from start to finish
    * verify important new insights are not trapped only inside fragmented wiki pages
    * print a change summary

### Ingest Priority Rule

Every ingest must update both:

* the **source-faithful preprocessing layer**
* the **modular knowledge layer**
* the **human mastery layer**

Do not let the raw material stay messy, the wiki become rich, and the structured layer become stale.

---

## Page Creation Rule

Not every mention deserves a standalone page.

Create or update an entity or concept page when at least one of the following is true:

* it is central to understanding the source
* it appears across multiple sources
* it is likely to be queried directly
* it connects multiple pages or themes together
* it is ambiguous enough that a dedicated definition would reduce confusion
* it materially improves the quality of `structured/god.md` or `structured/god.html`

Do **not** create standalone pages for items that are merely incidental, fleeting, obvious from context, or too narrow to justify independent navigation value.

When in doubt, prefer:

* a standalone page for reusable, query-worthy, or structurally important knowledge
* an inline explanation inside the source page for minor or one-off terms

The goal is not maximum page count.
The goal is maximum clarity, retrievability, and teaching value.

---

## Formula Creation Rule

Formulas, equations, identities, constraints, objective functions, scoring rules, symbolic definitions, and notational systems are **first-class knowledge units**.

Create or update a formula page when at least one of the following is true:

* the formula is central to understanding the topic
* the formula is used repeatedly across sources
* the formula defines a method, metric, law, rule, or objective
* the formula is likely to be queried directly
* the notation is dense enough that it deserves its own explanation
* the formula materially improves the quality of `structured/god.md` or `structured/god.html`
* the formula is needed to bridge surface understanding and deep understanding

If a formula is minor, trivial, or only mentioned in passing, explain it inline in the relevant source page instead of forcing a standalone formula page.

Granularity matters:

* a named formula may deserve its own page
* a notation system may deserve its own page
* a key constraint or objective function may deserve its own page
* a symbol-heavy definition may deserve its own page

Do not ignore formulas just because they are “small.”
Do not force a page for every symbol either.
Optimize for understanding.

---

## Source Page Format

```markdown
---
title: "Source Title"
type: source
tags: []
date: YYYY-MM-DD
source_file: raw/...
processed_file: raw-processed/...
last_updated: YYYY-MM-DD
---

## Summary
2–4 sentence summary.

## Key Claims
- Claim 1
- Claim 2

## Key Quotes
> "Quote here" — context

## Important Terms and Notation
- Term / symbol / formula — short explanation if it does not warrant its own page yet

## Connections
- [[EntityName]] — how they relate
- [[ConceptName]] — how it connects
- [[FormulaName]] — where the formalism matters

## Contradictions
- Contradicts [[OtherPage]] on: ...
```

### Entity Page Format

An entity is any concrete, identifiable thing with a distinct existence in the material.

Entities may include:

* people
* organizations
* teams
* companies
* institutions
* products
* projects
* systems
* platforms
* places
* events
* datasets
* documents
* tools
* or other named real-world objects relevant to the repository

Create entity pages selectively using the **Page Creation Rule**.

```markdown
---
title: "Entity Name"
type: entity
tags: []
sources: []
last_updated: YYYY-MM-DD
---

## Definition
What this entity is.

## Role in the Repository
Why this entity matters here.

## Key Characteristics
- Characteristic 1
- Characteristic 2

## Relationships
- [[ConceptName]] — how it connects
- [[FormulaName]] — formalism or rule associated with it
- [[OtherEntity]] — how it relates

## Notes
Important context, caveats, or changes over time.
```

### Concept Page Format

A concept is any reusable unit of meaning that helps explain the subject matter.

A concept may be:

* an idea
* a theory
* a framework
* a method
* a process
* a principle
* a pattern
* a term of art
* a model
* a doctrine
* a metric family
* a workflow
* a mechanism
* a research construct
* or any other abstract piece of knowledge that is useful beyond a single passing mention

Concept pages should be created selectively using the **Page Creation Rule**.
They exist to improve understanding, navigation, synthesis, and reuse — not to create one file per vocabulary item.

Each concept page should contain the sections that are actually useful for that concept.
Use the following template flexibly rather than mechanically.

```markdown
---
title: "Concept Name"
type: concept
tags: []
sources: []
last_updated: YYYY-MM-DD
---

## Definition
Clear explanation of what the concept is.

## Why It Matters
Why this concept is important in the context of this repository.

## Structure / Mechanics
How the concept works, how it is organized, or what its internal logic is.
Use this section only when it adds value.

## Variants / Interpretations
Alternative forms, schools of thought, implementations, or meanings, if relevant.

## Examples / Use Cases
Concrete examples showing the concept in practice.

## Relationships
- [[OtherConcept]] — how it connects
- [[EntityName]] — where it appears or matters
- [[FormulaName]] — formalism associated with it

## Notes / Caveats
Assumptions, limitations, edge cases, or common confusions.
```

### Formula Page Format

A formula page is for any formal object that benefits from dedicated explanation.

Formula pages may include:

* equations
* identities
* objective functions
* loss functions
* optimization criteria
* constraints
* probabilistic rules
* scoring metrics
* update rules
* symbolic definitions
* notation systems
* recurrence relations
* matrix forms
* logical forms
* grammars
* or other reusable formal representations

Formula pages should be created selectively using the **Formula Creation Rule**.

```markdown
---
title: "Formula Name"
type: formula
tags: []
sources: []
last_updated: YYYY-MM-DD
---

## Statement
The formula, rule, notation, or symbolic definition in its canonical form.

## Plain-Language Meaning
What it says in normal language.

## Symbols
- symbol 1 — meaning
- symbol 2 — meaning

## Role in the Repository
Why this formula matters in this subject.

## Assumptions / Conditions
When it applies, what assumptions it makes, and when it does not apply.

## Derivation / Intuition
A concise derivation sketch, intuition, or interpretive explanation, if useful.

## Examples
Concrete worked or semi-worked examples.

## Relationships
- [[ConceptName]] — conceptual connection
- [[EntityName]] — entity that uses or defines it
- [[OtherFormula]] — related formula

## Notes / Caveats
Edge cases, common errors, notation variants, or interpretation pitfalls.
```

### Domain-Specific Templates

If the source falls into a specific domain (e.g. personal diary, meeting notes), the agent should use a specialized template instead of the default generic one above.

#### Diary / Journal Template

```markdown
---
title: "YYYY-MM-DD Diary"
type: source
tags: [diary]
date: YYYY-MM-DD
source_file: raw/...
processed_file: raw-processed/...
last_updated: YYYY-MM-DD
---

## Event Summary
...

## Key Decisions
...

## Energy & Mood
...

## Important Terms / References
...

## Connections
...

## Shifts & Contradictions
...
```

#### Meeting Notes Template

```markdown
---
title: "Meeting Title"
type: source
tags: [meeting]
date: YYYY-MM-DD
source_file: raw/...
processed_file: raw-processed/...
last_updated: YYYY-MM-DD
---

## Goal
...

## Key Discussions
...

## Decisions Made
...

## Action Items
...

## Important Terms / Definitions
...
```

---

## Structured Workflow

Triggered by:

* *"build structured"*
* *"rebuild god document"*
* *"god mode"*

Purpose:
Create or rebuild the canonical structured mastery layer so a human can understand the topic deeply in one sitting.

Steps:

1. Read `wiki/index.md`
2. Read `wiki/overview.md`
3. Read all high-signal pages in:

   * `wiki/sources/`
   * `wiki/entities/`
   * `wiki/concepts/`
   * `wiki/formulas/`
   * `wiki/syntheses/` if relevant
4. Read the relevant files in `raw-processed/` when higher-fidelity wording or formatting context is needed
5. Identify:

   * foundational concepts
   * dependency order between concepts
   * key formulas and notation
   * key examples
   * hidden assumptions
   * tradeoffs
   * expert-level nuances
   * contradictions and unresolved tensions
6. Build or rewrite `structured/god.md`
7. Decide whether `structured/god.html` would materially improve understanding
8. If yes, build or rewrite `structured/god.html`
9. Update `structured/manifest.md`
10. Append to `structured/changelog.md`: `## [YYYY-MM-DD] structured rebuild | god document`
11. Validate:

* a first-time reader can follow it without using the rest of the repo
* terms are introduced before heavy use
* formulas and notation are explained before being relied on heavily
* the narrative is coherent and cumulative
* the document explains, not merely summarizes
* tradeoffs and contradictions are surfaced
* the result is deep, not merely long

### Structured Manifest Requirements

`structured/manifest.md` should track:

* which canonical files exist (`god.md`, `god.html`)
* current coverage level
* which sections are strong
* which sections are thin
* known contradictions
* unresolved gaps
* next best sources to ingest
* whether HTML currently provides meaningful pedagogical value

Suggested structure:

```markdown
# Structured Manifest

## Canonical Outputs
- [god.md](god.md) — canonical long-form structured explanation
- [god.html](god.html) — optional rich visual structured explanation

## Coverage Status
- Foundations: draft | partial | substantial | comprehensive
- Mechanics: draft | partial | substantial | comprehensive
- Formalisms / Notation: draft | partial | substantial | comprehensive
- Examples: draft | partial | substantial | comprehensive
- Tradeoffs: draft | partial | substantial | comprehensive
- Contradictions: draft | partial | substantial | comprehensive
- Open Questions: draft | partial | substantial | comprehensive

## Revised In Latest Pass
- Section name
- Section name

## Known Gaps
- Missing concept
- Missing formula
- Missing source type
- Missing comparison
- Missing contradiction resolution

## HTML Justification
- Why `god.html` exists or does not exist
- What pedagogical value HTML adds beyond Markdown

## Next Best Sources To Ingest
- raw/... because ...
```

---

## Query Workflow

Triggered by: *"query: <question>"*

Steps:

1. Read `wiki/index.md` to identify relevant pages
2. Read `structured/god.md` first if the question is broad, conceptual, educational, or asks for deep understanding
3. Read `structured/god.html` if it contains richer explanatory material relevant to the question
4. Read the relevant modular wiki pages for precision and traceability
5. Read formula pages when the question involves equations, notation, metrics, symbolic definitions, or formal reasoning
6. Read the corresponding `raw-processed/` file when precise wording, formatting, full detail, or translation context matters
7. Synthesize an answer with inline citations as `[[PageName]]` wikilinks
8. If useful, answer in layers:

   * **Direct answer**
   * **Deep explanation**
   * **Formula / notation explanation** if relevant
9. Ask the user if they want the answer filed as `wiki/syntheses/<slug>.md`

### Query Routing Rule

* Use `structured/` first for understanding
* Use `wiki/` first for retrieval
* Use `wiki/formulas/` when formalism matters
* Use `raw-processed/` when source-faithful wording or formatting matters
* Use all relevant layers when the user needs both explanation and evidence

---

## Lint Workflow

Triggered by: *"lint"*

Check for:

### Wiki Layer

* **Orphan pages** — wiki pages with no inbound `[[links]]`
* **Broken links** — `[[WikiLinks]]` pointing to missing pages
* **Contradictions** — claims that conflict across pages
* **Stale summaries** — pages not updated after newer sources
* **Missing processed sources** — raw files that do not yet have a corresponding `raw-processed/` version
* **Processed/raw drift** — processed files that appear to have lost structure or information from the raw source
* **Missing high-value pages** — entities, concepts, or formulas that clearly meet the Page Creation Rule or Formula Creation Rule but do not yet have their own pages
* **Over-fragmentation** — pages that exist but are too trivial, too isolated, or too low-value to justify standalone existence
* **Data gaps** — questions the wiki cannot answer; suggest new sources
* **Shallow pages** — pages whose sections exist but do not actually explain anything useful
* **Notation drift** — symbols or formula names used inconsistently across pages

### Structured Layer

* **Coverage gaps** — important concepts or formulas missing from the structured layer
* **Narrative breaks** — explanations that assume unstated knowledge
* **Terminology drift** — inconsistent use of terms
* **Formula drift** — inconsistent notation or unexplained symbolic jumps
* **Shallow sections** — sections that summarize without truly explaining
* **Source divergence** — wiki updated but structured layer not reconciled
* **False completeness** — the master document sounds complete while omitting known disputes
* **HTML/Markdown drift** — `god.md` and `god.html` disagree in substance

Output a lint report and ask if the user wants it saved to:

* `wiki/lint-report.md`
* `structured/lint-report.md`
* or both

---

## Graph Workflow

Triggered by: *"build graph"*

First try: `python tools/build_graph.py --open`

If Python/deps are unavailable, build manually:

1. Search for all `[[wikilinks]]` across wiki pages
2. Build nodes (one per page) and edges (one per link)
3. Infer implicit relationships not captured by wikilinks — tag `INFERRED` with confidence score; low confidence → `AMBIGUOUS`
4. Write `graph/graph.json` with `{nodes, edges, built: date}`
5. Write `graph/graph.html` as a self-contained visualization

### Graph Note

The graph helps users see relationships.
It does not replace the structured mastery layer.

Graphs help navigation.
The structured layer builds understanding.

---

## Tools Workflow

Triggered by: when a repetitive task arises, when something cannot be done with existing tools, or when the user requests a custom script.

Purpose:
Create ad-hoc scripts and tools to automate, convert, generate, or analyze content that would otherwise be inefficient or impossible to do manually.

### When to Build a Tool

Build a tool when:

* a task is repetitive
* a task requires computation beyond manual capacity
* a task is too complex for a one-off bash command
* the user needs a specific visual or data transformation
* the agent needs to perform an operation that existing tools cannot do

### Tool Naming Convention

Use `verb-object.py` naming:

* `build-graph.py`
* `convert-docx.py`
* `validate-links.py`
* `extract-formulas.py`
* `generate-dataset.py`
* `process-raw.py`

### Tool Construction Standards

Every tool in `tools/` must have:

1. a descriptive docstring at the top explaining purpose and usage
2. command-line argument parsing (`argparse` or similar)
3. a `--help` or `-h` flag
4. clear output
5. a corresponding entry in `tools/README.md`

### Tool Documentation

Maintain `tools/README.md` with:

* tool name and purpose
* usage examples with exact commands
* input/output specifications
* any dependencies required

### Tool Workflow Steps

1. **Identify** the need for a tool
2. **Design** the tool interface
3. **Implement** the tool in Python
4. **Test** the tool on a small sample
5. **Document** the tool in `tools/README.md`
6. **Run** the tool and verify output
7. **Report** to the user what was built and how to use it

### Tool Invocation

Tools are invoked directly via bash:

```bash
python tools/<tool-name>.py [args]
```

Or if the user triggers `build graph` or similar workflow triggers, the agent will run the appropriate tool automatically.

---

## Naming Conventions

* Source slugs: `kebab-case` matching source filename
* Processed source files: use the same slug as the raw source when possible
* Entity pages: `TitleCase.md` (e.g. `OpenAI.md`, `SamAltman.md`)
* Concept pages: `TitleCase.md` (e.g. `ReinforcementLearning.md`, `RAG.md`)
* Formula pages: `TitleCase.md` when the formula has a canonical name (e.g. `BayesRule.md`, `CrossEntropyLoss.md`, `BellmanEquation.md`)
* Formula pages: use a clear descriptive name when no canonical name exists (e.g. `PolicyObjectiveFunction.md`, `ScoringRule.md`, `ConstraintSet.md`)
* Structured canonical markdown: `structured/god.md`
* Structured canonical HTML: `structured/god.html`
* Structured support files:

  * `structured/manifest.md`
  * `structured/changelog.md`

---

## Index Format

```markdown
# Wiki Index

## Overview
- [Overview](overview.md) — living synthesis

## Sources
- [Source Title](sources/slug.md) — one-line summary

## Entities
- [Entity Name](entities/EntityName.md) — one-line description

## Concepts
- [Concept Name](concepts/ConceptName.md) — one-line description

## Formulas
- [Formula Name](formulas/FormulaName.md) — one-line description

## Syntheses
- [Analysis Title](syntheses/slug.md) — what question it answers
```

`wiki/index.md` indexes the modular layer.
`structured/manifest.md` indexes the mastery layer.

---

## Discussion Workflow

Triggered by: *"discuss <topic>"* or whenever a topic needs back-and-forth discussion during a session.

Steps:

1. Identify the discussion topic and its context
2. Check `discussion/index.md` to see if a related discussion already exists
3. Create a new discussion entry at `discussion/YYYY-MM-DD-topic.md` using the format below
4. Record the key points, decisions, and reasoning from the discussion
5. Update `discussion/index.md` — add entry under Discussions
6. Link relevant wiki pages using `[[PageName]]` wikilinks

### Discussion Entry Format

```markdown
---
title: "Discussion Topic"
type: discussion
date: YYYY-MM-DD
tags: []
---

## Context
What prompted this discussion.

## Key Points
- Point 1
- Point 2

## Decisions Made
- Decision 1

## Open Questions
- Question 1

## Connections
- [[WikiPageName]] — relevant connection
```

### Discussion Index Format

```markdown
# Discussion Index

## Discussions
- [Discussion Title](YYYY-MM-DD-topic.md) — brief description

## Recent
- Most recent discussions listed here
```

---

## Log Format

`## [YYYY-MM-DD] <operation> | <title>`

Operations:

* `ingest`
* `query`
* `lint`
* `graph`
* `discussion`
* `structured rebuild`
* `structured integration`

---

## Final Operating Rule

Do not confuse:

* many notes with understanding
* long text with depth
* coverage with coherence
* polished phrasing with real explanation

The repository is not truly complete until the structured layer contains a strong canonical god document — in Markdown, HTML, or both — that lets a serious human reader consume it in one session and emerge with deep, connected, expert-level understanding of the topic.

The raw layer exists as evidence.
The raw-processed layer exists to preserve that evidence in clean, usable form.
The modular layer exists to support navigation, retrieval, and maintenance.
The structured layer exists to produce mastery.
Formulas and notation are not optional details when they are part of real understanding.
