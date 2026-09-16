# Agent Workflow Skills Roadmap

Current-stage tasks: [`List.md`](List.md)
Execution checkpoint: [`NOW.md`](NOW.md)

## Objective

Publish reusable, sanitized workflow skills for durable project state and bounded subagent delegation.

## Phases

1. Initial public release
   - Deliver the two skill directories, README, LICENSE, and this small project-state set.
   - Gate: no private paths, credentials, logs, chat identifiers, server details, or private project data are present.

2. Future maintenance
   - Accept small clarifications, examples, and compatibility notes as users try the workflow.
   - Gate: additions remain agent-agnostic and do not embed private runtime assumptions.

## Document Index

- [`README.md`](README.md): public overview, install notes, authorship, and safety notes.
- [`LICENSE`](LICENSE): MIT license for Cora and South's co-created work.
- [`skills/project-task-state/SKILL.md`](skills/project-task-state/SKILL.md): durable project state workflow.
- [`skills/project-delegation-manager/SKILL.md`](skills/project-delegation-manager/SKILL.md): bounded subagent delegation workflow.
