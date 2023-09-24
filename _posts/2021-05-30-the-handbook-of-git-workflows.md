---
layout: post
title: The Handbook of Git Workflows
subtitle: Empowering a software development with the most suitable git strategies
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - software
  - workflow
  - git
  - note
---

## Introduction

Git and other version control systems give software developers the power to
track, manage, and organize their code. As every developer and development
team has different git workflows, we need to find a way to manage to make our
collaboration smooth during the software development. This handbook is a guide
for you to quickly master them.

![git-workflows](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/ed161d8f-ce60-4863-baae-5dd6aef8a3ef)

## Workflows

Nowadays, software development teams encompass contributors from various
backgrounds and experiences, and they're likely to feel comfortable with a
workflow they've used previously. However, there are many best practices for
modern continuous software development, and they have been used in different
popular open-source projects.

### Git Flow

Git workflows empower teams to determine roles and responsibilities, set
boundaries, and identify areas of improvement.
different features.

![git-flow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/fc8f2f26-50d1-4926-90b6-d6613545f1ea)

Here is the document of git-flow branching strategy:

```sh
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
```

We will keep 2 long-term branches, others are always short-term branches for
feature, bugfix and so on.

For examples:

```md
# Features
* feature/dark-theme-support
* feature/integrate-swagger
* feature/support-dark-theme
* ...

# Bugfix
* bugfix/more-gray-shades
* bugfix/patch-1
* bugfix/gray-on-blur-fix
* ...

# Hotfix
* hotfix/disable-endpoint-zero-day-exploit
* hotfix/increase-scaling-threshold
* ...

# Release
* release/v1.0.0
* release/myapp-1.01.123
* ...
```

### GitHub Flow

GitHub-Flow is pretty simple and effective way to support continuous deployment
and release, if our development teams are a small Agile team, and we have a
single release version for our product for each repository, we can try to run
teams this workflow.

![github-flow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/2c618dbe-d3a2-4bc9-a0c6-7cdf15d34a38)

To be done...

### Centralized Workflow

To be done...

### Feature Branch Workflow

To be done...

### Forking Workflow

To be done...

## References

- [Comparing Git Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [What is a Git workflow?](https://about.gitlab.com/topics/version-control/what-is-git-workflow/)
- [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow)
