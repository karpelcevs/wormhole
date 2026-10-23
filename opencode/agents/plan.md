---
model: openai/gpt-6-astra#high
permissions:
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
