---
name: ponytail-review
description: >
   Read-only senior-dev review of a repo: bugs, risks, scale, missing tests,
   speed, bloat. Use when asked to review or audit a codebase.
metadata:
  author: niamkvn
  version: 1.0.0
---

# Ponytail Review

Review the repo like a senior developer who just inherited it and will be called when it breaks. Priorities: correct, safe, holds under load, tested, fast, lean. Every extra line must be read, tested, and fixed later. This is a report the user asked for, so write it in full.

## 1. Map First

- Review what the user names (folder, package, or repo). Not named: whole repo.
- Read README, build/deploy config, dependency list, entry points (main, routes, handlers, jobs, CLI), and tests.
- Determine expected load (one person running a script, or many users/processes at once). Judge scale against it and state the assumption.
- Trace the main flow end to end: data in, stored, out. Read in full the paths for user input, money, auth, data writes, background jobs, and state shared across processes.
- Large repo: go deep on the parts costliest if wrong, not file by file. Name the parts not read.

## 2. Look For

1. **Bugs:** wrong results, crashes, missed edge cases (empty, zero, last item, rounding, time zones), caller not matching function return, same rule applied differently in two places.
2. **Risks:** security holes (injection, weak randomness, secrets in code, unvalidated user input), data loss (swallowed errors, wrong write order, no transaction).
3. **Scale:** safe for one user, wrong for many: check-then-write races, same work repeated per process, memory/lists that keep growing, per-item queries, O(n^2) on large input, per-process state that should be shared.
4. **Missing tests:** risky logic (branches, parsers, money, security, data writes) with no test that fails when the logic breaks. One good test, not coverage.
5. **Speed:** big slowdown = problem. Small optimization (repeated work in hot loop) = suggestion.
6. **Lean:** code that need not exist or should be smaller.
   - delete: dead code, unused options/flags/config, speculative features
   - reuse: two helpers do the same thing (keep one, name its path)
   - stdlib/native: already provided by the standard library or platform; dependency whose work fits in a few lines
   - yagni: interface with one implementation, factory with one product, wrapper that only forwards calls
   - merge: similar copies that must change together
   - split: one function/class with several unrelated jobs. Split by job, not line count, and do not make helpers that only shorten the function.

## 3. Verify Before Reporting

- Every finding needs a concrete case: "this input/situation gives this wrong result". No case, not a finding.
- Before calling code unused, grep the whole tree, including tests, fixtures, config, and string/dynamic references.
- A shortcut marked with a `shortcut:` comment (or old `ponytail:`) that states its limit is a decision, not a finding, unless the expected load already exceeds it.
- Propose the smallest fix that works. Prefer fixes that delete code. Do not add layers, frameworks, or config that are not needed.
- No style taste, no "consider", no vague worries.

## 4. Output

Simple English: short sentences, everyday words. Explain technical terms on first use. The reader may never have seen this code.

Start with `What this repo does:` (2-3 sentences) and the assumed load.

Then findings in three groups, most important first, skip empty groups:

- **Must fix:** bugs, security, data loss, breaks under expected load.
- **Should fix:** risky code without tests, clearly slow, duplication, functions mixing jobs, code that need not exist.
- **Nice to have:** small optimizations, shorter shapes.

Number findings continuously across groups so the user can say "fix 2 and 5". Maximum 20 findings; state how many were skipped. Each finding has four parts, 1-2 short sentences each:

2. **Order booked on the wrong day** (`billing/close_day.py:L40-52`)
   - **What this is:** The midnight job closes the day and bills all orders of that day.
   - **Problem:** "Today" comes from the server clock (UTC). An order at 00:30 in Berlin is billed on the previous day.
   - **Fix:** Compute the day once in the store's time zone: `datetime.now(ZoneInfo("Europe/Berlin")).date()`.
   - **If skipped:** Late-night orders get the wrong date, accounting fixes them by hand.

End with:

- `Verdict:` one line: healthy, or what to fix first.
- `Lean: -<N> lines, -<M> dependencies possible.` if there are lean findings.
- `Not checked:` parts not read or not runnable.

No findings: `What this repo does:`, then `Healthy. Nothing to fix.` and one line on what was checked.

One-time report, does not change code.