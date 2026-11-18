# Worked example: a stale price from a cached listing page

A real case from planning a used-GPU server build with Claude (November 2026).

## What happened

Claude was checking used datacenter GPU listings and quoted an NVIDIA V100 on eBay at **$259.99 with 10 in stock**. The page it had fetched was a cached copy. The live listing was **$385 with 182 in stock**: about 48% more per card, on a build that needed six to eight of them.

## The skill, step by step

**1. Say plainly what was missed.**
"I quoted $259.99 / 10 in stock from a cached page. The live price is $385 / 182 in stock, so the build estimate was low by about $125 per card."

**2. Find the process cause.**
Not "the page was wrong." The habit that let it through: *trusting a fetched page as current without checking whether it was.* The page had clues: its estimated delivery date was already in the past.

**3. Write the smallest check that would have caught it.**
> Before quoting a live price or stock count from a fetched listing page, compare its freshness clues (estimated delivery date, "last updated") with today's date. If they are stale or missing, label the price unconfirmed.

**4. Fix the instance now.**
Re-check every price in the build list with that check, and correct the totals.

**5. Save the lesson.**
It went into the project's lessons file, and because it applies to any project that quotes live web data, it was added to this skill's general lessons list (lesson 5).

## Why this matters

A one-off correction fixes one number. A saved check fixes the habit, so the same class of error is caught next time, in any project, without the user having to spot it again.
