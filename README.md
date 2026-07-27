# AI301 Cycle 2 Contribution README

## Student Information

Name: Rithika Sridharbabu  
GitHub: https://github.com/rithikasridharbabu-2007  
Course: CodePath AI301 — AI Open Source Capstone  
Cycle: 2  
Current Phase: Phase I — Issue Selection  
Status: Phase I Complete  

---

## Chosen Project

Project name: readme2demo  
Repository: https://github.com/alphacrack/readme2demo  
My fork: https://github.com/rithikasridharbabu-2007/readme2demo  

## Chosen Issue

Issue title: docs: test counts are stale/contradictory (README says 175, step-by-step guide says 163) and CHANGELOG links stop at 0.4.1  
Issue link: https://github.com/alphacrack/readme2demo/issues/43  

## Why I Chose This Issue

I chose this issue because it is a small, well-scoped documentation cleanup task that fits the Week 6 / Cycle 2 Phase I requirements. The issue is labeled `documentation` and `good first issue`, has no assignee, and has no linked pull request, which makes it a claimable issue for a new contribution cycle.

This issue also matches my current skills because it focuses on reading project documentation, checking consistency, and making careful updates to README and changelog files. After working on a much larger C++ project in Cycle 1, I wanted my second cycle to start with a smaller Python-related repository where I can move more steadily through the open source process.

## Problem Summary

The project documentation currently has stale and contradictory test-count claims. The README says there are 175 unit tests, while the step-by-step guide says there are 163 tests, but the issue says the current suite has 252 test functions. The CHANGELOG footer is also stale because the `[Unreleased]` link still compares `v0.4.1...HEAD` and there are no link entries for version `0.5.0`.

This matters because README and guide documentation should stay accurate for new users and contributors. Since readme2demo is a tool focused on keeping README content reliable, fixing stale claims in its own documentation is especially relevant.

## Issue Selection Checklist

| Check | Result |
|---|---|
| I understand the problem | Yes — stale test counts and changelog links need to be updated |
| Scope fits 3–4 weeks | Yes — the issue points to three specific files |
| Matches my skills | Yes — documentation cleanup and basic verification |
| Active and claimable | Yes — open, no assignee, no linked PR |
| Helpful context exists | Yes — issue lists exact files and suggested fix |
| Setup docs available | Yes — repository has README and project files to inspect |

## Initial Plan

For Phase II, I plan to clone my fork, inspect the files named in the issue, and verify the current test count using the project’s test collection command if setup works locally. Then I will document reproduction steps, expected versus actual documentation behavior, and a small solution plan before making any changes.

Likely files involved:

- `README.md`
- `docs/step-by-step.md`
- `CHANGELOG.md`

## Community Interaction

I commented on the issue to introduce myself and express interest in working on it.

Issue comment: https://github.com/alphacrack/readme2demo/issues/43  

## Phase I Completion Notes

For Week 6, I selected a new issue for Cycle 2, forked the project, created this public Contribution README, and documented why the issue is a good fit. This completes Phase I for my second contribution cycle.

---


## Phase II — Reproduce and Plan

## Phase II — Reproduce and Plan

Status: Phase II Complete

### Working Branch

Fork: https://github.com/rithikasridharbabu-2007/readme2demo  
Branch: `fix-stale-doc-test-counts`

I cloned my fork locally and created a working branch for the issue.

```bash
git clone https://github.com/rithikasridharbabu-2007/readme2demo.git
cd readme2demo
git checkout -b fix-stale-doc-test-counts
```

### Environment Setup

I set up the project locally on macOS. My first attempt used the default `python3`, which pointed to Python 3.14.6. Creating the virtual environment failed because `ensurepip` returned a non-zero exit status, so `.venv/bin/activate` was not created.

I checked the available Python versions and found Python 3.11 installed at `/opt/homebrew/bin/python3.11`. I then recreated the virtual environment with Python 3.11, activated it, upgraded pip, and installed the project in editable development mode.

```bash
/opt/homebrew/bin/python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install -U pip
python -m pip install -e ".[dev]"
```

Result: setup succeeded with Python 3.11.15.

### Reproduction Steps

1. Clone the fork and create a working branch.
2. Search the files named in the issue for stale test-count references:

   ```bash
   grep -n "175\|163\|252\|test" README.md docs/step-by-step.md CHANGELOG.md
   ```

3. Confirm that `README.md` says:

   ```text
   python -m pytest tests/ -q            # 175 unit tests, no docker/network needed
   ```

4. Confirm that `docs/step-by-step.md` says:

   ```text
   run its 163-test suite
   ```

   and:

   ```text
   You should see all 163 tests pass.
   ```

5. Set up a Python 3.11 virtual environment and install the project in editable development mode.
6. Run:

   ```bash
   python -m pytest --collect-only -q
   ```

### Expected vs. Actual Behavior

Expected behavior: The README, step-by-step guide, and CHANGELOG should describe the current project state accurately. Test-count references should either be current or avoid hardcoded numbers that can become stale.

Actual behavior: The documentation contains contradictory stale numbers. `README.md` says 175 unit tests, while `docs/step-by-step.md` says 163 tests. A fresh local collection run reports 277 tests collected, so both documented numbers are outdated.

### Evidence

Relevant stale documentation locations:

- `README.md` line 128: says 175 unit tests
- `docs/step-by-step.md` line 3: says 163-test suite
- `docs/step-by-step.md` line 33: says all 163 tests pass
- `CHANGELOG.md`: footer needs review for stale version comparison links

Local verification:

```text
Python 3.11.15
Successfully installed readme2demo-0.5.0 and development dependencies
277 tests collected in 0.76s
```

### Files Involved

Likely files to update:

- `README.md`
- `docs/step-by-step.md`
- `CHANGELOG.md`

### Root Cause

The root cause is documentation drift. The project’s test suite grew over time, but the README and step-by-step guide kept old hardcoded test-count numbers. The CHANGELOG footer also appears to have stayed on older version-link references instead of being updated for the current release.

### UMPIRE Plan

#### Understand

The issue is not a code behavior bug. It is a documentation accuracy issue. The project currently has stale test counts in multiple docs and stale CHANGELOG comparison links.

#### Map

The issue points to three main files:

- `README.md`
- `docs/step-by-step.md`
- `CHANGELOG.md`

The README and step-by-step guide contain hardcoded test counts. The CHANGELOG needs version footer link updates.

#### Plan

I will remove or update hardcoded test-count language so the docs do not become stale again. I will prefer wording like “the full test suite” or “250+ tests” instead of exact counts unless the maintainer clearly prefers exact numbers. I will also update the CHANGELOG footer so `[Unreleased]` compares from `v0.5.0...HEAD` and add a `0.5.0` link entry if missing.

#### Implement

For Phase III, I plan to update the documentation files only. I will avoid unrelated formatting changes and keep the diff small.

#### Review

I will run a text search again to make sure stale `175` and `163` references are removed or corrected. I will also run `python -m pytest --collect-only -q` again to confirm the current collected test count and run formatting/lint commands if the project documents them.

#### Evaluate
The fix will be complete when the README and step-by-step guide no longer contradict the current test collection count, the CHANGELOG footer points to the correct comparison ranges, and the final diff is limited to the documentation issue.

## Phase III — Build

Status: Phase III Complete

### Implementation Summary

For Phase III, I implemented the documentation cleanup for the stale test-count issue in `readme2demo`.

The change removes outdated hardcoded test-count references from the README and step-by-step guide, replacing them with wording that is less likely to become stale. I also updated the CHANGELOG footer so the `[Unreleased]` comparison starts from `v0.5.0...HEAD` and added a `[0.5.0]` comparison link.

### Branch and Commit

Fork: https://github.com/rithikasridharbabu-2007/readme2demo  
Branch: `fix-stale-doc-test-counts`  
Commit: `f82ee3d Fix stale documentation test counts`

### Files Modified

- `README.md`
- `docs/step-by-step.md`
- `CHANGELOG.md`

### What Changed

In `README.md`, I changed the development test command comment from:

```text
175 unit tests, no docker/network needed
```

to:

```text
full test suite, no docker/network needed
```

In `docs/step-by-step.md`, I changed references to the “163-test suite” and “all 163 tests pass” to refer to the full test suite instead.

In `CHANGELOG.md`, I updated the link footer from:

```text
[Unreleased]: https://github.com/alphacrack/readme2demo/compare/v0.4.1...HEAD
```

to:

```text
[Unreleased]: https://github.com/alphacrack/readme2demo/compare/v0.5.0...HEAD
```

and added:

```text
[0.5.0]: https://github.com/alphacrack/readme2demo/compare/v0.4.1...v0.5.0
```

### Testing and Verification

I ran test collection after the documentation changes:

```bash
python -m pytest --collect-only -q
```

Result:

```text
277 tests collected in 0.16s
```

I also ran a ruff check on the changed documentation paths:

```bash
ruff check README.md docs/step-by-step.md CHANGELOG.md || true
```

Result:

```text
warning: No Python files found under the given path(s)
All checks passed!
```

I also confirmed that the stale `175` and `163` references were removed from the changed documentation files.

### Challenges Faced

The main challenge was making sure the fix stayed small and matched the issue exactly. Since this was a documentation issue, I avoided changing unrelated content or code. I also chose “full test suite” instead of another exact number so the documentation is less likely to become stale again as tests are added.

### Phase III Completion Notes

This completes the build phase for Cycle 2. The implementation is committed and pushed to my fork branch, and the next step is to open an upstream pull request for Phase IV.

## Phase IV — Submit and Iterate

Status: Not started yet.
