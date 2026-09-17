# 简明使用说明（USAGE）

本技能包遵循 OpenAI Codex 的 Agent Skills 规范：每个技能是一个包含 `SKILL.md` 的目录，Codex 先读取元数据（name + description），命中任务后再加载完整指令。支持**显式调用**（`$skill-name`）与**隐式匹配**（Agent 根据 description 自动选择）两种方式。

---

## 1. 安装

### 方式 A：仓库内使用（团队共享，推荐）

将本仓库克隆或作为子模块放入你的项目，Codex 会从当前目录向上扫描至仓库根，自动发现 `.agents/skills/` 下的技能：

```bash
cd your-project
git clone https://github.com/JIANGEPLUS/senior-developer-codex.git
cd senior-developer-codex && codex   # 在仓库内启动，技能即生效
```

### 方式 B：用户级安装（个人全局生效）

```bash
mkdir -p ~/.agents/skills
cp -r senior-developer-codex/.agents/skills/* ~/.agents/skills/
```

安装后重启 Codex 即可生效（Codex 会自动检测技能变更；未出现时重启一次）。

### 方式 C：单目录手动安装

任意技能目录都可独立使用 —— 只需保证目录名与 `SKILL.md` 中 `name` 一致，放入上述任一位置即可。

---

## 2. 配置

| 项 | 说明 |
|----|------|
| 技能位置 | 仓库级 `.agents/skills/`；用户级 `~/.agents/skills/` |
| 启用/禁用 | 在 `~/.codex/config.toml` 中：`[[skills.config]] path = "/path/to/SKILL.md" enabled = false` |
| browser-use 依赖 | `browser-use` skill 需要 CLI：`curl -fsSL https://browser-use.com/cli/install.sh \| bash`，用 `browser-use doctor` 自检 |
| fullstack-dev 依赖 | 无外部依赖，按所选技术栈自行安装（Node/Python/Go 等） |
| frontend-dev 依赖 | 使用 MiniMax 生成媒体资产时需设置 `MINIMAX_API_KEY` 环境变量 |
| openai.yaml | 各技能的 `agents/openai.yaml` 提供 Codex CLI 显示名与图标，其他 Agent 会自动忽略 |

---

## 3. 调用示例

### 显式调用（推荐，行为最可控）

```text
$senior-developer 从零搭建一个 Express + React 的待办应用
$fullstack-dev   为现有 API 补上 JWT 认证、刷新令牌与全局错误处理
$frontend-dev    给产品落地页做滚动叙事动效，并生成 hero 视频与配图
$browser-use     打开 https://example.com，填写登录表单并截图
```

也可以用 `/skills` 查看已加载技能列表。

### 隐式调用（自然语言，自动匹配）

```text
帮我写一个带用户鉴权的博客系统后台      → 自动命中 fullstack-dev
这个页面滚动动画太生硬，优化一下        → 自动命中 frontend-dev
帮我抓取这个网站的价格数据到表格        → 自动命中 browser-use
审查一下这段代码的错误处理做得好不好     → 自动命中 senior-developer
```

### 组合使用

`senior-developer` 是总纲技能：接到复杂任务时先做任务分解与规划，实现阶段按场景路由到 `fullstack-dev` / `frontend-dev` / `browser-use`，最后按交付清单收尾。

---

## 4. 验证安装

在 Codex CLI 中运行：

```text
/skills
```

应看到 `senior-developer`、`fullstack-dev`、`frontend-dev`、`browser-use` 四个技能。也可以直接询问 Agent："列出当前可用的 skills"。
