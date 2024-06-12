# Git workflow

## Prerequisites for managing git

### main branch

Publishing and working the application in the production environment.

This branch will be merged from the `dev` branch.

It is supposed to hold the code that has been thoroughly tested and is ready for deployment to the production environment.

### dev branch

Working and testing in the development environment.

This branch will be merged from `feature` branches.

### feature branch

Developing new features and refactoring codes. Usually, the branch has its feature one on one.

### hotfix branch

Fixing critical bugs in the production environment. This branch is allowed to merge the main branch directly if it needed. However, it needs to pass the testing.

---

The idea is based on [github flow](https://docs.github.com/en/get-started/using-github/github-flow)

## Workflow

### Backend

<img src='./images/frog-blossom-cms-gitflow-be.drawio.png' />

### Frontend

<!-- later-->

## Versioning

Start from 0 until we publish the first version. After then we'll plus 0.1. If we publish a bunch of breaking changes, plus 1.

When publishing hotfix version, plus 0.01.
