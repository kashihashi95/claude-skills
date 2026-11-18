---
name: "lean-thread-work"
description: "Use when doing multi-step build or research work in a project thread, to keep token cost low: slice work into fresh threads with handoff notes, and wait for long runs with one scheduled wake-up."
---

# Lean thread work

Cost is driven by the number of steps times the context size: every step re-reads the whole conversation. Keep both small.

## 1. One slice per thread, started from a handoff note
- Before a thread's context grows past roughly 80-100k tokens, or when a slice of work is done (e.g. benchmark finished, a version built), stop and write a handoff note.
- Handoff note (save to the project folder, e.g. `handoffs/<topic>_<date>.md`, under ~1 page):
  - Goal and what the user decided (quote their words for decisions).
  - Current state: branch/commit, files touched, what works, what is verified.
  - Open items and the next concrete step.
  - Where things live (paths, artifacts, scripts) and gotchas found.
- Start a fresh thread for the next slice (or ask the coordinating agent to), with the note as its brief. The new thread reads the note, not the old conversation. A template is in `examples/handoff-note-template.md`.
- Aim for threads that stay near 50k context: a quarter the cost per step of a 200k thread.

## 2. Wait for long runs with one scheduled wake-up
- When starting anything that takes minutes (builds, benchmarks, exports, a run on the user's PC), estimate its duration, run it in the background writing to a log/result file, then schedule ONE wake-up (whatever scheduling tool the session has, such as a send-later or scheduled-task tool) slightly after the expected finish. If there is no scheduling tool, end the turn and say when to check back.
- Do not poll repeatedly. On wake, read only the tail of the log or the result file.
- If it is not finished, schedule one more wake-up based on remaining progress, not a fixed short interval.

## 3. Fewer, bigger steps
- Batch related commands into one script call (build + check + timing + staging), e.g. a project `dev.sh`.
- Read only the needed lines of files (grep, sed -n) instead of whole files; keep tool output short (tail, summaries).

## 4. Report
- When reporting, mention if a slice was handed off, and where the handoff note is.