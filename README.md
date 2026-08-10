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

## Relationship to Other Documentation

AGENTS.md states conventions for this repository. It does not replace the
[GeoLab Notebook template](https://github.com/EarthScope/GeoLab-learning-hub/blob/main/templates/GeoLab_Notebook_template.ipynb),
which defines the required structure for a GeoLab tutorial notebook.