# Lessons learned

## Problems hit and how they were fixed

| Problem | Fix |
|---|---|
| Decodo requests failing on authentication | Switched to the **Header Auth** credential type |
| Scraping an HTML page was brittle | Moved to the **RemoteOK JSON API** |
| Google Sheets node errors | Fixed mismatched **tab names** between the workflow and the sheet |
| Too many or too few matches | Tuned the **fitScore thresholds** over several runs |
| Free-tier limits on the LLM provider | Migrated scoring: Gemini -> OpenAI `gpt-4o-mini` -> Groq `llama-3.3-70b-versatile` (14,400 requests/day on the free tier) |

## What I would do differently

- Add an evaluation set of hand-labelled listings to measure scoring accuracy, not just eyeball it.
- Log every LLM failure and what fixed it.
- Version the scoring rubric alongside the workflow.
