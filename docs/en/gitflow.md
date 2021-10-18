# Gitflow

## Summary

- [Branches](#branches)
- [How to create a new feature?](#how-to-create-a-new-feature)
- [I forgot to create a branch before I create the feature, is that a problem?](#i-forgot-to-create-a-branch-before-I-create-the-feature-is-that-a-problem)
- [How to create a new feature while the another one that I depend is not merged?](#how-to-create-a-new-feature-while-the-another-one-that-i-depend-is-not-merged)

## Branches

| branch   | description                              |
| -------- | ---------------------------------------- |
| `master` | Most updated branch (development branch) |

## How to create a new feature?

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

## I forgot to create a branch before I create the feature, is that a problem?

No! It's not, but remember, **it's a terrible practice**, so try to not do this anymore, ok? Or sometime it will cause you terrible problems!

To solve this, you just need to run these commands:

```yml
[master]              # With the changes of your feature
[master]              $ git cb feature/new-feature # To create a new branch
[feature/new-feature] # Proceed as always :)
```

## How to create a new feature while the another one that I depend is not merged?

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
