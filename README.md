# 我的 Claude Code 配置

> **进行中。** 这并非面向所有人的完善指南。它主要是我使用 Claude Code 进行学术工作的摘要——创建讲座幻灯片、编写 R 脚本、管理 Beamer 到 Quarto 的工作流程等。我不断学习新东西，也会持续更新这些文件。这只是一种与朋友和同事分享我的经验的方式。

**在线演示：** [psantanna.com/claude-code-my-workflow](https://psantanna.com/claude-code-my-workflow/)

一个可供 fork 的学术入门套件，适用于使用 [Claude Code](https://code.claude.com/docs/en/overview) 配合 **LaTeX/Beamer + R + Quarto**。你描述你想要什么；Claude 规划方法、运行专业智能体、修复问题、验证质量并呈现结果——像一个承包商一样处理整个工作。从一个生产级博士课程中提取（6 讲，800+ 张幻灯片）。

---

## 快速开始（5 分钟）

### 1. Fork 并克隆

```bash
# 在 GitHub 上 Fork 此仓库（点击仓库页面上的 "Fork"），然后：
git clone https://github.com/YOUR_USERNAME/claude-code-my-workflow.git my-project
cd my-project
```

将 `YOUR_USERNAME` 替换为你的 GitHub 用户名。

### 2. 启动 Claude Code 并粘贴提示

```bash
claude
```

**使用 VS Code？** 改为打开 Claude Code 面板。一切功能相同——详见[完整指南](https://psantanna.com/claude-code-my-workflow/workflow-guide.html#sec-setup)。

然后粘贴以下内容，填写你的项目信息：

> 我现在开始在这个仓库中处理 **[项目名称]**。**[用 2-3 句话描述你的项目——你在构建什么、面向谁、使用什么工具。]**
>
> 我希望我们的合作是有条理、精确且严格的。创建可视化时，一切都必须打磨到可发表的水平。
>
> 我已设置好 Claude Code 学术工作流程（从 `pedrohcgs/claude-code-my-workflow` fork）。配置文件已在此仓库中。请阅读它们，理解工作流程，然后**更新所有配置文件以适配我的项目**——填写 `CLAUDE.md` 中的占位符，如需要可调整规则，并针对我的用例提出任何定制化建议。
>
> 之后，对所有非平凡任务使用计划优先工作流程。一旦我批准了计划，切换到承包商模式——自主协调一切，只在有歧义或需要做决定时才来找我。
>
> 进入计划模式，首先为此项目调整工作流程配置。

**这做了什么：** Claude 读取所有配置文件，填入你的项目名称、机构名称和偏好，然后进入承包商模式——自主规划、实施、审查和验证。当工作达到质量标准时，你会看到摘要。说"放手去做"它也会自动提交。

**更喜欢手动配置？** 详见[完整指南](https://psantanna.com/claude-code-my-workflow/workflow-guide.html#sec-setup)中的分步手动设置说明。

---

## 工作原理

### 承包商模式

你描述一个任务。Claude 规划方法、实施它、运行专业审查智能体、修复问题、重新验证，并根据质量门槛进行评分——全部自主完成。当工作达到质量标准时，你会看到一个摘要。说"放手去做"它也会自动提交。

### 专业智能体

不是单一的全能审查员，而是 10 个专注于各自领域的智能体各自检查一个维度：

- **proofreader** — 语法/拼写
- **slide-auditor** — 视觉布局
- **pedagogy-reviewer** — 教学质量
- **r-reviewer** — R 代码质量
- **domain-reviewer** — 领域特定正确性（模板——为你的领域定制）

每个智能体在其狭窄任务上都比通才做得更好。`/slide-excellence` 技能可并行运行它们全部。

### 对抗性 QA

两个智能体对立工作：**critic** 读取 Beamer 和 Quarto 并产生严厉的发现。**fixer** 完全按照 critic 的发现实施修复。它们循环直到 critic 说"APPROVED"（或最多 5 轮）。这能捕获单次审查遗漏的错误。

### 质量门槛

每个文件都会获得分数（0-100）。低于门槛的分数会阻止操作：

- **80** — 提交门槛
- **90** — PR 门槛
- **95** — 卓越（追求卓越）

---

## 指南

要获取全面演练，请阅读**[完整指南](https://psantanna.com/claude-code-my-workflow/workflow-guide.html)**（或查看[源码](guide/workflow-guide.qmd)）。

它涵盖：

1. **为何存在此工作流程** — 问题和愿景
2. **入门** — fork、粘贴一个提示，Claude 完成其余设置
3. **系统实际运作** — 专业智能体、对抗性 QA、质量评分
4. **构建块** — CLAUDE.md、规则、技能、智能体、钩子、记忆
5. **工作流程模式** — 讲座创建、翻译、复制、多智能体审查、研究探索
6. **为你的领域定制** — 创建你自己的审查员和知识库

---

## 包含内容

<details>
<summary><strong>10 个智能体、19 个技能、17 条规则、4 个钩子</strong>（点击展开）</summary>

### 智能体（`.claude/agents/`）

| 智能体 | 功能 |
|-------|-------------|
| `proofreader` | 语法、拼写、溢出、一致性审查 |
| `slide-auditor` | 视觉布局审核（溢出、字体一致性、间距） |
| `pedagogy-reviewer` | 13 模式教学法审查（叙述弧、符号密度、节奏） |
| `r-reviewer` | R 代码质量、可重现性和领域正确性 |
| `tikz-reviewer` | 无情的 TikZ 图表视觉批评 |
| `beamer-translator` | Beamer 到 Quarto 翻译专家 |
| `quarto-critic` | 对抗性 QA，将 Quarto 与 Beamer 基准对比 |
| `quarto-fixer` | 实施 critic 智能体的修复 |
| `verifier` | 端到端任务完成验证 |
| `domain-reviewer` | **模板** 用于你的领域特定内容审查员 |

### 技能（`.claude/skills/`）

| 技能 | 功能 |
|-------|-------------|
| `/compile-latex` | 3遍 XeLaTeX 编译 + bibtex |
| `/deploy` | 渲染 Quarto + 同步到 GitHub Pages |
| `/extract-tikz` | TikZ 图表到 PDF 再到 SVG 的流程 |
| `/proofread` | 对文件启动 proofreader |
| `/visual-audit` | 对文件启动 slide-auditor |
| `/pedagogy-review` | 对文件启动 pedagogy-reviewer |
| `/review-r` | 启动 R 代码审查员 |
| `/qa-quarto` | 对抗性 critic-fixer 循环（最多 5 轮） |
| `/slide-excellence` | 综合多智能体审查 |
| `/translate-to-quarto` | 完整 11 阶段 Beamer 到 Quarto 翻译 |
| `/validate-bib` | 交叉引用参考文献 |
| `/devils-advocate` | 提交前挑战设计决策 |
| `/create-lecture` | 完整讲座创建工作流程 |
| `/commit` | 暂存、提交、创建 PR 并合并到 main |
| `/lit-review` | 文献搜索、综合和差距识别 |
| `/research-ideation` | 生成研究问题和实证策略 |
| `/interview-me` | 交互式访谈以正式化研究想法 |
| `/review-paper` | 手稿审查：结构、计量经济学、审稿意见 |
| `/data-analysis` | 端到端 R 分析，输出可发表质量 |

### 研究工作流程

| 特性 | 功能 |
|---------|-------------|
| 探索文件夹 | 带有 graduate/archive 生命周期的结构化 `explorations/` 沙盒 |
| 快速通道工作流程 | 60/100 质量门槛用于快速原型制作 |
| 简化协调器 | implement → verify → score → done（无多轮审查） |
| 增强会话日志 | 变更、决策、验证的结构化表格 |
| 仅合并时报告 | 仅在合并时生成质量报告 |
| 数学行长度异常 | 长行对于有文档的公式可接受 |
| 工作流程快速参考 | `.claude/WORKFLOW_QUICK_REF.md` 中的单页速查表 |

### 规则（`.claude/rules/`）

规则使用路径作用域加载：**始终启用** 规则在每个会话中加载（约 100 行总计）；**路径作用域** 规则仅在 Claude 处理匹配文件时加载。Claude 可靠遵循约 150 条指令，所以少即是多。

**始终启用**（无 `paths:` 前言——每个会话加载）：

| 规则 | 强制内容 |
|------|-----------------|
| `plan-first-workflow` | 非平凡任务的计划模式 + 上下文保留 |
| `orchestrator-protocol` | 承包商模式：implement → verify → review → fix → score |
| `session-logging` | 三个日志触发器：计划后、增量、会话结束 |

**路径作用域**（仅在处理匹配文件时加载）：

| 规则 | 触发于 | 强制内容 |
|------|------------|-----------------|
| `verification-protocol` | `.tex`, `.qmd`, `docs/` | 任务完成检查清单 |
| `single-source-of-truth` | `Figures/`, `.tex`, `.qmd` | 无内容重复；Beamer 是权威 |
| `quality-gates` | `.tex`, `.qmd`, `*.R` | 80/90/95 评分 + 容差门槛 |
| `r-code-conventions` | `*.R` | R 编码标准 + 数学行长度异常 |
| `tikz-visual-quality` | `.tex` | TikZ 图表视觉标准 |
| `beamer-quarto-sync` | `.tex`, `.qmd` | 自动同步 Beamer 编辑到 Quarto |
| `pdf-processing` | `master_supporting_docs/` | 安全的大型 PDF 处理 |
| `proofreading-protocol` | `.tex`, `.qmd`, `quality_reports/` | 先提议，批准后应用 |
| `no-pause-beamer` | `.tex` | Beamer 中无叠加命令 |
| `replication-protocol` | `*.R` | 扩展前复制原始结果 |
| `knowledge-base-template` | `.tex`, `.qmd`, `*.R` | 符号/应用注册表模板 |
| `orchestrator-research` | `*.R`, `explorations/` | 简单协调器用于研究（无多轮审查） |
| `exploration-folder-protocol` | `explorations/` | 实验工作的结构化沙盒 |
| `exploration-fast-track` | `explorations/` | 轻量级探索工作流程（60/100 门槛） |

**模板**（`templates/`）—— 会话日志、质量报告和探索 README 的参考格式。非自动加载。

</details>

---

## 前置要求

| 工具 | 需要用于 | 安装 |
|------|-------------|---------|
| [Claude Code](https://code.claude.com/docs/en/overview) | 一切 | `npm install -g @anthropic-ai/claude-code` |
| XeLaTeX | LaTeX 编译 | [TeX Live](https://tug.org/texlive/) 或 [MacTeX](https://tug.org/mactex/) |
| [Quarto](https://quarto.org) | 网页幻灯片 | [quarto.org/docs/get-started](https://quarto.org/docs/get-started/) |
| R | 图表和分析 | [r-project.org](https://www.r-project.org/) |
| pdf2svg | TikZ 转 SVG | `brew install pdf2svg` (macOS) |
| [gh CLI](https://cli.github.com/) | PR 工作流程 | `brew install gh` (macOS) |

并非所有工具都需要——只安装你的项目使用的工具。Claude Code 是唯一硬性要求。

---

## 为你的领域适配

1. **填写知识库**（`.claude/rules/knowledge-base-template.md`），包含你的符号、应用和设计原则
2. **定制领域审查员**（`.claude/agents/domain-reviewer.md`），使用针对你领域的审查视角
3. **更新 Quarto 主题 SCSS 文件中的调色板**——更改顶部的颜色变量
4. **添加领域特定的 R 陷阱**到 `.claude/rules/r-code-conventions.md`
5. **填写 `.claude/rules/beamer-quarto-sync.md` 中的讲座映射**
6. **定制工作流程快速参考**（`.claude/WORKFLOW_QUICK_REF.md`），包含你的必选项和偏好
7. **设置探索文件夹**（`explorations/`）用于实验工作

---

## 额外资源

- [Claude Code 文档](https://code.claude.com/docs/en/overview)
- [编写好的 CLAUDE.md](https://code.claude.com/docs/en/memory) —— 关于项目记忆的官方指导

---

## 起源

此基础设施是从埃默里大学 **Econ 730: 因果面板数据** 中提取的，由 Pedro Sant'Anna 通过 Claude Code 在 6+ 次会话中开发。该课程产生了 6 个完整的博士讲座幻灯片组（800+ 张幻灯片）、带有 plotly 图表的交互式 Quarto 版本，以及完整的 R 复制包——全部通过此多智能体工作流程管理。

---

## 许可证

MIT 许可证。可自由用于教学、研究或任何学术目的。
