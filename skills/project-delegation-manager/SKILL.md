---
name: project-delegation-manager
description: Use when managing substantial project work with subagents: write a plan document, split bounded tasks, delegate 1-2 chunks at a time, review results, fix tiny issues directly, and keep the main agent responsible for acceptance.
---

# Project Delegation Manager

Use this skill after `project-task-state` has loaded the project's `roadmap.md`, `List.md`, and `NOW.md`, when the task is substantial enough to benefit from subagent execution.

Do not use this for tiny edits, routine single-file fixes, ordinary chat, or cases where delegation would cost more context than it saves.

## Purpose

The main agent acts as the project manager, not a hands-off dispatcher.

- The main agent owns the objective, safety boundaries, task order, context protection, final judgment, and acceptance.
- Subagents execute bounded implementation or research chunks.
- The owner's confirmed scope and acceptance requirements are not reduced just because the implementation should stay minimal.
- Low-quota discipline still applies: delegate only when the chunk is substantial and well-bounded.

## Startup Flow

1. Load `project-task-state` and read the project's `roadmap.md`, `List.md`, and `NOW.md` first.
2. If the next phase or workstream is not yet clear, update those files before delegating.
3. Create or update a phase plan document when the work needs more structure than `List.md` should carry.
4. Link that plan document from `roadmap.md`, and keep `List.md` as the ordered current-phase task list.
5. Update `NOW.md` before dispatching, so compaction during subagent work resumes safely.

## Plan Document

Use a separate `plan.md` or domain-specific plan document when the work needs task boundaries, adapter choices, migration rules, or acceptance criteria.

The plan document should usually include:

- goal and non-goals;
- current source authorities;
- implementation slices;
- delegation boundaries;
- verification gates;
- rollback or non-production safety rules;
- what must not be touched, read, or deployed.

Do not turn an existing runtime-neutral design document into a giant session log. Use the plan document for current execution structure, and leave detailed historical design docs as authority references.

## Delegation Pattern

Delegate one or two chunks at a time, not the whole project at once. Chunks delegated in parallel must be independent; if one chunk depends on another chunk's output, queue them instead of asking two subagents to guess each other's work.

Good chunks are concrete and bounded, for example:

- implement a schema and its tests;
- extract a helper behind focused tests;
- add a worker flow behind temporary-root tests;
- write synthetic fixtures;
- research a narrow API surface and return a concise summary.

Avoid delegating:

- live deployments;
- credential handling;
- production restarts;
- final migration judgment;
- broad code review with no boundary;
- private logs, private prompts, tokens, env files, chat IDs, or secret-bearing state.

Prefer available native subagent mechanisms according to fit and quota. Do not use expensive or prohibited models when local rules exclude them.

## Subagent Prompt Template

Each subagent prompt should state:

- project root and exact task goal;
- files or docs to read;
- files or systems that must not be touched;
- whether code edits are expected;
- verification commands to run;
- that dependencies must not be installed unless the task is blocked and the main agent approves;
- what to return: files changed, commands/results, caveats, and whether anything remains uncommitted.

Ask the subagent to report in owner-readable terms, not only raw command names. The report should make these four points clear:

- what files or areas changed;
- whether the checks passed or failed;
- whether it touched anything it was told not to touch;
- what remains undone or uncertain.

Keep private repository details, tokens, env values, chat IDs, OAuth material, live private prompts, and private logs out of subagent prompts unless the current task explicitly and safely requires them.

## Review And Acceptance

After a subagent returns, the main agent must inspect before trusting it.

Minimum review loop:

1. Check `git status`, relevant diff, and affected files.
2. Read the new or changed code/docs that matter.
3. Run targeted tests or syntax checks that match the delegated chunk.
4. Verify no production hook, live state, env file, credential, private prompt, or unrelated file changed unless explicitly authorized.
5. Fix small issues directly when that is cheaper and safer than a delegation round trip.
6. Update `List.md` and `NOW.md` based on the real reviewed state, not the subagent's claim.
7. Commit and push only according to the repository delivery rules.

When reporting to the owner after delegation, include the same four owner-readable points: what changed, whether checks passed, whether anything off-limits was touched, and what remains. This is not to make the owner audit technical details; it creates a visible acceptance hook and forces the main agent to actually inspect the result.

## Tiny Fix Versus Send Back

The main agent may fix a tiny issue directly when all of these are true:

- the cause is already clear during review;
- the fix is only a few lines or a small test/doc adjustment;
- it does not require rethinking the delegated design;
- it does not cross a safety, deployment, or credential boundary;
- fixing it directly costs less context than another subagent round.

Send it back or create a new subtask when:

- the bug requires re-understanding the whole chunk;
- tests or implementation need substantial rewriting;
- there is an architecture or acceptance-boundary question;
- the change approaches production, credentials, live state, or rollback-sensitive behavior;
- the main agent is getting tired or context-heavy and delegation would reduce risk.

## Rework Stop-Loss

Do not keep re-dispatching the same chunk indefinitely.

- A chunk may get at most one ordinary rework attempt after the first failed return.
- If it is still wrong after that, the main agent must pause and classify the failure before continuing.
- If both failures are in the same place, the task was probably underspecified; rewrite the task boundary or acceptance criteria before delegating again.
- If the failures are different execution mistakes, switch to a different suitable subagent or split the chunk smaller.
- The same chunk should have at most three total attempts; if the third attempt is still wrong, stop and ask the owner or redefine it as a new, smaller task instead of looping.
- If the remaining issue is a tiny fix under the criteria above, the main agent may patch it directly instead of creating another delegation round.
- If the issue is near production, credentials, live state, or a real architecture decision, stop and ask the owner or make a clean checkpoint instead of forcing more attempts.

The goal is to protect context and attention: reading three bad attempts can be more tiring than either clarifying the task or fixing a tiny issue.

Use this shorthand: subagents move bricks; the main agent checks the blueprint, guards boundaries, patches tiny nail holes, and decides whether the house is accepted.

## Completion

Before reporting completion:

- ensure the relevant phase items in `List.md` are accurate;
- keep `NOW.md` exactly three lines and pointed at the next executable step;
- update any plan or authority document affected by the work;
- state what changed, how it was checked, what remains, and whether anything was intentionally not touched.

If the next step approaches production adapters or live runtime behavior, stop at a clean checkpoint unless the owner explicitly wants to continue and the boundary is safe.
