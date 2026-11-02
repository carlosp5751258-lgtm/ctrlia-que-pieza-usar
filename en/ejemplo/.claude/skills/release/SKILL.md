---
name: release
description: Prepares the release notes since the last tag. Use it when asked for release notes or a changelog.
disable-model-invocation: true
---

1. List the commits since the last tag with `git log $(git describe --tags --abbrev=0)..HEAD --oneline`.
2. Group them into Features, Fixes and Documentation.
3. Write the result to CHANGELOG.md without deleting what's already there.
