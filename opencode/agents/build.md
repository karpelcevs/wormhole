---
model: openai/gpt-6.1-sol#high
permissions:
  - action: webfetch
    resource: "*"
    effect: allow
  - action: edit
    resource: "*"
    effect: allow
  - action: edit
    resource: "~/Downloads/*"
    effect: deny
  - action: edit
    resource: "~/Library/Mobile Documents/iCloud~md~obsidian/Documents/*"
    effect: ask
  - action: shell
    resource: "npm test *"
    effect: allow
  - action: shell
    resource: "npm run test *"
    effect: allow
  - action: shell
    resource: "npm run lint *"
    effect: allow
  - action: shell
    resource: "npm run typecheck *"
    effect: allow
  - action: shell
    resource: "npm run build *"
    effect: allow
  - action: shell
    resource: "pytest *"
    effect: allow
  - action: shell
    resource: "python -m pytest *"
    effect: allow
  - action: shell
    resource: "python3 -m pytest *"
    effect: allow
  - action: shell
    resource: "ruff check *"
    effect: allow
  - action: shell
    resource: "mypy *"
    effect: allow
---
