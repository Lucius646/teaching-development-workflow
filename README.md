# teaching-development-workflow

一个配合 superpowers 使用的导师型 skill。

它不替代 `brainstorming`、`writing-plans`、`test-driven-development`、`systematic-debugging` 等主工作流，而是在这些阶段旁路提供教学解释，并把关键过程整理成一份可持续追加的学习文档。

## 适用场景

当用户符合下面任一情况时，这个 skill 最有价值：

- 对软件开发几乎没有经验，需要被带着理解工程流程
- 希望在真实开发过程中学习，而不是只看抽象教程
- 希望把“为什么这样做”持续写入文档，便于回看
- 需要一份即使不先读 `spec` 或 `plan` 也能跟上的教学型日志

## 核心目标

这个 skill 的目标不是单纯“记日志”，而是把 superpowers 工作流翻译成适合初学者理解的过程文档。

它会强调这些信息：

- 当前处于哪个阶段
- 这个阶段在软件开发里是做什么的
- 为什么现在要做这一步
- 关键命令和文件分别起什么作用
- 选择某个方案的原因是什么
- 当前结果意味着什么
- 学习者此刻应该理解什么
- 下一步会进入什么阶段

## 设计原则

- 不改变 superpowers 原有工作流
- 不把日志写成命令流水账
- 不默认用户已经读过 `spec` 或 `plan`
- 只记录有教学价值的关键动作
- 由主代理统一维护总日志，避免多代理写入冲突

## 预期产物

默认目标文档为：

`docs/superpowers/global-dev-journal.md`

这份文档应当是：

- 单一总文档
- 追加式维护
- 自包含
- 面向零基础学习者

## 仓库结构

```text
.
├─ AGENTS.md
├─ README.md
├─ SKILL.md
├─ agents/
│  └─ openai.yaml
└─ references/
   ├─ journal_format.md
   └─ phase_explanations.md
```

各文件职责如下：

- `SKILL.md`：定义 skill 的定位、边界、触发逻辑和写作规则
- `references/journal_format.md`：定义每条教学日志的固定结构
- `references/phase_explanations.md`：定义各 superpowers 阶段的教学解释
- `agents/openai.yaml`：为 OpenAI agent 生态提供元数据
- `AGENTS.md`：仓库级文档约束

## 使用方式

### 1. 安装到本地 skills 目录

这个仓库本身是源码仓库。真正使用时，需要让 Codex 能在本地 skills 目录中发现它。

常见方式有两种：

- 把仓库内容复制到 `~/.codex/skills/teaching-development-workflow`
- 使用 skill 安装器，从 GitHub 仓库安装到本地 skills 目录

如果你已经有 `skill-installer` 工作流，也可以直接让 Codex 从这个仓库安装。

### 2. 在项目里配合 superpowers 使用

这个 skill 不是独立工作流，而是 superpowers 的教学扩展层。最合适的使用方式是：

- 用 superpowers 负责主流程，例如 `brainstorming`、`writing-plans`、`executing-plans`、`test-driven-development`、`systematic-debugging`
- 用 `teaching-development-workflow` 负责把这些阶段解释成初学者能读懂的日志

也就是说，它回答的是“为什么这样做、你应该学到什么”，而不是“替你发明另一套开发流程”。

### 3. 什么时候显式触发

在下面这些情况下，建议显式提到这个 skill：

- 你明确表示自己是开发新手
- 你希望把真实开发过程写进文档
- 你不想只看最终结果，而想理解阶段之间如何衔接
- 你希望生成的日志不依赖你先去读 `spec` 或 `plan`

典型说法例如：

- “使用 `teaching-development-workflow`，在遵循 superpowers 工作流时维护一份教学日志。”
- “我是开发新手，请在执行计划和调试时，把关键过程写成我能看懂的中文文档。”
- “请把这次 `systematic-debugging` 的过程追加到 `docs/superpowers/global-dev-journal.md`，并解释我现在应该理解什么。”

### 4. 建议和 `AGENTS.md` 一起使用

如果你希望它在整个项目里更稳定地生效，建议在项目仓库的 `AGENTS.md` 中加入规则，明确要求：

- 当用户处于学习模式时，进入 superpowers 相关阶段必须同时使用 `teaching-development-workflow`
- 所有教学记录统一追加到 `docs/superpowers/global-dev-journal.md`
- 除术语外，若无特殊要求，教学文档默认使用中文

这样做的意义不是“技术上自动 hook”，而是把它提升成项目级工作规则，减少漏记。

### 4.5 推荐触发方式

如果你只是在某一次任务里希望它生效，最稳的方式仍然是显式说明。

推荐直接这样说：

- “请在使用 superpowers 的同时，使用 `teaching-development-workflow`。”
- “这次按 superpowers 工作流推进，并同步维护教学日志。”
- “我是开发新手，这次请同时启用 `teaching-development-workflow`，把关键过程写成中文教学文档。”

这样做的原因很简单：

- `superpowers` 负责主工作流
- `teaching-development-workflow` 是附加教学层
- skill 不是一次开启后永久常驻的后台开关

所以更可靠的实践是：

- 单次任务：显式提到它
- 长期项目：把它写进 `AGENTS.md`
- 重要任务：显式提到它，同时用 `AGENTS.md` 做项目级约束

如果只依赖“代理应该自己想到”，它有机会生效，但不应该把这种不确定性当成默认方案。

### 5. 日志会写什么

每条日志不会机械记录所有命令，而是记录有教学价值的关键节点。默认包括：

- 当前阶段
- 阶段说明
- 当前问题
- 当前已知信息
- 为什么现在做这一步
- 关键动作
- 命令与含义
- 文件与角色
- 技术决策
- 结果
- 你现在应该理解什么
- 下一步

完整模板见 [references/journal_format.md](./references/journal_format.md)。

### 6. 它不会做什么

为了避免误用，这个 skill 有几个明确边界：

- 不替代 `spec` 或 `plan`
- 不替代 superpowers 主技能
- 不保证像系统 hook 一样捕获每一个内部思考
- 不把日志写成审计流水账
- 不让 subagent 直接写主日志

所以它最适合的定位是：在真实工程流程旁边，持续生成一份适合初学者学习的过程文档。

### 7. 一个推荐的完整用法

在一个实际项目里，可以按下面的方式配合使用：

1. 先用 superpowers 做需求澄清和设计。
2. 在进入 `writing-plans` 前，明确要求同时使用 `teaching-development-workflow`。
3. 在执行、测试、调试阶段，持续把关键节点追加到 `docs/superpowers/global-dev-journal.md`。
4. 回看时，优先读 `global-dev-journal.md` 理解流程；需要更精确工程细节时，再去看 `spec` 和 `plan`。

这也是本 skill 最推荐的工作方式。

## 当前状态

第一版已经完成，包含：

- skill 本体
- 中文文档
- journal 模板
- 阶段解释文件
- OpenAI agent 元数据
- 官方结构校验
- 基于真实场景的输出验证

## 验证情况

本仓库已通过 `skill-creator` 的结构校验：

- `quick_validate.py` 通过

并做过一次真实输出验证，用于确认生成的教学日志满足这些要求：

- 中文输出
- 自包含
- 不依赖先阅读 `spec` / `plan`
- 能解释阶段、命令、文件、决策、结果和学习要点

## 后续可扩展方向

- 增加更多阶段示例
- 提供安装说明自动化脚本
- 提供与 `AGENTS.md` 配合使用的推荐规则模板
- 增加更细的日志粒度策略样例
