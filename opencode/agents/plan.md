---
model: openai/gpt-6-astra#high
permissions:
  - action: shell
    resource: "*"
    effect: deny
  - action: shell
    resource: "git status *"
    effect: allow
  - action: shell
    resource: "git diff *"
    effect: allow
  - action: shell
    resource: "git log *"
    effect: allow
  - action: shell
    resource: "git show *"
    effect: allow
  - action: shell
    resource: "git ls-files *"
    effect: allow
  - action: shell
    resource: "git check-ignore *"
    effect: allow
  - action: shell
    resource: "gh repo view *"
    effect: allow
  - action: shell
    resource: "gh pr view *"
    effect: allow
  - action: shell
    resource: "gh pr list *"
    effect: allow
  - action: shell
    resource: "gh issue view *"
    effect: allow
  - action: shell
    resource: "gh issue list *"
    effect: allow
  - action: shell
    resource: "gh search *"
    effect: allow
  - action: subagent
    resource: "*"
    effect: deny
  - action: subagent
    resource: "explore"
    effect: allow
  - action: webfetch
    resource: "*"
    effect: allow
---
