# AI Frontier 🌐

> AI 前沿资料库 — 追踪趋势、技术、研究、能力。

一句话定位：**源头**。`atomlearn` 负责"消化"，这个仓库负责"收集"。

## 内容范围

- **趋势**：行业动向、产品发布、大模型迭代、关键事件
- **技术**：值得关注的库、框架、协议、架构模式
- **研究**：论文、博客、研究机构、关键人物
- **能力**：模型 benchmark、SOTA、对比测评、能力边界
- **工具**：开源仓库、产品、SaaS、命令行工具

## 不收什么

- ❌ 跟 AI 无关的内容（除非作为对比参照）
- ❌ 一手新闻快讯（用 RSS / newsletter 即可，沉淀过的才放这）
- ❌ 过时的库/工具（6 个月没更新会标注 ⚠️）
- ❌ 未读过的资料（每条资料至少要看过一遍，附一句"为什么值得"）

## 目录约定

```
ai-frontier/
├── README.md          ← 本文件
├── INDEX.md           ← 总览 + 标签云
├── topics/            ← 按主题分（AI 子领域）
│   ├── ai-languages/  ← 编程语言（DSL、Agent 语言等）
│   ├── llm/           ← 大模型本体
│   ├── agents/        ← Agent 框架与协议
│   ├── multimodal/    ← 多模态
│   ├── cogarch/       ← 认知架构
│   └── ...
├── tools/             ← 工具/产品/仓库
│   ├── ai-languages.md
│   ├── frameworks.md
│   └── ...
├── people/            ← 关键人物 + 他们的工作
├── papers/            ← 论文笔记
├── benchmarks/        ← benchmark + SOTA 追踪
└── notes/             ← 自己的思考、对比、决策
```

## 命名约定

- 文件名用 kebab-case：`gpt-5-rumors.md`
- 每个资料文件至少包含：
  - **链接**（原始来源）
  - **一句话定位**（这玩意是啥）
  - **为什么值得**（不超 3 行）
  - **状态**：🟢 活跃 / 🟡 观望 / ⚠️ 停滞 / ❌ 已弃
  - **入库时间**：YYYY-MM-DD

## 怎么贡献

- 手动：直接 PR（你 fork 后 commit + push，或我帮你写脚本批量）
- 自动：跟我说"加 xxx 到 ai-frontier"，我判断后入库
- 批量：从 RSS / arXiv / Twitter 拉一批 → 我筛 → 入库

## 关联仓库

- [wcaca/atomlearn](https://github.com/wcaca/atomlearn) — 把书变成沉浸式学习（消化资料）
- [wcaca/agent-memory](https://github.com/wcaca/agent-memory) — Mavis agent 跨会话记忆

---

最后更新：2026-06-21 · 入库 4 条 (+3 Claude Skills 方向)
