---
name: project-task-state
description: Use before starting or resuming substantive project work, after compaction or task takeover, and whenever roadmap.md/List.md/NOW.md state changes. Maintains a phased roadmap, an ordered current-stage task list, and a strict three-line execution checkpoint. Pure chat may use it optionally.
---

# Project Task State

Use `roadmap.md`, `List.md`, and `NOW.md` as a durable execution hierarchy for work that has a concrete deliverable. This covers code, configuration, deployment, research, application writing, maintained documentation, investigations, and other work that must survive a new session or compaction.

Pure conversation is different. When no concrete task is being executed, the agent may choose whether writing a checkpoint feels useful; do not create or update these files mechanically just because a chat occurred.

## File Scope

- Keep one `roadmap.md`, one `List.md`, and one `NOW.md` per durable project, not per chat session and not as a global workspace-wide diary.
- Also create `decisions.md` in the project root at project start. It is not part of the per-session read order; see Decision Record below.
- Also register the project in the machine-level project registry at project start; see Project Registry below.
- Use the existing trio in the active project's root when present.
- If the active durable project lacks any of the three files, initialize the missing file in that project's root before substantial work. Do not place unrelated projects into one state set merely because their sessions share a workspace.
- The workflow method and this skill may be shared, but an individual project's three state files and supporting documents remain inside that project's own authority.
- Shared memory or long-term notes may preserve durable cross-session rules or conclusions, but they are not a project task board or a mirror of `roadmap.md`, `List.md`, `NOW.md`, or project documentation.
- When multiple agents need the same project, keep one canonical project document set in that project's repository or directory and use the project's collaboration channel for status and handoff. Multi-agent access does not turn project documents into global shared files.
- When one agent is working alone and no cross-agent handoff, review, or coordination is needed, do not create external status reports merely to report routine progress. The project's own roadmap, List, NOW, and authoritative documents are sufficient.
- If no durable project root can be identified, ask one short location question rather than guessing or creating files across unrelated directories.
- Before doing substantive work in every session, read `roadmap.md` first, then `List.md` and `NOW.md`. Repeat this after compaction, task takeover, or session resumption. Never rely on a chat summary as a substitute.

## Responsibilities

`roadmap.md` is the detailed whole-project outline:

- state the project objective, scope, constraints, and success condition;
- divide the total work into ordered phases and list the steps, deliverables, dependencies, and completion gate for each phase;
- mark the current phase and preserve concise phase-level completion state so local work cannot obscure the whole plan;
- include a document index, or point to a dedicated index, covering every maintained supporting document and its authority/purpose;
- for evidence-sensitive work, define a source-authority map that names which primary evidence or authoritative project document controls each fact domain;
- update it when scope, phase order, dependencies, or the document graph changes, but do not turn it into a session log.

`List.md` is the ordered detailed TODO for the current roadmap phase:

- start the file with a short sentence such as: `This is the ordered TODO for the current roadmap phase.`;
- group tasks by an explicit sequence or dependency structure rather than accumulating an unordered backlog;
- record active, pending, blocked, completed, and intentionally cancelled work for the current phase;
- keep enough context to understand priority, dependency, and the phase completion gate;
- update an item when its real state changes, not only at final wrap-up;
- when a phase closes, summarize its durable outcome in `roadmap.md` and replace or reorganize `List.md` for the next phase instead of carrying an ever-growing task pile;
- do not turn it into a transcript, diary, whole-project roadmap, or duplicate of detailed project documentation.

`NOW.md` is the single current execution checkpoint. It contains exactly three non-empty-or-placeholder lines and no heading, bullets, history, or appended sections:

```text
Working on:
Verified so far:
Next step:
```

- Overwrite these three lines; never append a running log.
- `Working on` names the current task or workstream.
- `Verified so far` records the latest verified checkpoint, conclusion, or blocker.
- `Next step` gives the next executable action or the exact external condition being awaited.
- When no task remains active, clear it back to the same three-field empty template.

## Decision Record (`decisions.md`)

Why this file exists: the costly failure is not making a choice but re-deriving "why did we choose this" after compaction or handoff, sometimes reaching the opposite conclusion and undoing a correct choice. Reasons written at the time are cheap; reasons reconstructed later are usually lost.

- Create it at project start alongside the trio, and list it in the `roadmap.md` document index.
- One entry per real choice: date, what was chosen, why, and what was rejected when that matters. One or two lines each.
- Do not read it on every session start. Read it before overturning, reversing, or materially changing an earlier choice, and before re-arguing a direction the owner already settled.
- When a decision is overturned, keep the old entry, mark it superseded, and add the new one with its reason. Do not delete history.
- It records choices and reasons only. Not a task list, progress log, or copy of roadmap scope.

## Project Registry

Why this exists: one agent often carries several projects, and a single project often needs to look up or build on another. Each project's own files say nothing about its siblings, and after compaction the agent may not remember which projects exist or where they live. The global checkpoint should not carry project lists either, because that turns it into a second task board.

- Keep one registry per agent environment, outside every project root, in a place the agent sees at startup (for example, listed in an index the agent always loads). Do not inline the whole registry into the always-loaded instruction file; point to it.
- One line per project, exactly four fields: name | location (machine and directory when there is more than one machine) | one-sentence summary | coarse status. Status is one of in progress / waiting on external / paused / done, plus at most half a sentence on what it waits for.
- Keep each line short. Never put detailed progress, TODOs, decisions and reasons, process notes, chat quotes, or credentials in the registry. Those belong in the project's own `NOW.md`, `List.md`, `decisions.md`, and env files.
- Add the line at project start and keep the status word current. When a project ends, mark it done instead of deleting the line, so later projects can still find and reference it. Do not add a summary to finished entries.

## Mandatory Update Points

Update the relevant `List.md` item when its status, priority, or dependency changes, and overwrite `NOW.md` immediately when:

1. a concrete task starts or the active task changes;
2. a material conclusion is confirmed, overturned, or narrowed;
3. work becomes blocked or starts waiting on an external dependency;
4. the next executable action changes;
5. a task completes, is cancelled, or hands off to another participant.

Do not postpone all updates until the end. Use this self-check:

> If this session were compacted away now, would these three lines be enough to continue correctly?

If not, update `NOW.md` now.

Routine checkpoint progress may change only `NOW.md`; do not pad `List.md` with a duplicate activity log when its task state has not changed.

## Evidence Authority And Provenance

- Define the evidence hierarchy per project rather than imposing a universal "originals only" rule. Official or primary evidence normally controls institutional facts; current owner confirmation may control personal facts; current code, deployment evidence, or repository history may control implementation facts. Secondary sources may supply leads or context only when the project permits them.
- A derivative draft, summary, chat recollection, handoff, or old comment never silently overrides its named source of truth. Audit the higher-authority source and update the authoritative project document before reusing the conclusion.
- For important mutable or out-of-Git input files, record enough non-sensitive provenance to identify the reviewed version: source role, received or verification date, a sanitized filename or artifact label, and a cryptographic hash when practical.
- Fingerprinting an external file does not authorize copying it into Git or shared memory. Keep private originals in their approved location and never record secret values or unnecessary identifiers.

## Authority, Supersession, And Completion

- `roadmap.md` controls project scope, phase order, dependencies, gates, and the document/source authority map. A linked domain document controls the detailed conclusions assigned to it. `List.md` controls ordered current-phase task state. `NOW.md` controls the current execution checkpoint. A collaboration issue or ticket controls multi-agent status and handoff when that project uses one.
- When evidence overturns a conclusion, update the authoritative domain document first in the same work round. Then update `roadmap.md` if scope, phases, dependencies, gates, or authority changed; update `List.md` and `NOW.md` if execution changed; and append any required collaboration handoff/status update. Do not let stale lower-authority text continue to govern.
- Preserve useful decision history in the authoritative domain document, Git history, or collaboration history. Mark a prior conclusion superseded when losing the reason for reversal would create future risk; do not preserve every transient checkpoint.
- When work completes, put the durable outcome in `roadmap.md` at phase level and in the relevant authoritative domain document at fact/detail level. Reorganize `List.md` for the next phase and clear or advance `NOW.md`; do not grow any of the three into an append-only completion log.

## Document Graph

- Every maintained supporting document must be reachable from `roadmap.md` or from a dedicated index directly linked by `roadmap.md`.
- Give each document a clear authority/purpose in that index. Add a parent or related-document pointer inside child documents when practical, especially when their role would otherwise be ambiguous.
- When creating, renaming, splitting, archiving, or deleting a document, update all relevant pointers in the same change and check for orphan documents.
- Do not duplicate authoritative facts merely to create links. Point to the source-of-truth document instead.

## Concurrency And Authority

- Re-read all three state files immediately before editing them so another session's changes are not silently overwritten.
- Never revert or erase unrelated concurrent work. Merge durable backlog changes in `List.md`.
- `NOW.md` represents the project's current critical execution point. If another session is already advancing an independent stream, record both streams in `List.md` and keep `NOW.md` on the agreed critical path rather than replacing it blindly.
- Detailed facts stay in their authoritative project documents. `roadmap.md` controls the whole-project structure, `List.md` controls the current phase, and `NOW.md` is only a resumable checkpoint.
- In external collaboration systems, the external issue or ticket remains the collaboration and handoff authority. Mirror only the concise local execution state here; do not replace required collaboration updates.
- Never store credentials, tokens, private keys, chat IDs, or other secret values in these files.

## Owner-Facing Reports

- Report progress and completion in plain language the owner can use to judge the work. State what changed, how it was checked, and what remains or is blocked.
- Do not rely on unexplained workflow labels, English status jargon, commit terminology, hashes, tool names, or internal process names as the explanation. Include such details only as optional evidence after the plain-language result, and explain them when they matter.
- A technically accurate report is incomplete if the owner cannot tell whether the requested outcome was achieved.

## Compaction And Completion

- A compaction summary should still begin with the task goal and mention the project root, but execution resumes by reading the on-disk `roadmap.md`, `List.md`, and `NOW.md`.
- Before a final response, verify that the roadmap phase is current, `List.md` is ordered and limited to that phase, completed work and blockers are accurate, document pointers have no known orphan, the next action is current, and `NOW.md` still has exactly three lines.
- Do not add hooks or build a separate compaction system for this workflow. Timely file updates are the intended mechanism.
