---
name: update-github-info
description: Keep the GitHub Info website current with practical updates from official GitHub sources.
intent: Review the latest official GitHub Blog and Changelog updates and propose a concise, source-backed update to the GitHub Info website for Mona's review.
engine: 
  id: copilot
  model: claude-5.5-sonnet
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    draft: true
    base-branch: main
    allowed-files:
      - site/content/github-info.md

---

# Update GitHub Info

Read `notes/mona-notes.md` before making any decisions about the content or editorial style.

Use `web-fetch` to read all of these sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Review the existing content in `site/content/github-info.md`, then update that file with a short, practical addition or revision based only on relevant information from the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows. Keep the content useful for developers learning GitHub, follow Mona's editorial angle, and mention the source whenever an update comes from any of these sources. Do not change any other files.

If there is no meaningful, non-duplicative update to make, leave the file unchanged and report a clear no-op. Otherwise, request the `create-pull-request` safe output with a concise title and body explaining what changed and linking to the official source. Open the pull request for Mona to review; do not write directly to `main`.
