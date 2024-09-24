---
layout: post
title: Semantic Versioning
date: 2024-09-24 10:22 +0200
categories: [Coding, Versioning, Git]
tags: [Versioning, Semantic Versioning]
description: "Semantic Versioning is a must for every project."
---
# Semantic Versioning

Semantic Versioning is a must for every project.
It helps you communicate changes in your project in a clear and consistent way.
By following Semantic Versioning,
you can easily convey the impact of changes in your project to your users and other developers.
The benefits of Semantic Versioning is that it helps you avoid confusion and miscommunication,
and it makes it easier for you to manage dependencies in your project.

In general, every software developer should understand and be able to use semantic versioning,
to facilitate the use of software libraries and frameworks and to be able to familiarize themselves with a project more quickly.

## What is Semantic Versioning?
Semantic Versioning is a versioning scheme that defines how version numbers are assigned and incremented.

It works as follows:
- Given a version number MAJOR.MINOR.PATCH,
  increment the:
  - MAJOR version when you make incompatible API changes
  - MINOR version when you add functionality in a backwards-compatible manner
  - PATCH version when you make backwards-compatible bug fixes

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Example
For example, if you have a project with the version number `1.2.3`,
and you make a backwards-compatible bug fix,
you should increment the PATCH version to `1.2.4`.

If you add new functionality in a backwards-compatible manner,
you should increment the MINOR version to `1.3.0`.

If you make incompatible API changes,
you should increment the MAJOR version to `2.0.0`.

## Further Reading
- [Semantic Versioning 2.0.0](https://semver.org/)
