# Model-invoked vs user-invoked

此仓库中的每个 `SKILL.md` 都是一个技能。将它们区分开的一个维度是 **调用（invocation）** — 谁可以触发它：

- **User-invoked（用户调用）** — 仅能被人类在输入其名称时触发。在文件头部（frontmatter）设置 `disable-model-invocation: true`。`description` 是面向人类的：由人类阅读的一行摘要……  
- **Model-invoked（模型调用）** — 可被模型或用户触发。默认情况下省略 `disable-model-invocation`。`description` 是面向模型的，保留丰富的触发短语（例如：“当用户想要……”）……

因为用户调用的技能没有描述（description），所以除了人类之外没有任何东西可以访问它——其他技能无法触发它。因此用户调用的技能可以调用模型调用的技能，但它永远不能触发另一个用户调用的技能……

每个目录的 `README.md` 和顶层 `README.md` 都将条目分为 **User-invoked** 和 **Model-invoked**。

## 它们之间的依赖关系

依赖关系以 **`/skill` 风格的文本调用** 表达（例如 “Run the `/grilling` skill”），而不是深度的 `../other-skill/FILE.md` 跨引用。共享参考文档应放在拥有该文档的技能内部……

## 被动域工作 vs 主动域工作

仅仅 _阅读_ `CONTEXT.md` 来了解词汇是一个一行的文本指引，而不是 `domain-modeling` 技能。只有主动的构建/打磨工作（挑战术语、边缘案例场景、撰写 ADRs，……）
