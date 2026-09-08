# Pragmatic Agent Engineering

[English](./README.md) | [简体中文](./README.zh-CN.md) | [中文完整版](./README.full.zh-CN.md)
## 面向 AI Coding Agent 的务实软件工程规范

## 1. 背景

AI Coding Agent 正在把“写代码”的边际成本快速压低，但软件工程真正昂贵的部分并没有消失：理解、Review、测试、排障、迁移、运维和长期维护仍然由人类承担。

因此出现了一类很典型的新问题：Agent 能够非常快速地把一个局部问题解决得越来越严密，却不天然擅长判断“这个问题是否值得解决到这个程度”。

```text
代码生成成本 ↓↓↓

架构复杂度 ↑↑

长期维护成本 ↑↑↑
```

项目要解决的不是“AI 写太多代码”，而是：

> **如何让 AI 具备与编码能力相匹配的工程克制。**

## 2. Minimum Sufficient Complexity

本项目的核心不是简单的 KISS。

如果业务需要事务、安全隔离、强数据完整性或明确高可靠性，那么这些复杂度就是必要的。

真正的目标是：

> **满足现实约束的最低充分复杂度。**

可以粗略理解为：

```text
必要工程复杂度
≈
真实业务需求
+ 正确性
+ 安全/数据完整性
+ 与失败成本匹配的可靠性
+ 与现实规模匹配的性能
```

而不是：

```text
所有理论风险
+ 所有未来扩展
+ 所有最佳实践
+ 所有可能的治理机制
```

## 3. 为什么“Keep It Simple”不够

如果只告诉 Agent：

> Keep it simple.

Agent 很容易回答：

> “这个复杂方案虽然代码更多，但为了可靠性、并发安全和未来扩展是必要的。”

因此项目采用更强的约束：

> **Complexity Requires Evidence —— 复杂性承担举证责任。**

理论可能、极端场景、最佳实践、企业级、未来扩展，都只能是讨论线索，不能单独构成复杂设计的充分理由。

## 4. 事实、假设与第一性原理

Agent 必须区分：

- Confirmed Fact；
- Logical Deduction；
- Assumption；
- Speculation。

第一性原理用于摆脱历史实现和框架惯性，但不能被滥用为“所有成熟方案都重新发明一次”。

成熟、简单、可靠的现成方案能解决问题时，应优先复用。

## 5. 需求纪律

典型失控过程：

```text
需求：增加 CSV 导出
↓
未来可能 Excel
↓
未来可能 PDF
↓
未来可能定时导出
↓
Universal Export Engine
```

这不是扩展性，而是未经授权的 Scope Expansion。

因此 Core Policy 明确要求：

> **Do not silently enlarge the problem.**

同时也避免另一极端——Clarification Paralysis。只有会实质改变业务行为、架构、安全、数据、公共契约或不可逆结果的歧义，才应该阻塞并询问。

## 6. 风险驱动流程

流程本身也有成本，因此不能所有任务都走完整审批。

### Low Risk

```text
理解 → 实现 → 验证 → 交付
```

### Medium Risk

```text
理解 → 简要设计 → 实现 → 验证 → Complexity Check → 交付
```

### High Risk

```text
分析 → 推荐方案 → 风险/迁移 → 确认
→ 实现 → 完整验证 → Complexity/Deletion Review → 交付
```

这同时避免 Agent 太激进和太保守。

## 7. Fix-by-Adding-Layers

项目重点反对一种常见演化：

```text
问题 A
→ 增加机制 B
→ B 引入问题 C
→ 增加机制 D
→ D 与 B 需要协调
→ 增加 E
```

当一个机制需要其他机制不断保护时，应重新检查原模型、invariant、状态和边界，而不是默认继续加层。

## 8. Boundaries Over Layers

清晰架构意味着：

- 谁负责什么；
- 谁拥有数据；
- 数据如何流动；
- 谁依赖谁；
- 副作用在哪里。

并不意味着 Controller/Application/Domain/Factory/Adapter/Strategy 越多越好。

少量重复通常比错误抽象便宜。

## 9. Security & Data Integrity

反过度设计不能演化为“反安全”。

认证、授权、隔离、最小权限、敏感数据、不可信输入边界和核心数据完整性属于 Hard Constraints。

可以简化安全实现，但不能简化掉安全保证。

## 10. Reliability Appropriate to Risk

可靠性不是越高越好，而是与失败影响匹配。

可以使用下面的思维模型：

```text
Reliability Investment
≈
Failure Impact
× Irrecoverability
× Real Scale
× Hard Constraints
```

一年一次、低影响、十分钟即可人工恢复的问题，不一定值得建设常驻自动补偿平台。

## 11. Tests Protect Contracts

测试应该保护：

- 业务 invariant；
- 核心行为；
- 安全边界；
- 数据正确性；
- 外部契约；
- 重要失败行为。

而不是保护历史实现细节。

```text
测试全部通过
≠
架构合理
```

## 12. Deletion Review

传统 Review 常问：

> 还有什么没有考虑？

它天然推动“加法”。

本项目同时要求问：

> **现在有什么可以删除？**

删除状态、配置、workaround、兼容层、无价值抽象、无意义测试和多余依赖，都属于工程成果。

## 13. Complexity Warning Signs

出现两个以上信号，应暂停继续增加机制：

1. 业务能力几乎没增加，但状态/配置/治理快速增长；
2. 新机制需要其他机制保护；
3. 同一事实出现多个独立来源或同步状态；
4. 普通工程师无法清楚解释主流程。

## 14. 为什么采用 Playbook

Core 只负责“如何做工程判断”。

领域细节，例如：

- SQL Migration；
- Retry/Idempotency；
- Backpressure；
- 系统化 Debugging；
- 兼容层与 canonical model；
- Agent/Skill/Workflow/SSOT 边界；
- 前端状态；
- 安全输入边界；

全部下沉到 Playbook。

这样一个只修改按钮文案的 Agent 不需要加载分布式一致性规则。

原则是：

> **Minimum Sufficient Context。**

## 15. SSOT 设计

本仓库中：

> **`AGENTS.md` 是唯一 Core Engineering Policy 的 SSOT。**

README 负责介绍，Docs 负责解释，Playbook 负责领域规则，Examples 负责证据，Adapters 负责接入。

任何其他文件都不得重新定义一套平行 Core Rules。

这条规则本身就是项目对“多事实源”和治理漂移问题的实践。

## 16. 项目不反对复杂技术

本项目不反对：

- 分布式系统；
- 状态机；
- 缓存；
- CQRS；
- Event Sourcing；
- 强一致性；
- Workflow；
- 高可靠架构。

它反对的是：

> **没有足够现实证据时使用这些复杂度。**

复杂技术本身不是问题；复杂度与问题规模不匹配才是问题。

## 17. 治理也必须付租金

本项目本身也可能过度设计。

因此不要持续增加：

- 规则；
- Checklist；
- Gate；
- 评分系统；
- 强制流程。

新增 Core Rule 前必须证明：现有 Core + Playbook 无法合理覆盖一个真实、重复出现的问题。

## 18. Canonical Policy

完整执行规则请直接阅读：

[`AGENTS.md`](./AGENTS.md)

不要从本解释文档反向构造另一套规则。

## 19. 最终信条

> Understand before implementing.

> Correctness before cleverness.

> Facts before assumptions.

> Use minimum sufficient complexity.

> Complexity requires evidence.

> Fix causes before adding layers.

> Boundaries matter more than layers.

> Tests protect contracts, not accidental complexity.

> Measure before optimizing.

> Prefer reversible decisions under uncertainty.

> Deleting code is engineering.

> Stop when the problem is solved.

最终问题：

> **我们是否以与真实风险和业务价值相匹配的工程复杂度，可靠地解决了真实问题？**
