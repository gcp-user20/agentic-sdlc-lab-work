---
applyTo: "tests/**"
---

# Testing Instructions

## Unit tests

- Call service functions directly with `MagicMock` repositories.
- Do not use a database or make HTTP calls in unit tests.

## Test structure

- Test one behavior per test.
- Name tests `test_<function>_<situation>`.

## Bug fixes

- Start with a test that fails on the current code.
- Never weaken or delete an existing assertion; stop and ask a human instead.
