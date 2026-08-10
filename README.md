# README

This repository contains [AGENTS.md](AGENTS.md). This file gives instructions to
coding agents that work in this repository. This document explains the purpose of
AGENTS.md and describes how to use it.

## Purpose

AGENTS.md defines the conventions for four kinds of recurring work in this
repository:

1. Writing documentation that follows ASD-STE100 Simplified Technical English.
2. Building container images.
3. Writing Python code.
4. Writing Jupyter or Marimo notebooks, including notebooks for the GeoLab
   learning hub.

A coding agent reads AGENTS.md before it starts a task. The agent then applies the
matching section's rules to the files it creates or edits. The rules remove the need
to repeat the same instructions in every prompt.

## Section Map

| Section | Applies To |
| --- | --- |
| 1. Writing Documentation | Prose in any `.md` file or Markdown notebook cell |
| 2. Building Container Images | Dockerfiles, image build configuration, publishing workflows |
| 3. Python Coding Standards | Python code in a script or a notebook cell |
| 4. Writing IPython/Jupyter Notebooks | Any `.ipynb` file |
| 5. GeoLab Notebook Conventions | Notebooks written for the GeoLab learning hub |

Section 5 adds requirements on top of Section 4. It does not replace Section 4.

## How to Use AGENTS.md

### As a Coding Agent

1. Identify which section, or sections, apply to the current task.
2. Apply every rule in the matching section to new and edited content.
3. Apply Section 1 to any prose you write, even inside a section for a different
   file type (for example, Markdown cells in a notebook).
4. Complete the checklist at the end of a section (for example, "Before publishing
   a GeoLab notebook") before you report the task as done.

### As a Contributor

1. Read the section that matches the file type you plan to change.
2. Match new content to the existing conventions in that section.
3. Propose a change to AGENTS.md itself when a rule no longer fits the project, or
   when a new recurring task needs its own section.

## Adding AGENTS.md to a Repository

1. Copy [AGENTS.md](AGENTS.md) to the root directory of the target repository.
2. Do not rename the file. A coding agent looks for the exact name `AGENTS.md`.
3. Do not add a second copy in a subdirectory unless that subdirectory needs rules
   that differ from the root file. Most coding agents read the nearest AGENTS.md
   above the file they edit.
4. Remove any section that does not apply to the target repository (for example,
   Section 5 if the repository does not host GeoLab notebooks).
5. Commit the file to version control so every contributor and agent sees the same
   rules.

## Using AGENTS.md to Write a GeoLab Notebook

1. Open Section 5, GeoLab Notebook Conventions, in [AGENTS.md](AGENTS.md).
2. Start the notebook from the
   [GeoLab Notebook template](https://github.com/EarthScope/GeoLab-learning-hub/blob/main/templates/GeoLab_Notebook_template.ipynb).
3. Build the notebook's structure in the order Section 5 lists: Title cell,
   Metadata cell, Introduction, Learning Objectives, Relevant Documentation &
   Resources, Contents, then the numbered workflow sections.
4. Apply the Markdown style rules in Section 5 (heading levels, list markers,
   inline code, blockquotes) as you write each cell.
5. Apply the general notebook conventions in Section 4 (cell isolation, state
   management, execution guardrails) to every code cell.
6. Consult the
   [GeoLab Notebook Design Guide](https://docs.google.com/document/d/1VCtblHHW_laPqAx-R92_aKZdFRCflLrIMCl8tos4qZg/edit?tab=t.0)
   for writing guidance beyond the structural rules in Section 5.
7. Complete the "Before publishing a GeoLab notebook" checklist in Section 5 before
   you propose the notebook for publishing.

## Using AGENTS.md to Write Documentation

1. Open Section 1, Writing Documentation (ASD-STE100 Compliance), in
   [AGENTS.md](AGENTS.md).
2. Write each sentence to the sentence construction rules in Section 1: one idea per
   sentence, active voice, imperative mood for procedure steps, no contractions.
3. Check your vocabulary against the rules in Section 1: one approved term per
   concept, no vague qualifiers, "can" for capability, "must" for a requirement.
4. Structure the document with the rules in Section 1: numbered steps for a
   procedure, tables for a comparison, a plain-noun or imperative heading.
5. Define every acronym or product-specific term on its first use in the document.
6. If you edit an existing document, apply the "When editing existing docs" rules in
   Section 1: preserve heading anchors, leave code blocks unchanged, and flag mixed
   STE and non-STE prose instead of silently leaving it.

## Relationship to Other Documentation

AGENTS.md states conventions for this repository. It does not replace the
[GeoLab Notebook template](https://github.com/EarthScope/GeoLab-learning-hub/blob/main/templates/GeoLab_Notebook_template.ipynb),
which defines the required structure for a GeoLab tutorial notebook, or the
[GeoLab Notebook Design Guide](https://docs.google.com/document/d/1VCtblHHW_laPqAx-R92_aKZdFRCflLrIMCl8tos4qZg/edit?tab=t.0),
which gives additional writing guidance for GeoLab notebooks.
