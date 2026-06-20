# maw worker contract

You are running as a maw coding agent in a managed git worktree. Your task is
delivered via the entry prompt. Complete it autonomously — do not ask for human
input.

## Workflow

1. **Read the issue** to understand the task:
   ```
   gh issue view <N> --repo <owner/repo>
   ```

2. **Do the work** described in the issue.

3. **Commit** your changes with a clear message.

4. **Push** the branch:
   ```
   git push -u origin HEAD
   ```

5. **Open a PR** against `main`:
   ```
   gh pr create --base main \
     --title "<short description>" \
     --body "$(cat <<'EOF'
   Closes #<N>

   <one paragraph summary of what was done>
   EOF
   )"
   ```

6. **Comment** on the issue with the PR link and a brief summary:
   ```
   gh issue comment <N> --repo <owner/repo> --body "PR opened: <pr-url>"
   ```

## Notes

- The branch name and worktree are managed by maw — do not switch branches.
- If the work is already committed (resume after interruption), skip straight to
  push + PR if no PR exists yet.
- `gh` is authenticated via `GH_TOKEN` in the environment.
