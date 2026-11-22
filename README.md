### Agent Skills

When a task matches a skill below, read `.agents/skills/<name>/SKILL.md` and follow its instructions. Combine skills only when their scopes overlap; use the most specific skill for the task. Review skills are opt-in and must only be activated when the user requests a review or audit.

#### anti-slop-design

Use when creating or substantially redesigning a visual frontend interface, including pages, dashboards, games, or components. Preserve existing project design-system constraints.

#### caveman

Use when the user asks for caveman mode, terse replies, or fewer tokens, including `/caveman`, “talk like caveman,” “be brief,” or “less tokens.” Continue until the user says “stop caveman” or “normal mode.”

#### coding-style

Use when starting a module, refactoring for readability or consistency, reviewing maintainability or naming, or setting up linting, formatting, and type-checking conventions. Framework-specific skills take precedence for framework-specific details.

#### micro-interaction

Use when the user asks to specify or hand off a single micro-interaction. Cover trigger, rules, feedback, loops and modes, timing, and accessibility. For motion-only principles or implementation, use the relevant design or framework skill instead.

#### ponytail

Use by default for coding tasks, including writing, fixing, refactoring, and dependency choices. Also activate for “ponytail,” “be lazy,” “simplest solution,” “yagni,” or requests to reduce over-engineering. Remains active until the user says “stop ponytail” or “normal mode.” Level can be switched with `/ponytail lite|full|ultra`.

#### ponytail-review

Use only when the user asks for a code review or audit of a repo, folder, or package. Review connected code and report findings; do not make changes as part of the review.

#### shadcn-svelte

Use when the task involves shadcn-svelte, its CLI or components, or any frontend project containing `components.json`. Follow the project’s package manager and existing component configuration.

#### web-design

Use only when the user asks to review UI for accessibility, UX, or web-interface best-practice compliance, such as “review my UI,” “audit design,” or “check accessibility.”