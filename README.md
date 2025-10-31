# Authenticate to Google Cloud from Buildkite

[![usages](https://img.shields.io/badge/usages-white?logo=buildkite&logoColor=blue)](https://github.com/search?q=elastic%2Foblt-google-auth+%28path%3A.buildkite%29&type=code)

This is an opinionated plugin to authenticate to any Google Cloud project from Buildkite using [Workload Identity Federation](https://cloud.google.com/iam/docs/workload-identity-federation).
The Workload Identity Provider uses a hash for the GitHub repository with the format `owner/repo`, the
hash has a length of 28 characters.

## Properties

| Name                  | Description                                                                                           | Required | Default                 |
|-----------------------|-------------------------------------------------------------------------------------------------------|----------|-------------------------|
| `lifetime`            | The time (in seconds) the OIDC token will be valid for before expiry. Must be a non-negative integer. | `false`  | `1800`                  |
| `project-id`          | The GCP project id.                                                                                   | `false`  | `elastic-observability` |
| `project-number`      | The GCP project number.                                                                               | `false`  | `8560181848`            |
| `use-service-account` | Flag to generate and use a temporarly service account credentials                                     | `false`  | `false`                 |
| `slack-channel`       | Slack channel on which to receive notifications                                                       | `false`  | `#observablt-bots`      |

## Usage

```yml
steps:
  - command: |
      echo "Credentials are located at \$GOOGLE_APPLICATION_CREDENTIALS"
      gcloud container clusters list
    plugins:
      - elastic/oblt-google-auth#v1.3.0:
          lifetime: 1800 # seconds
          # project-id: "elastic-observability"
          # project-number: "8560181848"
          # use-service-account: false
          # slack-channel: "#observablt-bots"
```

## Requirements

This plugin needs the following requirements:

- bash
- buildkite-agent
- gcloud  *(Optional)*

>>>
> [!IMPORTANT]
> `gcloud` dependency is required only if `use-service-account` flag is set to `true`
>>>