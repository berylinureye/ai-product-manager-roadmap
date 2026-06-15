# Course Based AI PM Plan

这个版本按网页里的 B 站课程重新排布。原则：课程只看和产出强相关的部分，每次看完必须沉淀成 GitHub 笔记、PRD、评测集或 demo。

## 课程链接

| 优先级 | 课程 | 链接 | 怎么学 |
| --- | --- | --- | --- |
| P0 | 大模型认知与能力边界：AI 产品经理从零到精通 | https://www.bilibili.com/video/BV1txKPePExi/ | 先看 1 小时，建立 AI PM 岗位地图和模型边界。 |
| P0 | Prompt 工程：吴恩达《提示词工程》 | https://www.bilibili.com/video/BV1173jzNELG/ | 看 1-2 小时后，直接为 A-Level Plus 写 3 版 prompt。 |
| P0 | Agent / 工作流编排：Coze 扣子智能体全套教程 | https://www.bilibili.com/video/BV1Tx9ZYSEkc/ | 边看边做一个可演示 Agent。 |
| P0 | Dify · LLMOps 应用平台 | https://www.bilibili.com/video/BV116w5zuEbo/ | 用来搭 RAG/Agent，不完整刷完。 |
| P0 | Datawhale Hello-Agents | https://github.com/datawhalechina/hello-agents | Agent 系统化教程。先读第 1/4/5/8/10/12 章，建立原理、低代码、记忆检索、协议和评估框架。 |
| P0 | Datawhale All-in-RAG | https://github.com/datawhalechina/all-in-rag | RAG 全栈教程。先读第 1/2/3/4/6 章，重点是切块、向量、检索优化和评估。 |
| P1 | RAG / 知识库：RAGflow 知识库实战 | https://www.bilibili.com/video/BV16JoCYMEVc/ | 学 RAG 全链路，产出架构图和 bad case。 |
| P1 | 产品经理入门基础课 | https://www.bilibili.com/video/BV1kv4y1W7SQ/ | 只看 PRD、需求分析、竞品分析相关章节。 |
| P1 | MCP / 工具调用 | https://www.bilibili.com/video/BV1bDRcYFEhP/ | 看概念和案例，目标是面试能讲清。 |
| P2 | 金字塔原理实战 | https://www.bilibili.com/video/BV16s411u7FH/ | 只看结构化表达部分，用来优化面试表达。 |
| P2 | SQL 零基础一小时入门 | https://www.bilibili.com/video/BV1ZJ411i7YM/ | 你已有 SQL 基础，跳过或只复习漏斗/留存表达。 |
| P2 | LangChain 入门到实战 | https://www.bilibili.com/video/BV1cCXHYBE3t/ | 暂缓，除非投偏技术型 AI PM/FDE。 |

## 8 周压缩路线

### Week 1: 岗位地图 + 大模型边界 + Prompt

课程：

- AI 产品经理从零到精通：看 2-3 小时。
- 吴恩达提示词工程：看 1-2 小时。

产出：

- 模型能力边界笔记。
- AI PM 岗位能力词表。
- A-Level Plus prompt 迭代记录。

### Week 2: PRD + 数据指标 + 竞品

课程：

- 产品经理入门基础课：只看需求、PRD、竞品章节。
- SQL 课：只复习指标表达，不完整刷。

产出：

- `A-Level Plus 拍照批改优化 PRD v0.1`
- 指标体系：完成率、正确率、追问率、满意度、时延、成本。

## 阶梯式材料安排

### Level 1: 先建立概念

- B 站 `AI 产品经理从零到精通`
- B 站 `吴恩达提示词工程`

目标：能听懂岗位语言，能解释 LLM、Prompt、Agent、RAG、MCP、评测集、bad case。

### Level 2: 再用低代码做出手感

- Coze 扣子智能体教程
- Dify LLMOps 教程
- RAGFlow 知识库实战

目标：不陷入代码细节，先跑通一个能演示的 Agent/RAG demo。

### Level 3: 最后用 Datawhale 系统化

- `hello-agents`：把 Coze/Dify 里的节点，翻译成 Agent 原理、记忆、工具调用、协议和评估。
- `all-in-rag`：把知识库 demo，翻译成数据准备、切块、索引、检索优化、生成和评估。

目标：面试时不只说“我会用工具”，而是能讲清为什么这样设计、哪里会失败、怎么评估和优化。

### Level 4: 转成作品集

- A-Level Plus AI 拍照批改作品。
- AI 提升跨境下单转化 PRD。
- GitHub 周榜分析 Agent。

目标：每学一个概念，都要落到你自己的项目里。

### Week 3: Coze Agent Demo + Hello-Agents 入门

课程：

- Coze 扣子智能体全套教程。
- Datawhale Hello-Agents：读第 1 章“初识智能体”、第 4 章“智能体经典范式构建”、第 5 章“基于低代码平台的智能体搭建”。

产出：

- 一个可演示 Agent：GitHub 周榜分析 Agent 或跨境导购 Agent。
- Agent 说明文档：目标用户、工具列表、prompt、失败兜底。
- 一页 Agent 原理笔记：ReAct / Plan-and-Solve / Reflection 分别解决什么问题。

### Week 4: Dify + RAG + All-in-RAG 入门

课程：

- Dify 课程。
- RAGflow 课程选看。
- Datawhale All-in-RAG：读第 1 章“解锁 RAG”、第 2 章“数据准备”、第 3 章“索引构建”、第 6 章“RAG 系统评估”。

产出：

- 一个知识库问答 demo。
- RAG 架构图：切块、向量化、召回、重排、生成、引用、拒答。
- 10 条 bad case 和修复策略。
- 一页 RAG 评估笔记：检索命中、答案忠实度、引用准确性、拒答能力。

### Week 5: Agent/RAG 进阶补强

课程：

- Datawhale Hello-Agents：读第 8 章“记忆与检索”、第 10 章“智能体通信协议”、第 12 章“智能体性能评估”。
- Datawhale All-in-RAG：读第 4 章“检索优化”，重点看混合检索、查询构建、查询重构。

产出：

- 把 Agent demo 增加记忆/检索说明。
- 把 RAG demo 增加评估表。
- 写一篇 `Agent + RAG 为什么会失败，以及产品经理怎么兜底`。

### Week 6: A-Level Plus 作品集化

课程：

- 不刷课，集中整理作品。

产出：

- A-Level Plus 作品集文档。
- 30 秒 demo 讲稿。
- 3 分钟面试讲述。

### Week 7: 跨境下单转化 AI PRD

课程：

- 只按需回看 PRD/Agent/RAG 相关片段。

产出：

- `AI 提升跨境下单转化 PRD v1`
- 漏斗指标 + A/B 实验设计。

### Week 8: MCP + 面试语言 + 投递冲刺

课程：

- MCP / 工具调用。
- 金字塔原理选看。
- 不再新增系统课程，剩余时间用于投递和复盘。

产出：

- MCP 一页解释。
- 10 个 AI PM 高频面试问答。
- 简历 v1。
- 简历 v2。
- GitHub 主页 README。
- 投递清单。
- 两个月复盘。

## 今晚 2 小时计划

日期：2026-06-15

### 0:00-1:00 看课

看这个课的前 60 分钟：

https://www.bilibili.com/video/BV1txKPePExi/

只抓 4 个问题：

1. AI 产品经理和普通产品经理的差别是什么？
2. 大模型能力边界是什么？
3. AI PM 需要懂哪些技术词，但不需要写到什么程度？
4. 哪些内容能和我的美团/A-Level Plus 经历连接？

### 1:00-1:40 写总结笔记

建议写这 5 段：

1. 我今天对 AI PM 的新理解。
2. 我原本会的能力，哪些已经匹配 AI PM。
3. 我目前最缺的 3 个能力。
4. 我可以立刻包装的项目：A-Level Plus / 美团 AI 提效 / 跨境下单转化。
5. 明天要继续看的课或要补的 demo。

### 1:40-2:00 发给我

你把笔记贴给我后，我帮你做三件事：

1. 改成 GitHub 周记录格式。
2. 提炼成简历/面试可用表达。
3. 如果当前目录是 Git 仓库且你确认目标仓库，我帮你 commit/push。
