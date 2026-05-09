# Shopify 组织管理调研案例

本案例记录了 research-multi-agent 方法论在 Shopify 组织管理调研项目中的实战经验。

---

## 调研背景

**主题**：Shopify 组织管理模式研究
**目标读者**：CEO/高管、CTO/研发VP
**约束条件**：只讲 Shopify 自身，不做 300 人团队对标

---

## Day 3：约束条件生效

### 用户约束
- "舍弃掉对300人团队对标的执念，只要讲清楚shopify自己的组织发展即可"
- "考核机制没有讲，企业文化如何传递没有讲……你做了多轮迭代吗？"

### Role 1 行动
拆解为 4 个子方向并行搜索：
- 绩效评估机制（Flex Comp、AI in绩效、IC/Manager双轨）
- 文化传递（Engineering Blog、Code Review、Hack Days）
- 无架构师机制（工具链替代权威）
- CEO/VP Engineering 个人推动力

### Role 5 判定（发现问题）
Flex Comp 可信度只有"中"，低于最低门槛"中高"，但继续搜索触及结构性限制。→ 终止迭代。

---

## Day 4 Part 1：方法突破前的挫折

### 问题
3 个 agents 并行同时搜索 → 全部触发 MiniMax API 529 超限

### Role 5 判定
结构性限制，继续挖的边际收益极低。诚实标注缺口。

---

## Day 4 Part 2：方法突破——curl + sitemap 组合拳

### 第一步：curl 爬取已知的官方页面

```
curl 采集结果：
- shopify.engineering/building-flex-comp（Flex Comp 工程博客）
- shopify.com/editions/winter2026（Winter 2026 Editions）
- shopify.engineering/capturing-every-change-shopify-sharded-monolith
- shopify.engineering/fine-tuning-agent-shopify-flow
- shopify.dev/docs/apps/build/devmcp
```

**关键改进**：
- Flex Comp 章节**完全重写**（可信度从"中" → **"最高"**）
- 新增 Dev MCP 工具链章节
- 参考来源从 12 条 → **18 条**

### 第二步：JS bundle 无法提取文章列表，用户主动提供了 sitemap

当 curl 爬取 Engineering Blog 首页时，发现页面是 JS 渲染的，JS bundle 里只有组件代码，没有文章数据。**主动向用户说明障碍**，用户随后从官网找到了 `https://shopify.engineering/sitemap.xml` 的 URL。

用 curl 抓取 sitemap 后：**416 篇文章的完整列表**一目了然，时间跨度 2010-2026，最新日期、slug、URL 全部获取。按关键词筛选后发现了 5 篇此前未知的高价值文章：

| 文章 | 日期 | 新增内容 |
|------|------|---------|
| A Packwerk Retrospective | 2024-02-07 | Packwerk v3.0 移除 privacy checks 的教训 |
| How Shopify Scales Up Its Development Teams | 2019-09-26 | onboarding 1年铁律、5-9人跨职能团队 |
| Great Code Reviews | 2020-02-10 | 200-300行PR原则、Draft PR早反馈 |
| On the Importance of PR Discipline | 2022-10-13 | PR即提案、commit原子性 |
| Deconstructing the Monolith | 2019-02-21 | 模块化单体演进、为何不选微服务 |

**结论**：即使 curl 爬取失败，主动求助用户也能解锁关键资源。sitemap 是获取大量文章列表的最佳方式。

---

## 最终产出

| 报告 | 读者 | 章节结构 |
|------|------|---------|
| 通用版 | CEO/高管 | 10章（删除研发专项，第3章改为团队协作机制） |
| 研发专项版 | CTO/研发VP | 7章（第3章为核心章节） |

---

## 核心教训

### 教训一：API 超限时立即切换策略
当 agents 搜索遇到 API 超限时，不要重试——立即切换到 curl 爬取。curl 的信息质量更高（官方一手来源）、成功率更高（标准 HTTP，无 API 限流）、内容更完整（不是碎片化摘要）。

### 教训二：主动求助用户
当发现自己无法独立完成任务时，要主动向用户求助。在 Engineering Blog JS bundle 中提取不到文章内容时，不应该说"没有有用的信息"然后放弃。正确做法是：说出遇到的障碍，提出可能的替代路径（如 sitemap.xml），然后问用户是否有可以直接访问的 URL。用户帮我们找到了 sitemap.xml，解锁了 416 篇文章的完整列表——**协作的价值在于信息互补**。

> "当工具和能力受限时，明确说出来比假装继续有效工作更有价值。"

### 教训三：综合时必须先保存分维度研究文件
Day2 做到了（25个分维度 md → 综合报告），Day3 没做到（直接编辑 Agent 输出做重组）。后果是：当需要补充内容时，没有可追溯的中间产物，只能从 Agent 输出文件里翻找。

**正确顺序**：研究 → 保存 → 综合。

### 教训四：中间产物的可追溯性价值
Day3 sitemap 补充工作揭示的深层问题——当 agents 输出后没有先写分维度文件，综合报告（如 Day3 通用版）就直接成型了，等后来发现 Engineering Blog 有 416 篇文章可补充时，需要重新翻 Agent 的输出文件来对照哪些内容有缺口、哪些没有。

这说明"先落地再综合"不仅是工作流程问题，更是**信息可追溯性**的问题——没有分维度文件，综合报告和原始研究之间就失去了对应关系，补充工作只能靠记忆和猜测。

**每一次研究轮次结束，必须生成"分维度研究 md → 综合报告"的完整链路文档。**
