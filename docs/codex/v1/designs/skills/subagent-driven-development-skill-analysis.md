# subagent-driven-development 技能分析

## 1. 技能定位

`subagent-driven-development` 是 Superpowers 中最能体现“代理工程化执行”的技能。它不是简单地让多个代理并发写代码，而是把实施计划拆成任务后，为每个任务派发 fresh subagent，并在每个任务后做两阶段评审。

核心目标是：用隔离上下文、明确任务文本、TDD、自查和双评审，降低代理执行计划时偏离规格的风险。

## 2. 触发条件

frontmatter 触发条件是：当前会话中执行由独立任务组成的实施计划。

源码中的使用判断还包含三个决策点：

1. 是否已有实施计划。
2. 任务是否大体独立。
3. 是否留在当前会话执行。

如果没有计划，应回到手工执行或 brainstorming；如果任务耦合严重，不适合该流程；如果不是当前会话执行，则转向 `executing-plans`。

## 3. 内部角色

| 角色 | 来源 | 职责 |
|---|---|---|
| 控制器 | 当前主代理 | 读取计划、拆任务、准备上下文、派发子代理、处理状态 |
| 实现子代理 | `implementer-prompt.md` | 实现单个任务、写测试、提交、自查、报告状态 |
| 规格评审子代理 | `spec-reviewer-prompt.md` | 独立检查实现是否满足任务规格，查漏建多 |
| 代码质量评审子代理 | `code-quality-reviewer-prompt.md` | 在规格通过后检查质量、可维护性和风险 |
| 最终评审代理 | `requesting-code-review` 体系 | 全量实现完成后做整体评审 |

## 4. 执行流程

```text
读取实施计划
  |
  v
一次性提取所有任务全文和上下文
  |
  v
创建任务清单
  |
  v
对每个任务：
  |
  v
派发实现子代理
  |
  |-- 子代理提问 -> 控制器补上下文 -> 重新派发
  |
  |-- DONE / DONE_WITH_CONCERNS
        |
        v
      规格符合性评审
        |
        |-- 不通过 -> 同一实现子代理修正 -> 重新评审
        |
        |-- 通过
              |
              v
            代码质量评审
              |
              |-- 不通过 -> 同一实现子代理修正 -> 重新评审
              |
              |-- 通过 -> 标记任务完成
  |
  v
全部任务完成
  |
  v
最终代码评审
  |
  v
finishing-a-development-branch
```

## 5. 子代理状态机

| 状态 | 控制器处理 |
|---|---|
| `DONE` | 进入规格符合性评审 |
| `DONE_WITH_CONCERNS` | 先阅读 concerns，必要时处理后再评审 |
| `NEEDS_CONTEXT` | 补充信息并重新派发 |
| `BLOCKED` | 判断是上下文不足、模型能力不足、任务过大，还是计划错误 |

这个状态机很重要：它要求控制器把失败当作协作信号处理，而不是强迫同一个子代理硬做。

## 6. 关键设计取舍

### 每个任务 fresh subagent

优点是上下文干净，任务边界明确；缺点是每次都要提供完整任务文本和背景，控制器准备成本更高。

### 规格评审先于代码质量评审

这是最关键的质量门顺序。先确认“做的是不是要求的东西”，再评价“做得好不好”。如果顺序反了，可能会把一个错误方向的实现打磨得很漂亮。

### 计划文本由控制器提供

实现子代理不应自己读计划文件，而是由控制器粘贴完整任务文本。这减少了重复读文件，也避免子代理误读全局上下文。

### 不并行派发多个实现子代理

虽然名字包含 subagent，但该技能强调每个任务的串行闭环。并行实现容易产生文件冲突和规格漂移。

## 7. 风险点

| 风险 | 说明 |
|---|---|
| 调用成本高 | 每个任务至少涉及实现、规格评审、质量评审 |
| 控制器负担重 | 控制器必须准确提取计划、准备上下文、处理状态 |
| 计划质量依赖强 | 计划不清晰会导致子代理频繁 `NEEDS_CONTEXT` 或 `BLOCKED` |
| 任务耦合风险 | 多任务共享状态强时，该流程收益下降 |
| 评审循环可能变长 | 规格和质量双门都会产生回修循环 |

## 8. 源码证据

| 结论 | 文件 |
|---|---|
| 触发条件是执行独立任务计划 | `superpowers/skills/subagent-driven-development/SKILL.md` |
| 使用决策包含计划、独立性、当前会话 | `superpowers/skills/subagent-driven-development/SKILL.md` 的 `When to Use` |
| 每任务实现后有规格和质量两阶段评审 | `superpowers/skills/subagent-driven-development/SKILL.md` 的 `The Process` |
| 实现子代理状态包含四类 | `superpowers/skills/subagent-driven-development/SKILL.md` 的 `Handling Implementer Status` |
| 实现子代理模板要求实现、测试、提交、自查 | `superpowers/skills/subagent-driven-development/implementer-prompt.md` |
| 规格评审模板要求不信任实现报告，要读代码核对 | `superpowers/skills/subagent-driven-development/spec-reviewer-prompt.md` |
| 质量评审必须在规格通过后执行 | `superpowers/skills/subagent-driven-development/code-quality-reviewer-prompt.md` |
