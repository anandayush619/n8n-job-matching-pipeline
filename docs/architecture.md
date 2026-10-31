# Architecture

High-level flow: **Trigger -> Fetch -> Clean -> Score -> Filter -> Dedupe -> Store -> Digest**.

## Node-by-node

| # | Stage | Purpose |
|---|---|---|
| 1 | Schedule trigger | Runs the workflow daily |
| 2 | Decodo request (Header Auth) | Fetches listings from the RemoteOK JSON API |
| 3 | Clean / normalise | Flattens fields and removes unusable listings |
| 4 | LLM scoring | Sends each listing plus my profile to Groq and receives a `fitScore` and short reasoning |
| 5 | Filter | Keeps listings above the `fitScore` threshold |
| 6 | Deduplicate | Compares against rows already in Google Sheets |
| 7 | Google Sheets append | Stores new matches |
| 8 | Gmail digest | Builds and sends the HTML summary |

> TODO: replace this table with the real node names from your exported workflow, and add a canvas screenshot in `assets/`.

## Failure handling

- Missing or malformed LLM output is treated as "not scored" rather than trusted.
- Duplicate listings are skipped before writing to the sheet.
