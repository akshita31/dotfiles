---
description: Resume work on Airstack mesh automation — reads the project working doc, presents track status, and executes on whichever track you pick
---

You are resuming work on the Airstack mesh project at Airbnb.

## Step 1: Read the project doc

Read the working doc at https://docs.google.com/document/d/1XocB9DsNWQRqpZE9WeoP1GEBxtfS3QZPXJ--RSAbnZY/edit?tab=t.7rx4ctb5ord5. It is the single source of truth for this project — tracks, PR status, design decisions, and notes. Follow links to the doc's other tabs (e.g. the meshd migration and egressgw-specific tabs) for track-specific detail. Do not ask me to explain anything already in the doc.

## Step 2: Present track status

After reading the doc, show a compact status table:

| Track | Description | Status |
|-------|-------------|--------|
| 1 | Migrate meshd to Helm chart | ... |
| 2 | Migrate Egress Gateway to Helm chart | ... |

For each track, check the relevant open PRs (ergo, and kube-system if a release has been wired up) to determine real status rather than relying solely on the doc.

Then ask: **Which track do you want to work on?**

## Step 3: Execute

Once I pick a track:

1. Read the open PR(s) for that track using `gh pr view <number> --repo <org/repo>` to get the latest diff and review comments
2. Synthesize: current state + what's blocking + what the next concrete action is
3. Propose the action and discuss it with me before executing — especially for non-trivial changes

After opening or updating a PR, ask me: "Does the testing plan look right? Anything to add?" Iterate until I'm satisfied.

## Arguments

If $ARGUMENTS is provided, treat it as the track number or name to jump to directly — skip the track selection question and go straight to Step 3.
