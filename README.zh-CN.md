<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

[English](./README.md) | [繁體中文](./README.zh-TW.md) | **简体中文**

# 给真正工程师的 Skills

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

这是我每天用来做真正工程开发的 agent skills——不是 vibe coding。

开发真正的应用程序很难。GSD、BMAD、Spec-Kit 这类方法试图通过「接管整个流程」来帮忙，但这么做的同时，它们也夺走了你的掌控权，而且流程中一旦出错就很难排除。

这些 skills 的设计目标是小巧、容易调整、可组合。它们适用于任何模型，背后是数十年的工程经验。尽情改造它们，变成你自己的东西。Enjoy。

如果你想追踪这些 skills 的更新、以及我未来新增的技能，可以加入我的newsletter，与约 60,000 位开发者一起：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 安装（30 秒完成）

两种安装方式，两种哲学。**[Claude Code plugin](https://code.claude.com/docs/en/plugins)** 把整套 skills 安装为受管理的只读套件，我发布更新时你就会收到——你是订阅，而不是 fork。**[skills.sh](https://skills.sh/mattpocock/skills)** 则把可编辑的 skill 文件复制进你的项目，让你可以动手改造、据为己有。二选一——两个都装会让每个 skill 出现两次。

### 1. 获取 skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

或者，在 session 内：

```
/plugin install mattpocock-skills
```

它已在 Claude Code 官方 marketplace 中，不需要先添加任何东西，更新会自动送达。

</details>

<details>
<summary><strong>Codex 与其他 agents</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

挑选你想要的 skills，以及要安装到哪些 coding agents。**安装器让你自由选择要哪些 skills——请务必勾选 `setup-matt-pocock-skills`。**

原生 Codex plugin 已在 roadmap 上——详见 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

</details>

<details>
<summary><strong>给爱动手改造的人</strong></summary>

在任何 agent 上使用同一个安装器——包括 Claude Code：

```bash
npx skills@latest add mattpocock/skills
```

它会把 skills 以普通文件的形式写进你的 repo，归你所有、可以编辑。没有任何东西会在你背后偷偷更新；想要我的最新变更时，用 `npx skills update` 拉取即可。

</details>

### 2. 执行 `/setup-matt-pocock-skills`

在你的 agent 中，每个 repo 执行一次。它会：

- 问你想用哪个 issue tracker（GitHub、Linear，或本地文件）
- 问你在分诊（triage）tickets 时使用哪些标签（`/triage` 依赖标签运作）
- 问你想把我们生成的文档存放在哪里

### 3. 搞定——可以开始用了。

## 这些 Skills 为什么存在

我打造这些 skills，是为了修掉我在 Claude Code、Codex 和其他 coding agents 身上常见的失败模式。

### #1：Agent 做的不是我想要的

> 「没有人确切知道自己要什么。」
>
> David Thomas & Andrew Hunt，《[The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**问题**：软件开发中最常见的失败模式是认知落差（misalignment）。你以为开发者懂你要什么，直到你看到他做出来的东西——才发现他完全误解了你。

AI 时代也一样。你和 agent 之间存在沟通落差。解法是 **grilling session（连番追问）**——让 agent 针对你要做的东西，向你提出详细的问题。

**解法**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md)——非代码用途
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)——与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但多了更多好东西（见下文）

这是我最热门的 skills。它们帮你在动手之前先与 agent 对齐，并深入思考你要做的变更。**每次**要做变更时都该用它们。

### #2：Agent 太啰嗦了

> 有了统一语言（ubiquitous language），开发者之间的对话与代码的表达，都衍生自同一个领域模型。
>
> Eric Evans，《[Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)》

**问题**：在项目初期，开发者与软件的服务对象（领域专家）通常说的是不同的语言。

我和我的 agents 之间也感受到同样的张力。Agent 通常被丢进一个项目，被要求边做边摸索术语，于是它用 20 个字表达 1 个字就够的东西。

**解法**是建立共享语言：一份帮助 agent 解读项目术语的文档。

<details>
<summary>示例</summary>

这是来自我的 `course-video-manager` repo 的 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 示例。哪一种比较好读？

- **之前**：「当课程某个 section 里的一堂课被『实体化』（也就是在文件系统中取得一个位置）时会出问题」
- **之后**：「materialization cascade（实体化连锁）有问题」

这种简洁，在每一个 session 都持续带来回报。

</details>

这已内建于 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)。它是一场 grilling session，但同时帮你与 AI 建立共享语言，并把难以解释的决策记录在 ADR 中。

很难用言语形容这有多强大——它可能是这个 repo 里最酷的技巧。试试看就知道了。

> [!TIP]
> 共享语言的好处不只是减少啰嗦：
>
> - **变量、函数与文件的命名更一致**，都使用共享语言
> - 因此 **codebase 对 agent 来说更容易导航**
> - Agent 也**花更少 tokens 在思考上**，因为它能使用更精简的语言

### #3：代码不能跑

> 「永远采取小而审慎的步骤。反馈的速度就是你的限速。永远不要接下太大的任务。」
>
> David Thomas & Andrew Hunt，《[The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**问题**：假设你和 agent 已经对齐了要做什么，但 agent *还是*产出垃圾，怎么办？

该检视你的反馈回路（feedback loops）了。如果得不到「代码实际跑起来如何」的反馈，agent 就是在盲飞。

**解法**：你需要那一整套常见的反馈回路：静态类型、浏览器访问、自动化测试。

在自动化测试方面，red-green-refactor 回路至关重要：agent 先写一个会失败的测试，然后修好它。这能给 agent 稳定的反馈水准，产出好得多的代码。

我做了一个可以插进任何项目的 **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill**。它鼓励 red-green-refactor，并给 agent 大量关于好测试与坏测试的指引。

在调试方面，我也做了 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** skill，把调试最佳实践包装成一个按阶段把关的纪律化回路。

### #4：我们造出了一团泥球（Ball Of Mud）

> 「*每天*都要投资在系统的设计上。」
>
> Kent Beck，《[Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)》

> 「最好的模块是深的（deep）。它们让大量功能通过一个简单的接口被取用。」
>
> John Ousterhout，《[A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)》

**问题**：大多数用 agent 做出来的 app 都很复杂、难以修改。因为 agent 能大幅加速写代码，它们也同时加速了软件熵（entropy）。Codebase 正以前所未有的速度变得更复杂。

**解法**是一种激进的 AI 开发新路线：在乎代码的设计。

这个理念内建于这些 skills 的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在生成 spec 之前，会先拷问这次你会动到哪些模块

而最关键的是 [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md)：它扫描 codebase 找出 deepening（加深模块）的机会，并把候选清单交给你。我建议每隔几天就在你的 codebase 上跑一次。它是一场体检，不是急救：在真正老旧的 codebase 上它会找到真实的候选，但它不会帮你把泥球解开。

### 总结

软件工程基本功比以往任何时候都更重要。这些 skills 是我把这些基本功浓缩成可重复实践方式的最大努力，希望能帮你交付职业生涯中最好的 app。Enjoy。

## 技能一览

这些 skills 沿着一个轴线区分——谁可以触发它们。**User-invoked** skills 只有你亲自输入时才能触发（例如 `/grill-me`）；它们的职责是编排（orchestrate）。**Model-invoked** skills 可以由你触发，也可以在任务相符时由 agent 自动取用；它们承载的是可重复使用的纪律。User-invoked skill 可以调用 model-invoked skills，但绝不会调用另一个 user-invoked skill。

### Engineering

我每天写代码使用的 skills。

**User-invoked**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** — 询问哪个 skill 或 flow 适合你的情况。这是整个 repo 中 user-invoked skills 的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** — Grilling session，同时建立项目的领域模型：磨利术语，并就地更新 `CONTEXT.md` 与 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** — 让 issues 在一个由分诊角色组成的状态机中流转。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** — 扫描 codebase 找出 deepening 机会，以可视化 HTML 报告呈现，然后针对你挑选的候选进行 grilling。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** — 为 engineering skills 设置此 repo（issue tracker、triage 标签、domain 文档布局）。使用其他 engineering skills 前，每个 repo 先执行一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)** — 把目前的对话转化成 spec 并发布到 issue tracker。不做访谈——只综合你们已经讨论过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)** — 把任何计划、spec 或对话拆解成一组 tracer-bullet tickets，每张都宣告自己的 blocking 依赖——本地文件以文字书写，真正的 tracker 则用原生 blocking 链接。
- **[implement](./skills/engineering/implement/SKILL.md)** — 依据 spec 或一组 tickets 构建工作，在预先约定的 seams 驱动 `/tdd`，commit 前以 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)** — 把一大块超出单一 agent session 容量的工作，规划成 issue tracker 上由 decision tickets 组成的共享地图——一次解决一张，直到通往目的地的路清晰为止。

**Model-invoked**

- **[prototype](./skills/engineering/prototype/SKILL.md)** — 打造一次性 prototype 来回答设计问题——状态/逻辑问题产出单一可分享的 HTML 文件，UI 问题产出数个从同一路由切换的、截然不同的 UI 变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** — 针对难 bug 与性能退化的纪律化诊断回路：建立一条会对此 bug 变红的反馈回路 → 最小化 → 提出假设 → 插桩 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)** — 以后台 agent 的形式，针对问题查证高信任度的一手来源，并把发现整理成附引用的 Markdown 文件存进 repo。
- **[tdd](./skills/engineering/tdd/SKILL.md)** — 采用 red-green-refactor 回路的测试驱动开发。一次一个垂直切片地建功能或修 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** — 主动建立并磨利项目的领域模型——对照 glossary 挑战术语、用边界情境压力测试，并就地更新 `CONTEXT.md` 与 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** — 设计 deep modules 的共享纪律与词汇：大量行为藏在小接口后面、位于干净的 seam 上、可通过接口测试。
- **[code-review](./skills/engineering/code-review/SKILL.md)** — 对某固定点以来的 diff 做双轴审查：**Standards**（是否符合 repo 的编码标准，外加 Fowler 坏味道基线？）与 **Spec**（是否忠实实现原始 issue/spec？），以并行 sub-agents 执行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)** — 逐 hunk 处理进行中的 git merge 或 rebase 冲突，通过追溯双方一手来源中的意图来解决，然后完成整个操作——绝不 `--abort`。
- **[wizard](./skills/engineering/wizard/SKILL.md)** — 生成交互式 bash wizard，带着人类完成只有人类能做的步骤：开通基础设施、设置凭证或 CI secrets、操作陌生的第三方 dashboard，或执行一次性 migration / cutover。

### Productivity

一般工作流程工具，非代码专属。

**User-invoked**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** — 针对计划或设计接受无情的访谈，直到设计树的每个分支都被解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)** — 把目前的对话压缩成交接文档，让另一个 agent 能接续工作。
- **[teach](./skills/productivity/teach/SKILL.md)** — 跨多个 session 教用户学会新技能或概念，以目前目录作为有状态的教学 workspace。
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)** — 把你独自无法回答的决策，转化成给「唯一能回答的人」的 Markdown 问卷——异步填写，或在会议中一起填。它拷问的是「寄送」（寄给谁、需要拿回什么），而非主题本身。
- **[wait-what](./skills/productivity/wait-what/SKILL.md)** — 在消息看不懂的当下立刻触发。Agent 会用白话英文、补上你缺的上下文，并使用你 `CONTEXT.md` 中的词汇重新说明。

**Model-invoked**

- **[grilling](./skills/productivity/grilling/SKILL.md)** — 针对计划、决策或想法无情地访谈用户，直到设计树的每个分支都被解决。这是 `grill-me`、`grill-with-docs`、`triage`、`wayfinder` 与 `improve-codebase-architecture` 背后可重复使用的访谈 primitive。
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)** — 撰写给 agent 看的文档：skills、AGENTS.md/CLAUDE.md，以及任何 agent 经由 pointer 触达的文档。
