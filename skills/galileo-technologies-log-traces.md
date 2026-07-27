---
name: Log LLM traces to a Galileo log stream
description: Create a project and log stream, then log generative-AI traces to Galileo for observability and evaluation.
api: openapi/galileo-technologies-openapi-original.json
operations:
  - create_project_projects_post
  - create_log_stream_projects__project_id__log_streams_post
  - log_traces_projects__project_id__traces_post
  - get_trace_projects__project_id__traces__trace_id__get
---

# Log LLM traces to a Galileo log stream

Use this skill to send production or development traces from a generative-AI app to Galileo.

## Auth
- Send your API key in the `Galileo-API-Key` header on every request. Base URL: `https://api.galileo.ai`.
- Keys are created at https://app.galileo.ai/settings/api-keys.

## Steps
1. **Create a project** — `POST /projects` (`create_project_projects_post`). Save the returned `project_id`.
2. **Create a log stream** — `POST /projects/{project_id}/log_streams` (`create_log_stream_projects__project_id__log_streams_post`). Save the `log_stream_id`.
3. **Log traces** — `POST /projects/{project_id}/traces` (`log_traces_projects__project_id__traces_post`) with your trace/span payloads, targeting the log stream.
4. **Verify** — `GET /projects/{project_id}/traces/{trace_id}` (`get_trace_projects__project_id__traces__trace_id__get`) to read a logged trace back.

## Conventions
- List/query endpoints paginate with `starting_token` + `limit`.
- Errors follow the FastAPI envelope: `{ "detail": ... }`; validation errors return `HTTPValidationError` with a `detail[]` list.
- No idempotency-key contract is published — do not assume safe retries on writes.
