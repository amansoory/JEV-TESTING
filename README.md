# Jev CI investigator test repository

This repository is a deliberately small public test target for the Jev CI investigator. The workflow is manually triggered and has three selectable failure scenarios. It contains no secrets and is not intended for production use.

## Run a scenario

In GitHub, open **Actions → Jev CI investigator failure scenarios → Run workflow**, choose a scenario, and start it. The workflow is intentionally failing.

Expected evidence:

| Scenario | Expected failing steps | Expected relationship |
| --- | --- | --- |
| `assertion-cleanup` | `Run assertions`; `Cleanup report` | The assertion error is the first observed failure. `Cleanup report` explicitly says it cannot write the report because `Run assertions` did not complete. |
| `build-tests` | `Compile application`; `Run test suite` | The compiler error is the first observed failure. `Run test suite` explicitly says it could not run because `Compile application` failed. |
| `independent` | `Run lint checks`; `Run integration tests` | These are separate substantive errors: an unused variable and a refused database connection. Neither message attributes one to the other; they must remain separate/ambiguous rather than forming a causal chain. |

The harmless output before each substantive error and the final informational message are included to make log source selection inspectable. The exact GitHub log line numbers include runner-generated prefixes and may vary; match the distinctive error text above.
