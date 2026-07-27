---
name: Run an offline evaluation experiment on a dataset
description: Create a dataset, populate it, and run a Galileo experiment to evaluate an AI application against metrics.
api: openapi/galileo-technologies-openapi-original.json
operations:
  - create_dataset_datasets_post
  - upsert_dataset_content_datasets__dataset_id__content_put
  - create_experiment_projects__project_id__experiments_post
  - get_experiment_metrics_projects__project_id__experiments__experiment_id__metrics_post
---

# Run an offline evaluation experiment on a dataset

Use this skill to evaluate a prompt/agent offline against a dataset in Galileo.

## Auth
- Send your API key in the `Galileo-API-Key` header. Base URL: `https://api.galileo.ai`.

## Steps
1. **Create a dataset** — `POST /datasets` (`create_dataset_datasets_post`). Save `dataset_id`.
2. **Add rows** — `PUT /datasets/{dataset_id}/content` (`upsert_dataset_content_datasets__dataset_id__content_put`) with your input/expected records.
3. **Create the experiment** — `POST /projects/{project_id}/experiments` (`create_experiment_projects__project_id__experiments_post`) referencing the dataset and the scorers/metrics to run.
4. **Read results** — `POST /projects/{project_id}/experiments/{experiment_id}/metrics` (`get_experiment_metrics_projects__project_id__experiments__experiment_id__metrics_post`) to fetch computed metric values.

## Conventions
- You need a `project_id` first (see the trace-logging skill's create-project step).
- Errors use the FastAPI `{detail}` envelope; 422 returns `HTTPValidationError`.
- Long-running metric computation may be asynchronous — poll the metrics endpoint.
