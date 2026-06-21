# Agent Skills / 技能系统

> 把"如何完成某类任务"的指令、脚本、资源打包成可组合模块的机制。
> Agent 在判断任务匹配时自动加载（渐进式披露）。

---

## Claude Skills

- **链接**：https://github.com/anthropics/skills
- **官方公告**：https://www.anthropic.com/news/skills
- **工程博客**：https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- **构建指南 PDF**：https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf (33 页)
- **作者**：Anthropic
- **类型**：技能系统 / Agent 能力扩展 / 渐进式披露
- **协议**：Apache-2.0（文档技能 source-available）
- **Stars**：~40k（含 anthropics/skills 主仓库，社区 skills 仓库数以万计）
- **首次发布**：2025-10-16
- **入库时间**：2026-06-21
- **状态**：🟢 活跃（已成为事实标准）

### 一句话定位

Claude 通过加载"S文件夹"获得专业能力——每个 Skill = 一个 SKILL.md + 脚本/资源，按需加载，跨 Claude 应用/Code/API 复用。

### 为什么值得

1. **设计精巧**：三层渐进式披露（YAML 元数据 → SKILL.md 完整指令 → 关联引用文件）。Agent 启动时只预加载元数据，需要时再读详情，**Token 节省 60-80%** 是真实数字。
2. **可组合 + 可执行**：Skill 可以含 Python 脚本或 Bash 命令，Claude 在沙箱中执行。比 prompt-only 更可靠（确定性操作交给代码，模糊判断交给 LLM）。
3. **跨平台**：同一 Skill 在 Claude.ai / Claude Code / Messages API 都可用，写一次到处跑。
4. **官方示范 + 社区爆发**：50+ 官方 Skill（docx/pdf/pptx/xlsx/webapp-testing/server-generation/skill-creator…），社区 1000+ 公开 Skill 仓库。

### 适用场景

- 把团队的"专业知识 + 工作流"沉淀成可复用模块（新人入职第一天就有专家级能力）
- 文档处理（自动 Excel/PPT/Word/PDF）走 Anthropic 官方 Skill 即可
- Agent 需要确定性操作时（数据处理、文件操作）用代码 Skill 替代 prompt

### 不适用 / 风险

- **安全**：Skill 可执行任意代码，必须从可信源安装
- **维护**：含代码的 Skill 需要持续更新依赖
- **复杂流程**：SKILL.md 太长时应拆成多文件 + 引用，避免单文件膨胀

### 关键命令

```sh
# Claude Code 安装
git clone https://github.com/anthropics/skills
cp -r skills/* ~/.claude/skills/

# 调用 (自动加载)
"用 PDF skill 提取这个 PDF 的所有表单字段"

# 创建 Skill
"用 skill-creator 帮我做一个 xxx skill"
```

### 我的判断

> Skills 是 2025-2026 年最重要的 Agent 范式转变之一——把"调教 prompt"升级成"沉淀可复用能力"。
> Anthropic 用 33 页官方指南 + 主仓库示范 + 全平台同步推进，节奏非常明确。
> 当前定位：**接入**——agent-memory 的 profile 已记录此方向；Mavis 等 agent 平台应考虑用 Skill 形式组织能力包。

### 参考

- 官方仓库 README：https://github.com/anthropics/skills
- Anthropic 工程博客（设计哲学）：https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- 33 页构建指南 PDF（强烈推荐读）：The Complete Guide to Building Skill for Claude
- 行业研报：华福证券《Claude Skills — AI Agent 的 C 端新标杆》（2026-01）

---

## agentskills.io（开放标准）

- **链接**：https://agentskills.io
- **类型**：开放标准 / 跨平台协议
- **首次发布**：2025-12-18
- **入库时间**：2026-06-21
- **状态**：🟡 观望（标准刚发布 6 个月，生态在形成）

### 一句话定位

Anthropic 把 Claude Skills 规范发布为跨平台开放标准，让其他 Agent 也能用同一种格式分发技能。

### 为什么值得

1. **去 Anthropic 中心化**：VSCode、GitHub 已采纳；Cursor、Goose、Amp 等编程 Agent 跟进
2. **互操作**：未来 Skill 写一次，跨 Claude/GPT/Gemini/Cursor 都能跑
3. **生态萌芽**：早期事实标准制定者的关键时点

### 我的判断

> 类似 MCP 的演化路径（Anthropic 提出 → 跨厂商采纳 → 事实标准）。值得观察 6-12 个月。
> 当前定位：**观察**——等 Cursor/Codex 真正支持后考虑给 Mavis agent 平台接入。

---

## OpenSkills（通用安装器）

- **链接**：https://github.com/numman-ali/openskills
- **作者**：numman-ali
- **类型**：通用安装器 / 跨 Agent 兼容层
- **主语言**：TypeScript
- **Stars**：~7.2k
- **入库时间**：2026-06-21
- **状态**：🟢 活跃

### 一句话定位

让任何能读 AGENTS.md 的 AI Agent 都能用 Claude Skills——通过在 AGENTS.md 中注入 `<available_skills>` XML 并提供 `npx openskills read` 命令。

### 为什么值得

1. **打通生态**：Claude Skills 原本只服务 Claude Code；OpenSkills 让 Cursor/Cline/Aider 等也能用同一套 Skill 仓库
2. **零依赖**：不依赖 Claude Code 本身，纯 CLI
3. **社区驱动**：作为"SKILL.md 的通用安装器"，未来可能成为所有 Agent 平台的中间层

### 关键命令

```sh
npm i -g openskills
npx openskills install anthropics/skills
npx openskills sync  # 写入 AGENTS.md 的 <available_skills>
npx openskills read <skill-name>  # Agent 调用时使用
```

### 适用

- 想在非 Claude Code Agent 里用 Claude Skills 的团队
- 多 Agent 平台统一管理 Skill 资产

### 我的判断

> 跟 agentskills.io 标准形成互补（标准 + 安装器）。Cursor 用户首选 OpenSkills。
> 当前定位：**试用**——如果未来 Mavis agent 要支持任意 Agent 平台，OpenSkills 是参考实现。