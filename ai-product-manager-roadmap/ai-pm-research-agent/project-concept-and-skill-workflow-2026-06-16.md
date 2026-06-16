# AI PM Research Agent - Skill Experiment 01

Date: 2026-06-16

Goal: Use the newly installed PM / Agent skills to explore an `AI PM Research Agent` concept, then record what worked and what should be improved.

Skills used:

- `competitor-analysis`
- `market-segments`
- `value-proposition`
- `create-prd`
- `strategy-red-team`
- `context-engineering` as meta guidance

Reference signals:

- [phuryn/pm-skills](https://github.com/phuryn/pm-skills): PM Skills Marketplace, with PM skills and chained workflows.
- [ChatPRD](https://www.chatprd.ai/): commercial AI product manager platform for product docs and coaching.
- [MindStudio: 10 AI Agents for Product Managers](https://www.mindstudio.ai/blog/ai-agents-for-product-managers): examples of PM workflows such as roadmap visualization, app review analysis, PRD chatbot, and dashboards.
- [Product Compass PM Skills Marketplace article](https://www.productcompass.pm/p/pm-skills-marketplace-claude): open-source PM skills and workflows for AI-assisted product work.

## 1. Competitor Analysis

### Market Definition

`AI PM Research Agent` sits between three markets:

1. AI writing tools for product docs.
2. Product management workflow tools.
3. Research agents that collect, summarize, and structure external information.

The target job is not just "write a PRD." The real job is:

> Help a PM quickly understand a new product, repo, market, or user problem, then turn that research into usable product judgment.

### Direct / Adjacent Competitors

| Competitor | Type | Strength | Gap / Opportunity |
| --- | --- | --- | --- |
| ChatPRD | Commercial AI PM platform | Clear PM positioning, doc generation, coaching, team workflow | More focused on product docs than open-ended trend/repo/market research |
| phuryn/pm-skills | Open-source PM skills marketplace | Broad PM frameworks: discovery, strategy, execution, GTM, analytics | Skills are modular, but not packaged around "AI PM transition / portfolio building" |
| Productboard AI / Aha! AI / Linear AI style features | PM SaaS with AI features | Embedded in existing product workflows and customer data | Usually assumes a company context; less useful for solo research and public-source analysis |
| Generic LLMs: ChatGPT / Claude / Gemini | General AI assistant | Flexible, strong reasoning, easy to use | No fixed PM workflow, weak repeatability, depends heavily on prompt quality |
| Perplexity / NotebookLM / research agents | Research and synthesis | Better citation and source grounding | Less PM-specific; usually does not output PRD, segmentation, roadmap, or portfolio framing |

### Differentiation Opportunity

The strongest opening is not "another PRD generator." It is:

> A research-to-product-decision workflow for AI PMs, especially people evaluating new AI products, GitHub repos, and market opportunities from public information.

Potential differentiators:

- GitHub repo / trend scan as a first-class input.
- Source-backed product analysis, not just generic advice.
- Output optimized for PM artifacts: segment, JTBD, value prop, assumptions, MVP, metrics, PRD.
- Built-in "portfolio angle": how this research can become a public project, case study, or interview story.
- Red-team step by default, so every idea includes kill assumptions and cheap tests.

## 2. Market Segments

### Segment A: AI PM Career Switchers

Profile:

- Product managers, operations people, analysts, or business students moving into AI PM.
- Often have product intuition but weak public portfolio.
- Need to learn fast and show proof of work.

JTBD:

> When I discover a new AI product or GitHub repo, help me understand whether it matters and how I can turn it into a portfolio artifact.

Pain points:

- Too many AI products and repos.
- Hard to distinguish hype from useful product signal.
- Hard to turn reading into concrete PRD / case study / demo.

Product fit:

- Very strong for MVP.
- This is the best first segment because the user can operate with public data and does not require company integrations.

### Segment B: Solo PMs / Early Startup Founders

JTBD:

> Help me research competitors, user segments, and product positioning before I build.

Pain points:

- Limited time for structured market research.
- Need fast decisions, but generic LLM outputs are too vague.
- Need investor / team-ready docs.

Product fit:

- Good, but they may require more real market validation and deeper GTM support.

### Segment C: PM Teams Inside Companies

JTBD:

> Help the team synthesize customer feedback, market signals, and strategy docs into product decisions.

Pain points:

- Internal context is scattered across docs, tickets, analytics, sales calls.
- Security and permission boundaries matter.

Product fit:

- Valuable but not ideal for MVP because it needs integrations, access control, and trust.

### Segment D: Product Educators / PM Coaches

JTBD:

> Help students practice structured product thinking using live products and repos.

Pain points:

- Need repeatable exercises.
- Need rubrics and feedback, not only final answers.

Product fit:

- Good secondary segment.
- Could become a course companion or training tool.

## 3. Value Proposition

Target first segment: AI PM career switchers.

### Who

Aspiring AI product managers who want to build a public portfolio from real AI products, open-source repos, and market trends.

### Why

They need to learn fast, but passive reading does not create visible proof. They need to convert scattered signals into product judgment.

### What Before

They manually browse GitHub, newsletters, product websites, YouTube videos, and articles. Notes are scattered. Outputs are often vague summaries, not product artifacts.

### How

The agent takes a topic, product URL, GitHub repo, or market question and returns a structured PM analysis:

- What it is.
- Who it serves.
- What problem it solves.
- Competitor / alternative landscape.
- Segment and JTBD.
- Product opportunity.
- MVP scope.
- Metrics.
- Risks and cheap validation tests.
- Portfolio angle.

### What After

The user can turn one research session into:

- A GitHub weekly review.
- A PRD draft.
- A portfolio case study.
- An interview talking point.
- A concrete demo idea.

### Alternatives

- Generic LLM chat: flexible but inconsistent.
- ChatPRD: strong for docs but less focused on public-source research and career portfolio.
- Notion / NotebookLM / Perplexity: good research support but not PM artifact workflow.
- Manual research: high quality possible, but slow and hard to repeat.

Concise value proposition:

> AI PM Research Agent helps aspiring AI product managers turn public AI product signals into structured product decisions, PRD drafts, and portfolio-ready case studies.

## 4. MVP PRD

### 1. Summary

AI PM Research Agent is a research workflow that helps users analyze an AI product, GitHub repo, or market topic and convert it into PM-ready artifacts.

The first version focuses on public-source research and structured outputs, not internal company data.

### 2. Contacts

| Name | Role | Comment |
| --- | --- | --- |
| Chen Zhuoxin | Product owner / target user | First user and evaluator |
| Codex | Build and research assistant | Helps run skill workflows and produce artifacts |

### 3. Background

AI product work is moving quickly. PMs need to track tools, repos, workflows, and competitors. Existing tools can write documents, but they often do not help users decide what matters or how to turn research into a public proof-of-work artifact.

This is now easier because LLMs can search, summarize, classify, and draft structured product documents from public information.

### 4. Objective

Objective:

> Help an aspiring AI PM turn one product/repo/topic into a structured product analysis in under 30 minutes.

Key results for MVP:

- 5 completed research runs across different topics.
- Each run produces at least 1 usable artifact: PRD, GitHub review, opportunity brief, or portfolio note.
- User rates output usefulness at 4/5 or above in 3 of 5 runs.
- At least 3 repeated output sections become stable templates.

### 5. Market Segment

First target:

- AI PM career switchers who need portfolio artifacts.

Do not target first:

- Large enterprise PM teams with private data.
- Fully automated product strategy for executives.

### 6. Value Proposition

For aspiring AI PMs who need proof of product thinking, AI PM Research Agent turns live AI market signals into structured product artifacts with citations, assumptions, and validation tests.

### 7. Solution

MVP input:

- Topic text, such as `AI PM Research Agent`.
- Product website URL.
- GitHub repo URL.
- Optional user goal: learn, compare, write PRD, find portfolio angle.

MVP output:

1. One-line summary.
2. Market and competitor scan.
3. User segments and JTBD.
4. Value proposition.
5. MVP PRD draft.
6. Red-team assumptions.
7. Portfolio angle.
8. Next action checklist.

Key features:

- Source collection and citation.
- PM framework selection.
- Artifact generator.
- Red-team review.
- Experiment log saved as Markdown.

Not in MVP:

- Login and multi-user team workspace.
- Enterprise integrations.
- Full analytics dashboard.
- Automatic publishing.
- Paid subscription.

### 8. Release

Version 0:

- Manual workflow using installed skills and Markdown output.

Version 1:

- A repeatable prompt/workflow template.
- A saved experiment folder.
- 3-5 completed examples.

Version 2:

- Lightweight web or CLI interface.
- Input URL parser.
- Output artifact selector.

## 5. Red-Team

### Top Kill-Assumptions

#### 1. Claim: AI PM career switchers will repeatedly use this.

Fails if:

- They prefer general chat and do not value fixed PM artifacts.

Evidence to get this week:

- Run 3 real topics and ask whether the structured output is better than a normal chat answer.

Kill criterion:

- If fewer than 2 of 3 runs produce something worth saving to GitHub, the workflow is not sharp enough.

Cheapest test:

- Use this exact Markdown workflow for 3 topics: `pm-skills`, `ChatPRD`, and `cross-border AI shopping agent`.

#### 2. Claim: Public information is enough for useful PM judgment.

Fails if:

- Outputs remain too generic without internal user data or interviews.

Evidence to get this week:

- Compare one public-source run against one run that includes personal project context, such as A-Level Plus.

Kill criterion:

- If public-only runs cannot produce concrete assumptions, metrics, or MVP scope, source strategy must change.

Cheapest test:

- Require every run to cite at least 3 sources and list 3 falsifiable assumptions.

#### 3. Claim: The product is meaningfully different from ChatPRD or generic LLM chat.

Fails if:

- The output is only a PRD generator with nicer formatting.

Evidence to get this week:

- Run the same input through a generic chat prompt and compare output quality.

Kill criterion:

- If the agent does not add better source grounding, portfolio framing, or red-team testing, reposition it.

Cheapest test:

- Create a comparison table: generic LLM vs ChatPRD-like PRD workflow vs AI PM Research Agent.

#### 4. Claim: Skills can be chained into a reliable workflow.

Fails if:

- Each skill produces isolated artifacts that do not feed into the next step cleanly.

Evidence to get this week:

- Run one full chain from competitor analysis to PRD and inspect repeated or conflicting sections.

Kill criterion:

- If more than 30% of sections are redundant or inconsistent, add an orchestrator template.

Cheapest test:

- Build a single "Research Run Template" that defines inputs, intermediate outputs, and final artifact.

### What's Well-Reasoned

- Starting with manual skill usage is the right first step. It tests product workflow before building software.
- The first segment is clear and reachable because it can use public information.
- The red-team step is valuable because it prevents the output from becoming motivational but non-actionable.

### What I Couldn't Assess

- Will users pay for it?
- Which workflow has the highest repeat usage?
- Whether GitHub trend data is enough to sustain weekly content.
- Whether the tool should become a web app, a Codex skill, or a GitHub repo template.

## 6. Skill Experience Notes

### What Worked

- The skills created a good chain: competitor analysis -> segments -> value prop -> PRD -> red-team.
- The output became more product-like than a generic brainstorm.
- The red-team skill is especially useful because it converts "sounds good" into testable assumptions.

### What Was Weak

- The skills are independent. They do not automatically preserve a shared context model.
- `competitor-analysis` expects a known market, but this topic is partly a new category.
- The default PRD template is useful, but too formal for early exploration unless shortened.
- There is no built-in "portfolio angle" section, which is important for this use case.

### Enhancement Ideas

Create a custom skill:

`ai-pm-research-run`

It should chain these steps:

1. Source scan.
2. Competitor and alternative map.
3. Segment and JTBD.
4. Product opportunity.
5. MVP PRD.
6. Red-team assumptions.
7. Portfolio / interview angle.
8. Saved Markdown output.

Add mandatory fields:

- Source links.
- Confidence level.
- What evidence is missing.
- Why this matters for AI PM.
- How to turn it into a GitHub artifact.

