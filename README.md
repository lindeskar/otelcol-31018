# Persistent Queue in Loki exporter breaks Headers Setter extension

Repo for testing issue: open-telemetry/opentelemetry-collector-contrib#31018

The Loki exporter in combination with the Headers Setter extension seems to break when adding the `sending_queue.storage` config.

## Testing

Run:

```sh
docker-compose down --remove-orphans && docker-compose up
```

Query Loki:

```sh
logcli --org-id foobar query '{exporter="OTLP"}'
```

Enabling `sending_queue.storage` in [otelcol_config.yaml](otelcol_config.yaml) causes:

```txt
otelcol-1       | 2024-02-02T15:14:01.829Z      error   exporterhelper/common.go:95     Exporting failed. Dropping data.        {"kind": "exporter", "data_type": "logs", "name": "loki/loki_gateway", "error": "not retryable error: Permanent error: HTTP 401 \"Unauthorized\": no org id", "dropped_items": 179}
```
