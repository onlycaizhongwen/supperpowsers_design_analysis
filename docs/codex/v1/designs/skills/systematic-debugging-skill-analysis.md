# systematic-debugging 技能分析

## 1. 技能定位

`systematic-debugging` 是 Superpowers 的故障排查纪律技能。它用于 bug、测试失败、异常行为、构建失败、性能问题等技术问题，核心目标是阻止代理猜修复。

它和 `test-driven-development` 的关系是：先通过系统化调试找到根因，再用 TDD 写失败测试并修复。

## 2. 触发条件

frontmatter 触发条件是：遇到任何 bug、测试失败或异常行为，在提出修复前使用。

源码中进一步说明，它适用于：

- 测试失败
- 生产 bug
- 异常行为
- 性能问题
- 构建失败
- 集成问题

尤其在“看起来有明显快速修复”“已经试过多个修复”“压力很大”时更不能跳过。

## 3. 核心铁律

```text
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

如果还没完成 Phase 1，就不能提出修复方案。这个规则专门对抗代理最常见的问题：看到症状后直接改代码。

## 4. 四阶段流程

```text
出现 bug / 失败 / 异常
  |
  v
Phase 1：根因调查
  - 读完整错误
  - 稳定复现
  - 检查近期变化
  - 多组件边界加诊断
  - 追踪数据流
  |
  v
Phase 2：模式分析
  - 找工作样例
  - 完整阅读参考实现
  - 对比差异
  - 理解依赖和假设
  |
  v
Phase 3：假设与验证
  - 写下单一假设
  - 做最小实验
  - 成功则进入修复
  - 失败则形成新假设
  |
  v
Phase 4：实施修复
  - 写失败测试
  - 做单一根因修复
  - 验证修复和回归
  - 失败则回到调查
```

如果连续 3 次修复失败，流程要求停止并质疑架构，而不是继续尝试第 4 个补丁。

## 5. 关键机制

### 多组件证据采集

当系统跨 CI、构建、签名、API、服务、数据库等多个组件时，技能要求先在组件边界加诊断，确认数据在哪一层断掉。

### 数据流回溯

当错误出现在深层调用栈时，要求从坏值出现的位置往上追踪，直到找到最初引入坏值的源头。

### 单一假设原则

每次只验证一个假设，只做最小变更。多个修复一起上会导致无法判断到底哪个因素有效。

### 架构质疑门槛

3 次以上修复失败，被视为可能的架构问题信号，需要和用户讨论基础模式是否错误。

## 6. 上下游关系

上游：

- `using-superpowers` 在 bug、失败测试、异常行为时触发它。

下游：

- Phase 4 中调用 `test-driven-development` 写失败测试和修复。
- 完成后使用 `verification-before-completion` 证明修复有效。

相关参考：

- `root-cause-tracing.md`
- `defense-in-depth.md`
- `condition-based-waiting.md`

## 7. 风险点

| 风险 | 说明 |
|---|---|
| 初始速度看似慢 | 相比直接改代码，前期调查更多 |
| 需要复现和证据 | 不稳定问题可能需要额外日志或观察 |
| 对经验主义有冲突 | “我知道大概是哪”不能替代根因证据 |
| 可能暴露架构问题 | 3 次失败后会推动讨论架构，而不是继续局部修 |

## 8. 源码证据

| 结论 | 文件 |
|---|---|
| bug/失败/异常前触发 | `superpowers/skills/systematic-debugging/SKILL.md` frontmatter |
| 铁律是先根因调查后修复 | `superpowers/skills/systematic-debugging/SKILL.md` 的 `The Iron Law` |
| 四阶段流程定义完整排查路径 | `superpowers/skills/systematic-debugging/SKILL.md` 的 `The Four Phases` |
| 多组件系统先加诊断 | `superpowers/skills/systematic-debugging/SKILL.md` 的 `Gather Evidence in Multi-Component Systems` |
| 深层错误要追数据流 | `superpowers/skills/systematic-debugging/SKILL.md` 的 `Trace Data Flow` |
| 修复阶段要求失败测试 | `superpowers/skills/systematic-debugging/SKILL.md` 的 `Phase 4: Implementation` |
| 3 次失败后质疑架构 | `superpowers/skills/systematic-debugging/SKILL.md` 的 `If 3+ Fixes Failed` |
