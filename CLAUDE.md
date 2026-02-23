# CLAUDE.MD -- 使用 Claude Code 进行学术项目开发

<!-- 使用说明：用你的项目信息替换方括号占位符。
     根据你的主题自定义 Beamer 环境和 CSS 类。
     保持此文件在约 150 行以内 — Claude 每次会话都会加载它。
     详细文档见 docs/workflow-guide.html -->

**项目名称：** [你的项目名称]
**所属机构：** [你的机构名称]
**分支：** main

---

## 核心原则

- **先做计划** — 对于非平凡任务，先进入计划模式；将计划保存到 `quality_reports/plans/`
- **完成后验证** — 每个任务结束时进行编译/渲染并确认输出
- **单一真相来源** — Beamer `.tex` 是权威版本；Quarto `.qmd` 由它衍生
- **质量门槛** — 任何交付物不低于 80/100 分
- **[LEARN] 标签** — 当被纠正时，将 `[LEARN:分类] 错误 → 正确` 保存到 MEMORY.md

## 🚫 绝对约束（禁忌）

### 1. 永不删除数据

**在任何情况下都不得删除任何数据文件。**

包括：

- `.dta` 文件（Stata 数据集）
- `.csv` 文件
- `.xlsx` / `.xls` 文件
- `.txt` 文件
- 空间数据（`.shp`、`.dbf`、`.spmat` 等）
- 任何其他数据文件

**如果文件看起来冗余：** 移动到 `legacy/`，不要删除。

### 2. 永不删除程序

**在任何情况下都不得删除任何代码或脚本。**

包括：

- Stata do 文件（`.do`）
- R 脚本（`.R`、`.r`）
- Python 脚本（`.py`）
- Jupyter notebooks（`.ipynb`）
- MATLAB 脚本（`.m`）
- 任何其他程序文件

**如果脚本已过时：** 移动到 `legacy/`，不要删除。

### 3. 停留在此文件夹

**你可以进入子目录，但不能向上跳转。**

- ✅ 允许：`code/sub/`、`in/map_db/`、`out/figures/`
- ❌ 禁止：任何以 `..` 开头或超出项目根目录的路径

---

## 文件夹结构

```text
[你的项目]/
├── CLAUDE.MD                    # 本文件
├── .claude/                     # 规则、技能、智能体、钩子
├── Bibliography_base.bib        # 集中式参考文献库
├── Figures/                     # 图表和图片
├── Preambles/header.tex         # LaTeX 预设置
├── Slides/                      # Beamer .tex 文件
├── Quarto/                      # RevealJS .qmd 文件 + 主题
├── docs/                        # GitHub Pages（自动生成）
├── scripts/                     # 实用脚本 + R 代码
├── quality_reports/             # 计划、会话日志、合并报告
├── explorations/                # 研究沙盒（见规则）
├── templates/                   # 会话日志、质量报告模板
└── master_supporting_docs/      # 论文和现有幻灯片
```

---

## 命令

```bash
# LaTeX（3遍编译，仅使用 XeLaTeX）
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
BIBINPUTS=..:$BIBINPUTS bibtex file
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex

# 部署 Quarto 到 GitHub Pages
./scripts/sync_to_docs.sh LectureN

# 质量评分
python scripts/quality_score.py Quarto/file.qmd
```

---

## 质量门槛

| 分数 | 门槛 | 含义 |
|-------|------|---------|
| 80 | 提交 | 足够好，可以保存 |
| 90 | PR | 准备好部署 |
| 95 | 卓越 | 追求卓越 |

---

## 技能快速参考

| 命令 | 功能 |
|---------|-------------|
| `/compile-latex [文件]` | 3遍 XeLaTeX + bibtex |
| `/deploy [LectureN]` | 渲染 Quarto + 同步到 docs/ |
| `/extract-tikz [LectureN]` | TikZ → PDF → SVG |
| `/proofread [文件]` | 语法/拼写/溢出检查 |
| `/visual-audit [文件]` | 幻灯片布局审核 |
| `/pedagogy-review [文件]` | 叙述、符号、节奏审核 |
| `/review-r [文件]` | R 代码质量审核 |
| `/qa-quarto [LectureN]` | Quarto 对比 Beamer 质量检查 |
| `/slide-excellence [文件]` | 多智能体综合审核 |
| `/translate-to-quarto [文件]` | Beamer → Quarto 翻译 |
| `/validate-bib` | 交叉引用验证 |
| `/devils_adocate` | 挑战幻灯片设计 |
| `/create-lecture` | 完整课程创建 |
| `/commit [消息]` | 暂存、提交、PR、合并 |
| `/lit-review [主题]` | 文献搜索与综合 |
| `/research-ideation [主题]` | 研究问题与策略 |
| `/interview-me [主题]` | 交互式研究访谈 |
| `/review-paper [文件]` | 手稿审核 |
| `/data-analysis [数据集]` | 端到端 R 分析 |

---

<!-- 自定义：用你自己的 Beamer 环境和 Quarto CSS 类替换下面的示例。
     删除它们并添加你自己的。 -->

## Beamer 自定义环境

| 环境 | 效果 | 使用场景 |
|-------------------|---------------|----------------|
| `[your-env]` | [描述] | [何时使用] |

<!-- 示例条目（删除并替换为你自己的）：
| `keybox` | 金色背景框 | 关键点 |
| `highlightbox` | 金色左边框 | 高亮 |
| `definitionbox[标题]` | 蓝色边框带标题框 | 正式定义 |
-->

## Quarto CSS 类

| 类 | 效果 | 使用场景 |
|--------------------|---------------|----------------|
| `[.your-class]` | [描述] | [何时使用] |

<!-- 示例条目（删除并替换为你自己的）：
| `.smaller` | 85% 字体 | 密集内容幻灯片 |
| `.positive` | 绿色粗体 | 好的注释 |
-->

---

## 当前项目状态

| 课程 | Beamer | Quarto | 核心内容 |
|---------|--------|--------|-------------|
| 1: [主题] | `Lecture01_主题.tex` | `Lecture1_主题.qmd` | [简要描述] |
| 2: [主题] | `Lecture02_主题.tex` | -- | [简要描述] |
