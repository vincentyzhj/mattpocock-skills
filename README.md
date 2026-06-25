<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 面向真实工程师的技能集

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

这是我每天用于真实工程工作的 agent 技能集合 —— 不是“氛围化”编码。

开发真实应用很难。像 GSD、BMAD 和 Spec-Kit 之类的方法试图通过掌控流程来帮助。但在这么做的同时，它们也会剥夺你的控制权，并让流程中的 bug 难以排查[...]

这些技能被设计得小、易改、可组合。它们可与任何模型协同工作，基于多年工程经验。随意折腾它们，把它们改造成你的工具。希望你喜欢。

如果你想跟进这些技能的变化以及我创建的新技能，可以订阅我的通讯，已有约 60,000 名开发者订阅：

[订阅通讯](https://www.aihero.dev/s/skills-newsletter)

## 快速开始（30 秒安装）

1. 运行 skills.sh 安装器：

```bash
npx skills@latest add mattpocock/skills
```

2. 选择你想要的技能，以及要安装到哪些编码 agent 上。**确保选择 `/setup-matt-pocock-skills`**。

3. 在你的 agent 中运行 `/setup-matt-pocock-skills`。它会：
   - 询问你想使用哪个问题跟踪器（GitHub、Linear 或本地文件）
   - 询问你在进行问题初步分类时会使用哪些标签（`/triage` 使用这些标签）
   - 询问你希望将生成的文档保存到哪里

4. 完成 —— 你就可以开始使用了。

## 这些技能存在的理由

我创建这些技能是为了解决我在使用 Claude Code、Codex 和其他编码 agent 时常见的故障模式。

### #1：Agent 没有做我想要的事

> “没有人确切知道他们想要什么”
>
> David Thomas & Andrew Hunt，《The Pragmatic Programmer》

问题：软件开发中最常见的失败模式是目标不一致。你以为开发者明白你的意图，但看到成果时发现它没理解你[...]

在 AI 时代也是同样的问题。你和 agent 之间存在沟通差距。解决方法是一次“拷问式”会话——让 agent 对你进行详细提问，弄清楚需求的各个分支[...]

解决方案：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) — 用于非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) — 与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 类似，但增加了更多功能（见下文）

这是我最受欢迎的技能。它们能在开始之前帮助你和 agent 对齐，并迫使你深入思考要做的改动。每次想要变更时都用它们。

### #2：Agent 太冗长

> “拥有统一语言后，开发者间的对话和代码表达都源自相同的领域模型。”
>
> Eric Evans，《Domain-Driven-Design》

问题：在项目初期，开发者和领域专家通常说着不同的语言。我在 agent 上也遇到同样的问题。agent 初来乍到需要自己学习术语，所以常常用 20 个词表达 1 个词能做到的事。

解决方法是建立共享语言——一个帮助 agent 解码项目术语的文档。

示例（可折叠细节部分）

这里有一个示例 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md)，来自我的 `course-video-manager` 仓库。哪个更容易理解 [...]

- **之前**: “当课程的一个节内的 lesson 被标为 'real'（即在文件系统中占有位置）时会出现问题”
- **之后**: “关于 materialization cascade 的问题”

这种简洁带来的收益是长期的。

这个功能被内置在 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 中：这是一次拷问式会话，但它帮助你与 AI 建立共享语言，并更新 `CONTEXT.md` 和 ADRs（在代码库中内联）[...]

这很难用文字说明它有多强大。可能是本仓库中最酷的技术之一。试一试，你会看到效果。

> [!提示]
> 共享语言还有许多其他好处：
>
> - **变量、函数和文件命名会更一致**，使用共享术语
> - 因此 **代码库更易被 agent 导航**
> - agent **思考时消耗的 tokens 更少**，因为有更简洁的语言可用

### #3：代码不工作

> “总是采取小而有意识的步骤。反馈率是你的速度上限。不要承担太大的任务。”
>
> David Thomas & Andrew Hunt，《The Pragmatic Programmer》

问题：假设你和 agent 就该构建什么达成一致，但 agent 仍然产出糟糕的结果怎么办？

是时候检查你的反馈回路了。若没有关于代码实际运行情况的反馈，agent 就在盲飞。

解决方法：需要常规的反馈回路：静态类型、浏览器访问和自动化测试。

对于自动化测试，红-绿-重构的循环至关重要。先写一个失败的测试，然后修复它。这能给 agent 提供一致的反馈水平[...]

我为此构建了 **[`/tdd`](./skills/engineering/tdd/SKILL.md)**，可以插入任何项目。它鼓励红-绿-重构，并给 agent 充足的指导关于什么是好/坏的测试[...]

用于调试的，我也做了 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)**，把最佳调试实践包装成一个简单循环。

### #4：我们构建了一个泥球（ball of mud）

> “每天都要投资于系统设计。”
>
> Kent Beck，《Extreme Programming Explained》

> “最好的模块很深。它们允许通过简单接口访问大量功能，并放在干净的位置。”
>
> John Ousterhout，《A Philosophy Of Software Design》

问题：使用 agent 构建的应用往往复杂难以修改。agent 可以极大加速编码，但也会加速软件熵的增长。代码库会变得越来越难以维护[...]

解决方法是对代码设计采取一种激进的日常关注方式。

这体现在这些技能的每一层：

- [`/to-prd`](./skills/engineering/to-prd/SKILL.md) 会在创建 PRD 前询问你将触及哪些模块
- 尤其是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 会帮助你从“泥球”中挽救代码库，生成可视化 HTML 报告并进行逐步改进。我推荐在感觉代码库已失控时运行它[...]

### 总结

软件工程基础比以往任何时候都更重要。这些技能是我把这些基础凝练为可重复实践的最佳尝试，帮助你交付职业生涯中最好的应用。希望你喜欢。

## 参考

下面按“谁可以调用”这个维度划分。**用户调用（User-invoked）** 的技能只有在你输入它们时才可达（例如 `/grill-me`）；它们负责编排。**模型调用（Model-invoked）** 的技能可以被模型或用户调用[...]

### Engineering（工程类）

我每天用于代码工作的技能。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** — 询问哪个技能或流程适合你的情况。对本仓库中用户调用技能的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** — 拷问式会话，同时构建你的项目领域模型，精炼术语并更新 `CONTEXT.md` 和内联 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** — 将 issue 在一个分级的 triage 状态机中推进。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** — 扫描代码库以发现可深化设计的机会，呈现为视觉化 HTML 报告，然后通过拷问改进实现。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** — 为工程类技能配置本仓库（问题跟踪器、triage 标签、领域文档布局）。运行一次即可完成初始配置。
- **[to-issues](./skills/engineering/to-issues/SKILL.md)** — 将任何计划、规范或 PRD 拆成可独立领取的问题（垂直切片）。
- **[to-prd](./skills/engineering/to-prd/SKILL.md)** — 将当前对话转成 PRD 并发布到问题跟踪器。无需再面试 —— 直接综合你已经讨论的内容。
- **[prototype](./skills/engineering/prototype/SKILL.md)** — 构建一个可丢弃的原型来完善设计 —— 要么是可运行的终端应用用于状态/业务逻辑问题，要么是若干激进的原型来验证想法[...]

**模型调用**

- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** — 用于难以定位的 bug 和性能回归的有纪律诊断循环：复现 → 最小化 → 假设 → 仪器化 → 验证。
- **[tdd](./skills/engineering/tdd/SKILL.md)** — 带有红-绿-重构循环的测试驱动开发。逐个垂直切片构建功能或修复 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** — 主动构建和精炼项目的领域模型 —— 挑战术语的定义，用边界案例进行压力测试。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** — 一套用于设计“深”模块的共同纪律和词汇：少而精的接口后有大量行为，放在清晰的边界上。

### Productivity（生产力类）

通用工作流工具，非代码特定。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** — 对计划或设计进行无情面询，直到决策树的每个分支都被解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)** — 将当前对话压缩为交接文档，以便另一个 agent 可以继续工作。
- **[teach](./skills/productivity/teach/SKILL.md)** — 在多个会话中教用户新技能或概念，使用当前目录作为有状态的教学工作区。
- **[writing-great-skills](./skills/productivity/writing-great-skills/SKILL.md)** — 编写和编辑技能的参考：使技能可预测的词汇和原则。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)** — 对用户进行无情面询，直到决策树的每个分支被解决。它是 `grill-me` 背后的可重用循环[...]

### Misc（杂项）

我保留但很少使用的工具。

- **[git-guardrails-claude-code](./skills/misc/git-guardrails-claude-code/SKILL.md)** — 设置 Claude Code 钩子，在执行危险 git 命令（push、reset --hard、clean 等）前阻止它们执行[...]
- **[migrate-to-shoehorn](./skills/misc/migrate-to-shoehorn/SKILL.md)** — 将测试文件从 `as` 类型断言迁移到 @total-typescript/shoehorn。
- **[scaffold-exercises](./skills/misc/scaffold-exercises/SKILL.md)** — 创建带有章节、问题、答案和解释器的练习目录结构。
- **[setup-pre-commit](./skills/misc/setup-pre-commit/SKILL.md)** — 使用 lint-staged、Prettier、类型检查和测试设置 Husky pre-commit 钩子。
