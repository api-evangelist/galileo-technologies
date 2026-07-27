---
name: Configure a log-stream alert with a generic webhook
description: Set up alert settings and an alert config on a Galileo log stream so triggered alerts POST to a generic webhook.
api: openapi/galileo-technologies-openapi-original.json
operations:
  - create_or_update_alert_settings_projects__project_id__log_streams__log_stream_id__alert_settings_post
  - create_projects__project_id__log_streams__log_stream_id__alerts_post
  - send_test_generic_webhook_projects__project_id__log_streams__log_stream_id__alert_settings_test_post
---

# Configure a log-stream alert with a generic webhook

Use this skill to get notified via an outbound webhook when a Galileo log stream trips an alert condition.

## Auth
- Send your API key in the `Galileo-API-Key` header. Base URL: `https://api.galileo.ai`.

## Steps
1. **Configure alert settings (webhook target)** — `POST /projects/{project_id}/log_streams/{log_stream_id}/alert_settings` (`create_or_update_alert_settings_projects__project_id__log_streams__log_stream_id__alert_settings_post`) with your generic webhook URL.
2. **Create an alert config** — `POST /projects/{project_id}/log_streams/{log_stream_id}/alerts` (`create_projects__project_id__log_streams__log_stream_id__alerts_post`) defining the condition/metric threshold.
3. **Send a test** — `POST /projects/{project_id}/log_streams/{log_stream_id}/alert_settings/test` (`send_test_generic_webhook_projects__project_id__log_streams__log_stream_id__alert_settings_test_post`) to verify your endpoint receives the payload.

## Conventions
- Requires an existing `project_id` and `log_stream_id`.
- Webhook alert support shipped 2026-07-07; the delivery is an outbound generic webhook (Galileo POSTs to your URL).
- Errors use the FastAPI `{detail}` envelope; 422 returns `HTTPValidationError`.
