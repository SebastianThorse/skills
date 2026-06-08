# SebastianThorse skills

This repository is a collection of reusable **GitHub Copilot CLI agent skills**.

Each published skill lives in its own directory and can be copied into:

- `~/.copilot/skills` for personal use across projects
- `.github/skills` inside a repository for project-specific use

## Repository layout

```text
skills/
  <skill-name>/
    SKILL.md
    ...
templates/
  skill-template/
    SKILL.md
```

## How to use a skill

1. Clone or download this repository.
2. Copy the skill folder you want from `skills\<skill-name>` into either:
   - `%USERPROFILE%\.copilot\skills\<skill-name>`
   - `<your-repo>\.github\skills\<skill-name>`
3. Start Copilot CLI, or run `/skills reload` in an existing session.
4. Confirm the skill is available with `/skills info <skill-name>`.

## Install from this repo with GitHub CLI

If you have GitHub CLI 2.90.0 or later, you can inspect and install skills directly from this repository with `gh skill`.

Preview a skill before installing it:

```shell
gh skill preview SebastianThorse/skills check-wcag
```

Install a specific skill from this repo:

```shell
gh skill install SebastianThorse/skills check-wcag
```

Open an interactive picker for all skills in this repo:

```shell
gh skill install SebastianThorse/skills
```

After installation, reload skills in Copilot CLI with:

```shell
/skills reload
```

## Authoring rules

- Use one folder per skill.
- Name skill folders in lowercase with hyphens.
- Name the manifest file `SKILL.md`.
- Add YAML frontmatter with at least `name` and `description`.
- Keep scripts, examples, and reference files in the same skill directory.

Use `templates\skill-template` as the starting point for new skills.