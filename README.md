# ff-action

This repository contains a GitHub Action that implements a
fast-forward-only workflow from a staging branch to a main branch.

## Branches

Four branches are in the repository to test the workflow.

- `main` -- This is the base branch. That is, it is the branch
  potentially being advanced by the workflow.
- `is-main` -- As the name suggests, the branch is the same as
  `main`. It exists to verify a noop workflow.
- `main-ff` -- This is the happy case. It is a branch that has
  advanced beyond `main`, but `main` can still be fast-forwarded to
  it.
- `no-main-ff` -- The unhappy case. This branch has advanced beyond
  its common ancestor with `main`, but `main` has also advanced beyond
  their common ancestor. In this case, `main` cannot be
  fast-forwarded.

## The Action
### Prerequisites

The GitHub Action pushes to `main` when `main` can be
fast-forwarded. By default, Actions cannot write to the repository. In
order to make it possible for Actions to do this, the repository
configuration needs to be changed. The steps to do this are:

1. In the GitHub UI for the repository, go to Settings > Actions >
   General.
2. In "Workflow permissions", click the "Read and write permissions"
   radio button, and then click "Save".

### Running the Action

1. In the GitHub UI for the repository, go to "Actions".
2. Click the "Fast Forward Main" Action.
3. Click "Run workflow", select a compare branch, and click "Run
workflow".

Note: after running the Action with `main-ff` as the compare branch,
the `main` branch will be altered. To restore to the starting
conditions, force push `main` after removing its new `HEAD` commit.
