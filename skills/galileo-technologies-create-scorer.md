---
name: Create and validate a custom LLM scorer/metric
description: Define a custom Galileo scorer, add an LLM scorer version, and validate it before use in evaluations.
api: openapi/galileo-technologies-openapi-original.json
operations:
  - create_scorers_post
  - create_llm_scorer_version_scorers__scorer_id__version_llm_post
  - manual_llm_validate_scorers_llm_validate_post
---

# Create and validate a custom LLM scorer/metric

Use this skill to author a custom LLM-as-a-judge metric in Galileo.

## Auth
- Send your API key in the `Galileo-API-Key` header. Base URL: `https://api.galileo.ai`.

## Steps
1. **Create the scorer** — `POST /scorers` (`create_scorers_post`). Save `scorer_id`.
2. **Add an LLM scorer version** — `POST /scorers/{scorer_id}/version/llm` (`create_llm_scorer_version_scorers__scorer_id__version_llm_post`) with the judge prompt, model, and output config.
3. **Validate** — `POST /scorers/llm/validate` (`manual_llm_validate_scorers_llm_validate_post`) with sample inputs to confirm the scorer produces a well-formed rating before wiring it into experiments or log-stream metrics.

## Conventions
- Scorers are versioned; reference a specific version from experiments/log streams.
- Errors use the FastAPI `{detail}` envelope; 422 returns `HTTPValidationError`.
- Code scorers have a parallel validate flow (`/scorers/code/validate`).
