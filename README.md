# GitHub Actions

[![Build](https://github.com/DevSecOpsSamples/githubactions/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/DevSecOpsSamples/githubactions/actions/workflows/build.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=DevSecOpsSamples_githubactions&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=DevSecOpsSamples_githubactions) [![Lines of Code](https://sonarcloud.io/api/project_badges/measure?project=DevSecOpsSamples_githubactions&metric=ncloc)](https://sonarcloud.io/summary/new_code?id=DevSecOpsSamples_githubactions)

## Overview

Provides GitHub Workflow and Action samples.

## Sample Repositories

| Repository                          | Workflow File | Actions | Description | Plugins |
|---|--------------------------------|------|--------------------------------|---------------|
| gke-workload-identity | [build.yml](https://github.com/DevSecOpsSamples/gke-workload-identity/blob/master/.github/workflows/build.yml)     | [actions](https://github.com/DevSecOpsSamples/gke-workload-identity/actions/workflows/build.yml) | GCP, gcloud, Docker, Terraform <br/> Python, pytest, publish unittest result, Sonarqube  | hashicorp/setup-terraform@v2.0.3 <br/>jacobtomlinson/gha-find-replace@v2 <br/> actions/github-script@v6 <br/>actions/setup-java@v1 <br/>actions/setup-python@v4 <br/> google-github-actions/auth@v1 <br/> EnricoMi/publish-unit-test-result-action/composite@v2 <br/> actions/cache@v3 <br/> |
| jenkins-fargate-cdk   | [build.yml](https://github.com/DevSecOpsSamples/jenkins-fargate-cdk/blob/master/.github/workflows/build.yml)     | [actions](https://github.com/DevSecOpsSamples/jenkins-fargate-cdk/actions/workflows/build.yml) | Docker, CDK, Sonarqube | |

## Docker

- Build multi-platform docker image files: [docker-buildx-gcr.yml](docker-buildx-gcr.yml)

## Cache

- Optimize build speed using the `cache` plugin: [java/README.md](java/README.md)

    [java/.github/workflows/build-java.yml](java/.github/workflows/build-java.yml)

    [java/.github/workflows/build-java-sonarqube.yml](java/.github/workflows/build-java-sonarqube.yml)

## Matrix

- [gke-workload-identity](https://github.com/DevSecOpsSamples/gke-workload-identity/blob/master/.github/workflows/build.yml)

## Terraform

- [terraform.yml](terraform.yml)

    <details><summary>Terraform Plan</summary>

    ![terraform-plan.png](./screenshots/terraform-plan.png?raw=true)

    </details>

## Python Unittest

- [python-unittest.yml](python-unittest.yml) [setup.cfg](setup.cfg)

    <details><summary>Unittest Results</summary>

    ![test-failed.png](./screenshots/test-failed.png?raw=true)

    ![test-failed-details.png](./screenshots/test-failed-details.png?raw=true)

    </details>

## Plugins

| Plugin      |  Description                   |
|-------------|--------------------------------|
| [actions/setup-java@v3](https://github.com/actions/setup-java) |  |
| [actions/setup-python@v4](https://github.com/actions/setup-python) |  |
| [actions/cache@v3](https://github.com/actions/cache) |  |
| [actions/github-script@v6](https://github.com/actions/github-script) |  |
| [hashicorp/setup-terraform@v2.0.3](https://github.com/hashicorp/setup-terraform) | |
| [jacobtomlinson/gha-find-replace@v2](https://github.com/jacobtomlinson/gha-find-replace) | Find and Replace Action |
| [google-github-actions/auth@v1](https://github.com/google-github-actions/auth) |  GitHub Action authenticates to Google Cloud |
| [EnricoMi/publish-unit-test-result-action/composite@v2](https://github.com/EnricoMi/publish-unit-test-result-action) |  Publish Test Results |

## Dispatch

```bash
cp .github/workflows/dispatch-request-exmple.json request-body.json
cat request-body.json

curl -d @request-body.json \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  -H "Authorization: Bearer <your-token>" \
  https://github.com/DevSecOpsSamples/githubactions/actions/workflows/dispatch-example.yml/dispatches
```

develop branch:

[.github/workflows/dispatch-request-exmple.json](.github/workflows/dispatch-request-exmple.json)

```json
{ 
   "ref": "develop",
    "inputs": {
        "test-url-tag": "gcr.io/project-id/source-image:2650c2f7c04640b8c67df560510914f7ba2033e2",
        "prod-url": "gcr.io/project-id/target-image"
    }
}
```

master branch:

```json
{ 
   "ref": "develop",
    "inputs": {
        "test-url-tag": "gcr.io/project-id/source-image:2650c2f7c04640b8c67df560510914f7ba2033e2",
        "prod-url": "gcr.io/project-id/target-image"
    }
}
```


## Reference

- [GitHub Actions /Using workflows / Cache dependencies / Caching dependencies to speed up workflows](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows#managing-caches)

- https://github.com/actions/cache

- https://github.com/actions/cache/blob/main/examples.md#java---gradle

- https://docs.github.com/en/rest/actions/workflows?apiVersion=2022-11-28#create-a-workflow-dispatch-event
