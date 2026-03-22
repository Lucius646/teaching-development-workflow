---
name: teaching-development-workflow
description: Use when a user is new to software development and wants to learn through superpowers-style workflows by keeping a self-contained teaching journal that explains phases, commands, files, decisions, results, blockers, and next steps without requiring the user to read the spec or plan first.
---

# Teaching Development Workflow

## 概述

把这个 skill 当作 superpowers 工作流之上的教学层来使用。保持原始工作流不变，同时写出一份自包含的学习日志，解释当前发生了什么、为什么重要，以及用户下一步应该理解什么。

**核心原则：** 讲清工作流，而不是替代工作流。

## 硬边界

- 不要替代 `superpowers:brainstorming`、`superpowers:writing-plans`、`superpowers:test-driven-development`、`superpowers:systematic-debugging` 或其他主工作流 skill。
- 不要为了让日志更好看就发明额外的工程阶段，或打乱现有工作流顺序。
- 不要假设用户会去读 `spec` 或 `plan`。日志里要总结足够上下文，保证它可以独立成立。
- 不要把日志写成审计记录或命令转录。
- 不要记录每一次按键、每一个琐碎改动，或任何没有新增信息的重复命令。
- 不要让 subagent 直接写主日志。由主代理统一整合后写入最终条目。

## 日志目标

把所有教学记录写入 `docs/superpowers/global-dev-journal.md`。

- 如果文件不存在，就创建它。
- 只允许追加，不要改写更早的内容。
- 每出现一个有教学价值的节点，就新增一条 entry。

## 何时写入

在以下任一情况发生时，写入一条 journal entry：

- 一个 superpowers 阶段开始。
- 一个重要的技术决策或流程决策被做出。
- 一个重要的验证动作完成。
- 出现阻塞、回归、错误假设或返工循环。
- 一个 superpowers 阶段结束。

## 什么算关键动作

当一个动作至少满足以下任意一条时，把它视为值得记录的关键动作：

- 改变了当前阶段的目标。
- 引入或消除了一个重要不确定性。
- 证实或证伪了一个假设。
- 改变了实现方向或调试方向。
- 产出了一个有意义的验证结果。
- 能让初学者学到一个无法仅靠原始命令推断出来的概念。

不要为纯格式修改、没有新增信号的重复命令、或不改变理解的小型机械修改单独写 entry。

## 阶段教学规则

用当前 superpowers 阶段来组织解释。当你需要某个阶段的教学目标时，阅读 `references/phase_explanations.md`。

- 在 `brainstorming` 期间，解释为什么设计要先于实现。
- 在 `writing-plans` 期间，解释为什么设计必须被拆成可执行步骤。
- 在 `executing-plans` 或 `subagent-driven development` 期间，解释计划内工作如何变成经过验证的改动。
- 在 `test-driven development` 期间，解释 `RED-GREEN-REFACTOR` 循环，以及为什么“证明”很重要。
- 在 `systematic debugging` 期间，解释为什么必须先找根因，再谈修复。
- 在验证与收尾阶段，解释为什么所有“完成”声明都必须有证据支撑。

## Entry 编写规则

严格遵循 `references/journal_format.md` 中的结构。

每一条 entry 都必须：

- 标明当前阶段。
- 解释当前问题是什么，以及为什么现在会进入这一步。
- 用面向初学者的语言总结有意义的命令和文件上下文。
- 记录改变理解或推进工作的决策与结果。
- 明确说明用户应该从这一步学到什么。
- 指出下一步最可能进入的动作或阶段。
- 在存在具体命令和文件路径时，必须写具体值；如果还不存在，就直说“尚未产生”，不要留下 `...` 这类占位符或模糊路径。

当 `spec` 或 `plan` 已存在时，优先总结相关内容，而不是先让用户自己去读原文。

## 常见错误

| 错误 | 修正方式 |
|--------|-----|
| 把每个命令都记下来 | 合并重复动作，只保留真正带来教学价值的命令 |
| 假设用户已经读过 `spec` 或 `plan` | 在 journal entry 里重新引入当前问题和阶段上下文 |
| 只写改了什么 | 补上为什么改，以及学习者应该注意什么 |
| 把日志写成纯事后总结 | 同时记录阶段开始、阻塞点和验证节点 |
| 让 subagent 直接写日志 | 先整合它们的结果，再由主代理写一条主 entry |

## 红旗信号

- “日志照着终端抄一遍就行。”
- “上下文让用户自己去看 spec 吧。”
- “这个命令太 obvious 了，不用解释。”
- “虽然没发生重要变化，但每个小动作都记一下吧。”
- “subagent 已经解释过了，我就不用再写了。”

如果你出现上述想法，停下来重写这条 entry，把目标从“原始完整性”切回“教学价值最大化”。
