# Decisions

Read before overturning a choice. Superseded entries stay, marked as superseded.

- 2026-10-06: Added `decisions.md` as a fourth project-start file in `project-task-state`. Reason: decision reasons get lost across compaction and handoff, and re-deriving them can undo correct choices. Kept out of the per-session read order so startup cost does not grow.
- 2026-10-06: Added a machine-level project registry to `project-task-state`. Reason: after compaction an agent carrying several projects could not tell which projects exist or where they live, and projects that build on each other could not find their siblings. Finished projects are marked done, not deleted, so they stay referenceable; the registry is pointed to from an always-loaded index rather than inlined into the instruction file.
