# AGENTS.md

Guidance for coding agents working in this repository. This project involves four
recurring kinds of work: building container images, writing Python code, writing
Jupyter/IPython notebooks, and writing documentation that follows ASD-STE100
Simplified Technical English. The sections below apply whenever a task falls into
one of these areas, regardless of which files or directories it touches. Section 5
adds GeoLab-specific requirements on top of the general notebook conventions in
Section 4.

**Project context:** target Python 3.11 or newer. Notebooks run as Jupyter
notebooks (`.ipynb`) or Marimo notebooks. Use `pip` or `uv` as the package manager;
inside a notebook, install a missing dependency with `%pip install <package>`, not
`!pip install`.

---

## 1. Writing Documentation (ASD-STE100 Compliance)

All documentation prose (not code, not code comments) must follow **ASD-STE100
Simplified Technical English** principles. This is a best-effort manual application
of STE, not a certified pass through the official dictionary tool — but every rule
below is non-negotiable when writing or editing documentation prose.

### Sentence construction

- One idea, one instruction, per sentence. Split compound sentences.
- Keep sentences short: aim for 20 words or fewer in procedures, 25 in descriptive text.
- Use active voice. "The tool builds the file," not "the file is built by the tool."
- Use imperative mood for procedure steps: "Open the file," not "You should open the file."
- No contractions: "do not," "cannot," "it is" — never "don't," "can't," "it's."
- No rhetorical questions, no humor, no idioms, no metaphors, no analogies. Describe
  the mechanism directly instead of comparing it to something else.

### Vocabulary

- One approved term per concept, used consistently across the whole document and
  across documents. Do not vary terminology for style — pick one name for a thing
  and reuse it everywhere.
- Avoid vague qualifiers and subjective words: "genuinely," "simply," "just,"
  "obviously," "powerful," "beautiful," "handy," "smart."
- Prefer "can" for possibility or capability. Avoid "may" and "might."
- Prefer "must" for a hard requirement, not "should" or "need to."
- Avoid "there is / there are" constructions — name the subject and use an active verb.
- Limit noun clusters (stacked nouns/adjectives before a noun) to 3 words. Rewrite a
  4+ word noun stack as a phrase (e.g. "a framework for processing sensor data," not
  "sensor data processing framework").
- Do not drop articles ("a," "the") for brevity.

### Structure

- Numbered steps or bold **Step N:** labels for any sequential procedure — never bury
  steps inside a paragraph.
- Tables for comparisons (options, trade-offs, side-by-side settings) instead of
  prose paragraphs describing the same thing.
- Headings should not be gerunds where an imperative or plain noun phrase works
  ("Connect to the server," not "Connecting to the server").
- Every acronym or product-specific term gets a one-sentence definition on first use
  in a document.

### When editing existing docs

- Preserve any existing heading anchors and update cross-references or a table of
  contents if a heading's visible title changes.
- Do not rewrite code blocks or shell commands for STE style — STE applies to prose,
  not code. Code comments can be lightly clarified but must stay accurate to the code.
- If a document mixes STE-compliant and non-STE prose (e.g. older drafts merged with
  new sections), flag the inconsistency rather than silently leaving mixed style on
  the same page.

---

## 2. Building Container Images

Apply these conventions whenever a task involves writing, editing, or debugging a
Dockerfile, image build configuration, or a container publishing workflow.

### General conventions

- Treat the image definition (Dockerfile plus any package/dependency manifests) as
  the source of truth; do not hand-edit a running container as a substitute for
  changing the image definition.
- A base template can mark some files as generated, for example a provided
  `Dockerfile`. Do not edit those files. Edit only the package and dependency
  manifests layered on top. State this rule explicitly in any procedure that
  touches the template.
- Prefer a package manager that resolves cross-package dependency conflicts before
  install (e.g. conda) over one that does not (e.g. plain pip) when both are
  available, and state the reason when explaining the choice.
- Only add system-level package installs when a dependency genuinely requires them.
  Do not add system packages speculatively.
- The build pipeline is always: edit configuration → build the image → tag the image
  → push to a registry → reference the pushed image where it will run. Keep this
  order in any procedure or diagram.
- A platform can offer an automatic build-from-repository option: it builds the image
  from a Dockerfile in a Git repository, with no local build and no manual registry
  push. Document this as a distinct alternative path. Do not merge it with the manual
  build-and-push workflow. State clearly which files and steps each path needs.
- Keep registry-specific authentication and push instructions (personal access
  tokens, CLI login, tagging syntax) together in one place per registry; do not
  duplicate the same steps across multiple documents.
- If the project ships a smoke test for a built image (a test script or test
  notebook), reference it as the verification step instead of inventing a new one.

### When asked to write or debug an image definition

- Confirm which path the user wants (a manually built and pushed image, versus an
  automatic build-from-repository option) before writing configuration — they
  require different files and different instructions.
- Pin versions where reproducibility matters (e.g. a language runtime version), but
  do not over-pin every transitive dependency.
- Build locally before suggesting a push. Do not suggest pushing to a registry
  without confirming the user has credentials configured for that registry.

---

## 3. Python Coding Standards

Apply these conventions to all Python code, in a notebook cell or a standalone script.

- Follow PEP 8 for all Python code.
- Add an explicit type hint to every parameter and return value of a custom helper
  function.
- Never use a bare `except:`. Catch a specific exception, for example `KeyError` or
  `ValueError`.
- Prefer vectorized operations over `.iterrows()` on a DataFrame.
- After a DataFrame mutation, display `df.head()` or `df.info()` in the next cell or
  the next statement to verify the result.

---

## 4. Writing IPython/Jupyter Notebooks

Apply these conventions whenever a task involves creating or editing a `.ipynb` file.

### For any notebook

- Structure: a title Markdown cell, a short introduction, then alternating Markdown
  (explanation) and code (executable) cells. Narrative should carry the reader
  between code cells, not just serve as captions.
- Markdown cells in any notebook intended for publication or sharing must follow the
  same ASD-STE100 rules as `.md` documentation (Section 1): short sentences, active
  voice, no filler language ("we're thrilled," "a robust and dynamic platform").
  Draft or exploratory notebooks can stay conversational, but flag STE violations
  before a notebook is proposed for publishing.
- Code cells should run top-to-bottom without hidden state. Do not write a notebook
  that only works if cells are executed out of order.
- Clear cell outputs before committing, unless the output is the point of the
  notebook (for example, an expected plot or dataframe result). Large binary outputs
  bloat version control and produce noisy diffs.
- Do not hardcode user-specific paths, tokens, or credentials in any cell, Markdown
  or code, for any notebook that can be shared or published.
- Use relative paths for any referenced asset, matching how the notebook will
  actually be opened by a reader.

### Cell isolation

- Put one concept in each cell. Keep each cell small enough to test on its own.
- Do not mix a library import with data mutation logic in the same cell.
- Structure each data processing step as three cells, in this order:
  1. **Markdown cell** — one or two sentences that state why this step happens.
  2. **Code cell** — the Python or pandas logic for the step.
  3. **Verification cell** — a check of the result, for example a plot, a printed
     table, or an `assert` statement.

### State management

- Do not write code that depends on cells running out of sequential order.
- When a cell modifies a variable or a DataFrame, either overwrite the same name or
  assign the result to a clearly named new variable (for example `df_cleaned` or
  `df_encoded`). This keeps kernel state traceable and avoids hidden state bugs.

### Execution guardrails

- In an agentic or autonomous run, if a cell raises an error, read the traceback,
  fix the underlying code, and re-execute the cell. Do not stop to ask permission
  for a routine syntax or logic fix.
- Before an operation with O(n²) or higher complexity on a DataFrame larger than
  50,000 rows, print a progress status or log the elapsed time with `time.time()`.

### Before publishing a draft notebook

- Confirm it is linked from wherever the project's navigation or index expects
  published content to be listed.
- Confirm all Markdown cells meet the ASD-STE100 bar in Section 1 before treating the
  work as done — do not publish non-compliant prose just because the code works.
- Restart the kernel and run all cells fresh to confirm there is no out-of-order
  execution dependency before publishing.

---

## 5. GeoLab Notebook Conventions

Notebooks written for the GeoLab learning hub must follow the structure defined in
the [GeoLab Notebook template](https://github.com/EarthScope/GeoLab-learning-hub/blob/main/templates/GeoLab_Notebook_template.ipynb).
Start every new GeoLab tutorial notebook from this template. These rules add to the
general notebook conventions in Section 4; they do not replace them.

### Required structure

1. **Title cell** — a single `#` heading with the notebook title.
2. **Metadata cell** — state the Version, Last updated date, Author(s) and
   institution, License, and Estimated Time. State the Maintainer, Maintainer
   contact, Pathway, and Citation only when they apply.
3. **Introduction** — write three parts: what the notebook does (one sentence), why
   it is useful (the geophysical application it addresses), and what the user will
   accomplish (the concrete output). Follow this with a Prerequisites checklist and
   a GeoLab Compute Resources table that states the recommended image and server
   size.
4. **Learning Objectives** — list 2 to 4 objectives. Start each objective with an
   action verb (Load, Stream, Calculate, Visualize, Apply). Match each objective to
   a skill the notebook actually demonstrates.
5. **Relevant Documentation & Resources** — link to every external tool, API, or
   dataset the notebook uses.
6. **Contents** — list each section as a numbered link to an in-page anchor (for
   example `#id-2-data-loading`). Match this list to the notebook's actual section
   headings and their order.
7. **Numbered workflow sections** — for example Setup & Imports, Data Loading, Data
   Exploration, one section per core workflow step, Visualization, Practice &
   Exploration, and Troubleshooting & Support. Give each section the same number in
   Contents and in its heading.

### Markdown style inside the notebook

- Use `##` for section headers and `###` for sub-sections. Do not skip a level (for
  example, do not put `####` directly under `##`).
- Use `*` for unordered lists and `1.` for ordered or sequential steps.
- Use backticks for inline code, variable names, and file paths (for example,
  `DATA_DIR`).
- Use `>` blockquotes for notes, checks, and warnings.

### Content conventions

- Put every user-editable setting (a file path, a date range, an area of interest) in
  one labeled Configuration code cell. Place this cell directly after Setup &
  Imports.
- Before a code cell that loads data or runs a workflow step, add a Markdown cell
  that states three things: what the code does, why the notebook uses this
  approach, and what the expected output looks like.
- After a key step, add a **Check:** blockquote. State the expected result and link
  to the Troubleshooting & Support section.
- In Practice & Exploration, give 2 to 4 concrete modifications the user can try.
  Tie each modification to a Learning Objective.
- In Troubleshooting & Support, add a table of common errors, their likely causes,
  and their fixes. Add links to GeoLab documentation and the GeoLab community forum.

### Before publishing a GeoLab notebook

- Delete the template's instruction cell and every `AUTHOR NOTE (Remove this text)`
  blockquote.
- Replace every `[Bracketed Placeholder]` with real content. A remaining placeholder
  blocks publishing.
- Confirm each Contents link matches its heading's actual anchor. Hover the rendered
  heading, click its `¶` icon, and copy the anchor from the browser address bar.
- Apply the general notebook rules in Section 4 — Markdown cells follow ASD-STE100,
  no hardcoded paths or credentials, kernel restarted and run end to end — before
  treating the notebook as ready to publish.
