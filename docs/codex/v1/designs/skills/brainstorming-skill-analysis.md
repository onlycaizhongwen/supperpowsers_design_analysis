# brainstorming 技能分析

## 1. 技能定位

`brainstorming` 是 Superpowers 的需求澄清和设计生成技能。它处理从“模糊想法”到“可评审设计”的前置阶段，核心目标是阻止代理直接写代码。

它的硬门槛是：未展示设计并获得用户确认前，不允许进入实现、脚手架或其他实施动作。

## 2. 触发条件

frontmatter 明确要求在任何创意工作前使用，包括：

- 创建功能
- 构建组件
- 添加功能
- 修改行为

它覆盖范围很广，甚至强调“简单任务也需要设计”。这说明 Superpowers 把“简单所以跳过设计”视为高风险反模式。

## 3. 内部阶段

| 阶段 | 作用 |
|---|---|
| 探索上下文 | 先读项目文件、文档和近期提交 |
| 视觉辅助判断 | 如果问题适合可视化，单独询问是否使用 visual companion |
| 澄清问题 | 一次只问一个问题，理解目标、约束和成功标准 |
| 方案比较 | 给出 2-3 个方案和取舍 |
| 分段确认设计 | 按复杂度展示设计，并逐段获得用户认可 |
| 写设计文档 | 保存到 `docs/superpowers/specs/...` |
| 自查设计 | 查占位符、矛盾、范围和歧义 |
| 用户复核 | 等用户确认 written spec |
| 转入计划 | 只允许进入 `writing-plans` |

## 4. 执行流程

```text
用户提出想法或功能请求
  |
  v
探索项目上下文
  |
  v
是否需要视觉辅助？
  |-- 是 -> 单独询问 visual companion -> 等用户答复
  |-- 否 -> 继续文本澄清
  |
  v
一次一个澄清问题
  |
  v
提出 2-3 个方案和推荐
  |
  v
分段展示设计
  |
  |-- 用户不认可 -> 修改设计并重新展示
  |
  |-- 用户认可
        |
        v
      写设计文档
        |
        v
      自查设计文档
        |
        v
      用户复核文档
        |
        |-- 要求修改 -> 回到文档修改
        |-- 认可 -> 进入 writing-plans
```

## 5. 设计关注点

### 先理解目的，再谈实现

技能要求先理解用户真正想达成什么，特别关注目的、约束和成功标准。这避免代理把一句话需求直接翻译成代码。

### 方案比较是必经步骤

`brainstorming` 不鼓励只有一个方案。它要求提出 2-3 个选项并说明取舍，这让用户能在设计层面参与选择。

### 设计按复杂度分段确认

复杂设计不能一次性倾倒给用户。技能要求按 section 展示并确认，降低用户误读或漏审的概率。

### Visual companion 是工具，不是模式

即使用户同意视觉辅助，也不是所有问题都走浏览器。每个问题都要判断“看图是否比文字更清楚”。

## 6. 上下游关系

上游：

- `using-superpowers` 在创意或行为修改请求中触发它。

下游：

- 终点只能是 `writing-plans`，不能直接跳到实现技能。
- 视觉问题可进入 `skills/brainstorming/visual-companion.md` 和配套 server。

## 7. 风险点

| 风险 | 说明 |
|---|---|
| 对小任务显得重 | 简单任务也要求设计，可能增加交互成本 |
| 需要用户持续确认 | 用户不配合时流程会停在设计确认阶段 |
| 文档和提交要求较强 | 要写 spec 并 commit，适合正式开发，不适合临时问答 |
| 视觉辅助可能增加复杂度 | visual companion 需要浏览器和本地 server 支持 |

## 8. 源码证据

| 结论 | 文件 |
|---|---|
| 创意工作前必须使用 | `superpowers/skills/brainstorming/SKILL.md` frontmatter |
| 未确认设计前禁止实现 | `superpowers/skills/brainstorming/SKILL.md` 的 `<HARD-GATE>` |
| checklist 定义 9 个步骤 | `superpowers/skills/brainstorming/SKILL.md` 的 `Checklist` |
| 终点只能进入 `writing-plans` | `superpowers/skills/brainstorming/SKILL.md` 的 `Process Flow` 和 `Implementation` |
| 设计文档需要自查 | `superpowers/skills/brainstorming/SKILL.md` 的 `Spec Self-Review` |
| spec reviewer 模板检查完整性、一致性、清晰度、范围和 YAGNI | `superpowers/skills/brainstorming/spec-document-reviewer-prompt.md` |
