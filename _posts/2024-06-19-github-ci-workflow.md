---
layout: post
title: GitHub CI workflow
date: 2024-06-19 10:18 +0200
categories: [Knowledge, Coding, DevOps]
tags: [coding, java, github, ci, spring-boot, maven]
description: "In this post we look at a simple GitHub CI workflow for a Java project."
---
For a Github repository, you can create a simple CI workflow by adding a file in the `.github/workflows` directory. This file should be a YAML file with a name that ends in `.yml`. For example, `.github/workflows/workflow.yml`.

Here is an example of a simple CI workflow for a Java project:

```yaml
name: Build and Test Java Spring Boot Application with Maven
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - name: Setup JDK 21
        uses: actions/setup-java@v4
        with:
          java-version: '21'
          distribution: 'adopt'
          cache: maven

      - name: Build with Maven
        run: mvn clean verify
```
It begins with the name of the workflow, `Build and Test Java Spring Boot Application with Maven`. The `on` section specifies when the workflow should run. In this case, it runs on `push` and `pull_request` events on the `main` branch.
Under the section jobs every job is defined.
In this case, there is only one job, `build-and-test`.
It runs on the `ubuntu-latest` runner.
So the steps run on the latest version of Ubuntu.
The steps are:
- `actions/checkout@v4` checks out the repository.
- `actions/setup-java@v4` sets up the JDK. In this case, it sets up JDK 21 from the AdoptOpenJDK distribution and caches Maven. In with you can specify the version of Java and the distribution. Cache can be maven, gradle or none. It's recommended to cache with the same package manager you use in the project.
- `run: mvn clean verify` builds the project with Maven. This command cleans the project and runs the tests.

This is a simple CI workflow for a Java project. You can customize it to fit your project's needs.

### Maven Build Lifecycle
As a reminder, the maven Build Lifecycle is composed of phases. The default phases are:
- `validate` - validate the project is correct and all necessary information is available
- `compile` - compile the source code of the project
- `test` - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- `package` - take the compiled code and package it in its distributable format, such as a JAR.
- `verify` - run any checks on results of integration tests to ensure quality criteria are met
- `install` - install the package into the local repository, for use as a dependency in other projects locally
- `deploy` - done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects
