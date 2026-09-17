# AGENTS.md

本仓库是一套面向 Codex（兼容 ChatGPT / Claude Code 等支持 Agent Skills 标准的 Agent）的技能包，角色原型为「高级开发工程师（Senior Developer）」。

## 技能清单

| Skill | 用途 |
|-------|------|
| `senior-developer` | 高级工程师角色 + 工作流总纲（任务分解 → 增量实现 → 验证 → 交付） |
| `fullstack-dev` | 全栈架构与前后端集成（REST API、鉴权、实时、生产加固） |
| `frontend-dev` | 前端精品 UI、动效系统、AI 媒体资产生成 |
| `browser-use` | browser-use CLI 浏览器自动化（导航、截图、表单、数据提取） |

## 在本仓库内使用

技能位于 `.agents/skills/`，Codex 从当前目录向上扫描至仓库根时会自动发现它们。
在 Codex CLI 中可用 `$senior-developer`、`$fullstack-dev` 等显式调用，或由 Agent 根据任务描述隐式匹配。

## 修改约定

- 每个 skill 的入口永远是 `SKILL.md`；深度内容放 `references/`，按需加载
- `description` 决定隐式触发质量：触发词前置、写清 DO / DO NOT 边界
- 新增 skill 请遵循 `docs/SPEC.md` 中的字段定义与目录结构
