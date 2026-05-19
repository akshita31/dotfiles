Run the airmeshOnly legacy flag cleanup for a repo and create a PR.

The repo name is: $ARGUMENTS

Steps:
1. Find all uses of the `airmeshOnly` flag in the repo (it's a legacy flag that is no longer needed when kube-gen version > 92.0.0)
2. Remove all occurrences of the `airmeshOnly` flag and any associated logic
3. Verify the changes compile and tests pass
4. Create a PR with a test plan that verifies kube-gen version > 92.0.0 no longer needs that flag
