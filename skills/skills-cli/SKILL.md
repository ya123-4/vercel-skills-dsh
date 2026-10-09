---
name: skills-cli
description: Reference for the `skills` CLI from vercel-labs/skills (the package manager for the open agent skills ecosystem). Use when the user wants to install, update, list, remove, or use agent skills from GitHub or the skills.sh ecosystem, or asks about managing skills in this environment. Covers `npx skills add/use/list/update/init/remove`, supported source formats, and installation options.
---

# skills CLI reference

The `skills` CLI is the package manager for the open agent skills ecosystem (https://skills.sh/). It installs skills from git repos, URLs, or local paths into agent skill directories. Run it without installing via `npx skills <command>`.

## Install a skill

```bash
npx skills add vercel-labs/agent-skills
```

- `-g, --global`: install to the user directory instead of the project
- `-a, --agent <agents...>`: target specific agents (e.g. `claude-code`)
- `-s, --skill <skills...>`: install specific skills by name (`'*'` for all)
- `-l, --list`: list available skills without installing
- `--copy`: copy files instead of symlinking to agent directories
- `-y, --yes`: skip all confirmation prompts
- `--all`: install all skills to all agents without prompts

Examples:

```bash
npx skills add vercel-labs/agent-skills --list
npx skills add vercel-labs/agent-skills --skill frontend-design --skill skill-creator
npx skills add vercel-labs/agent-skills --skill '*' -a claude-code
npx skills add vercel-labs/agent-skills -g -y
```

## Use a skill without installing

Generate a prompt for one skill, or start a supported coding agent interactively:

```bash
npx skills use vercel-labs/agent-skills@web-design-guidelines | claude
npx skills use vercel-labs/agent-skills --skill web-design-guidelines --agent claude-code
```

`skills use` resolves sources the same way as `skills add`, writes the selected skill files to a temporary directory, and prints only the generated prompt to stdout unless `--agent` is provided.

## Source formats

```bash
# GitHub shorthand (owner/repo)
npx skills add vercel-labs/agent-skills

# Full GitHub URL
npx skills add https://github.com/vercel-labs/agent-skills

# Direct path to a skill in a repo
npx skills add https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines

# GitLab URL
npx skills add https://gitlab.com/org/repo

# Azure Repos
npx skills add https://dev.azure.com/org/project/_git/repo
npx skills add https://dev.azure.com/org/project/_git/repo?path=/skills/web-design&version=GBmain

# Any git URL
npx skills add git@github.com:vercel-labs/agent-skills.git

# Local path
npx skills add ./my-local-skills
```

For private repositories, the CLI uses the authentication already configured for the repository URL (Git credential helper, GitHub CLI, then SSH fallback). `GITHUB_TOKEN` or `GH_TOKEN` can be set explicitly for GitHub API access.

## Manage installed skills

```bash
npx skills list                 # list installed skills (alias: ls)
npx skills ls -g                # list only global skills
npx skills ls -a claude-code -a cursor   # filter by agents
npx skills update [skills...]   # update installed skills to latest versions
npx skills remove [skills...]   # remove installed skills from agents
npx skills init [name]          # create a new SKILL.md template
```

Update options: `-g, --global` (only global), `-p, --project` (only project), `-y, --yes` (skip scope prompt; auto-detect project vs global).

Remove examples:

```bash
npx skills remove owner/repo
npx skills remove web-design-guidelines
npx skills remove frontend-design web-design-guidelines
npx skills remove --global web-design-guidelines
npx skills remove --agent claude-code cursor my-skill
npx skills remove --all
```

`skills experimental_install` restores skills from `skills-lock.json`; `skills experimental_sync` crawls `node_modules` for skills and syncs them into agent dirs.

## Find skills

```bash
npx skills find [query] [--owner <owner>]
```

Browse the leaderboard at https://skills.sh/ before recommending; verify install counts (prefer 1K+), source reputation, and stars before recommending a skill.

## Notes for this environment

- Prefer `npx skills` (no global install) unless the user asks for a persistent install.
- Installed skills land in agent-specific directories (e.g. `~/.agents/skills/`); in DeepSeek Harness, the `dsh-skill-filesystem` provider already scans some of these roots, but a newly installed skill may need a catalog refresh or a new session to appear.
- `npx skills init` creates a SKILL.md with YAML frontmatter (`name`, `description`) — the same format DeepSeek Harness skills use.
