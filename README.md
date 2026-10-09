# vercel-skills-dsh

DeepSeek Harness skill bundle for [vercel-labs/skills](https://github.com/vercel-labs/skills) v1.7.1 — the CLI for the open agent skills ecosystem.

Skill-only bundle: no native tools, no Web client, no install hooks.

## Bundled skills

| Skill | Source | Purpose |
|---|---|---|
| `find-skills` | upstream `skills/find-skills` (unmodified) | Discovery workflow: help users find, verify, and install skills from the skills.sh ecosystem |
| `pr-labeling` | upstream `.factory/workflows/pr-labeling/skills/pr-labeling` (unmodified) | Classify a skills CLI pull request from its description and patch |
| `skills-cli` | written for this bundle from the upstream README | CLI reference: `npx skills add/use/list/find/update/remove/init`, source formats, and options |

## Usage

The skills call the `skills` CLI on demand — no global install required:

```bash
npx skills find react
npx skills add vercel-labs/agent-skills --skill frontend-design
```

## Adaptation notes

- Upstream skill content is unmodified; `skills-cli` is a reference skill distilled from the upstream README (command table, source formats, options) because the repo itself is a CLI tool rather than a skill collection.
- The repository's TypeScript CLI source is not bundled; `npx skills` resolves the published npm package.

## License

Skills content: MIT, Copyright Vercel — see [LICENSE](LICENSE) and [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
