# AI 编程语言 / DSL

> Agent 用的编程语言、领域特定语言、图编程语言等。

---

## zerolang

- **链接**：https://github.com/vercel-labs/zerolang
- **首页**：https://zerolang.ai
- **作者**：vercel-labs
- **类型**：编程语言 / Agent 编程 / 图编程
- **主语言**：C
- **协议**：Apache-2.0
- **Stars**：5099 · **Forks**：335
- **入库时间**：2026-06-18
- **状态**：🟢 活跃（v0.x 实验性，作者明确警告 breaking changes）

### 一句话定位

The Programming Language for Agents — 把"程序 = 文本"换成"程序 = 语义图"，agent 操作图而不是文本。

### 为什么值得

1. **思路翻转**：传统 agent 写代码是 "agent 写 text → check → format → build → inspect → 改"，zerolang 把回路搬到 agent 直接和编译器交互（"agent query graph → submit checked patch → compiler accept → run"），agent 更接近编译器。
2. **`.0` 文件是图的投影**：源码仍可读可审，但底层是 `zero.graph`（程序数据库），文本只是视图。改图用 `zero patch --op ...`，query 用 `zero query`。
3. **图原生 + 可证**：每次 patch 经过 typecheck、scope check、permission check；agent 想绕过编译器直接改 text 走不通。设计目标就是"agent 写出能被 verify 的代码"。
4. **vercel 背书 + Apache-2.0**：实验性（v0.x），但有真团队在做，不是 PoC。

### 适用场景（推测）

- Agent 需要在大量代码库上做小幅、验证性改动（修 bug、加 feature、refactor）
- 想让 agent 操作更"接近编译器"而不是"碰字符串"
- 对"agent 改坏代码"有强安全需求

### 不适用

- 通用业务代码（生产系统还是用 TS/Python/Go）
- 学习新语言的项目（C 写的虚拟机 + 图存储 + DSL 不是入门级）

### 关键命令

```sh
zero init
zero patch --op 'addMain' --op 'addCheckWrite fn="main" text="hello from zero\n"'
zero run
```

### 我的判断

> 思路有意思，但"agent 写代码 = 操作图"是否真比"agent 写代码 = 操作文本"更安全有效，要等真有人跑通大规模改造案例才知道。
> 当前定位：**观察**——记下思路，等生态（IDE、agent 集成、benchmark）起来再深入。

### 参考

- 官方仓库 README（含架构图）：https://github.com/vercel-labs/zerolang
- 官网：https://zerolang.ai