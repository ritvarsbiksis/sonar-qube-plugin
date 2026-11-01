# sonar-qube-plugin

A Claude Code plugin marketplace with one plugin, **`sonarqube`**. It gives Claude two SonarQube skills: one for
running the SonarQube platform (scanner, quality gates, PR analysis, CI), and one that sweeps every code file Claude
touches against the highest-signal Sonar rules.

## What's included

| Skill | What it does | When it loads |
|---|---|---|
| **`sonarqube-rules`** | Sets up and runs SonarQube Server / SonarQube Cloud: `sonar-scanner` and `sonar-project.properties`, Sonar Way profiles, quality gates on new code, branch and PR analysis, CI with `sonarqube-scan-action`, the REST API, and a mandatory false-positive triage workflow (`NOSONAR`, `@SuppressWarnings`, server-side resolutions). | Claude picks it up when you work on SonarQube or SonarCloud setup, or call it directly. |
| **`sonar-rules`** | A rule catalogue and sweep procedure: the highest-signal Sonar rules (S100, S107, S125, S3776, S6606 …), the full 269-rule SonarJS catalogue, wiring `eslint-plugin-sonarjs`, per-file overrides for legitimate exceptions, a no-suppression policy, and per-language equivalents (golangci-lint, ruff, SonarJava, SonarC#, SwiftLint, clippy). | Limited by `paths:` to source files (TS/JS, Python, Go, Ruby, Rust, Java, Kotlin, Swift, Dart, C#, C/C++, Lua, PHP, Vue) and ESLint / Sonar config files. |

Once installed, the skills are namespaced as `sonarqube:sonarqube-rules` and `sonarqube:sonar-rules`.

`sonar-rules` uses Sonar's default thresholds. It also documents an optional **strict profile** (for example, cognitive
complexity ≤ 10 instead of 15) that Claude applies only when a project or user opts in.

## Install

Inside Claude Code:

```text
/plugin marketplace add /path/to/sonar-qube-plugin
/plugin install sonarqube@sonarqube-skills
```

Or from a shell:

```bash
claude plugin marketplace add /path/to/sonar-qube-plugin
```

```bash
claude plugin install sonarqube@sonarqube-skills
```

To try it for one session without installing:

```bash
claude --plugin-dir /path/to/sonar-qube-plugin
```

Once the repo is on GitHub, replace the path with `ritvarsbiksis/sonar-qube-plugin`.

## Requirements

Neither skill needs an MCP server. `sonarqube-rules` assumes a SonarQube Server or SonarQube Cloud instance plus a
`SONAR_TOKEN` when you actually scan. `sonar-rules` works in any repo, and its TS/JS checks use
`eslint-plugin-sonarjs`.

## Layout

```
.claude-plugin/
  marketplace.json      # marketplace "sonarqube-skills"
  plugin.json           # plugin "sonarqube"
skills/
  sonarqube-rules/SKILL.md
  sonar-rules/SKILL.md
  sonar-rules/references/   # eslint-setup, typescript-rules, sweep-and-reporting, cross-language, sonarjs-catalog
```

## Credits

Both skills are adapted from MIT-licensed upstream projects:

- `sonarqube-rules` — [testland/qa](https://github.com/testland/qa) by testland
- `sonar-rules` — [Nmor/the-council](https://github.com/Nmor/the-council) by nmor

[NOTICE.md](NOTICE.md) lists the pinned upstream commits, the license texts, and every change made for this plugin.
SonarQube, SonarCloud and SonarLint are trademarks of SonarSource SA. This project is not affiliated with SonarSource.

## License

MIT — see [LICENSE](LICENSE). Upstream content stays under its original MIT licenses (see [NOTICE.md](NOTICE.md)).
