---
type: Change Record
title: Update supported Python versions to 3.11 through 3.15
description: Drops Python 3.10 and adds Python 3.15 to the versions supported by both the template repository and the projects it generates.
resource: https://github.com/gt-csse/copier-UvScaffolding
tags:
  - python-versions
  - template
  - ci-cd
status: stable
generated:
  by: claude-code/claude-opus-5-5
  at: 2026-10-05T11:27:00-04:00
sources:
  - id: copier
    resource: copier.yml
  - id: pyproject
    resource: pyproject.toml
  - id: cicd
    resource: .github/workflows/CICD.yml
  - id: bug_report
    resource: .github/ISSUE_TEMPLATE/bug_report.md
  - id: template_bug_report
    resource: template/.github/ISSUE_TEMPLATE/bug_report.md
  - id: uv_lock
    resource: uv.lock
  - id: snapshots
    resource: tests/__snapshots__/All_EndToEndTest.ambr
---

# Summary

The supported Python range moves from 3.10–3.14 to 3.11–3.15, both for this template repository and
for the default answers used when generating new projects.

# What Changed

## Generated projects

- The `python_versions` question defaults to `3.11, 3.12, 3.13, 3.14, 3.15`.[^copier] Generated
  projects therefore get `requires-python = ">= 3.11"`, a `Python :: 3.15` classifier in place of
  `Python :: 3.10`, a CI matrix of 3.15 through 3.11, and `build_python_version: "3.11"`.[^snapshots]
- The generated bug report template derives its example Python versions from the `python_versions`
  answer instead of a hardcoded list, so it no longer drifts from the project's supported versions.[^template_bug_report]

## Template repository

- `requires-python` raised to `>=3.11`.[^pyproject]
- CI matrix updated to 3.15, 3.14, 3.13, 3.12, 3.11.[^cicd]
- Bug report template example versions updated to include 3.15.[^bug_report]
- `uv.lock` re-resolved for `>=3.11`, removing the 3.10-only `exceptiongroup` backport.[^uv_lock]
- `pyproject.toml` and `CICD.yml` reformatted (single-line short arrays, aligned ruff ignore comments,
  double-quoted cron string); no behavioral effect.[^pyproject][^cicd]
- End-to-end test snapshots regenerated.[^snapshots]

# Why

Python 3.10 reaches end of life in October 2026 and Python 3.15 is released the same month. Keeping
the default supported range aligned with the actively supported CPython releases ensures generated
projects test against current interpreters and do not carry support for an unmaintained one.

[^copier]: copier.yml
[^pyproject]: pyproject.toml
[^cicd]: .github/workflows/CICD.yml
[^bug_report]: .github/ISSUE_TEMPLATE/bug_report.md
[^template_bug_report]: template/.github/ISSUE_TEMPLATE/bug_report.md
[^uv_lock]: uv.lock
[^snapshots]: tests/__snapshots__/All_EndToEndTest.ambr
