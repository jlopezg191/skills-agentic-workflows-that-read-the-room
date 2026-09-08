---
name: update-github-info
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
  metadata: read
engine: copilot
model: copilot/auto
tools:
  edit:
  github:
  web-fetch:
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    draft: true
    title-prefix: "[mona] "
---

# Update GitHub Info

Keep the GitHub Info website current with concise, practical updates for developers.

1. Read `notes/mona-notes.md` and `site/content/github-info.md` using the GitHub repository API tools. Do not use terminal, CLI, or sandboxed shell commands to read repository guidance or reference files.
2. Use the `web-fetch` tool to fetch `https://github.blog/latest/`.
3. Use the `web-fetch` tool to fetch `https://github.blog/changelog/`.
4. Use the `web-fetch` tool to fetch `https://awesome-copilot.github.com/workflows/`.
5. Identify only useful, recent updates that fit Mona's editorial angle. Cite the relevant GitHub Blog, GitHub Changelog, or Awesome Copilot source for every update you add.
6. Use the `edit` tool to update `site/content/github-info.md`. Keep summaries short and practical, preserve the existing structure, and avoid unrelated changes.
7. Review the resulting diff for accuracy, relevance, and valid Markdown.
8. When there are meaningful changes, use the `create-pull-request` safe-output tool to open a pull request containing the update for Mona to review. The pull request should explain the sources used and the changes made. Do not write directly to `main`.
9. If there are no meaningful updates, do not modify the file and do not open a pull request.
