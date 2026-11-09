# Copilot Critique: Missing-Field Test

**Date:** November 9, 2026
**Author:** Angela Jeske

## What I asked for

One test: a POST to /api/quote with no `coverageAmount` returns 400.

## Result

9 tests, 9 pass, 0 fail (up from 8 before the Copilot test).

## Critique

Copilot got the structure right: it matched the file's existing pattern, sent a request with no `coverageAmount`, and asserted a 400. The suite went from 8 to 9 passing tests, so it works. What it missed is precision: it checks only the status code, not that the error names `coverageAmount`, so any validation failure would satisfy it. I would ship it, with that gap noted as a possible improvement. What checks Copilot's output is the same safety net that caught Tuesday's AI-drafted premium bug: the test suite, run again by CI on every push.
