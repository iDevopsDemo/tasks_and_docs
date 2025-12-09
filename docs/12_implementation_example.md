# Implementation examples

## Github Actions CI/CD Pipeline

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up JDK 11
        uses: actions/setup-java@v1
        with:
          java-version: '11'

      - name: Build with Gradle
        run: ./gradlew build

      - name: Run tests
        run: ./gradlew test

      - name: Publish to Artifactory
        uses: jfrog/artifactory-github-action@v1
        with:
          artifactory_url: ${{ secrets.ARTIFACTORY_URL }}
          artifactory_user: ${{ secrets.ARTIFACTORY_USER }}
          artifactory_password: ${{ secrets.ARTIFACTORY_PASSWORD }}
          file: build/libs/*.jar
          target: libs-release-local
```