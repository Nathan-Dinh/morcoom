# Squashing Existing Commits

## Prerequisites

Before squashing commits:

- Ensure you are on the correct branch.
- Make sure your working directory is clean.
- Identify which commits you want to combine.
- Confirm that nobody else is actively working on the same branch.

Check your current branch:

```bash
git branch --show-current
```

Check for uncommitted changes:

```bash
git status
```

## Identify Commits

View the recent commit history:

```bash
git log --oneline
```

Example:

```text
a82f91d Add environment variables
b72f10a Configure dependencies
c91d20b Create project structure
d81e30c Initial commit
```

In this example, the latest three commits will be combined into one.

## Start Interactive Rebase

Run the following command:

```bash
git rebase -i HEAD~3
```

The number represents how many recent commits you want to review.

Git will open an editor containing the selected commits:

```text
pick c91d20b Create project structure
pick b72f10a Configure dependencies
pick a82f91d Add environment variables
```

## Select Commits to Squash

Change `pick` to `squash` for the commits you want to combine.

```text
pick c91d20b Create project structure
squash b72f10a Configure dependencies
squash a82f91d Add environment variables
```

The first commit is retained as the base. The remaining commits are combined into it.

### Available Rebase Commands

| Command | Description |
|---|---|
| `pick` | Keep the commit as is. |
| `squash` | Combine the commit with the previous commit and retain its message. |
| `fixup` | Combine the commit with the previous commit and discard its message. |
| `reword` | Change the commit message. |
| `edit` | Stop and allow modifications to the commit. |
| `drop` | Remove the commit from history. |

Save and close the editor to continue.

## Create the New Commit Message

Git will prompt you to edit the combined commit message.

Use a descriptive message that represents all the changes.

Example:

```text
feat: initialize project structure

- Establish the initial directory structure.
- Configure application dependencies.
- Add environment configuration.
```

Save and close the editor.

## Update the Remote Repository

Since the original commits have already been pushed, the remote branch must be updated to reflect the rewritten history.

Run:

```bash
git push --force-with-lease origin <branch-name>
```

Replace `<branch-name>` with your current branch.

`--force-with-lease` checks that the remote branch has not changed unexpectedly before overwriting its history.

## Verify the Changes

Check the updated commit history:

```bash
git log --oneline
```

The original three commits should now appear as one combined commit.

Verify that your local and remote branches are synchronized:

```bash
git status
```