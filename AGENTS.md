# AGENTS.md

## What this repository is

[Towano/skills](https://github.com/Towano/skills) is a fork of
[yspbwx2010/skills](https://github.com/yspbwx2010/skills). The eight
[Agent Skills](https://agentskills.io/specification) come from upstream; this fork adapts the
repository entry points and maintenance preferences. Each skill lives in its own top-level
directory and installs on its own:

The adaptation lives on `feature/personal-guidance`; pin that branch when installing this fork:

- `npx skills add 'Towano/skills#feature/personal-guidance' --skill <skill>`
- `/plugin marketplace add Towano/skills#feature/personal-guidance`, then `/plugin install <skill>@Towano-skills`

| Skill | Directory | Purpose |
| --- | --- | --- |
| miuix | [miuix/](miuix/AGENTS.md) | Build Compose Multiplatform apps with the Miuix UI library |
| kpm | [kpm/](kpm/AGENTS.md) | Write/build/load KernelPatch Modules (KPM) for the arm64 kernel |
| apm | [apm/](apm/AGENTS.md) | Build Magisk modules: standard Magisk-style systemless modules as used by APatch |
| metamodule | [metamodule/](metamodule/AGENTS.md) | Develop a metamodule: the mount/install backend for KernelSU/APatch modules |
| mcpp | [mcpp/](mcpp/AGENTS.md) | Build C++23 module projects with mcpp; package libraries for mcpp-index |
| xlings | [xlings/](xlings/AGENTS.md) | Use the xlings package manager; write xim-pkgindex packages |
| mcpp-style-ref | [mcpp-style-ref/](mcpp-style-ref/AGENTS.md) | Modern/Module C++ (C++23) coding style, copied from upstream (CC BY-NC-SA 4.0) |
| gki | [gki/](gki/AGENTS.md) | Build Android GKI (android15-6.6) kernel modules and make KMI-safe kernel changes |

Before changing anything in `<skill>/`, read `<skill>/AGENTS.md`. It says what that skill is for
and holds its rules. More specific nested guidance takes precedence within its scope.
Run a skill's commands from its own directory.

## Layout

```
<skill>/                         one directory per skill, self-contained
  skills/<skill>/                the installable skill: SKILL.md and what it loads
  AGENTS.md, CLAUDE.md           what the skill is for and its rules; CLAUDE.md is `@AGENTS.md`
  README.md, README.en.md        for users: what it does, how to install it (README.md is Chinese, the default)
  CHANGELOG.md, CONTRIBUTING.md  as needed
  .claude-plugin/plugin.json     Claude Code plugin manifest (name, version)
  tools/, data/, ...             maintainer tooling, never installed
.claude-plugin/marketplace.json  one plugin per skill
tools/check_repo.py              repository layout gate, run by .github/workflows/repo.yml
.github/workflows/<skill>.yml    a skill's own gates, if it has any
```

## Rules

- Keep a skill's files inside its directory. Don't put one skill's tooling at the repository root.
- Both `npx skills` and the Claude Code marketplace find skills **only** through
  `.claude-plugin/marketplace.json`. A skill that isn't registered there cannot be installed.
- Anything under `<skill>/skills/<skill>/` is copied onto users' machines on its own, so it must
  not link outside that directory.
- `python3 tools/check_repo.py` must exit 0.

### Maintainer preferences

These supplementary preferences apply only to maintenance of this fork, not to installed skills.
Follow upstream's layout and documentation conventions. Existing directory rules, domain guidance,
checks and license terms take precedence; use preferences only for choices those requirements leave
open, never to replace or relax them.

Keep personal preferences in private guidance; project and skill guides hold concrete constraints
and experience.

- Lead with the conclusion; keep wording concise, plain and concrete.
- Background is not automatically a task or question. Verify facts first; ask only questions that change direction, results or action boundaries. Discussion is not execution authority.
- Before adding anything, find equivalent implementations and identify the concrete gap.
- Reuse code with the same responsibility; do not force unrelated work together, add frameworks just for deduplication, speculative abstractions/configuration/compatibility, or unrelated refactors.
- Explaining a method does not prove usefulness; additions must solve a real problem.
- Make deliverables self-contained, without correction history or rejected approaches; retain necessary reasons for the current design. Do not turn "omit X" into "no X".
- Distinguish completed, failed and unverified work in reports.
- Skills add domain or tool knowledge, not harness basics. Put machine-checkable requirements in existing tooling, not a new governance system.

For this fork, push only to `Towano/skills` when authorized. Upstream
[yspbwx2010/skills](https://github.com/yspbwx2010/skills) and `Towano/agent-practices` are
reference only, not push targets.

## Adding a skill

1. Create `<skill>/skills/<skill>/SKILL.md`. The directory name must equal the frontmatter `name`.
2. Write `<skill>/AGENTS.md`: what the skill is for, who uses it, what gets installed, its layout
   and its rules. Add `<skill>/CLAUDE.md` containing exactly `@AGENTS.md`, so Claude Code loads it.
3. Add `<skill>/README.md` (Chinese, the default) and `<skill>/README.en.md` (English). To set a version for Claude Code, also
   add `<skill>/.claude-plugin/plugin.json` with the same `name`.
4. Register it in `.claude-plugin/marketplace.json` as `{"name": "<skill>", "source": "./<skill>", ...}`.
5. Add a row to the skill table in both root READMEs (linking to the skill's README in the same
   language) and in this file.
6. If the skill has its own gates, add `.github/workflows/<skill>.yml` with
   `paths: ["<skill>/**", ".github/workflows/<skill>.yml"]` and `defaults.run.working-directory: <skill>`
   (copy `miuix.yml`).
7. Check: `python3 tools/check_repo.py` exits 0, and `npx skills add . --list` lists the skill.
