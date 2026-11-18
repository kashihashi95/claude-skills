---
name: "mistake-to-system"
description: "When Claude or the user catches a mistake or a miss in Claude's work, find the process cause, add a check that would have caught it, and save the lesson."
---

# Mistake to system

Use this whenever a mistake or a miss is caught, by the user or by you. That includes a wrong fact, a skipped file, a claim that turned out false, or a step that was forgotten.

## Steps

1. **Say plainly what was missed.** Name it and its effect, without excuses.
2. **Find the process cause.** Look for the habit that let it through, not the one-off slip. Common causes:
   - Answering from what is in view instead of measuring the whole set.
   - Trusting memory or a summary instead of checking the source.
   - Testing only the happy path.
   - Stopping at the first plausible cause.
3. **Write the smallest check that would have caught it.** Make it a concrete action at a named moment. For example: "Before any claim about the biggest, which ones or all, run the measurement over the whole set and quote the numbers."
4. **Fix the instance now** with that check.
5. **Save the lesson.**
   - Put it in the project's memory in a single lessons file. Merge it with any overlapping lesson rather than adding a near-duplicate.
   - If it applies beyond this project, propose it as an edit to this skill's lessons list below.
6. **Keep the list short.** At 15 lessons, merge or retire the ones that no longer fire. A lesson that has not mattered in a long time is dead weight.

## Lessons that apply to any project

1. **Measure the whole set, don't answer from what's in view.** Before saying which files, threads or items are the biggest, oldest or affected, run the measurement across all of them (`wc -l`, a repo-wide grep, a full listing) and quote the numbers.
2. **Size delegated work to the delegate's quota, in slices that each finish.** Before handing a job to a metered tool or another agent, check or ask how much quota it has left. Split the job so each slice ends in a usable, handed-back state, and tell it to skip work you already have (such as baseline test runs).
3. **Facts from the source, end to end; then scan for the same bug everywhere.** Before saying what something does or how long it lasts, trace it in the code from start to stop. A gap in logs means read the code, not guess. When a bug class turns up, check every instance of it, not just the one reported.
4. **Options shouldn't silently inherit a limit.** When a choice keeps an existing number or cap, say where it comes from, and offer one option without it, modeled on the closest existing system.
5. **Check a live page's freshness before quoting it.** Before quoting a price, stock count or status from a fetched page, compare its freshness clues (estimated delivery date, "last updated") with today's date. If they are stale or missing, label the figure unconfirmed.

See `examples/stale-price.md` for a full worked example.