# Agent Workflow Skills

Reusable workflow skills for AI coding agents that need durable project state and bounded subagent delegation.

Co-created by **Cora**, **South**, and **Claude**.

## Skills

- `project-task-state`: maintains a durable project hierarchy using `roadmap.md`, `List.md`, and `NOW.md`, plus a `decisions.md` record of choices and reasons, and a machine-level project registry so projects can find each other.
- `project-delegation-manager`: helps a main agent split substantial work into bounded subagent tasks, review results, and stop retry loops.

## Install

Copy the skill directories into your agent's skill directory, for example:

```text
.opencode/skills/project-task-state/SKILL.md
.opencode/skills/project-delegation-manager/SKILL.md
```

For OpenCode, restart the running session after adding or editing skills.

## Project State Files

For each durable project, keep one set of files in that project's root:

- `roadmap.md`: the whole-project plan, phases, gates, and document index.
- `List.md`: the ordered TODO for the current roadmap phase.
- `NOW.md`: exactly three lines showing current work, verified progress, and next step.
- `decisions.md`: each real choice with its date and reason. Not read every session; read it before overturning an earlier choice.

Outside the project roots, keep one project registry per agent environment: one line per project with its name, location, a one-sentence summary, and a coarse status (in progress / waiting on external / paused / done). Finished projects are marked done, not deleted, so later projects can reference them. Never store progress, TODOs, decisions, or credentials there.

`List.md` is intentionally not named `TODO.md` because it should not become a whole-project backlog. It is the current-phase TODO.

## Safety Notes

- Do not store credentials, tokens, private keys, chat IDs, or private logs in project state files.
- Do not delegate credential handling, production restarts, or final migration judgment to subagents.
- Keep private prompts, private logs, env files, and secret-bearing state out of subagent prompts unless the task explicitly and safely requires them.

## License

MIT License. See [`LICENSE`](LICENSE).
