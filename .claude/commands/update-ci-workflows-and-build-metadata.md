---
name: update-ci-workflows-and-build-metadata
description: Workflow command scaffold for update-ci-workflows-and-build-metadata in qlib.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /update-ci-workflows-and-build-metadata

Use this workflow when working on **update-ci-workflows-and-build-metadata** in `qlib`.

## Goal

Update CI workflow YAMLs and build/version metadata for releases or dependency changes.

## Common Files

- `.github/workflows/*.yml`
- `pyproject.toml`
- `qlib/__init__.py`
- `setup.py`
- `Makefile`
- `CHANGELOG.md`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit one or more .github/workflows/*.yml files to adjust CI behavior.
- Update version metadata in pyproject.toml, qlib/__init__.py, and/or setup.py.
- Optionally update Makefile or CHANGELOG.md.
- Commit all related changes together.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.