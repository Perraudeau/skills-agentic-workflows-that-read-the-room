---
name: update-github-info
description: Refresh Mona's GitHub Info content from official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine: copilot
model: gpt-4.1
tools:
  edit:
  github:
    toolsets: [repos]
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    draft: true
    title-prefix: "[mona] "
    max: 1
---

# Update GitHub Info

Refresh the repository's GitHub Info content for Mona's review.

## Sources and guidance

1. Use the GitHub repository API tools to read `notes/mona-notes.md` before drafting anything. Also read the current `site/content/github-info.md` so the update preserves its existing structure and avoids repeating stale entries.
2. Use `web-fetch` to read https://github.blog/latest/.
3. Use `web-fetch` to read https://github.blog/changelog/.
4. Use `web-fetch` to read https://awesome-copilot.github.com/workflows/.
5. Prefer practical, concise updates that help developers learn GitHub faster. Every item based on the blog, changelog, or Awesome Copilot workflows must name its source and link back to the official page.

## Required change

Use the edit tool to update `site/content/github-info.md` with a small set of the most useful, current updates from the official sources. Preserve the file's editorial voice and Markdown structure. Do not modify unrelated files.

When the content is ready, use the `create-pull-request` safe output to open one draft pull request containing the change for Mona to review. Do not write directly to the default branch. Summarize the selected updates and source links in the pull request body.
