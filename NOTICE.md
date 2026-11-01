# Third-party notices

This plugin redistributes adapted versions of two MIT-licensed skills. For each one, this file lists its source, its
license, and every change made for this plugin.

## `skills/sonarqube-rules/` — testland/qa

- Source: https://github.com/testland/qa/blob/47218e9b696bc443c6e3673800b2a6c4e1c34646/plugins/qa-security-scanning/skills/sonarqube-rules/SKILL.md
- Listing: https://www.skillsdirectory.com/skills/testland-sonarqube-rules
- Pinned commit: `47218e9b696bc443c6e3673800b2a6c4e1c34646`
- License: MIT, Copyright (c) 2026 testland

Changes from upstream:

1. Replaced the references to sibling skills that aren't part of this plugin (`semgrep-rules`, `codeql-queries`,
   `language-native-sast`) with plain tool names (Semgrep, CodeQL, language-native SAST tools).
2. Fixed the licensing claim in "Limitations". Upstream said "License changed from LGPL to SSPL in 2024". According to
   sonarsource.com/license, the analyzers bundled with SonarQube Community Build and SonarQube for IDE have been under
   the Sonar Source-Available License v1 (SSALv1) since 29 November 2024, while the platform stays LGPLv3.
3. Left out `.tessl-plugin/plugin.json` (another tool's manifest).

## `skills/sonar-rules/` — Nmor/the-council

- Source: https://github.com/Nmor/the-council/tree/22e5312f797bf68ce4811ef8d0bac34e798c36bd/skills/sonar-rules
- Listing: https://www.skillsdirectory.com/skills/nmor-sonar-rules-the-council
- Pinned commit: `22e5312f797bf68ce4811ef8d0bac34e798c36bd`
- License: MIT, Copyright (c) 2026 nmor. Upstream also notes that the standards it cites (OWASP, NIST, ISO/IEC and
  others) remain the property of their respective organisations and are referenced by citation only.

Changes from upstream — `SKILL.md`:

1. Removed `disable-model-invocation: true` from the frontmatter. It contradicted the description ("Use when touching
   any code file") and made the `paths:` globs useless. `paths:` is unchanged.
2. Retitled the skill from "SonarLint / SonarQube Checks (Global Default)" to "SonarLint / SonarQube Checks". Removed
   the size-budget line (`~/.claude/scripts/token-budget.mjs`) and the migration note (`~/.claude/rules-library/…`,
   "Phase H").
3. Rewrote the "Threshold-tightening note". Upstream, a private `extreme-lint-policy.md` overrode Sonar's defaults.
   Here Sonar's defaults are the baseline, the project's own config wins, and the same stricter caps (S3776 10,
   S138 80, S107 5, S104 500, S134 3, S1067 2, S109 `0, 1, -1, 2`) are offered as an opt-in "strict profile". Removed
   the "Rule 5: Zero Tolerance" label but kept its intent: fix every violation in the touched file.
4. Renamed "Why this is global" to "Why this applies everywhere". Removed the references to
   `feedback_check_sonar_proactively`, "The Council's verification-loop" and the author's VS Code / ErrorLens setup,
   and generalized that line to "if SonarQube for IDE (SonarLint) is enabled".
5. Renamed "Learning hooks" to "Maintaining this skill" and removed the reference to
   `~/.claude/rules/common/continuous-learning-mandate.md`. The `extreme-lint-policy.md` drift signal is now
   "Strict-profile thresholds out of sync with the project's lint config".

Changes from upstream — `references/`:

1. All five files: removed the "Size budget … `token-budget.mjs --check`" line.
2. `cross-language.md`: "per `no-silent-failures.md`" → "(swallowed errors, unchecked returns)".
3. `eslint-setup.md`: "CI and the Council's verification-loop" → "CI and automated verification".
4. `sweep-and-reporting.md`: step 2 now names `typescript-rules.md` as the source of the literal-pattern checks
   (upstream said "above", referring to its original single file). Step 3 now refers to "IDE diagnostics available in
   the session" instead of an `<ide_diagnostics>` PostToolUse hook. Removed "Per `feedback_no_silencers`:".
5. `typescript-rules.md`: rewrote "every rule the user has flagged as recurring … global no-silent-* / no-discards
   hooks" without the private hooks. "Error handling (sister to `no-silent-failures.md`)" → "Error handling (no silent
   failures)". In both S2068 rows, "The PostToolUse `no-discards` hook will reject the edit." → "Never commit the
   literal."
6. `sonarjs-catalog.md`: no changes other than item 1.

## MIT License (applies to both upstream projects)

```
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
