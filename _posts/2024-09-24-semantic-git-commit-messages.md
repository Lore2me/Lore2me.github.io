---
layout: post
title: Semantic Git Commit Messages
date: 2024-09-24 10:57 +0200
categories: [Coding, Versioning, Git]
tags: [Versioning, Semantic Commit Messages, Git]
description: "Semantic Git Commit Messages is a must for every project."
---
# Semantic Git Commit Messages
Semantic Git Commit Messages is a must for every project and in this post I will explain why.

## What is a Semantic Git Commit Message?
A semantic Git commit message follows a specific format that allows for better understanding of the changes that were made in a commit. The format is as follows:

```
<type>(<scope>): <subject>

<scope> is optional
```

Following types are allowed:
- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc -> no production code change)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **test**: Adding missing tests or correcting existing tests
- **chore**: Changes to the build process or auxiliary tools and libraries such as documentation generation

## Why use Semantic Git Commit Messages?
Semantic Git Commit Messages provide a lot of benefits to a project. Some of the key benefits are:
- **Easier to maintain**: By using specific types, it is easier to understand what changes were made in a commit. This makes it easier to maintain the codebase.
- **Easier to search**: By using specific types, it is easier to search for commits that are related to a specific type of change.
- **Easier to generate changelogs**: By using specific types, it is easier to generate changelogs that are meaningful and easy to understand.
- **Analyze the development** of the project in github or gitlab by the commits by type and scope
- **Analyze developer behavior** to see who is working on what and how much work is being done by each developer. (it is not recommended to use this to evaluate developer performance)

## Use automated tools
There are automated tools such as conventional commits that can help you enforce the format of your commit messages. These tools can be integrated into your workflow to ensure that all commits follow the format.

Or you can use a git hook to enforce the format of your commit messages. You can create a pre-commit hook that checks the format of the commit message and rejects the commit if it does not follow the format.

## Conclusion
Semantic Git Commit Messages are a must for every project. They provide a lot of benefits and make it easier to maintain, search, and generate changelogs. By following the format, you can improve the quality of your commits and make it easier for others to understand the changes that were made in a commit.

