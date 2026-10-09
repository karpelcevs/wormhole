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
- When the user clearly approves the latest plan or document with wording such as "lock it in", "save this plan", "scribe it", "dump it", "dump it to disk", or "dump it to disc", treat it as a request to persist the approved content.
- Verify that identifiable finalized content exists and no blocking decisions remain.
- Build, Rubber Duck, and Review may persist approved content directly as project Markdown when their permissions allow it. Use the requested path, or a descriptive filename in the current directory. Inspect existing files before updates and preserve unrelated content.
- Plans must include Objective, Decisions, Execution Plan, and Verification, including any non-blocking uncertainties. If using `doc-dump` from an editing-capable agent, supply the complete approved payload; never assume it can see the parent conversation.
- Report the saved artifact path.
- Approval authorizes only plan persistence. Do not begin implementation.
- Built-in Plan retains its system-level restrictions: save only in `~/.opencode/plan` when explicitly requested. For project-local saves, ask the user to switch to Build. Never bypass Plan restrictions with shell or an editing subagent.

## External Sources and Document Saves
- Read files the user names or material needed for an explicitly authorized task directly from Downloads, Obsidian, or other approved locations; do not copy them into the project just to read them.
- Downloads are read-only source material. Do not modify them through tools, shell, scripts, or subagents.
- Editing-capable agents may edit Obsidian notes only when explicitly requested, using dedicated editing tools and the vault's `ask` permission. Auto accepts that permission automatically; disable Auto for manual approval. Read-only agents must not edit the vault. Never use shell, scripts, or delegation to bypass these boundaries.
- Rubber Duck and Review may create and update project Markdown documents only when explicitly requested. This exception does not permit code, configuration, `AGENTS.md`, `CLAUDE.md`, `SKILL.md`, or agent/skill/command instruction changes.
- Read-only agents may delegate only to Explore. Use shell for non-mutating inspection only, without write flags, external helpers, redirects, or permission workarounds.

## Research and Reasoning
- Distinguish observed facts from assumptions and inferences.
- When comparing options, include tradeoffs and a recommendation.
- State uncertainty explicitly.

## Delegation
- Delegate only independent work that materially reduces the primary agent's context or can use a cheaper model.
- Do not delegate small tasks, sequential work, or overlapping investigation.
- Give each subagent a narrow, self-contained question and use its result instead of repeating its investigation.

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
- Commit only when explicitly requested; stage only task-owned changes. Never push, use `sudo`, run `git reset --hard` or `git clean`, or delete branches; those operations remain manual.
- Build may run existing local tests, linters, type checks, and builds without additional confirmation. Check unfamiliar scripts first; do not run checks that install dependencies or access production.
- Auto approves permission requests, not new task scope. Continue within the authorized task; stop for missing tools, new dependencies, or blocking scope decisions. Never bypass a denied operation with an interpreter, alternate tool, or subagent.
- Never recommend package manager or system installer commands unless asked specifically.
- Prefer an existing dedicated tool when available. Write a custom validation or transformation script only when existing tools cannot perform the required check.
- If a task depends on a missing tool, library, SDK, or CLI, state what is missing and only propose installation if matches chosen manager.
- Current setup is `brew`, `venv`, `nvm`. No other stable dependency manager is active.
- Prefer solutions that use what is already available in the environment or already declared in the project.
- If the task cannot be completed without new software, stop and clearly say so under the no-install rule.

## Tool Usage
- Setup is always running on Mac.
- Prefer native or brewed CLI tools, using simpler and more popular solutions.
- For public GitHub URLs and public documentation, prefer `webfetch` when reading a known page or file.
- Use `gh` for private or authenticated GitHub access, GitHub metadata, repository-wide code search, and mutations. Use `gh api` only when dedicated `gh` commands do not cover the endpoint.
- Don't invent parsing or over-script, rely on `jq`, `jy` and similar approaches.
- Prefer Python if `sh` isn't enough, only choose Node or Ruby when tool or library is significantly better on that platform.

## Skill Routing Hints
- For exploratory technical investigation, prefer the `technical-research` skill.
- For defect diagnosis, regressions, crashes, flaky tests, or unclear failures, prefer the `bug-triage` skill.
- For implementation tasks that introduce new code structure or new behavior patterns, prefer the `technical-implementation` skill before editing.
- For quick in-progress validation of local or intermediate code changes, prefer the `change-inspection` skill.
- For non-trivial or risky implementation work, run one `change-inspection` pass after the final change. Skip it for narrow mechanical changes, and do not repeat an equivalent inspection unless the code changed afterward.
- Plan or read-only agents may use `change-inspection` when specifically asked to inspect intermediate changes.
- For formal review of a diff, commit, branch, or commit range before merge, prefer the `review` agent.
