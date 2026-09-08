# Pragmatic Agent Engineering

[English](./README.md) | [简体中文](./README.zh-CN.md) | [中文完整版](./README.full.zh-CN.md)

> **AI 写代码很便宜，人类维护复杂度依然昂贵。**

Pragmatic Agent Engineering 是一套面向 **AI Coding Agent** 的通用软件工程原则、风险驱动工作流与按需领域 Playbook。

它关注的不是“如何让 AI 写更多代码”，而是：

> **如何让 AI 用与真实风险和业务价值相匹配的复杂度，可靠地解决真实问题。**

项目不绑定具体模型、IDE、编程语言或技术栈。

## 为什么需要它？

AI 大幅降低了代码生成成本，却没有同步降低以下成本：

- 理解复杂代码；
- Review 架构；
- 排查生产故障；
- 维护状态机和兼容层；
- 数据迁移与恢复；
- 团队交接和长期演进。

因此，Coding Agent 很容易形成一种新的工程失衡：

```text
边缘问题
→ 增加 fallback
→ 增加 watchdog
→ 增加状态/版本
→ 增加补偿/对账
→ 增加更多测试保护这些机制
```

每一步都可能“技术上合理”，但整体已经偏离真实业务。

## 核心思想：Minimum Sufficient Complexity

我们不追求“最简单的软件”，也不追求“最完整、最企业级的架构”。

我们追求：

> **在满足正确性、安全、数据完整性、明确可靠性和现实性能要求的前提下，选择最低充分复杂度。**

必要的复杂度应该保留；没有现实证据的复杂度应该承担举证责任。

## 主要原则

- Correctness before cleverness
- Facts before assumptions
- Solve the real requirement
- Complexity requires evidence
- Fix causes before adding layers
- Boundaries matter more than layers
- Design for known change
- Security and data integrity are hard constraints
- Tests protect contracts, not accidental complexity
- Measure before optimizing
- Prefer reversible decisions under uncertainty
- Deleting code is engineering
- Stop when the problem is solved

完整可执行规则见 [`AGENTS.md`](./AGENTS.md)。

## 风险驱动工作流

### Low Risk

```text
理解 → 实现 → 验证 → 交付
```

适用于局部、可逆、易验证且不改变关键契约的修改。

### Medium Risk

```text
理解 → 简要设计 → 实现 → 验证 → Complexity Check → 交付
```

适用于跨模块、有明显设计选择但仍容易回滚的修改。

### High Risk

```text
分析 → 推荐方案 → 风险/迁移分析 → 确认
→ 实现 → 完整验证 → Complexity / Deletion Review → 交付
```

适用于不可逆、数据破坏、安全边界、Breaking Change、核心架构替换和高影响基础设施变更。

## Playbooks

核心规则保持稳定，领域知识按需加载：

- [`security.md`](./playbooks/security.md)
- [`backend.md`](./playbooks/backend.md)
- [`frontend.md`](./playbooks/frontend.md)
- [`database.md`](./playbooks/database.md)
- [`reliability.md`](./playbooks/reliability.md)
- [`distributed-systems.md`](./playbooks/distributed-systems.md)
- [`data-engineering.md`](./playbooks/data-engineering.md)
- [`debugging.md`](./playbooks/debugging.md)
- [`compatibility.md`](./playbooks/compatibility.md)
- [`agent-systems.md`](./playbooks/agent-systems.md)
- [`testing.md`](./playbooks/testing.md)

原则是：

> **Minimum Sufficient Context —— 当前任务需要什么，就加载什么。**

## 案例

首批案例位于 [`examples/overengineering/`](./examples/overengineering/)：

1. 通知中心：可靠性治理如何超过业务问题本身；
2. 数据管道：为什么“全链路 exactly once”可能是错误目标；
3. 前端状态：普通管理后台如何被设计成协同编辑器级状态系统。

案例关注的不是“复杂技术不好”，而是：

> **复杂度从什么时候开始不再值得它的长期成本。**

## 仓库结构

```text
pragmatic-agent-engineering/
├── README.md
├── README.zh-CN.md
├── README.full.zh-CN.md
├── AGENTS.md               # 唯一 Core SSOT
├── CONTRIBUTING.md
├── LICENSE
│
├── playbooks/
├── docs/
├── examples/
└── adapters/
```

`AGENTS.md` 是唯一核心规则源。README、Docs 和 Examples 可以解释和示范，但不得重新定义一套 Core Rules。

## 这不是什么？

本项目不是：

- “最佳实践大全”；
- 强制 ADR / Checklist 流程；
- 架构评分系统；
- 设计模式集合；
- 要求 AI 每次改一行代码都先审批的治理框架。

如果项目最终变成“几百条规则 + 数十个 Gate + 治理的治理”，它就违背了自己的核心理念。

## 贡献

欢迎贡献：

- 真实 AI 过度设计案例；
- 简化重构案例；
- Playbook 改进；
- 各 Coding Agent 的轻量适配；
- 删除重复规则的提案。

贡献新核心规则前，请先回答：

1. 它解决什么重复出现的真实问题？
2. 有什么证据？
3. 为什么现有规则无法覆盖？
4. 新规则增加了多少认知和执行成本？

详见 [`CONTRIBUTING.md`](./CONTRIBUTING.md)。

## License

MIT License。详见 [`LICENSE`](./LICENSE)。

---

> **AI can generate code cheaply. Humans still pay for complexity.**

最终判断标准：

> **我们是否以与真实风险和业务价值相匹配的工程复杂度，可靠地解决了真实问题？**
