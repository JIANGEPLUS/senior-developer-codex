<div align="center">

# senior-developer-codex

**Senior Developer skill pack for OpenAI Codex — production-ready Agent Skills (SKILL.md)**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/JIANGEPLUS/senior-developer-codex?style=social)](https://github.com/JIANGEPLUS/senior-developer-codex/stargazers)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/JIANGEPLUS/senior-developer-codex/pulls)
[![Docs](https://img.shields.io/badge/docs-USAGE%20%7C%20SPEC-blue)](docs/USAGE.md)

</div>

「高级开发工程师（Senior Developer）」专家能力的 Codex 标准技能包 —— 依据 **OpenAI Codex / Agent Skills 开放规范（SKILL.md）** 转换，可直接被 Codex CLI、Codex IDE 扩展、ChatGPT 以及其他兼容 Agent Skills 标准的 Agent 加载使用。

> **English**: `senior-developer-codex` converts a battle-tested "Senior Developer" expert workflow into production-ready [Agent Skills](https://agentskills.io/) (`SKILL.md`) for [OpenAI Codex](https://github.com/openai/codex). It ships **4 skills** covering fullstack development, frontend UI, and browser automation — loadable by the Codex CLI and any Agent Skills-compatible agent in under a minute.

## ✨ Why senior-developer-codex?

- **即装即用**：无需手工编写提示词，克隆后 Codex 自动发现技能目录
- **生产级工作流**：任务分解 → 增量实现 → 自动验证 → 交付确认，内置代码自检清单与错误恢复策略
- **覆盖全栈场景**：REST API、鉴权、实时通信、生产加固、前端动效、浏览器自动化一站配齐
- **标准兼容**：遵循 Agent Skills（SKILL.md）开放规范，同样兼容 ChatGPT / Claude Code 等 Agent

## 📦 包含的技能

| Skill | 路径 | 说明 |
|-------|------|------|
| `senior-developer` | `.agents/skills/senior-developer/` | 高级工程师角色与工作流总纲：任务分解 → 增量实现 → 自动验证 → 交付确认，含代码自检清单与错误恢复策略 |
| `fullstack-dev` | `.agents/skills/fullstack-dev/` | 全栈架构与前后端集成：REST API、鉴权、实时通信、生产加固（含 9 篇 references） |
| `frontend-dev` | `.agents/skills/frontend-dev/` | 精品前端 UI：动效系统选型矩阵、AI 媒体资产生成、文案框架（含 11 篇 references） |
| `browser-use` | `.agents/skills/browser-use/` | browser-use CLI 浏览器自动化：导航、截图、表单、数据提取、云浏览器（含 2 篇 references） |

## 🚀 快速开始

```bash
# 1. 克隆本仓库
git clone https://github.com/JIANGEPLUS/senior-developer-codex.git
cd senior-developer-codex

# 2a. 方式一：在本仓库内启动 Codex，技能自动被发现
codex

# 2b. 方式二：安装到用户级目录，对所有项目生效
mkdir -p ~/.agents/skills
cp -r .agents/skills/* ~/.agents/skills/
```

在 Codex CLI 中：

```text
$senior-developer 帮我从零搭建一个 Next.js + Prisma 的待办应用
$fullstack-dev   给这个项目补上 JWT 认证和刷新令牌流程
$frontend-dev    为落地页做滚动叙事动效并生成 hero 图
$browser-use     打开 example.com 登录并截图
```

也可以不指定技能，直接描述任务，Codex 会根据 description 隐式匹配。

## 📖 文档

- 🌐 [项目主页（GitHub Pages）](https://jiangeplus.github.io/senior-developer-codex/) — 产品介绍、技能总览与常见问题
- 📗 [docs/USAGE.md](docs/USAGE.md) — 简明使用说明：安装、配置、调用示例
- 📘 [docs/SPEC.md](docs/SPEC.md) — 完整说明：文件结构、字段定义、扩展与维护

## ❓ FAQ

**Q1：和直接让 Codex 干活有什么区别？**
直接使用 Codex 时，Agent 缺少稳定的"高级工程师"工作流约束。本技能包通过 SKILL.md 将任务分解、增量实现、自动验证、交付确认等最佳实践固化为可复用技能，产出更稳定、更接近资深工程师水准。

**Q2：支持哪些 Agent？**
任何兼容 Agent Skills 开放规范（SKILL.md）的 Agent 均可加载，包括 Codex CLI、Codex IDE 扩展、ChatGPT、Claude Code 等。

**Q3：可以只安装其中一个技能吗？**
可以。`.agents/skills/` 下每个技能目录相互独立，按需复制单个目录即可；建议保留 `senior-developer` 作为总纲。

**Q4：免费吗？采用什么许可？**
完全免费，基于 MIT 许可开源，可自由用于个人与商业项目。

## 📎 相关规范与资源

- [OpenAI Codex](https://github.com/openai/codex) — Codex CLI 官方仓库
- [Agent Skills 规范](https://agentskills.io/) — SKILL.md 开放规范说明

## 📄 来源与许可

内容转换自 WorkBuddy「吴八哥 / senior-developer」专家插件（agent + 3 个内置 skill）。以 MIT 许可发布，见 [LICENSE](LICENSE)。
