---
layout: post
title: The Handbook of Git Workflows
subtitle: The software development is not only the code, but also with the most suitable git workflow
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
collaboration smooth during the software development.

![git-workflows](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/ed161d8f-ce60-4863-baae-5dd6aef8a3ef)

Organizations moving to Git from other version control systems may have
difficulty identifying an effective workflow, a suitable git workflow for your
team depends on many things:

- The number of developers working on one project
- The complexity and scale of the project
- The number of repos (i.e. mono or multiple) per project
- The experience with git your developers have
- The type of your git service (GitHub, GitLab, Bitbucket, ...)
- How you release your projects
- ...

This handbook is a guide for you to quickly master them.

## Workflows

Nowadays, software development teams encompass contributors from various
backgrounds and experiences, and they're likely to feel comfortable with a
workflow they've used previously. However, there are many best practices for
modern continuous software development, and they have been used in different
popular open-source projects.

The main well-known workflows for git are:

- Centralized Workflow
- Feature Branch Workflow
- Pull Request Workflow
- Gitflow Workflow
- GitHub Flow
- GitLab Flow
- Forking Workflow

We will explore each one of these workflows in detail here.

### Centralized Workflow

The centralized workflow, as known as Basic Workflow, is a simple and
straightforward approach to using Git. In this model, there is a single central
repository with a "master" branch where all developers push their changes.

![centralized-workflow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/29f971ff-bda2-4fa9-a13f-45435e02dcc7)

As its simplicity and reduced overhead, this workflow is quite suitable for
simple projects, especially for those projects with only one contributor. With
a single branch, developers can focus on making changes without the complexity
of managing multiple branches.

### Feature Branch Workflow

This workflow is almost the same as the centralized workflow, but, instead of
committing directly on their local master branch, developers create a new branch
every time they start work on a new feature.

![feature-branch-workflow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/83bd8de7-5e19-44c9-9b2d-5f0473830344)

### Pull Request Workflow

In this workflow, you would use PR to lead the feature, but what's PR?

PR, also known as Pull Request, is a dedicated forum for discussing
the proposed feature. If there are any problems with the changes, teammates can
post feedback in the pull request and even tweak the feature by pushing
follow-up commits. All of this activity is tracked directly inside of the pull
request.

The pull request workflow is centered around the concept of code reviews and
collaboration. In this model, developers create branches for their work and
submit pull requests when their changes are ready for review. Team members
review the changes, provide feedback, and approve or request modifications
before the changes are merged into the main branch.

![pull-request-workflow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/eb8147ad-2026-44d2-98d8-5993c89c3e87)

### Gitflow Workflow

Gitflow was presented by [Vincent Driessen](https://nvie.com/about/) in the
article [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
in 2010 and looks like this.

![git-flow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/fc8f2f26-50d1-4926-90b6-d6613545f1ea)

It empowers teams to determine roles and responsibilities, set boundaries, and
identify areas of improvement.

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

![github-flow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/a6c1f5a3-e65a-40dd-accd-fd8ea1d27558)

### GitLab Workflow

GitLab Flow is a simpler alternative to GitFlow and combines feature driven
development and feature branches with issue tracking. With GitLab Flow, all
features and fixes go to the main branch while enabling production and stable
branches. GitLab Flow includes a set of best practices and guidelines to
ensure software development teams follow a smooth process to ship features
collaboratively.

![gitlab-workflow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/3243e1fb-b0e7-4e84-a6ed-8c5524206f61)

### Forking Workflow

The forking workflow is to emphasize on maintaining a clean and stable main
repository,  it is commonly used in open-source projects and encourages
collaboration by allowing contributors to work independently. In this model,
each developer forks the main repository, creating their own copy. They make
changes in their fork and submit pull requests to the original repository
when their work is complete.

![forking-workflow](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/45b8aa77-4731-467b-87fb-85e532310a06)

## References

- [Comparing Git Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [What is a Git workflow?](https://about.gitlab.com/topics/version-control/what-is-git-workflow/)
- [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [What is GitLab Flow?](https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/)
