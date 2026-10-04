# Skills

[简体中文](README.md) | English

[Towano/skills](https://github.com/Towano/skills) is a fork of [yspbwx2010/skills](https://github.com/yspbwx2010/skills). It keeps the eight [Agent Skills](https://agentskills.io/specification) supplied by the upstream author and adapts the fork's repository entry points and maintenance preferences.

Each skill installs on its own, take only the ones you want

Individual skill docs are inherited from upstream and may still show upstream installation commands. Use this page to install from the fork.

## Skill list

| Skill | For |
| --- | --- |
| [miuix](miuix/README.en.md) | Build apps with [Miuix](https://github.com/compose-miuix-ui/miuix) |
| [kpm](kpm/README.en.md) | Write [KernelPatch](https://github.com/bmax121/KernelPatch) modules (KPM) |
| [apm](apm/README.en.md) | Write Magisk modules (APM) |
| [metamodule](metamodule/README.en.md) | Write a [metamodule](https://kernelsu.org/guide/metamodule.html) |
| [mcpp](mcpp/README.en.md) | Build C++23 module projects with [mcpp](https://github.com/mcpp-community/mcpp); package libraries for mcpp-index |
| [xlings](xlings/README.en.md) | Use the [xlings](https://github.com/openxlings/xlings) package manager; write xim-pkgindex packages |
| [mcpp-style-ref](mcpp-style-ref/README.en.md) | Modern / Module C++ (C++23) coding style |
| [gki](gki/README.en.md) | Write Android GKI kernel modules; change the kernel without breaking the KMI |

## Install

> Replace `<skill>` with a name from the table above. The current adaptation lives on `feature/personal-guidance`; the commands below pin that experimental branch.

### 1. Skills CLI (Claude Code, Codex, Cursor, OpenCode and 40+ other agents)

```bash
npx skills add 'Towano/skills#feature/personal-guidance' --skill <skill>
npx skills add 'Towano/skills#feature/personal-guidance' --list      # list every skill in the repo
```

### 2. Claude Code plugin marketplace

```text
/plugin marketplace add Towano/skills#feature/personal-guidance
/plugin install <skill>@Towano-skills
```

### 3. Manual copy

Copy `<skill>/skills/<skill>/` into your agent's skills directory, e.g. `~/.claude/skills/` for Claude Code

See each skill's README for other agents' directories

## Layout

One directory per skill; the README, changelog, maintenance notes and tooling all live in it, and only `<skill>/skills/<skill>/` is installed

For the full layout and the steps to add a skill, see [AGENTS.md](AGENTS.md)

This fork follows upstream's layout and documentation conventions, with existing requirements taking precedence. The root AGENTS.md preferences only supplement otherwise unspecified choices in maintaining this fork; they are not included in skill installs.

## License

[MIT](LICENSE), except [mcpp-style-ref](mcpp-style-ref/README.en.md) (CC BY-NC-SA 4.0, copied from upstream)
