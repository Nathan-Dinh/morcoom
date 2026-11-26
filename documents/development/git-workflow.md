# Git Workflow & Conventions


## Branch Naming



### Naming Convention


```text
<type>/<issue-number>-<short-description>
```

### Branch Types

| Type | Purpose | Example |
|---|---|---|
| `feature` | New functionality | `feature/12-user-authentication` |
| `fix` | Bug fixes | `fix/24-login-error` |
| `refactor` | Code restructuring | `refactor/18-database-structure` |
| `docs` | Documentation changes | `docs/31-project-architecture` |
| `chore` | Maintenance and configuration | `chore/5-dependency-updates` |
| `test` | Testing-related changes | `test/42-authentication-tests` |

### Creating a Branch

Create a branch from the latest main branch:

```bash
git switch main
git pull origin main
git switch -c feature/12-user-authentication
```

## Commit Messages

Commit messages should clearly describe the changes introduced.

### Naming Convention

Use the following format:

```text
<type>: <short-description>
```

### Commit Types

| Type | Purpose |
|---|---|
| `feat` | Introduces new functionality |
| `fix` | Fixes a bug |
| `refactor` | Restructures existing code |
| `docs` | Adds or updates documentation |
| `test` | Adds or modifies tests |
| `chore` | General maintenance |
| `build` | Changes build configuration or dependencies |
| `ci` | Changes CI/CD configuration |

### Examples

```text
feat: add user registration endpoint

fix: resolve authentication timeout

docs: document database architecture

refactor: separate authentication services
```

## Commit Descriptions


```text
<type>: <short-description>

<detailed explanation of the changes>

<issue references>
```

### Example

```text
feat: initialize project structure

- Establish the initial directory structure.
- Configure application dependencies.
- Add environment configuration.
- Set up development scripts.

Refs #12
```

The commit title should summarize the change. The body should explain what changed and why.

## GitHub Issue References

GitHub Issues should be referenced in commits and pull requests to maintain traceability between development work and project requirements.

### Referencing an Issue

Use:

```text
Refs #12
```

This links the commit to issue #12 without automatically closing it.

### Closing an Issue

Use one of the following keywords:

```text
Closes #12
Fixes #12
Resolves #12
```

GitHub automatically closes the referenced issue when the commit or pull request reaches the repository's default branch.

### Multiple Issue References

```text
Refs #12
Refs #13
```

Issues can also be referenced directly in pull request descriptions.

## 6. Squashing Commits

Squashing combines multiple commits into a single commit.

This is useful when a feature branch contains temporary commits, incremental changes, or fixes that do not need to appear separately in the final project history.

### Interactive Rebase

View recent commits:

```bash
git log --oneline
```

Start an interactive rebase:

```bash
git rebase -i HEAD~3
```

Change the commits you want to combine from `pick` to `squash` or `fixup`.

Example:

```text
pick c91d20b Create project structure
squash b72f10a Configure dependencies
squash a82f91d Add environment variables
```

Save and close the editor. Git will prompt you to create the final commit message.

### Squashing Guidelines

- Squash temporary or redundant commits before merging.
- Preserve meaningful commit history where individual changes provide value.
- Use descriptive commit messages for the resulting commit.
- Avoid rewriting shared branch history without coordinating with other contributors.

If the branch has already been pushed, update it using:

```bash
git push --force-with-lease
```

## Pull Requests

All changes intended for the main branch should be submitted through a pull request.

### Pull Request Naming

Use the following format:

```text
<type>: <short-description>
```

Example:

```text
feat: implement user authentication
```

### Pull Request Description

Use the following structure:

```markdown
## Summary

Briefly explain the changes introduced.

## Changes

- Change 1
- Change 2
- Change 3

## Testing

Explain how the changes were tested.

## Related Issues

Closes #12
```

### Pull Request Guidelines

- Ensure the branch is up to date with the target branch.
- Verify that relevant tests pass.
- Review the changes before submitting.
- Link all related GitHub Issues.
- Resolve review comments before merging.
- Avoid including unrelated changes in a pull request.

## Merging

Use pull requests to merge development branches into the main branch.

### Recommended Merge Strategy

Use **Squash and merge** for feature branches.

This combines all commits from a pull request into one commit on the main branch.

Benefits:

- Keeps the main branch history clean.
- Avoids unnecessary intermediate commits.
- Makes it easier to understand when a feature was introduced.
- Keeps related changes grouped together.


## References

- Git Documentation: https://git-scm.com/doc
- GitHub Issues: https://docs.github.com/en/issues
- GitHub Pull Requests: https://docs.github.com/en/pull-requests
- GitHub CLI: https://cli.github.com/