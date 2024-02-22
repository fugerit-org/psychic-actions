# Maven build and scan GitHub action

This action executes a project build and scan with sonar (if enabled).


## parameters

| parameter                           | required | default    | description                                        |
|-------------------------------------|----------|------------|----------------------------------------------------|
| github-token                        | false    |            | Github authorization token                         |
| sonar-token                         | false    |            | Sonar authorization token                          |
| snyk-token                          | false    |            | Snyk authorization token                           |
| snyk-dockercontext                  | false    |            | Docker context folder                              |
| snyk-dockertag                      | false    |            | Docker tag name                                    |
| snyk-image                          | false    |            | Snyk image parameter                               |
| snyk-args                           | false    |            | Snyk args parameter                                |
| java-version                        | true     | '17'       | Java version                                       |
| java-description                    | true     | 'corretto' | Java distribution                                  |
| maven-version                       | true     | '3.9.6'    | Maven version                                      |
| maven-additional-profiles           | false    |            | Additional maven profiles, should start with comma |
| node-version                        | true     | '20'       | Node version                                       |
| disable-maven-dependency-submission | true     | 'false'    | Disable maven dependency submission                |


## steps

| step                                                 | note                                                          |
|------------------------------------------------------|---------------------------------------------------------------|
| actions/checkout                                     |                                                               |
| actions/setup-java                                   |                                                               |
| actions/cache                                        |                                                               |
| actions/setup-node                                   |                                                               |
| Build and analyze                                    | if ${github-token} and ${sonar-token} are both set            |
| Build only                                           | if ${github-token} or ${sonar-token} are not set              |
| Build a Docker image                                 | if ${snyk-dockercontext} and ${snyk-dockertag} are both set   |
| snyk/actions/docker                                  | if ${snyk-token} , ${snyk-image} and ${snyk-args} are all set |
| github/codeql-action/upload-sarif                    | if ${snyk-token} , ${snyk-image} and ${snyk-args} are all set |
| advanced-security/maven-dependency-submission-action | if ${disable-maven-dependency-submission } is not 'true'      |


## example

Some examples can be found in this project test workflows : 

- [CI maven build and scan test latest](../.github/workflows/maven-build-scan-test-latest.yml)
- [CI maven build only](../.github/workflows/maven-build-scan-test-build-only.yml)
- [CI maven build only (java 8)](../.github/workflows/maven-build-scan-test-build-only-8.yml)

```yaml
# CI with maven build and scan
#
# version 1.0.0

name: CI maven build and scan test latest

on:
  # Trigger analysis when pushing in master or pull requests, and when creating
  # a pull request.
  push:
    branches:
      - main
      - develop
      - branch-preview
  pull_request:
    types:
      - opened
      - synchronize
      - reopened

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - uses: fugerit-org/psychic-actions/maven-build-scan@main
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          sonar-token: ${{ secrets.SONAR_TOKEN }}
          disable-maven-dependency-submission: ${{ vars.DISABLE_MAVEN_DEPENDENCY_SUBMISSION }}
```