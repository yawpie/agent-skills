# Agent Skills

Reusable agent skills for Codex and compatible agents. Each skill lives in its own directory and has a required `SKILL.md` entrypoint.

**Bahasa Indonesia:** [README.id.md](README.id.md)

## Available skills

| Skill | Purpose |
| --- | --- |
| [`atomic-commits`](skills/atomic-commits/SKILL.md) | Split task-related code changes into focused, reviewable, traceable Git commits with safety checks. |

## Install in Codex

Inside Codex, ask the skill installer:

```text
$skill-installer install https://github.com/yawpie/agent-skills/tree/main/skills/atomic-commits
```

If the skill is not detected after installation, restart Codex.

Alternatively, clone this repository and copy `skills/atomic-commits` into `~/.codex/skills/` (Windows: `%USERPROFILE%\.codex\skills\`).

## Usage

Explicitly invoke `$atomic-commits` when asking Codex to organize changes into separate commits, or describe a task that matches the skill's metadata. The skill does not commit changes unless you authorize commits.

Example:

```text
$atomic-commits Organize these changes into logical Conventional Commits, run appropriate checks, and commit only files belonging to this task.
```

## Repository layout

```text
agent-skills/
├── README.md
├── README.id.md
├── LICENSE
├── CONTRIBUTING.md
└── skills/
    └── atomic-commits/
        └── SKILL.md
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Each proposed skill should have a narrow responsibility, valid YAML frontmatter with `name` and `description`, and clear guardrails.

## License

MIT, see [LICENSE](LICENSE).
