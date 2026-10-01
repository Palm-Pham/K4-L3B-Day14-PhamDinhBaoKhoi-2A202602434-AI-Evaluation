# Task 1 / CP1 Completion Report

Completed Task 1 — Data Models, following the CP1 requirements in CHECKPOINTS.md and the lab's README.md, SUBMISSION.md, RUBRIC.md, and RULES.md.

## Changes

| File | Changes |
|---|---|
| `template.py` | Implemented the `QAPair` and `EvalResult` dataclass fields with type hints. Implemented `EvalResult.overall_score()`. |
| `solution/solution.py` | Applied the same Task 1 implementation because the existing solution file takes priority in the test suite. |
| `CP1_REPORT.md` | Added this completion and validation report. |

`QAPair` now stores `question`, `expected_answer`, `context`, `metadata`, and `retrieved_contexts`. Context defaults to an empty string. Metadata and retrieved contexts use `field(default_factory=...)`, so separate instances do not share mutable containers.

`EvalResult` now stores the original QA pair, actual answer, faithfulness, relevance, completeness, pass status, optional failure type, and optional retrieval scores. Failure type and retrieval scores default to `None`.

`overall_score()` returns `(faithfulness + relevance + completeness) / 3.0`. Context recall and context precision remain diagnostic fields and do not contribute to this average.

Class names, function names, and existing method signatures were preserved. Tests and later-task implementations were not changed.

## Validation

- Before implementation, the three CP1 tests failed because `QAPair` had no fields.
- `.venv/bin/pytest tests/test_solution.py::TestEvalResultOverallScore -v`: **3 passed** after implementation.
- Direct checks on both implementation files passed for default values, independent mutable containers, and exclusion of retrieval scores from the overall average.
- `.venv/bin/pytest tests/ -q --tb=no`: **3 passed, 39 failed**, matching the documented full-suite result after Task 1. Remaining failures belong to unfinished later tasks and the bonus test's prerequisites.

CP1 is complete. The entire lab is not yet complete; subsequent checkpoints remain pending. No API calls were needed for this task.
