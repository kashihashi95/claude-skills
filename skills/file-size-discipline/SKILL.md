---
name: "file-size-discipline"
description: "Keep source files at a workable size in any codebase: check sizes when planning changes, and split a file by responsibility past the caps, with a map of what moved and proof behaviour is unchanged."
---

# File size discipline

Large files make every change cost more. More of the file has to be read, more rules have to be checked, and edits collide. Keep files small on purpose.

## When to check

Check sizes at the start of planning any change, and before answering any question about code size or structure. Measure every source file, not just the one at hand:

```
find . -name '*.<ext>' -not -path '*/node_modules/*' | xargs wc -l | sort -rn | head -15
```

## Caps (lines of code; adjust for very terse or very verbose languages)

| Size | What to do |
|---|---|
| Under about 800 | Fine. |
| Over 1,200 | The next change that touches the file includes a split in its plan. |
| Over 2,000 | Split before adding any new feature to the file. |

One function over about 150 lines is a split candidate too.

## How to split

1. **Split by responsibility**, the parts of the system a person would name, not by alphabet or line count. Keep hot paths and shared core state where they are when moving them would cost performance.
2. **Keep the public surface stable.** Callers use the same names, through a thin forwarder if needed.
3. **Prove nothing changed.** Run the same tests before and after, plus any seeded or deterministic runs the project has. A pure split changes no behaviour.
4. **Update the map.** Keep one short doc, or the project's interaction table or flowchart, that says which file owns what and which parts depend on which. Regenerate it from the code if the project has a generator.
5. **Do the split as its own commit**, separate from feature work, so it can be reviewed and reverted alone.

## Report

When you mention sizes to the user, give the measured numbers for the largest few files and say which ones cross a cap.