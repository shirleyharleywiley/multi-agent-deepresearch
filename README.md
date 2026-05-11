# Multi-Agent Deep Research Framework
# 多智能体深度调研框架

> 让 AI Agent 像专业分析师一样做深度调研——系统化迭代、可信度分级、信息源优先。
> Enable AI agents to conduct deep research like professional analysts—systematic iteration, credibility grading, source prioritization.

---

## 为什么需要这个框架？
## Why Do You Need This Framework?

做深度调研时，你是否遇到过这些问题？
When conducting deep research, have you encountered these problems?

- **信息碎片化**：搜了一堆网页，最后不知道哪些是真的
- **Information Fragmentation**: You searched dozens of pages but don't know which ones are trustworthy.

- **浅尝辄止**：搜完第一页就停了，错过了高价值内容
- **Shallow Exploration**: You stop after the first page and miss high-value content.

- **不知何时停**：总觉得还能再挖一点，报告永远写不完
- **No Stop Signal**: You always feel you can dig more, so reports never finish.

- **来源混乱**：媒体报道和官方文件混在一起，置信度不清
- **Source Confusion**: Media reports and official documents are mixed, with unclear credibility.

这个框架用 **六角色分工 + 多轮迭代 + 终止判断**，让你的 AI 调研输出达到专业分析师水平。
This framework uses **Six-Role Division + Multi-Round Iteration + Termination Judgment** to make your AI research output reach professional analyst standards.

---

## 特性
## Features

- **六角色三层架构**：将调研过程分为快速洞察层、元认知层和判断层，各司其职
- **Six-Role Three-Layer Architecture**: Divides the research process into QuickInsight, MetaInsight, and XInsight layers, each with distinct responsibilities.

- **多轮迭代**：通过多轮迭代逐步填补信息缺口，确保报告置信度
- **Multi-Round Iteration**: Progressively fills information gaps through multiple rounds to ensure report credibility.

- **工具前置**：curl 爬取优先于 API 搜索，获取官方一手来源
- **Tools-First**: Prioritizes curl crawling over API search to obtain official first-hand sources.

- **8种调研类型**：支持竞品分析、技术选型、市场研究、人物研究、政策研究、供应链研究、观点论证、企业研究
- **8 Research Types**: Supports competitor analysis, technology selection, market research,人物研究, policy research, supply chain research, viewpoint validation, and enterprise research.

- **可信度分级**：每项发现标注来源和可信度等级（A+ 至 D）
- **Credibility Grading**: Each finding is labeled with source and credibility level (A+ to D).

- **中国信源覆盖**：内置天眼查、艾瑞、36kr 等中国特有信息源
- **Chinese Sources Coverage**: Built-in Chinese-specific information sources like Tianyancha, iResearch, and 36Kr.

---

## 核心架构
## Core Architecture

```
输入：调研主题 + 约束条件
Input: Research topic + constraints
  ↓
【快速洞察层 QuickInsight】
  ↓ Phase A → curl 爬取（官方一手来源）
  ↓ Phase A → curl crawling (official first-hand sources)
  ↓ Phase B → Role 1（并行探针）
  ↓ Phase B → Role 1 (parallel probes)
  ↓ Phase C → Role 4（信息综合）
  ↓ Phase C → Role 4 (information synthesis)
  ↓ Phase D → Role 6（边界守卫）
  ↓ Phase D → Role 6 (boundary guard)
  ↓
【元认知层 MetaInsight】
  ↓ Phase E → Role 2（差距分析）
  ↓ Phase E → Role 2 (gap analysis)
  ↓ Phase F → Role 3（知识整合）
  ↓ Phase F → Role 3 (knowledge integration)
  ↓
【判断层 XInsight】
  ↓ Phase G → Role 5（终止判断）
  ↓ Phase G → Role 5 (termination judgment)
  ↓
输出：完整调研报告 + 信息缺口说明 + 参考来源
Output: Complete research report + information gap explanation + references
```

---

## 快速开始
## Quick Start

### 一键安装
### One-Click Install

```bash
git clone https://github.com/shirleyharleywiley/multi-agent-deepresearch.git /tmp/mad && cp -r /tmp/mad/skills/* ~/.claude/skills/ && rm -rf /tmp/mad
```

或者分步操作：
Or step-by-step:

1. 克隆仓库：`git clone https://github.com/shirleyharleywiley/multi-agent-deepresearch.git`
1. Clone repository: `git clone https://github.com/shirleyharleywiley/multi-agent-deepresearch.git`

2. 复制 skill：`cp -r skills/* ~/.claude/skills/`
2. Copy skill: `cp -r skills/* ~/.claude/skills/`

3. 开始使用：`/research-multi-agent <主题>`
3. Start using: `/research-multi-agent <topic>`

### 使用命令
### Usage

```
research-multi-agent <主题> --readers <读者类型> --constraints <约束条件>
```

### 示例
### Examples

```bash
# 竞品分析
# Competitor Analysis
research-multi-agent "分析拼多多与京东的竞争策略" --readers "CEO,COO" --constraints "中国市场"

# 技术选型
# Technology Selection
research-multi-agent "Vue vs React 技术选型分析" --readers "CTO" --constraints "最关注性能"

# 企业研究
# Enterprise Research
research-multi-agent "Shopify 组织管理模式研究" --readers "CEO,CTO" --constraints "仅调研其自身"
```

如果用户未在开始调研时输入读者类型和约束条件，则智能体将自动启动对话程序向读者询问相关消息。
If the user doesn't input reader type and constraints at the start, the agent will automatically initiate a dialog to ask for relevant information.

如果读者在开展调研前已经有部分明确待调研的网址，若能配合抓包工具拿到完整URL，发送给智能体，将获得更佳的深度调研结果。
If you already have specific URLs to research, sending them to the agent with a packet capture tool will yield better deep research results.

---

## 调研类型
## Research Types

| 类型 | 核心问题 | 适用场景 |
| Type | Core Question | Use Cases |
|------|---------|---------|
| 竞品分析 | X vs Y 谁更好？ | 产品决策、市场定位 |
| Competitor Analysis | Which is better: X vs Y? | Product decisions, market positioning |
| 技术选型 | 选 A 还是 B？ | 架构决策、技术投资 |
| Technology Selection | Choose A or B? | Architecture decisions, tech investment |
| 市场研究 | 市场规模和趋势？ | 战略规划、投资决策 |
| Market Research | Market size and trends? | Strategic planning, investment decisions |
| 人物研究 | 这人是谁？ | 尽职调查、关系研究 |
| People Research | Who is this person? | Due diligence, relationship research |
| 政策研究 | 政策如何影响行业？ | 合规分析、风险评估 |
| Policy Research | How do policies affect the industry? | Compliance analysis, risk assessment |
| 供应链研究 | 产业链上下游关系？ | 供应商评估、风险管控 |
| Supply Chain Research | Upstream and downstream relationships? | Supplier evaluation, risk management |
| 观点论证 | 验证某个观点是否成立？ | 投资论点、战略假设 |
| Viewpoint Validation | Validate if a viewpoint is correct? | Investment theses, strategic assumptions |
| 企业研究 | 这个企业是如何运作的？ | 竞品研究、投资尽调 |
| Enterprise Research | How does this enterprise operate? | Competitor research, investment due diligence |

---

## 信息源分类
## Information Source Classification

| 等级 | 来源类型 | 可信度上限 |
| Level | Source Type | Credibility Ceiling |
|------|---------|-----------|
| A+ | 官方一手文件（年报、SEC、招股书） | 极高 |
| A+ | Official first-hand documents (annual reports, SEC filings, prospectuses) | Extremely High |
| A | 官方博客、工程文档、官方新闻稿 | 高 |
| A | Official blogs, engineering docs, official press releases | High |
| B | 媒体一手采访、行业研究报告 | 中高 |
| B | First-hand media interviews, industry research reports | Medium-High |
| C | 媒体转述、第三方分析 | 中 |
| C | Media paraphrasing, third-party analysis | Medium |
| D | 无来源推断、匿名爆料 | 低 |
| D | Unsupported inferences, anonymous tips | Low |

---

## 效果对比
## Effect Comparison

| 维度 | 没有框架 | 有框架 |
| Dimension | Without Framework | With Framework |
|------|---------|--------|
| **信息源** | 随机搜索，质量参差 | curl 优先官方一手来源 |
| **Sources** | Random search, varying quality | Prioritize curl for official first-hand sources |
| **覆盖度** | 搜到哪算哪，可能遗漏 | 多轮迭代，主动识别信息缺口 |
| **Coverage** | Search as far as possible, may miss | Multi-round iteration, proactive gap identification |
| **可信度** | 混在一起，不分高低 | A+/A/B/C/D 分级标注 |
| **Credibility** | Mixed together, no distinction | A+/A/B/C/D grading and labeling |
| **终止时机** | 不知道什么时候停 | 四条件判断，明确终止 |
| **Stop Signal** | Don't know when to stop | Four-condition judgment, clear termination |
| **输出** | 碎片化发现 | 结构化报告 + 缺口说明 |
| **Output** | Fragmented findings | Structured report + gap explanation |

---

## 项目结构
## Project Structure

```
multi-agent-deepresearch/
├── README.md           # 项目说明
├── README.md           # Project documentation
├── skills/
│   └── research-multi-agent/
│       └── SKILL.md    # 完整方法论文档
│       └── SKILL.md    # Complete methodology documentation
└── examples/
    └── shopify-case.md # Shopify 企业研究实战案例
    └── shopify-case.md # Shopify enterprise research case study
```

---

## 方法论要点
## Key Methodology Points

1. **curl 优先于 agents**：官方来源质量更高，成功率更高
1. **Prioritize curl over agents**: Official sources are higher quality with higher success rate.

2. **错峰并行**：agents 之间间隔 3-5 分钟，避免 API 超限
2. **Staggered parallel**: Agents are spaced 3-5 minutes apart to avoid API overload.

3. **先落地再综合**：每轮研究结果保存为分维度文件，再做综合
3. **Save first, then synthesize**: Save each round's research results as dimension-specific files before synthesizing.

4. **终止四条件**：核心问题已解决 + 最低可信度达标 + 约束合规 + 剩余缺口属结构性
4. **Four termination conditions**: Core questions resolved + minimum credibility met + constraints compliant + remaining gaps are structural.

---

## 适用场景
## Applicable Scenarios

- 企业/竞品深度调研
- Enterprise/competitor deep research

- 技术选型决策
- Technology selection decisions

- 投资尽职调查
- Investment due diligence

- 行业研究报告
- Industry research reports

- 政策影响分析
- Policy impact analysis

---

## License
## 许可证

MIT License - 欢迎使用、修改和分发
MIT License - Welcome to use, modify, and distribute.

---

## 贡献
## Contributing

欢迎提交 Issue 和 Pull Request！
Welcome to submit Issues and Pull Requests!

---

## 支持一下
## Show Your Support

如果这个框架对你有帮助，欢迎：
If this framework helps you, welcome to:

- **Star** ⭐：给仓库点个 Star，让更多人看到
- **Star** ⭐: Give the repository a Star to help more people discover it.

- **Fork** 🍴：基于这个框架二次开发
- **Fork** 🍴: Build upon this framework for secondary development.

- **Issue** 💬：提出问题或建议
- **Issue** 💬: Ask questions or provide suggestions.

你的支持是我继续优化的动力！
Your support is my motivation for continued optimization!
