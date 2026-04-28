# test-driven-development 技能分析

## 1. 技能定位

`test-driven-development` 是 Superpowers 中最刚性的实现纪律技能。它要求任何生产代码之前必须先有失败测试，并且必须亲眼看到测试因为预期原因失败。

它的目标不是提高测试覆盖率这么简单，而是约束代理按“需求 -> 测试 -> 实现”的顺序思考，避免先写实现再补看似通过的测试。

## 2. 触发条件

frontmatter 触发条件是：实现任何功能或 bugfix 前使用。

源码进一步扩展为：

- 新功能
- bug 修复
- 重构
- 行为变化

例外情况包括临时原型、生成代码和配置文件，但要求先询问用户。

## 3. 核心铁律

```text
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
```

如果已经先写了生产代码，技能要求删除并从测试重新开始。它明确禁止把已有代码当参考、边写测试边改造，或用“测试后补也一样”做合理化。

## 4. 执行流程

```text
选择一个行为
  |
  v
RED：写一个最小失败测试
  |
  v
运行测试，确认失败
  |
  |-- 测试通过 -> 测试没有覆盖新行为，改测试
  |-- 测试报错 -> 修测试，直到正确失败
  |
  v
GREEN：写最小生产代码
  |
  v
运行测试，确认通过
  |
  |-- 当前测试失败 -> 修代码，不改测试
  |-- 其他测试失败 -> 立刻修复
  |
  v
REFACTOR：只在全绿后清理
  |
  v
保持测试全绿
  |
  v
进入下一个行为
```

## 5. 好测试标准

| 标准 | 说明 |
|---|---|
| 最小 | 一个测试只覆盖一个行为 |
| 清晰 | 测试名说明行为，而不是 `test1` 这类占位 |
| 表达意图 | 测试展示期望 API 和行为 |
| 测真实代码 | 避免只验证 mock 行为 |

## 6. 设计取舍

### 强制删除先写代码

这是该技能最强硬的地方。它认为先写代码再补测试会让测试被实现污染，无法证明测试真的能捕获问题。

### 测试失败原因必须正确

仅仅“红”不够，必须确认失败是因为功能缺失，而不是拼写错误、测试配置错误或环境问题。

### 最小实现优先

GREEN 阶段只写刚好通过测试的代码，不允许顺手加配置项、扩展点或“以后可能用到”的能力。

### bug 修复也纳入 TDD

调试修复最后必须写能复现 bug 的失败测试，再实施修复，形成回归保护。

## 7. 风险点

| 风险 | 说明 |
|---|---|
| 对遗留项目不友好 | 既有代码无测试时，写首个测试可能成本高 |
| 探索性工作需要丢弃 | 允许探索，但探索代码不能保留为实现 |
| 过度刚性 | 某些配置、生成代码场景需要用户确认例外 |
| 测试质量依赖强 | 如果测试只测 mock 或实现细节，TDD 纪律会失效 |

## 8. 源码证据

| 结论 | 文件 |
|---|---|
| 实现前触发 | `superpowers/skills/test-driven-development/SKILL.md` frontmatter |
| 铁律是不允许无失败测试的生产代码 | `superpowers/skills/test-driven-development/SKILL.md` 的 `The Iron Law` |
| RED-GREEN-REFACTOR 是核心流程 | `superpowers/skills/test-driven-development/SKILL.md` 的 `Red-Green-Refactor` |
| 失败原因必须正确 | `superpowers/skills/test-driven-development/SKILL.md` 的 `Verify RED` |
| 通过后才能重构 | `superpowers/skills/test-driven-development/SKILL.md` 的 `REFACTOR` |
| bug 修复必须先写失败测试 | `superpowers/skills/test-driven-development/SKILL.md` 的 `Debugging Integration` |
