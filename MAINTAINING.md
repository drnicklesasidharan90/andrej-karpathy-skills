# Maintaining this repository

Notes for maintainers and AI assistants working **inside** `andrej-karpathy-skills`. Downstream users who copy `CLAUDE.md` into their own projects do not need this file.

## What this repo is

A documentation-only distribution. There is **no build, no tests, no lint, no package manifest, no CI**. The repo ships one document — the four behavioral principles — in several mirrored formats, plus human-facing READMEs and a plugin manifest.

`CLAUDE.md` is itself the distributed artifact (see the `curl` snippet in `README.md`). Editing it changes what every downstream project receives the next time they re-run that snippet. Treat it as published.

## Files that mirror the four principles

After any change to the principle text, these three files must say the same thing:

- `CLAUDE.md` — root, copied verbatim via `curl` per `README.md`
- `.cursor/rules/karpathy-guidelines.mdc` — Cursor project rule with `alwaysApply: true` frontmatter
- `skills/karpathy-guidelines/SKILL.md` — Agent Skill, also what the Claude Code plugin ships

Frontmatter and surrounding framing differ; only the four-principle body must match.

## Files that summarize or extend the principles

- `README.md` and `README.zh.md` — English and Chinese human-facing summaries (the principle table, bullet lists, install instructions). Keep them aligned with each other.
- `EXAMPLES.md` — good/bad code examples per principle. Update if an example becomes inconsistent with revised principle wording.
- `CURSOR.md` — Cursor-specific setup. Already states the sync rule for principle files.

## Plugin distribution

- `.claude-plugin/marketplace.json` defines marketplace `karpathy-skills` with one plugin entry (`andrej-karpathy-skills`, source `./`).
- `.claude-plugin/plugin.json` references `./skills/karpathy-guidelines`.
- `version` appears in both manifests — bump together when shipping.

The install commands published in `README.md` reference these exact names:

```
/plugin marketplace add forrestchang/andrej-karpathy-skills
/plugin install andrej-karpathy-skills@karpathy-skills
```

Do not rename `andrej-karpathy-skills`, `karpathy-skills`, or the `skills/karpathy-guidelines/` path without updating both manifests and `README.md`.

## Sync checklist for principle changes

1. Update `CLAUDE.md`, `.cursor/rules/karpathy-guidelines.mdc`, and `skills/karpathy-guidelines/SKILL.md` so the four-principle body matches.
2. Update `EXAMPLES.md` if any example references wording that changed.
3. Update `README.md` and `README.zh.md` summaries together.
4. Bump `version` in `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` if releasing.

## Validation

No automated checks. After changes, diff the three principle files side-by-side and confirm the four-principle body is identical.

## Constraints downstream consumers depend on

- `CLAUDE.md` lives at repo root and is fetched by the raw GitHub URL in `README.md`'s `curl` instructions — do not rename or relocate it.
- `.cursor/rules/karpathy-guidelines.mdc` keeps `alwaysApply: true` so Cursor users get the rule automatically.
- The plugin and marketplace names above are referenced by external install commands.
