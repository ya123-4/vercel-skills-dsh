# vercel-skills-dsh（中文说明）

[vercel-labs/skills](https://github.com/vercel-labs/skills) v1.7.1 —— 开放 agent skills 生态的 CLI —— 的 DeepSeek Harness skill 插件包。

纯 skill 插件：不含原生工具、不含 Web 客户端、不含安装钩子。

## 包含的 skill

| Skill | 来源 | 用途 |
|---|---|---|
| `find-skills` | 上游 `skills/find-skills`（未修改） | 发现工作流：帮助用户从 skills.sh 生态查找、验证并安装 skill |
| `pr-labeling` | 上游 `.factory/workflows/pr-labeling/skills/pr-labeling`（未修改） | 依据 PR 描述和补丁为 skills CLI 的 pull request 分类打标签 |
| `skills-cli` | 依据上游 README 为本插件编写 | CLI 参考：`npx skills add/use/list/find/update/remove/init`、来源格式与选项 |

## 使用方式

这些 skill 按需调用 `skills` CLI，无需全局安装：

```bash
npx skills find react
npx skills add vercel-labs/agent-skills --skill frontend-design
```

## 适配说明

- 上游 skill 内容未做修改；由于该仓库本身是 CLI 工具而非 skill 集合，`skills-cli` 是从上游 README（命令表、来源格式、选项）提炼的参考 skill。
- 仓库的 TypeScript CLI 源码不随包分发；`npx skills` 解析的是 npm 上已发布的包。

## 许可证

skill 内容：MIT，版权归 Vercel — 见 [LICENSE](LICENSE) 与 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
