# Claude skills for reliable, low-cost agent work

Three Agent Skills I wrote and use daily with Claude and Claude Code. Each one fixes a problem I kept running into on long, multi-step AI projects.

| Skill | Problem it solves | What it makes the agent do |
|---|---|---|
| [mistake-to-system](skills/mistake-to-system/SKILL.md) | The same kind of mistake comes back in a later session | Turn every caught mistake into a root cause, a concrete check, a fix and a saved lesson |
| [lean-thread-work](skills/lean-thread-work/SKILL.md) | Long threads burn through usage limits | Work in short threads joined by handoff notes, and wait for long jobs with one wake-up instead of polling |
| [file-size-discipline](skills/file-size-discipline/SKILL.md) | AI-written code grows into huge files that are slow and error-prone to edit | Measure file sizes when planning, and split by responsibility past set caps, with proof nothing changed |

## Why I built these

I spent years in aerospace manufacturing, where a defect isn't closed until you've found the root cause and changed the process so it can't happen again. When I started building software with AI agents, I saw the same pattern: fixing a mistake once didn't stop it from coming back. These skills apply that manufacturing habit (root cause, standard work, waste reduction) to how an AI agent works.

## mistake-to-system

When the user or the agent catches a mistake, the agent:

1. Says plainly what was missed.
2. Finds the habit that let it through, not just the one-off slip.
3. Writes the smallest concrete check that would have caught it.
4. Fixes the current instance with that check.
5. Saves the lesson, merging it with similar ones and capping the list at 15.

Worked example: [a stale price quoted from a cached page](skills/mistake-to-system/examples/stale-price.md).

## lean-thread-work

Every step an agent takes re-reads the whole conversation, so cost grows with **steps × context size**. A step in a 200k-token thread costs about four times as much as one in a 50k-token thread. This skill keeps both numbers small:

- Ends a thread at around 80–100k tokens, or when a slice of work is done, and writes a one-page handoff note ([template](skills/lean-thread-work/examples/handoff-note-template.md)) that the next thread starts from.
- Runs long jobs in the background and schedules one wake-up near the expected finish instead of polling.
- Batches commands and reads only the lines it needs.

## file-size-discipline

| Lines in a file | Action |
|---|---|
| Under ~800 | Fine |
| Over 1,200 | The next change that touches it plans a split |
| Over 2,000 | Split before adding any feature |

Splits are by responsibility, keep the public interface the same, run the same tests before and after, and land as their own commit.

## Install

Each skill is a folder with a `SKILL.md`.

- **Claude Code:** copy a skill folder into `~/.claude/skills/` (all projects) or `.claude/skills/` in a repo (that project only).
- **Claude apps:** zip a skill folder and upload it as a custom skill in Claude's settings.

## License

MIT. See [LICENSE](LICENSE).
