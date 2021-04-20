---
layout: post
title: git_basic_workflow
---

[git_basic_workflow](https://github.com/dayarthvader/git_basic_workflow)

This page should serve as a ready reckoner for typical git workflow.

# Getting a local repo
Two ways to get a local repo to work with
1. Make one of the already existing set of files in directory not under any version control and convert that into a gir repository.
```
git init
```
`init` helps with the tracking of the current working directoy as a git repository. Note, it only creates a local repo.

2. Cloning an existing repository.
```
git clone <url>
```
or
```
git clone <url> <local_repo_directory_name>
```
