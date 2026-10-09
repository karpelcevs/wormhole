# Wormhole

## Within cells interlinked

This setup targets [OpenCode](https://github.com/anomalyco/opencode) and is managed with [GNU Stow](https://www.gnu.org/software/stow/).

```
stow .
```

### Agents

#### Primary agents
- Rubber-Duck :duck:
- Plan <sup>[Built-in]</sup>
- Build <sup>[Built-in]</sup>
- Review
- `Pair-Programmer` :ghost:

#### Sub-agents
- general <sup>[Built-in]</sup>
- explore <sup>[Built-in]</sup>
- prompt-editor
- doc-dump <sup>[Hidden; optional writer for new approved artifacts in `.plans/`]</sup>
- tech-skill-smith

### Auto workflow (OpenCode V2)

Keep permission prompting as the default. For a scoped task, start a separate TUI with:

```sh
opencode --auto /path/to/project
```

1. Select **Build** with `Ctrl+A`; Auto still starts with the default Rubber Duck.
2. Check the session model with `Ctrl+M` and reasoning variant with `Ctrl+I`. Switching agents does not necessarily change the session model.
3. Describe the result, scope, and required checks. Build may use installed tools and run existing tests, linters, type checks, and builds. Missing dependencies are blockers, not permission to install.
4. Review `/diff` and the verification summary. Ask explicitly for a commit if wanted; push manually.

For a noninteractive task, run from the project directory:

```sh
opencode run --auto --agent build --model 'openai/gpt-6.1-sol#high' \
  "Implement the approved change, run relevant checks, and leave it uncommitted."
```

Auto accepts `ask` requests; it never overrides an effective `deny`. Do not assume its TUI toggle is isolated to one tab. If background tabs or child sessions stall on approvals, use one TUI process per task and inspect pending permissions.

### Permissions and document saves

- Every agent can read named files in Downloads and the Obsidian vault without copying them. Other external directories normally ask; Auto accepts those requests. OpenCode's managed output/temp and global config directories are explicitly allowed.
- Downloads remain read-only. Obsidian edits use `ask` in Build, Pair Programmer, General, Prompt Editor, and Tech Skill Smith; read-only agents remain blocked. Edit notes only when explicitly requested. Disable Auto if you want manual approval, since Auto accepts `ask` automatically. Agent-specific vault rules follow the general edit allowance because the last matching rule wins.
- Commits require an explicit request. Pushes, `sudo`, hard Git resets, `git clean`, and branch deletion remain manual. Build may remove individual project files when necessary for the requested change.
- Rubber Duck and Review can create or update project Markdown on request: “Save this as `notes.md`” or “Update `review.md` with these findings.” Code, configuration, and agent/skill/command instruction files remain protected.
- Built-in Plan keeps its restrictions. Switch to Build to save a plan alongside the project files; no custom Planner is added.
- Read-only agents can delegate only to Explore and have a narrow Git/GitHub-inspection shell allowlist. Build/Auto keeps flexible shell access.

Scope, explicit-request requirements, and avoiding source mutations through shell are behavioral instructions. Shell is not sandboxed; command patterns cannot cover every script, alias, flag arrangement, or indirect side effect. Later agent/project rules can override ordinary permissions, so inspect the effective rules when adding an agent. Markdown wildcards also match nested documents, not just root files. The documented experimental policy format was rejected by the installed 2.0.26 runtime; this setup uses verified ordinary permission rules instead.

References: [V2 permissions](https://opencode.ai/v2/docs/permissions), [Auto background-tab issue](https://github.com/anomalyco/opencode/issues/44007).
