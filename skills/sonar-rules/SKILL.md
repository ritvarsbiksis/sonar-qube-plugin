---
name: sonar-rules
description: SonarLint / SonarQube / SonarJS rule catalogue (full 269-rule reference) plus per-language equivalents (golangci-lint, ruff, rubocop, errorlint, NullAway, clippy). Use when touching any code file to sweep against the highest-signal Sonar rules (S100, S107, S125, S138, S1192, S1481, S1854, S2068, S3358, S3776, S5547, S6571, S6606, S6594, S6644, S6759, S7755, S7773, S7780, S7781), apply per-file overrides for legitimate exceptions (test files, SSRF validators, domain nouns), and configure eslint-plugin-sonarjs at sonarjs/recommended.
paths:
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.js"
  - "**/*.jsx"
  - "**/*.mjs"
  - "**/*.cjs"
  - "**/*.mts"
  - "**/*.cts"
  - "**/*.py"
  - "**/*.go"
  - "**/*.rb"
  - "**/*.rs"
  - "**/*.java"
  - "**/*.kt"
  - "**/*.kts"
  - "**/*.swift"
  - "**/*.dart"
  - "**/*.cs"
  - "**/*.c"
  - "**/*.cpp"
  - "**/*.cc"
  - "**/*.cxx"
  - "**/*.h"
  - "**/*.hpp"
  - "**/*.lua"
  - "**/*.php"
  - "**/*.vue"
  - "**/.eslintrc*"
  - "**/eslint.config.*"
  - "**/.sonarcloud.properties"
  - "**/sonar-project.properties"
---

# SonarLint / SonarQube Checks

## Standards Cited

- **SonarSource Rule Specifications** (rules.sonarsource.com) — canonical authority for every
  `S<number>` rule in this catalog (S100, S107, S125, S138, S1192, S3776, S6571, S6594, S6606, etc.)
- **CWE-94** — Improper Control of Generation of Code (S2076 / S6587 + family)
- **CWE-89** — SQL Injection (S2077 / S3649)
- **CWE-79** — Cross-Site Scripting (S5247 / S6299)
- **CWE-798** — Hard-coded Credentials (S2068)
- **CWE Top 25** Most Dangerous Software Weaknesses (mitre.org/cwe) — Sonar rule severity ladder
  maps to CWE
- **OWASP Top 10 A03:2021** Injection — S2076 / S2077 / S5247 cluster
- **OWASP Top 10 A07:2021** Identification + Authentication Failures — S2068 / S5547 cluster
- **OWASP ASVS 4.0.3 §5** Validation — S2755 (XXE) / S4502 (CSRF disabled)
- **ISO/IEC 25010:2011** Quality Model — Sonar maintainability / reliability / security ratings
  derive from this
- **NIST SP 800-53** SI-10 Information Input Validation — Sonar's injection-class rules align

> This skill applies to every code file. Whenever Claude touches code in any project — new or
> legacy, with or without a project-level Sonar setup — it verifies the file against the rules below
> and fixes every violation in the touched file before declaring the task done.
>
> **Thresholds**: this skill lists the Sonar rule IDs with their canonical default thresholds, and
> those defaults are the baseline. A project's own Sonar or ESLint configuration always wins. Teams
> that want a stricter bar can adopt this optional **strict profile**: cognitive complexity (S3776)
> cap **10** (default 15), function lines (S138) cap **80** (default 200), function parameters
> (S107) cap **5** (default 7), file lines (S104) cap **500** (default 1000), nested control-flow
> depth (S134) cap **3** (default 4), boolean expression operators (S1067) cap **2** (default 3),
> magic-number tolerance (S109) allows only `0, 1, -1, 2`. Apply the strict profile only when the
> project or the user opts in.

## Why this applies everywhere

SonarLint is a quality safety net that catches the same bugs across every language. Applying it by
default means:

- Every project benefits, even ones that don't have SonarLint installed locally.
- Claude doesn't wait to be asked — it sweeps touched files proactively.
- Verification has a concrete checklist instead of "looks fine."

If SonarQube for IDE (SonarLint) is enabled in the editor, it flags the same rules inline. Claude's
job is to address them before declaring a task done.

## Where each topic lives

This file is the routing table. Read the reference file for the topic in hand;
do not carry the whole catalogue to answer one question.

| Topic | Reference file |
| ---- | ---- |
| Wiring SonarJS into a TypeScript / JavaScript repo (mandatory step); stylistic rules to disable; per-file overrides for legitimate exceptions; Eqeqeq + null; Vue / React projects; ESLint guardrails for every TS/JS project | [`references/eslint-setup.md`](references/eslint-setup.md) |
| Mandatory checks on every touched file — the comprehensive TypeScript / JavaScript rule reference (string / regex idioms, style / idiom, type / control-flow, error handling, security, suppression / meta, numerical) and the cross-language quick table | [`references/typescript-rules.md`](references/typescript-rules.md) |
| Sweep procedure; Don't silence — fix; Output expectation | [`references/sweep-and-reporting.md`](references/sweep-and-reporting.md) |
| Cross-language Sonar coverage — Go (SonarGo / golangci-lint), Python (SonarPy / ruff), Java (SonarJava), C# (SonarC#), Swift (SwiftLint), Rust (clippy) | [`references/cross-language.md`](references/cross-language.md) |
| Full SonarJS catalog — every rule, all 269, with ESLint rule name and `sonarjs/recommended` default | [`references/sonarjs-catalog.md`](references/sonarjs-catalog.md) |

## Maintaining this skill

**Signals to watch**:

- New TS/JS repo opened without `eslint-plugin-sonarjs` wired (mandatory-step weakening)
- SonarLint IDE warnings ignored / dismissed across multiple sessions on the same project
- Per-line `// eslint-disable` / `// @ts-ignore` introduced to silence a Sonar rule (rule-violation
  shortcut)
- File-level grep sweep skipped on touched-file audit (sweep procedure step 2 weakening)
- Recurring rule fires in the same file (e.g., S1192 fires 3× per quarter on `apiClient.ts`) — the
  underlying pattern needs structural fix
- Strict-profile thresholds out of sync with the project's lint config (threshold drift)
- Cross-language equivalents missing on touched files (Go / Python / Java / C# / Swift / Rust
  per-language equivalents skipped)
- Stylistic disable-list grows with rules that produce real bugs (over-disabling — recurrence audit
  needed)

**Refinement candidates**:

- New rule row when a new SonarJS rule ships (the catalog regularly grows; add columns + fix
  recipes)
- Tightening of the disabled-rules list when a previously-stylistic rule starts catching real bugs
- New cross-language entry when a recurring shape gains a Sonar equivalent in another language
  (e.g., SonarRust ships)
- Promotion of a per-file Sonar exception to a project-wide allowlist with documented rationale
  (e.g., SSRF validator file exempt from S1313 by design)
