# pi 学习计划与进度

## 目标

用 4 周时间理解 pi 的核心架构，然后基于 pi SDK 构建一个 XML Agent：读取组内项目文档和代码，生成符合 XSD 和组内规则的 XML，并记录关键字段的来源。

## 当前进度

- 当前阶段：第 1 周
- 当前天数：第 1 天
- 最近完成：
- 下一步：
- 阻塞问题：

## 每日节奏（2 小时）

- 30 分钟：阅读文档
- 60 分钟：阅读代码或做实验
- 20 分钟：写笔记或画流程图
- 10 分钟：总结问题和下一步

## 第 1 周：使用 pi 并理解基本原理

- [ ] 第 1 天：运行 `./pi-test.sh`，阅读 [quickstart.md](../packages/coding-agent/docs/quickstart.md) 和 [usage.md](../packages/coding-agent/docs/usage.md)。产出：说明 pi 能做什么。
- [ ] 第 2 天：阅读 [how-pi-works.md](../packages/coding-agent/docs/how-pi-works.md)。产出：画出“用户输入 -> LLM -> 工具 -> 结果”流程。
- [ ] 第 3 天：阅读 [pi-ai README](../packages/ai/README.md) 的 streaming、tools 和 faux provider 部分。产出：解释 tool call 和 tool result。
- [ ] 第 4 天：阅读 [agent README](../packages/agent/README.md) 的 Core Concepts 和 Event Flow。产出：列出一次执行产生的事件。
- [ ] 第 5 天：阅读 [agent-loop.ts](../packages/agent/src/agent-loop.ts)。产出：标出 agent 继续或停止的判断位置。
- [ ] 第 6 天：运行 [01-minimal.ts](../packages/coding-agent/examples/sdk/01-minimal.ts) 和 [05-tools.ts](../packages/coding-agent/examples/sdk/05-tools.ts)。产出：跑通只读 agent。
- [ ] 第 7 天：复习第 1 周。产出：一页架构图。

## 第 2 周：理解 coding-agent 的组合方式

- [ ] 第 8 天：阅读 [main.ts](../packages/coding-agent/src/main.ts) 的启动流程。产出：记录 CLI 启动时创建的对象。
- [ ] 第 9 天：阅读 [sdk.md](../packages/coding-agent/docs/sdk.md) 和 SDK 示例 11、12。产出：说明如何控制模型、工具和 session。
- [ ] 第 10 天：阅读 [sessions.md](../packages/coding-agent/docs/sessions.md) 和 [compaction.md](../packages/coding-agent/docs/compaction.md)。产出：说明长上下文如何保存和压缩。
- [ ] 第 11 天：阅读 [skills.md](../packages/coding-agent/docs/skills.md) 和 [prompt-templates.md](../packages/coding-agent/docs/prompt-templates.md)。产出：设计 XML 规则 skill。
- [ ] 第 12 天：阅读 [extensions.md](../packages/coding-agent/docs/extensions.md)。产出：说明如何注册工具、事件和命令。
- [ ] 第 13 天：阅读 [hello.ts](../packages/coding-agent/examples/extensions/hello.ts)、[tools.ts](../packages/coding-agent/examples/extensions/tools.ts)、[protected-paths.ts](../packages/coding-agent/examples/extensions/protected-paths.ts) 和 [structured-output.ts](../packages/coding-agent/examples/extensions/structured-output.ts)。产出：写一个最小自定义工具。
- [ ] 第 14 天：复习第 2 周。产出：确定 XML Agent 允许和禁止的工具。

## 第 3 周：构建 XML Agent 原型

- [ ] 第 15 天：收集 5 到 10 个真实需求和正确 XML，整理 XSD 和组内规则。产出：测试数据集。
- [ ] 第 16 天：实现 `validate_xml`。产出：返回错误位置和原因。
- [ ] 第 17 天：实现 `submit_xml`。产出：未通过校验的 XML 不能提交。
- [ ] 第 18 天：编写 system prompt 或 skill。产出：固定生成流程和输出规则。
- [ ] 第 19 天：用 SDK 组合只读工具和自定义工具。产出：第一个端到端例子。
- [ ] 第 20 天：用 faux provider 编写确定性测试。产出：不调用真实模型也能测试流程。
- [ ] 第 21 天：用真实案例评估。产出：失败类型记录。

## 第 4 周：提高可靠性

- [ ] 第 22 天：优化文档和代码检索。产出：稳定找到相关资料。
- [ ] 第 23 天：加入字段来源追踪。产出：关键字段附带文件和行号。
- [ ] 第 24 天：加入修复循环和最大重试次数。产出：可控的自动修复。
- [ ] 第 25 天：实现只读、目录白名单和敏感信息过滤。产出：基础安全策略。
- [ ] 第 26 天：制作 CLI 或简单 UI。产出：组员可试用版本。
- [ ] 第 27 天：统计 XSD 通过率、规则通过率和人工修改量。产出：评估报告。
- [ ] 第 28 天：复盘。产出：决定继续使用 pi SDK，或改用 `pi-agent-core`。

## XML Agent 设计约束

- 只开放 `read`、`grep`、`find` 和 `ls` 等只读工具。
- 使用确定性的 `validate_xml` 检查 XML 格式、XSD 和组内规则。
- 使用 `submit_xml` 提交最终结果；只有校验通过后才写入输出文件。
- 为每个关键 XML 字段记录来源文件和行号。
- 设置最大修复次数，避免无限重试。

## 学习日志

| 日期 | 天数 | 完成内容 | 问题 | 下一步 |
|---|---:|---|---|---|
| | | | | |
