# AI Assistants / 主力 AI 产品

> 跟 AI 直接对话的产品 (ChatGPT / Claude / Gemini 等)。
> 跟 [tools/ai-languages.md](./ai-languages.md) 不同 — 那些是 Agent 用的语言,
> 这里是用户用的产品。

---

## Claude Tag (2026-06-23 发布)

- **链接**：https://claude.com/product/tag · https://claude.com/docs/claude-tag/overview
- **作者**：Anthropic
- **类型**：AI 虚拟团队成员 / Slack 集成 / Claude Code 进化版
- **底层**：Claude Opus 4.8
- **首次发布**：2026-06-23
- **入库时间**：2026-06-24
- **状态**：🟢 Beta (Claude Enterprise / Team 用户)

### 一句话定位

Claude Tag 让 Claude 以"团队成员"身份加入 Slack — 管理员授权频道 + 工具 (GitHub/Jira/Linear/Figma/Notion) + 数据源后, 任何人在频道 @Claude 派任务, 它自己拆解步骤、调用工具执行、异步跑完在线程里回报。

### 四个核心特性

1. **Multiplayer**: 一个频道一个 Claude, 全员可见进度, 张三派活李四接力, 告别孤岛对话。
2. **持续记忆**: Claude 跟着频道上下文积累项目背景 + 技术栈偏好 + 决策习惯。私聊/私密频道不会越权读。
3. **Ambient Mode (主动介入)**: 开启后主动提醒冷落讨论、跟进悬置问题、标记待决策项 — 像个真在盯频道的同事。
4. **异步执行**: 派完活你可以走开, 它自己排计划数小时甚至数天。

### 为什么重要

- **Anthropic 自己 65% 代码由内部版 Claude Tag 生成** (Karpathy 转推)
- **Karpathy**: "LLM 第三次 UI 变革 — 1.0 访问网站, 2.0 本地应用, 3.0 持久运行异步实体"
- 底层跑 Opus 4.8, 跟前代 Opus 4.7 比自主调用 Agent 更可靠
- 30 天内替代现有 "Claude in Slack" 应用

### 跟 system-self 关联

- 这是 AI Agent "伙伴化" 的范式信号 — 跟 wcaca 推的 "PARTNER_PROTOCOL" 不谋而合
- 异步执行 + 主动介入 + 持续记忆 = 用户偏好的 partner-protocol 模型已经产业落地
- 后续 system-self 如果接 Slack, Claude Tag 是参考实现

### 我的判断

🟢 **观察** — Anthropic 自己 65% 代码自给 + Karpathy 站台 + 完整企业权限模型,
证明这个方向产品上跑得通。但 slack-only 限制大, 飞书/Teams 还没接,
3 个月后看 ambient mode 噪音控制 + 跨平台扩展速度。

---

## Claude Opus 4.8 (2026-05-29 发布)

- **链接**：https://www.anthropic.com/news/claude-opus-4-8
- **作者**：Anthropic
- **类型**：前沿 LLM
- **前置**：Opus 4.7 (2026-02)
- **首次发布**：2026-05-29
- **入库时间**：2026-06-24
- **状态**：🟢 GA · 已上 Cursor / Claude Code / Messages API

### 关键数据

- **SWE-Bench Pro**: 69.2% (超 GPT-5.5 + Gemini 3.1 Pro)
- **TerminalBench 2.1**: GPT-5.5 仍领先
- **USAMO 2026 数学**: 96.7% (Opus 4.7 是 69.3%)
- **价格**: 同 Opus 4.7 — $5/$25 (常规), $10/$50 (快速)
- **快速模式**: 2.5x 速度, 1/3 成本

### 增量更新要点

1. **动态工作流** (Claude Code 研究预览): 接到大任务 → 自主规划数十到数百个并行子 Agent → 汇总校验。Bun 移植 Zig→Rust 用这个: 11 天完成 75 万行 Rust 代码合并, 99.8% 测试通过。
2. **投入度控制** (claude.ai): 用户可调模型生成回复的算力 (速度 vs 质量)。
3. **Messages API 新增 "系统条目"**: 任务执行中实时更新 Claude 指令。

### 对齐表现

- "放任自己代码缺陷不加说明" 概率 ↓ 4x (vs Opus 4.7)
- 欺骗等失配行为出现率 ↓
- 证据不足时主动停下等用户补充信息 (而不是硬编)

### Glasswing / Mythos

- 已有少数机构开始试用 "Claude Mythos 预览版" 做网络安全
- Anthropic 预计未来数周内将 Mythos 级模型正式向更多客户开放
- = "智能水平超越现有 Opus 的新一类模型"

### 我的判断

🟢 **采用** — system-self 用的 `MINIMAX_API` 是 M2.7 系列, 跟 Opus 4.8 不在同一栈 (M2 是 MiniMax 模型), 但 Opus 4.8 的 "动态工作流" 思路值得借鉴到 system-self 的 multi-agent (cobweb/landscape/agent/step 多 agent 并行)。

---

## Claude Skills 完整构建指南 (2026-01-29 发布)

- **链接**：https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf
- **作者**：Anthropic
- **类型**：技术指南 PDF
- **页数**：33 页
- **首次发布**：2026-01-29
- **入库时间**：2026-06-24
- **状态**：🟢 GA · Anthropic 官方

### 核心设计 (三层渐进式披露)

| 层 | 内容 | 加载时机 | Token 预算 |
|----|------|---------|----------|
| 1. 元数据 | YAML frontmatter (`name` + `description`) | 始终在上下文 | ~100 词 |
| 2. SKILL.md | 完整指令和工作流 | Skill 触发时加载 | <5k 词 |
| 3. 资源 | `scripts/` `references/` `assets/` | 按需加载 | 无限制 |

### 三种应用模式

1. **文档与资产创作**: API 文档 / 项目模板 / 测试报告
2. **工作流自动化**: 代码审查 / 数据处理管道 / 部署工作流
3. **MCP 增强**: 数据库查询 / API 调用 / 外部工具集成

### 关键设计原则

- Skill = 完整系统 (SKILL.md + 脚本 + 文档 + 资产), 不是简单提示词
- 按需加载 → 显著减少 token 消耗 + 避免上下文窗口过载
- 标准化 → 跨平台 (Claude Code / OpenClaw / Cursor) 可移植
- 最佳实践固化到执行层 → API 调用和任务处理更稳定

### 实际案例

- **墨问 OpenAPI Skill**: Claude Code / OpenClaw 都用
- **Atlassian Skills**: 一键产品需求 → Jira 看板 + Confluence 报告
- **Notion Skills**: 提问到执行无缝衔接

### 社区反响

- Reddit r/ClaudeAI 1.5K+ 点赞 112+ 评论
- 评价: "great read for anyone new to skills"

### 我的判断

🟢 **采用** — 这跟 wcaca agent-memory 的 SKILL.md 模式完全对齐, 也是 Mavis 自己用的渐进披露思路。33 页 PDF 值得一读, 至少学它的"元数据 + 主体 + 资源"三层模型。我们的 `.skills/` 目录就是这模式, 可以对照官方指南补 frontmatter 的元数据规范。

---

## GPT-5.5 / Gemini 3.1 Pro / Claude Opus 4.8 对比

(2026-05-20 节点的状态)

| 模型 | 编程 (SWE-Bench Pro) | 终端 (TerminalBench 2.1) | 数学 (USAMO 2026) | 发布 |
|------|----|----|----|----|
| Claude Opus 4.8 | 69.2% ✅ | 第二 | 96.7% ✅ | 2026-05-29 |
| GPT-5.5 | 第二 | 第一 | - | 2026-Q2 |
| Gemini 3.1 Pro | 第三 | - | - | 2026-Q2 |

来源: Anthropic 官方评测 + Karpathy 转推。

---

## 历史存档

_(Claude 3 / 3.5 / Sonnet 4 系列没单独建条目, 已在 wcaca agent-memory
Sonnet/Opus 升级决策里有引用)_
