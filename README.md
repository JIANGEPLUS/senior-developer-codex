# senior-developer-codex

「高级开发工程师（Senior Developer）」专家能力的 Codex 标准技能包 —— 依据 OpenAI Codex / Agent Skills 开放规范（SKILL.md）转换，可直接被 Codex CLI、Codex IDE 扩展、ChatGPT 以及其他兼容 Agent Skills 标准的 Agent 加载使用。

## 包含的技能

| Skill | 路径 | 说明 |
|-------|------|------|
| `senior-developer` | `.agents/skills/senior-developer/` | 高级工程师角色与工作流总纲：任务分解 → 增量实现 → 自动验证 → 交付确认，含代码自检清单与错误恢复策略 |
| `fullstack-dev` | `.agents/skills/fullstack-dev/` | 全栈架构与前后端集成：REST API、鉴权、实时通信、生产加固（含 9 篇 references） |
| `frontend-dev` | `.agents/skills/frontend-dev/` | 精品前端 UI：动效系统选型矩阵、AI 媒体资产生成、文案框架（含 11 篇 references） |
| `browser-use` | `.agents/skills/browser-use/` | browser-use CLI 浏览器自动化：导航、截图、表单、数据提取、云浏览器（含 2 篇 references） |

## 快速开始

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

## 文档

- 📗 [docs/USAGE.md](docs/USAGE.md) — 简明使用说明：安装、配置、调用示例
- 📘 [docs/SPEC.md](docs/SPEC.md) — 完整说明：文件结构、字段定义、扩展与维护

## 来源与许可

内容转换自 WorkBuddy「吴八哥 / senior-developer」专家插件（agent + 3 个内置 skill）。以 MIT 许可发布，见 [LICENSE](LICENSE)。
