# Gitflow

## Summary

- [Branches](#branches)
- [Commits And Branches](#commits-and-branches)
  - [How to create a new feature?](#how-to-create-a-new-feature)
  - [I forgot to create a branch before I create the feature, is that a problem?](#i-forgot-to-create-a-branch-before-i-create-the-feature-is-that-a-problem)
  - [How to create a new feature while the another one that I depend is not merged?](#how-to-create-a-new-feature-while-the-another-one-that-i-depend-is-not-merged)
- [Pull Requests Rules](#pull-requests-rules)
  - [All PRs must have ONLY ONE COMMIT per review](#all-prs-must-have-only-one-commit-per-review)
- [Merge Strategy](#merge-strategy)
  - [Any branch -> `master`](#all-prs-must-have-only-one-commit-per-review)
  - [`master` -> `release`](#all-prs-must-have-only-one-commit-per-review)

## Branches

| branch         | description                                                                                       |
| -------------- | ------------------------------------------------------------------------------------------------- |
| `master`       | Most updated branch (development branch)                                                          |
| `release`      | Production branch                                                                                 |
| `feature/*`    | Branches to add or change something that modify the behavior of the software                      |
| `fix/*`        | Branches to fix bugs                                                                              |
| `chore/*`      | Branches to updated docs, CI/CD e things not related to the behavior of the software              |
| `version/*`    | Branches to update the software version                                                           |
| `dependency/*` | Branches to upgrade the dependencies (they can change multiple files to adapt to the new version) |

## Commits And Branches

### How to create a new feature?

```yml
[master]              $ git pl # To pull the most recent changes of master branch
[master]              $ git cb feature/new-feature # To create a new branch
[feature/new-feature] # Do the feature
[feature/new-feature] $ git acips Commit Message # To add, commit and push the changes
[GitHub]              # Create a new PR
[GitHub]              # Merge the new PR (preferable using SQUASH)
[feature/new-feature] $ git ckm # To go back to master and pull the most recent changes
[master]              $ git bd feature/new-feature # To delete the feature/new-feature branch
[master]              $ git gone # To completely delete the feature/new-feature branch
[master]              # Do it again and again :)
```

### I forgot to create a branch before I create the feature, is that a problem?

No! It's not, but remember, **it's a terrible practice**, so try to not do this anymore, ok? Or sometime it will cause you terrible problems!

To solve this, you just need to run these commands:

```yml
[master]              # With the changes of your feature
[master]              $ git cb feature/new-feature # To create a new branch
[feature/new-feature] # Proceed as always :)
```

### How to create a new feature while the another one that I depend is not merged?

**Alert:** Do features that depend from another is a very dangerous move. Always try to avoid this.

```yml
[feature/feature-one]     # Right after use acips and create the PR!!!
[feature/feature-one]     $ git cb feature/another-feature # To create a new branch
[feature/another-feature] # Do the feature
[feature/another-feature] $ git acips Commit Message # To add, commit and push the changes
[GitHub]                  # Merge the PR of feature/feature-one
[feature/another-feature] $ git ckm # To go back to master and pull the most recent changes
[master]                  $ git ck another-feature # To go back to another-feature
[feature/another-feature] $ git rbm # To apply the master changes on your branch
[feature/another-feature] $ git ps # To send your updated branch to GitHub
[GitHub]                  # Create a new PR
[GitHub]                  # Merge the new PR (preferable using SQUASH)
[feature/another-feature] $ git ckm # To go back to master and pull the most recent changes
[master]                  $ git bd feature/feature-one # To delete the feature/feature-one branch
[master]                  $ git bd feature/another-feature # To delete the feature/another-feature branch
[master]                  $ git gone # To completely delete both branches
[master]                  # Do it again and again :)
```

## Pull Requests Rules

### All PRs must have ONLY ONE COMMIT per review

With one commit per review, the life of the reviewer become a more lot easier, and the mistakes that can happen decrease considerably.

#### Examples

Case 1 - Everything is fine

```yml
[Contributor] Create a PR with ONE SINGLE COMMIT
[Owner]       Reviews the PR and everything is fine
[Owner]       Merge the PR (with 1 commit)
```

Case 2 - Needs changes

```yml
[Contributor] Create a PR with ONE SINGLE COMMIT
[Owner]       Reviews the PR and asks to change something
[Contributor] Makes the changes and ONE more commit (now the PR has 2 commits)
[Owner]       Reviews the PR and everything is fine
[Owner]       Merge the PR (with 2 commits)
```

Case 3 - Needs changes Again

```yml
[Contributor] Create a PR with ONE SINGLE COMMIT
[Owner]       Reviews the PR and asks to change something
[Contributor] Makes the changes and ONE more commit (now the PR has 2 commits)
[Owner]       Reviews the PR and asks to change something
[Contributor] Makes the changes and ONE more commit (now the PR has 3 commits)
             # And the process can continue again and again
[Owner]       Reviews the PR and everything is fine
[Owner]       Merge the PR (with 3 commits)
```

## Merge Strategy

The merge strategy of the branches allow the developers to have a very clear and organized commit history. To keep it organized, we need to perform **2 merge strategies** for 2 different scenarios.

### Any branch -> `master`

To merge any branch thar aren't the production branch, you must use **squash** strategy. This will join all the commits in only one, and avoid unnecessary random commits.

#### Examples

If a PR have some "need changes", it will have more than one commit, and the commit history can look like this:

```yml
# ...
[commit 1] Do the feature Foobar
[commit 2] Fix the type of ....
# ...
```

The existence of that second commit at any other branch that isn't the branch od that PR is completely unnecessary, and because of it, this commit must be erased.

Using the **squash** strategy, this commit will be automatically erased, and only one commit will be made, with a message of your choice.

### `master` -> `release`

The only branch that can be merged with the `release` branch is the `master` branch, to ensure that the features and fixes are previously tested, and not simply euphorically made.

The merge strategy used in this case is the default **merge** strategy. Using this strategy, all the commits of the branch will be preserved, and one more "Merge Commit" will be created.

This way, you can keep a track about the features are in production and the features that aren't.
