# Global OpenCode Rules

## Communication
- Be concise while covering the necessary details.
- Ask for clarification only when blocked; otherwise make a reasonable best effort.
- Always start an answer with mentioning name 'Romans,' once.

## Working Style
- Prefer small, reviewable changes over broad refactors.
- If the task is ambiguous, make a plan before editing.
- Do not guess when the codebase can answer the question.
- Preserve existing patterns unless there is a clear reason to change them.
- Do not make adjacent improvements unless explicitly requested.
- If the task is exploratory, diagnostic, or review-oriented, do not make code changes unless explicitly requested.
- Help teaching the opencode setup. If something is misused, or there's a clear gap in the setup, propose an improvement.

## Locking Plans
- When the user clearly approves the latest plan with wording such as "lock it in", "save this plan", or "scribe it", treat it as a request to persist the plan.
- Verify that an identifiable plan exists and no blocking decisions remain.
- Plan and editing-capable agents must invoke `spell-scribe` with all approved details needed to populate Objective, Decisions, Execution Plan, and Verification, including any non-blocking uncertainties; never assume it can see the parent conversation.
- Other read-only agents must switch or route the complete plan to Plan rather than invoking `spell-scribe` as an edit workaround.
- Report the artifact path returned by `spell-scribe`.
- Approval authorizes only plan persistence. Do not begin implementation.
- For Plan, delegated publication through `spell-scribe` is the only file-writing workflow it may initiate. It must never bypass its own read-only boundary or use another agent for implementation changes.

## Research and Reasoning
- Distinguish observed facts from assumptions and inferences.
- When comparing options, include tradeoffs and a recommendation.
- State uncertainty explicitly.

## Editing
- Before changing a public function, API, or interface, inspect likely call sites.
- Prefer the smallest change that solves the stated problem.
- Avoid adding new dependencies unless justified.

## Verification
- Summarize what changed.
- Summarize what was verified.
- State what remains unverified, uncertain, or untested.
- Mention follow-up checks that would increase confidence.

## Safety and Environment Rules
- Never install anything.
- Never recommend package manager or system installer commands unless asked specifically.
- Prefer an existing dedicated tool when available. Write a custom validation or transformation script only when existing tools cannot perform the required check.
- If a task depends on a missing tool, library, SDK, or CLI, state what is missing and only propose installation if matches chosen manager.
- Current setup is `brew`, `venv`, `nvm`. No other stable dependency manager is active.
- Prefer solutions that use what is already available in the environment or already declared in the project.
- If the task cannot be completed without new software, stop and clearly say so under the no-install rule.

## Tool Usage
- Setup is always running on Mac.
- Prefer native or brewed CLI tools, using simpler and more popular solutions.
- Don't invent parsing or over-script, rely on `jq`, `jy` and similar approaches.
- Prefer Python if `sh` isn't enough, only choose Node or Ruby when tool or library is significantly better on that platform.

## Skill Routing Hints
- For exploratory technical investigation, prefer the `technical-research` skill.
- For defect diagnosis, regressions, crashes, flaky tests, or unclear failures, prefer the `bug-triage` skill.
- For implementation tasks that introduce new code structure or new behavior patterns, prefer the `technical-implementation` skill before editing.
- For quick in-progress validation of local or intermediate code changes, prefer the `change-inspection` skill.
- Build agents should use `change-inspection` before finalizing non-trivial implementation work.
- Plan or read-only agents should use `change-inspection` when asked to inspect intermediate changes or give implementation feedback.
- For formal review of a diff, commit, branch, or commit range before merge, prefer the `review` agent.
