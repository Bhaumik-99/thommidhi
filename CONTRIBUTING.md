# Contributing

Contributions should expand evaluation coverage or improve evidence quality without overstating what the suite proves.

## Add a scenario

1. Add one JSON object per line to `cases.jsonl` with a new stable ID (`E21`, `E22`, and so on).
2. Include a realistic user request, expected call sequence, required arguments, and prohibited actions. Use tool names in `tool_catalog.json`; document any verified schema change before depending on it.
3. Include the important safety boundary. Read-only requests should explicitly forbid relevant write tools.
4. When the request lacks information required to call a tool safely, encode the expected no-call behavior and explain the clarification needed in `expected_outcome`.
5. Add a focused unit test for new parser or scoring behavior.

## Run checks locally

```bash
python -m py_compile score_eval.py
python -m unittest discover -s tests -v
python score_eval.py --cases cases.jsonl --transcript transcripts/synthetic_fixture.json --out /tmp/smoke-results.json --summary-only
```

## Trace and privacy standards

- Use synthetic names and placeholder IDs in committed fixtures.
- Never commit credentials, tokens, private rate floors, personal information, or unredacted brand communications.
- Label synthetic fixtures as synthetic and report-derived summaries as summaries; neither is a raw execution trace.
- Do not mark a case as passed when its raw trace is missing. Preserve `INCONCLUSIVE` and `null` metrics when evidence is unavailable.
- For writes, distinguish an attempted tool call from a confirmed persisted change. Record independent read-back evidence separately.
- Do not run mutating tests against a real creator deal desk to manufacture a passing example.
