# pi 学习计划与进度

## 目标

通过阅读 pi 的源码，理解设计一个 agent 需要考虑哪些问题，以及每个问题有哪些取舍。学完后，设计并实现一个 XML Agent：读取组内项目文档和代码，生成符合 XSD 和组内规则的 XML，并记录关键字段的来源。

## 当前进度

- 当前阶段：第 1 周
- 当前天数：第 1 天
- 最近完成：
- 下一步：
- 阻塞问题：

## 学习方法

每天围绕一个设计问题：

1. 这个设计问题是什么，不处理会出什么问题
2. pi 是怎么解决的（读源码）
3. 这个方案有哪些取舍，还有哪些替代方案
4. 我的 XML Agent 应该怎么做

每天产出一条设计决策记录，追加到本文件末尾的“设计决策记录”。

## 每日节奏（2 小时）

- 30 分钟：阅读文档，理解设计问题
- 60 分钟：追踪源码，必要时做小实验
- 20 分钟：写设计决策记录
- 10 分钟：总结问题和下一步

## 第 1 周：agent 的核心结构

- [ ] 第 1 天：agent 由哪些部分组成？阅读 [how-pi-works.md](../packages/coding-agent/docs/how-pi-works.md)，运行一次 `./pi-test.sh` 观察工具调用。产出：agent 组成图（模型、循环、工具、上下文、状态）。
- [ ] 第 2 天：如何屏蔽不同模型厂商的差异？阅读 [ai/types.ts](../packages/ai/src/types.ts) 和 [event-stream.ts](../packages/ai/src/utils/event-stream.ts)。产出：统一消息、流式事件和停止原因的设计说明；决定 XML Agent 是否需要支持多个模型。
- [ ] 第 3 天：agent 什么时候继续，什么时候停止？阅读 [agent-loop.ts](../packages/agent/src/agent-loop.ts)。产出：循环流程图和停止条件列表。
- [ ] 第 4 天：工具接口怎么设计？参数错误怎么处理？阅读 [agent/types.ts](../packages/agent/src/types.ts) 和 [validation.ts](../packages/ai/src/utils/validation.ts)。产出：工具接口设计原则。
- [ ] 第 5 天：工具输出太长怎么办？哪些工具有风险？阅读 [read.ts](../packages/agent/src/harness/tools/read.ts)、[truncate.ts](../packages/agent/src/harness/utils/truncate.ts) 和 [bash.ts](../packages/agent/src/harness/tools/bash.ts)。产出：XML Agent 的工具清单和每个工具的输出限制。
- [ ] 第 6 天：工具可以并行吗？怎么控制副作用？阅读 [file-mutation-queue.ts](../packages/agent/src/harness/tools/file-mutation-queue.ts) 和 [effect-gate.ts](../packages/agent/src/harness/execution/effect-gate.ts)。产出：并行与副作用控制策略。
- [ ] 第 7 天：复习第 1 周。产出：整理第 1 周的设计决策。

## 第 2 周：上下文、状态、可靠性和安全

- [ ] 第 8 天：每次请求应该给模型哪些上下文？阅读 [system-prompt.ts](../packages/agent/src/harness/system-prompt.ts) 和 [messages.ts](../packages/coding-agent/src/core/messages.ts)。产出：XML Agent 的上下文组成。
- [ ] 第 9 天：上下文超过模型限制时怎么办？阅读 [compaction.ts](../packages/agent/src/harness/compaction/compaction.ts) 和 [overflow.ts](../packages/ai/src/utils/overflow.ts)。产出：长文档和大仓库的上下文策略。
- [ ] 第 10 天：领域知识怎么按需提供给模型？阅读 [skills.ts](../packages/agent/src/harness/skills.ts)。产出：XML 规则知识的组织方式。
- [ ] 第 11 天：状态怎么保存、恢复和追溯？阅读 [session.ts](../packages/agent/src/harness/session/session.ts)。产出：XML Agent 是否需要 session，以及如何保存生成过程。
- [ ] 第 12 天：模型调用失败、中断或超时怎么办？阅读 [retry.ts](../packages/ai/src/utils/retry.ts)。产出：错误处理和重试策略。
- [ ] 第 13 天：agent 的权限边界在哪里？阅读 [security.md](../packages/coding-agent/docs/security.md) 和 [project-trust.ts](../packages/coding-agent/src/core/project-trust.ts)。产出：XML Agent 的权限和安全边界。
- [ ] 第 14 天：怎么扩展、观察和测试 agent？阅读 [extensions/types.ts](../packages/coding-agent/src/core/extensions/types.ts)、[telemetry.ts](../packages/agent/src/harness/telemetry.ts)、[faux.ts](../packages/ai/src/providers/faux.ts) 和 [test/suite/harness.ts](../packages/coding-agent/test/suite/harness.ts)。产出：扩展点、日志和测试方案。

## 第 3 周：设计 XML Agent（先不写代码）

- [ ] 第 15 天：明确需求、输入、输出和成功标准。产出：需求说明和 5 到 10 个测试样例。
- [ ] 第 16 天：设计文档和代码的检索方式。产出：检索策略。
- [ ] 第 17 天：定义 `validate_xml`、`submit_xml` 和来源引用的接口。产出：工具契约。
- [ ] 第 18 天：设计 system prompt 和规则知识的提供方式。产出：上下文设计。
- [ ] 第 19 天：设计修复循环、停止条件和人工审核点。产出：流程设计。
- [ ] 第 20 天：设计评估指标。产出：评估方案。
- [ ] 第 21 天：设计评审。产出：完整设计文档。

## 第 4 周：实现原型并验证设计

- [ ] 第 22 天：基于 pi SDK 搭建项目骨架，接入只读工具。
- [ ] 第 23 天：实现 `validate_xml`。
- [ ] 第 24 天：实现 `submit_xml` 和来源追踪。
- [ ] 第 25 天：实现修复循环和停止条件。
- [ ] 第 26 天：用 faux provider 编写确定性测试。
- [ ] 第 27 天：用真实案例评估。产出：评估报告。
- [ ] 第 28 天：复盘哪些设计决策正确，哪些需要调整。

## XML Agent 初步约束

- 只开放 `read`、`grep`、`find` 和 `ls` 等只读工具。
- 使用确定性的 `validate_xml` 检查 XML 格式、XSD 和组内规则。
- 使用 `submit_xml` 提交最终结果；只有校验通过后才写入输出文件。
- 为每个关键 XML 字段记录来源文件和行号。
- 设置最大修复次数，避免无限重试。

## 设计决策记录

每条记录使用以下格式：

```text
### 第 N 天：设计问题
- 问题：
- pi 的做法：
- 取舍和替代方案：
- XML Agent 的决定：
- 理由：
```

## 学习日志

| 日期 | 天数 | 完成内容 | 问题 | 下一步 |
|---|---:|---|---|---|
| | | | | |
