# 完整说明（SPEC）：文件结构、字段定义、扩展与维护

本技能包依据 OpenAI Codex 官方技能规范与 Agent Skills 开放标准构建。Skills 是"编写格式"，Plugins 是"分发单元"；本仓库以纯 skills 形式组织，可直接被 Codex CLI / IDE 扩展 / ChatGPT 加载。

---

## 1. 文件结构

```
senior-developer-codex/
├── AGENTS.md                          # 仓库级 Agent 指引（Codex 启动时读取）
├── README.md                          # 仓库总览与快速开始
├── LICENSE                            # MIT
├── docs/
│   ├── USAGE.md                       # 简明使用说明（安装/配置/调用示例）
│   └── SPEC.md                        # 本文件
└── .agents/
    └── skills/
        ├── senior-developer/          # 总纲技能：工程师角色 + 工作流
        │   ├── SKILL.md
        │   └── agents/openai.yaml     # Codex CLI 专属元数据（可选）
        ├── fullstack-dev/             # 全栈架构技能
        │   ├── SKILL.md
        │   ├── agents/openai.yaml
        │   └── references/            # 9 篇深度参考（架构/API/鉴权/DB/测试…）
        ├── frontend-dev/              # 前端精品 UI 技能
        │   ├── SKILL.md
        │   ├── agents/openai.yaml
        │   └── references/            # 11 篇深度参考（设计/动效/媒体生成/排障…）
        └── browser-use/               # 浏览器自动化技能
            ├── SKILL.md
            ├── agents/openai.yaml
            └── references/            # 2 篇深度参考（CDP/多会话）
```

**设计原则（渐进式披露 / progressive disclosure）**：Codex 平时只加载各技能的 name + description（初始技能列表有上下文预算限制，约 2% 上下文窗口或 8,000 字符）；命中任务后才读取完整 SKILL.md；references 仅在需要深入指导时按需读取。因此 SKILL.md 保持工作流骨架，重内容下沉到 references/。

---

## 2. SKILL.md 字段定义

### 2.1 Frontmatter（YAML，必需字段加粗）

| 字段 | 必需 | 说明 |
|------|------|------|
| **`name`** | ✅ | 技能唯一标识，小写字母 + 连字符，须与目录名一致（如 `senior-developer`）。用于 `$name` 显式调用 |
| **`description`** | ✅ | 触发条件描述。Codex 依据它做隐式匹配，且列表超预算时会**截断 description** —— 因此必须把核心用途与触发词**前置**，并写清 DO / DO NOT 边界。本包采用"TRIGGER when / DO NOT TRIGGER when / 中文触发词"三段式 |
| `license` | ❌ | 许可证（本包统一 MIT） |
| `metadata` | ❌ | 任意键值：`version`（语义化版本）、`category`（技能分类）、`origin`（来源）、`language`（正文语言）、`requires`（外部依赖，如 browser-use CLI） |

> 兼容性说明：原始 WorkBuddy skill 中的 `allowed-tools`、`description_zh/en`、`metadata.clawdbot` 等宿主专属字段已归并或移除，以保证跨 Agent 可移植。Codex 会忽略无法识别的字段。

### 2.2 正文（Markdown）

正文是交给 Agent 的指令。本包四个技能的正文结构约定：

| 技能 | 正文核心章节 |
|------|-------------|
| senior-developer | 核心原则 → 技术能力 → 工作流（规划/增量验证/交付） → 自检清单 → 错误恢复 → 输出规范 → 子技能路由 |
| fullstack-dev | 强制工作流（需求→决策→脚手架→实现→验证→交付） → 7 条铁律 → references 索引 → 反模式速查 |
| frontend-dev | 六阶段工作流 → 动效工具选型矩阵与冲突规则 → 资产生成速查 → 性能规则 → references 索引 |
| browser-use | 前置检查 → 核心工作流 → 浏览器模式 → 命令全集 → 云 API/隧道/多会话 → 排障 |

### 2.3 agents/openai.yaml（可选，Codex CLI 专属）

```yaml
display_name: "Senior Developer"   # UI 显示名
icon: "code"                       # 图标名
# mcp_tools: [github, sentry]      # 可选：声明依赖的 MCP 连接
```

其他 Agent 会自动忽略此文件，不影响跨平台使用。

### 2.4 references/

纯 Markdown 深度文档，由 SKILL.md 正文以相对路径引用（如 `references/auth-flow.md`）。Agent 判断需要时才读取，避免上下文浪费。

---

## 3. 加载位置（Codex 技能扫描规则）

| 作用域 | 位置 | 说明 |
|--------|------|------|
| 仓库级 | `<任意目录>/.agents/skills/`（向上扫描至仓库根） | 团队共享，随仓库分发 |
| 用户级 | `~/.agents/skills/` | 个人全局技能 |
| 管理级 | `/etc/codex/skills` | 机器级共享（容器/组织镜像） |
| 系统级 | Codex 内置 | 如 skill-creator、plan |

同名技能不合并，会同时出现在技能选择器中。Codex 支持符号链接的技能目录。

---

## 4. 扩展：新增一个 Skill

1. 创建目录：`.agents/skills/my-skill/`
2. 编写 `SKILL.md`：

```markdown
---
name: my-skill
description: >
  TRIGGER when: <核心场景与触发词，前置>. DO NOT TRIGGER when: <边界>.
  触发词：<中文触发词>。
license: MIT
metadata:
  version: 0.1.0
  category: <分类>
---

# 技能标题

<指令正文：工作流步骤、清单、速查表…>

深入内容 → references/xxx.md
```

3. （可选）添加 `agents/openai.yaml`、`references/*.md`、`scripts/*.sh`、`assets/`
4. 重启 Codex 或等待其自动检测变更，用 `/skills` 验证

也可以在 Codex 内用内置创建器：`$skill-creator`。

## 5. 维护约定

- **版本**：修改技能内容时递增 frontmatter 中的 `metadata.version`（语义化版本），并在 commit message 中注明
- **description 即契约**：任何触发行为的变化都应同步修改 description；保持触发词前置，防止被截断后失配
- **单一入口**：`SKILL.md` 永远是入口；新增深度内容一律放 `references/` 并在正文中建立索引
- **可移植性**：不要在 SKILL.md 中使用宿主专属字段或本机绝对路径；脚本引用相对路径
- **验证**：改动后运行 `codex --sandbox read-only --ask-for-approval on-request "Summarize the current instructions and list all instruction files you loaded."` 确认技能被正确加载

## 6. 转换溯源（WorkBuddy Expert → Codex Skills）

| 原始（WorkBuddy 专家插件） | 转换后（本仓库） |
|---------------------------|------------------|
| `agents/senior-developer.md`（专家人设） | `.agents/skills/senior-developer/SKILL.md` |
| `skills/fullstack-dev/SKILL.md` + `references/`（9 篇） | 同名目录，frontmatter 规范化 |
| `skills/frontend-dev/SKILL.md` + `references/`（10 篇） | 同名目录；`canvas-fonts/` 二进制字体与 `scripts/`（依赖宿主运行时）未纳入，已在正文中改写为通用描述 |
| `skills/browser-use/SKILL.md` + `references/`（2 篇） | 同名目录，frontmatter 规范化 |
| 专家→技能的路由关系 | senior-developer 正文的「子 Skill 路由」章节 |
