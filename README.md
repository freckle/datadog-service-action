# datadog-service-action

Validates a `service.datadog.yaml` file located at the root of the repository.

## Example setup

`service.datadog.yaml`:

```yaml
---
schema-version: v2
dd-service: example
repos:
  - name: Source
    provider: github
    url: https://example.com
links:
  - name: About
    type: wiki
    url: https://example.com/wiki/
```

`.github/workflows/datadog.yml`:

```yaml
name: Validate Datadog Service Metadata

on:
  pull_request:
    paths:
      - service.datadog.yaml
      - .github/workflows/datadog.yml

jobs:
  validate-datadog-service-metadata:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
        with:
          sparse-checkout: |
            service.datadog.yaml
      - uses: freckle/datadog-service-action@v1
```
