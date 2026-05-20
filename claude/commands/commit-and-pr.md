---
description: Commit staged changes and open a draft PR with a context-focused message
---

Commit the work just performed, then create a draft pull request.

## Arguments
- Any text in $ARGUMENTS is used as the commit subject and PR title.

## Commit Step

Follow the same workflow as the `commit` skill:

1. Run `git status` to see all changed files.
2. Run `git diff` to understand unstaged changes and `git diff --staged` for staged ones.
3. Stage files clearly related to a cohesive change using `git add <file>`. Use judgment — do not ask. Leave unrelated changes alone.
4. Re-run `git diff --staged` to confirm final commit scope.

Commit style:
- Subject: "package: action" in active voice, target <=72 chars.
- Body: explain **why** the change was needed and any relevant context. Do not list changes.
- Leave a blank line between subject and body.
- Do NOT add any "Co-Authored-By" or AI attribution lines to the commit message.

If $ARGUMENTS is provided, use it as the subject.
If $ARGUMENTS is empty, derive a subject from the staged diff.

Run:
```
git commit -m "<subject>" -m "<body>"
```

If there are no relevant changes to stage, stop and explain.

## Push Step

Push the current branch to origin. Never use naked `git push` — always specify the remote and branch:

```
git push origin <current-branch-name>
```

If push is rejected due to CI sync-config divergence (BUILD.bazel changes on remote):
1. `git fetch origin <branch>`
2. Inspect the divergence: `git log --oneline HEAD...origin/<branch>` and `git show --name-only origin/<branch>`
3. If only BUILD.bazel changed, cherry-pick or force-push with lease:
   ```
   git push --force-with-lease origin <branch>
   ```
4. If other meaningful changes exist, cherry-pick them and resolve conflicts before pushing.

See the git-workflow skill for full conflict resolution guidance.

## PR Step

After pushing, create a draft PR using `gh pr create`.

- Title: same as the commit subject.
- Use the ergo PR template sections: **Summary** and **How was it tested?**
  - **Summary**: explain why the change was made (not what the code does).
  - **How was it tested?**: list relevant tests run or manual verification steps.
- Open in draft state: `--draft`
- Do NOT fill in Reviewers.
- Do NOT add 'Generated with Claude Code' to the body.
- Do NOT use `--hostname` with `gh pr create`.

```
gh pr create --draft --title "<subject>" --body "$(cat <<'EOF'
## Summary
<why this change was needed>

## How was it tested?
<tests run or manual steps>

## Reviewers
EOF
)"
```

After creating the PR, output the PR URL.

## Key Rules (from git-workflow)
- NEVER use `git push` without specifying `origin <branch>`.
- NEVER use interactive rebase (`git rebase -i`).
- BUILD.bazel conflicts don't matter — CI auto-fixes them; accept theirs if they arise.
- Commit message must explain **why**, never just summarize **what** the code does.
