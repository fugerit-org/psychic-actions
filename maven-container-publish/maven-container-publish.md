# Maven container build and publish GitHub action

[![back to index](https://img.shields.io/badge/back-to%20index-teal.svg)](../README.md)

This action executes a project maven build, docker build and push (if enabled).

## parameters

| parameter          | required | default            | description                |
|--------------------|----------|--------------------|----------------------------|
| github-token       | true     |                    | Github authorization token |
| java-type          | true     | 'openjdk'          | deprecated (1), (2)        |
| java-version       | true     | '21'               | Java version               |
| java-description   | true     | 'corretto'         | Java distribution          |
| maven-version      | true     | '3.9.6'            | Maven version              |
| maven-options      | true     | '-B clean package' | Maven goals and options    |
| node-version       | true     | '20'               | Node version               |
| docker-context     | true     | '.'                | Docker context             |
| docker-file        | true     | 'Dockerfile'       | Docker file                |
| docker-tags        | true     | 'latest'           | Comma separated image tags |
| docker-platforms   | true     | 'linux/amd64'      | Comma separated platforms  |
| dockerhub-username | false    |                    | Docker hub username (3)    |
| dockerhub-password | false    |                    | Docker hub password (3)    |


## notes

- (1) , (2) <https://github.com/graalvm/setup-graalvm> is not used anymore, as now graalvm is handled by <https://github.com/actions/setup-java>
- (3) image push will be done only if **dockerhub-username** or **dockerhub-password** are both set

## versions

Aside project versions there is a floating stable tag available : **mcp**

## example

- [CI maven container publish test latest](../.github/workflows/maven-container-publish-latest.yml)

```yaml
# CI with maven container publish
#
# version 1.0.0

name: CI maven container publish latest

on:
  # Trigger analysis when pushing in master or pull requests, and when creating
  # a pull request.
  push:
    branches:
      - main
      - develop
      - branch-preview
      - 1-action-for-maven-build-container-build-and-publish
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
      - uses: fugerit-org/psychic-actions/maven-container-publish@mcp
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          java-type: 'native'
          java-version: '22-ea'
          java-distribution: 'graalvm'
          docker-file: 'src/test/docker/Dockerfile.jvm'
```