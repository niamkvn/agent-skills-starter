---
name: web-design
description: >
   Reviews files against the Web Design guidelines (accessibility, performance,
   best practices). Use after coding to audit UI files.
metadata:
  author: niamkvn
  version: 1.0.0
---

# Web Design

Review files against the Web Design guidelines.

## Guidelines Source

Load the latest guidelines via Context7, Tavily, BraveSearch, or Serper.dev (or IDE docs). If all fail, use WebSearch or WebFetch. The guidelines contain all rules and the output format.

## Workflow

1. Load the guidelines
2. Read the specified files. If none given, ask which files or pattern to review
3. Apply all rules
4. Output findings in terse `file:line` format per the guidelines

## Related Skills

- [anti-slop-design](../anti-slop-design/SKILL.md): before coding, for design principles
- web-design (this): after coding, to audit accessibility, performance, and best practices

Flow: design (anti-slop-design) -> code -> audit (this skill) -> fix findings.