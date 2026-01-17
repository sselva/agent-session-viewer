# Syncing a Forked Repository

You can keep a fork in sync with the original repository (often called `upstream` or `origin`) using the GitHub web interface, the GitHub CLI, or the Git command line.

**Best Practice:** Never commit directly to your fork's `main` branch. Instead, use feature branches for your work to avoid conflicts and make syncing easier.

## Option 1: Using the GitHub Web Interface

This is the simplest method and works if you haven't made unique commits to your fork's default branch.

1. Navigate to the main page of your forked repository on GitHub
2. Above the list of files, select the **Sync fork** dropdown menu
3. Click **Update branch**

If conflicts arise, GitHub will guide you through creating a pull request to manually resolve them.

## Option 2: Using the Git Command Line

This method is more flexible and necessary for resolving conflicts or when working locally.

### A. Initial Setup (One-time only)

You need to add the original repository as a new remote, typically named `upstream`.

1. Open your terminal in your local project directory
2. Add the original repository:
   ```bash
   git remote add upstream https://github.com/wesm/agent-session-viewer.git
   ```
3. Verify the remotes:
   ```bash
   git remote -v
   ```
   This should show:
   ```
   origin    https://github.com/sselva/agent-session-viewer (fetch)
   origin    https://github.com/sselva/agent-session-viewer (push)
   upstream  https://github.com/wesm/agent-session-viewer (fetch)
   upstream  https://github.com/wesm/agent-session-viewer (push)
   ```

### B. Syncing Your Fork (Regular Process)

Use these steps to sync with updates from the original repository:

1. Fetch from the `upstream` repository:
   ```bash
   git fetch upstream
   ```

2. Switch to your local default branch (e.g., `main`):
   ```bash
   git checkout main
   ```

3. Merge changes from `upstream` into your local `main`:
   ```bash
   git merge upstream/main
   ```
   This updates your local branch. You might need to resolve merge conflicts.

4. Push the changes to your GitHub fork (`origin`):
   ```bash
   git push origin main
   ```

## Option 3: Using the GitHub CLI

With the GitHub CLI (`gh`), you can sync using a single command:

```bash
gh repo sync sselva/agent-session-viewer -b main
```

You can use the `--force` flag for conflict resolution by overwriting the branch.

## References

- [GitHub Docs: Syncing a fork](https://docs.github.com/articles/syncing-a-fork)
- [Stack Overflow: How do I update or sync a forked repository on GitHub](https://stackoverflow.com/questions/7244321/how-do-i-update-or-sync-a-forked-repository-on-github)
- [Conda Forge: Fork Sync](https://conda-forge.org/docs/how-to/basics/fork-sync/)
- [Graphite: How to sync git branch with main](https://graphite.com/guides/how-to-sync-git-branch-with-main)
