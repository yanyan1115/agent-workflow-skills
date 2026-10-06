# Decisions

Read before overturning a choice. Superseded entries stay, marked as superseded.

- 2026-10-06: Added `decisions.md` as a fourth project-start file in `project-task-state`. Reason: decision reasons get lost across compaction and handoff, and re-deriving them can undo correct choices. Kept out of the per-session read order so startup cost does not grow.
