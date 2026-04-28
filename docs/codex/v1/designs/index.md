# superpowers 分析文档入口

本文档是 `superpowers` 源码分析的阅读入口。

## 推荐阅读顺序

1. [总体架构与流程说明](superpowers-architecture-design.md)
2. [分支执行流程说明](superpowers-branch-flow-design.md)
3. [总体流程图 HTML 预览](assets/superpowers-flow.html)
4. [分支流程图 HTML 预览](assets/superpowers-branch-flows.html)

## 核心结论

| 结论 | 说明 | 源码证据 |
|---|---|---|
| `superpowers` 不是传统应用服务 | 它主要是跨编码代理平台分发的一组技能、hook、manifest 和文档 | `superpowers/skills/`、`superpowers/.codex-plugin/plugin.json`、`superpowers/.cursor-plugin/plugin.json` |
| `using-superpowers` 是入口纪律层 | 它要求代理在行动前检查并加载相关 skill | `superpowers/skills/using-superpowers/SKILL.md` |
| Claude 和 Cursor 通过 hook 注入启动上下文 | 会话启动时读取 `using-superpowers` 并输出额外上下文 | `superpowers/hooks/session-start`、`superpowers/hooks/hooks.json`、`superpowers/hooks/hooks-cursor.json` |
| Codex 通过插件清单暴露技能目录 | `.codex-plugin/plugin.json` 声明 `skills` 路径和插件展示信息 | `superpowers/.codex-plugin/plugin.json` |
| OpenCode 通过插件 JS 注册技能路径并注入 bootstrap | 插件修改运行时 config，并向首个用户消息注入引导内容 | `superpowers/.opencode/plugins/superpowers.js` |
| Gemini 通过 `GEMINI.md` 引用入口技能 | Gemini extension 使用上下文文件拉起 `using-superpowers` | `superpowers/GEMINI.md`、`superpowers/gemini-extension.json` |
| 标准开发主线是设计 -> 计划 -> 实现 -> 评审 -> 收尾 | README 和多个 skill 共同定义这条路径 | `superpowers/README.md`、`superpowers/skills/brainstorming/SKILL.md`、`superpowers/skills/writing-plans/SKILL.md` |
| 子代理执行有两道质量门 | 实现后先做规格符合性评审，再做代码质量评审 | `superpowers/skills/subagent-driven-development/SKILL.md` |
| 调试分支先找根因再修复 | `systematic-debugging` 要求先调查、分析、验证假设，再实施修复 | `superpowers/skills/systematic-debugging/SKILL.md` |
| 完成声明必须有证据 | `verification-before-completion` 要求先运行完整验证命令，再声明完成 | `superpowers/skills/verification-before-completion/SKILL.md` |
| 收尾分支由用户选择合并/PR/保留/丢弃 | `finishing-a-development-branch` 定义测试验证和四类收尾选项 | `superpowers/skills/finishing-a-development-branch/SKILL.md` |

## 图表文件

| 图表 | 文件 |
|---|---|
| 总流程图 | `assets/superpowers-flow.svg` |
| 平台接入分支 | `assets/superpowers-platform-branch-flow.svg` |
| 请求分流分支 | `assets/superpowers-request-routing-flow.svg` |
| 设计计划分支 | `assets/superpowers-design-plan-flow.svg` |
| 实现执行分支 | `assets/superpowers-implementation-branch-flow.svg` |
| 调试修复分支 | `assets/superpowers-debug-branch-flow.svg` |
| 评审收尾分支 | `assets/superpowers-finish-branch-flow.svg` |

## 维护提示

- 更新 `superpowers` submodule 后，应重新核对两份分析文档中的源码证据。
- 如果 Markdown 预览器不显示 SVG 图片，优先打开对应 HTML 预览页。
