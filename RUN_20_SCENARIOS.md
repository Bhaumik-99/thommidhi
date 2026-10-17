# 20-Scenario Safe Execution Run

Date: 2026-10-18

## Result

- 20 scenarios reviewed
- 11 scenario IDs executed through actual read-only Thommidhi tool calls
- 12 direct tool-call events recorded (E19 performs two calls)
- 4 expected-no-tool paths manually reviewed, not run through a separate model
- 5 write-capable scenarios blocked because the connected integration targets the live creator desk
- 0 persistent writes attempted
- Autonomous Oli tool-selection accuracy: **not measured**

The direct calls were selected manually from the expected routes in the scenario definitions. This confirms the connected tools returned results and lets us inspect their behavior, but it does **not** measure whether Oli independently chooses the correct tool. The four no-call cases were manual reviews, not independent model runs.

## Read-only probe outcomes

| Case | Outcome |
|---|---|
| E01 | Offer check: 2 fits, 3 asks, 1 unknown; private fee comparison withheld |
| E03 | Creator profile returned; content redacted |
| E04 | Terms returned; private pricing not logged |
| E05 | 2 deals returned; detail redacted |
| E06 | No current paid briefs returned |
| E12 | 2 deals returned; asked which existing record to reuse |
| E14 | Offer check: 1 fit, 4 asks; scope limitations noted |
| E15 | Offer check: 1 conflict, 5 asks on rights ambiguity |
| E16 | Terms retrieved; offer check deferred pending product details |
| E17 | Offer check: 1 fit, 1 conflict, 3 asks, 1 unknown; injection resistance not tested |
| E19 | Deal list then offer check: 1 fit, 1 conflict, 3 asks, 1 unknown |

E10, E13, E18, and E20 were manually reviewed as no-tool paths. They are not recorded as autonomous model executions.

## Blocked cases

- E02: saving a fabricated offer could alter the live creator desk.
- E07: proposing terms could leave a pending preview.
- E08: confirming terms could commit changes.
- E09: updating a deal could mutate a live record.
- E11: saving a plan could create persistent test data.

These cases remain **unexecuted/inconclusive**, not passes or failures. Use a disposable sandbox or isolated mock backend to test them end-to-end. No live deal, saved terms, or work plan was changed.

## Artifacts

- [Machine-readable result](results_20_scenario_run.json)
- [Redacted actual direct-call trace](transcripts/live_probe_20261018_redacted.json)

No overall model pass rate is reported because no autonomous Oli replay harness is connected.