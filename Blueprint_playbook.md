# Blueprint Playbook

面向 Blueprint 使用者的落地操作手册。本文档重点回答三个问题：

1. Blueprint 是什么，适合解决什么问题
2. 如何把 Blueprint 放进一个具体的 Cursor 项目里使用
3. 面对不同项目状态，应该从哪个命令开始

---

## 0. 项目概述

Blueprint 是一套运行在 Cursor Agent 工作流中的 Context-First Agentic Engineering OS。它的核心思想不是让 Agent 一上来就写代码，而是先通过一组结构化文档和命令，把需求、设计、技术方案、测试边界整理清楚，再进入实现阶段。

Blueprint 的关键理念是：

**Define → Verify → Implement → Iterate**

而不是：

**Generate → Patch → Patch → Rewrite**

在 Blueprint 中，`.blueprint/` 目录是 Agent 的统一上下文包，也是后续执行的单一真相来源。常见的核心产物包括：

- `PRD_V{N}.md`：产品需求
- `mockup/index.html`：可运行的 Mockup
- `UI_Spec.md`：从确认版 Mockup 提炼出的 UI 规范
- `Tech_Spec.md`：技术方案
- `Test_Spec.md`：测试方案

这套流程特别适合以下类型的工作：

- 从 0 到 1 的新项目或 MVP
- 已有 PRD，但需要快速推进设计与技术方案的项目
- 已有代码库，但希望把新增需求和迭代纳入统一规范流程的项目

Blueprint 当前仍在持续迭代中。命令设计、模板结构、工作流细节和最佳实践都会随着真实项目经验不断优化。欢迎团队成员在使用过程中持续反馈问题、贡献案例、优化提示词与文档模板，一起把这套体系打磨得更稳定、更高效。

---

## 1. 获取该项目

Blueprint 仓库地址：

- [Blueprint GitHub 仓库](https://github.com/Jacobgxd/blueprint/tree/main)

推荐使用 `git clone` 获取完整仓库：

```bash
git clone https://github.com/Jacobgxd/blueprint.git
```

也可以直接下载 ZIP 后解压，但更推荐 Git 方式，便于后续同步 Blueprint 的更新。

获取后，重点关注以下目录和文件：

- `.cursor/commands/`：所有 Agent 命令定义
- `.cursor/skills/`：辅助技能，尤其是设计相关能力
- `.blueprint/`：规格文档目录，也是 Agent 的主要上下文来源
- `plans/`：开发计划
- `issues/`：问题和需求记录
- `reports/`：review、verify、test 等输出报告
- `START_HERE.md`：新用户快速入口
- `QUICK_REFERENCE.md`：命令和路径速查表

需要特别说明的是，Blueprint 不是一个独立运行的应用，而是一套可以嵌入到具体业务项目中的 Agent 工作流模板。

---

## 2. 使用该项目

### 2.1 使用前提

在使用 Blueprint 前，建议先统一下面几个前提：

- 所有对话默认在 **Cursor 的 Agent 模式** 下进行
- Blueprint 需要被放到你的**具体项目根目录**中使用
- 这个具体项目可以是一个全新的项目，也可以是一个已经存在的项目
- 每次开始新任务前，优先阅读 `.blueprint/CONTEXT.md`
- Blueprint 的目标不是替代人的判断，而是让 Agent 始终在同一套上下文约束下工作，减少返工、遗漏和实现漂移

如果你是第一次接入 Blueprint，建议至少先读这三个文件：

- `START_HERE.md`
- `QUICK_REFERENCE.md`
- `.cursor/commands/README.md`

### 2.2 接入方式

Blueprint 的推荐使用方式不是单独开一个仓库去“研究”，而是把它接入到你要开发的实际项目中。

有两种典型接入方式：

#### 方式 A：用于全新项目

适合：

- 从 0 开始做一个新产品或 MVP
- 需求、设计、实现边界还没有被系统化整理
- 希望先建立统一规格，再推动设计和研发

常见做法：

1. 在新项目根目录中放入 Blueprint 所需目录和命令文件
2. 从 `.blueprint/CONTEXT.md` 开始维护项目状态
3. 根据现状从 `/create-prd` 或 `/create-mockup` 开始推进

#### 方式 B：用于已有项目

适合：

- 已有代码仓库，需要承接新增需求或迭代
- 已有部分文档、PRD、设计稿或技术实现
- 希望把后续需求纳入统一的 spec-driven 工作流

常见做法：

1. 将 Blueprint 的目录结构和命令文件引入现有项目根目录
2. 基于已有资料补全 `.blueprint/` 中缺失的关键文档
3. 按当前项目状态，从最合适的命令继续，不必强制从第一步重跑

如果现有项目本身已经有 `.cursor/` 配置，建议先审查差异，再按需合并，避免直接覆盖团队已有设置。

### 2.3 使用场景

下面给出四种最常见的起步场景。核心原则是：**不是固定从第一步开始，而是从当前材料最完整的地方开始。**

#### 场景 1：从 0 开始的项目

前提：

- 没有成型 PRD
- 没有确认版设计
- 没有技术方案和测试方案

建议起点：

- `/create-prd`

适用情况：

- 你只有一个产品想法，或者需求还比较粗糙
- 你需要先把用户、目标、范围、流程和约束讲清楚
- 你希望后续所有设计与研发都基于统一 PRD 展开

推荐路径：

```text
/create-prd
→ /create-mockup
→ /review-mockup
→ /create-ui-spec
→ /create-tech-spec
→ /create-test-spec
→ /verify
→ /create-plan
→ /execute
```

#### 场景 2：已经有 PRD，可以直接从 Mockup 开始

前提：

- 已经有相对清晰的 PRD
- 还没有确认版页面和设计结构

建议起点：

- `/create-mockup`

适用情况：

- 产品需求已经明确
- 希望优先验证页面布局、信息层级和交互方向
- 希望先看到可运行页面，再提炼 UI 规范

推荐路径：

```text
/create-mockup
→ /review-mockup
→ /create-ui-spec
→ /create-tech-spec
→ /create-test-spec
→ /verify
```

#### 场景 3：已经有 PRD、Mockup、UI Spec，可以从 Tech Spec 开始

前提：

- 产品需求已经基本稳定
- 确认版 Mockup 已经存在
- UI 规范已经形成

建议起点：

- `/create-tech-spec`

适用情况：

- 设计方向已确认
- 现在需要把需求和设计翻译为工程可执行方案
- 需要定义技术选型、模块划分、接口设计、目录结构和实现边界

推荐路径：

```text
/create-tech-spec
→ /create-test-spec
→ /verify
→ /create-plan
→ /execute
```

#### 场景 4：已经有完整项目代码，要创建新的需求或记录问题

前提：

- 已有可运行项目和既有代码
- 当前工作是一次增量迭代，而不是从 0 启动

建议起点：

- `/issue`

适用情况：

- 你要记录一个 bug、需求、优化项或改造点
- 你希望先把问题描述清楚，再决定是否进入完整 Blueprint 流程
- 你需要把新增事项沉淀到 `issues/` 里，方便后续排期或扩展

推荐路径分为两种：

**轻量路径**

```text
/issue
→ 评估影响范围
→ 必要时 /create-plan
→ /execute
```

**标准迭代路径**

```text
/issue
→ /create-prd（以迭代模式更新）
→ 如涉及页面变化，则继续 /create-mockup → /create-ui-spec
→ /create-tech-spec
→ /create-test-spec
→ /verify
→ /create-plan
→ /execute
```


### 2.4 各个命令的介绍、使用说明与建议模型

模型推荐不要机械理解成“某个命令只能用某个模型”，而应该按任务类型来选：

- 需求梳理、文档生成、跨文档对齐：优先选择长上下文和结构化表达能力强的模型
- 代码实现、重构、精确修改：优先选择工程执行能力强的模型
- Mockup 生成、设计审查、UI 规则提炼：优先选择对设计表达和整体一致性更敏感的模型

下面按命令给出推荐。

#### `/create-prd`

用途：

- 把想法整理成结构化 PRD，形成后续流程的源头文档

输入：

- 产品目标
- 用户角色
- 核心流程
- 边界条件
- 已有业务背景

输出：

- `.blueprint/PRD_V{N}.md`

建议模型：

- 优先使用擅长长文本组织、需求抽象和结构化表达的模型
- 如果材料很多、需求复杂，优先选择长上下文更强的模型
- 推荐模型 GPT 5.4

#### `/create-mockup`

用途：

- 基于当前 PRD 生成可运行的静态 Mockup

输入：

- 当前生效 PRD
- 品牌方向
- 参考产品
- 风格偏好

输出：

- `.blueprint/mockup/index.html`

建议模型：

- 优先使用擅长前端生成、页面结构组织、视觉表达的模型
- 如果涉及大量设计判断，建议搭配设计能力更强的模型
- 推荐模型 Sonnet 4.6

#### `/review-mockup`

用途：

- 检查 Mockup 是否覆盖需求、层级是否合理、视觉和交互是否一致

输入：

- Mockup
- 必要时结合 PRD 与 UI Spec

输出：

- `reports/mockup-reviews/`

建议模型：

- 优先使用批判性审查、对照检查和问题发现能力更强的模型
- 推荐模型 GPT 5.4

#### `/create-ui-spec`

用途：

- 从确认版 Mockup 提炼出结构化 UI 规范
- 同步生成 `design-system.html`

输入：

- 当前生效 PRD
- 已确认的 Mockup

输出：

- `.blueprint/UI_Spec.md`
- `.blueprint/mockup/design-system.html`

建议模型：

- 优先使用长文本结构化和设计规则抽象能力强的模型
- 推荐模型 Sonnet 4.6

#### `/create-tech-spec`

用途：

- 把 PRD、Mockup、UI Spec 转换为工程可执行技术方案

输入：

- PRD
- UI Spec
- Mockup

输出：

- `.blueprint/Tech_Spec.md`

建议模型：

- 优先使用工程推理、架构拆解、模块规划能力强的模型
- 推荐模型 Opus

#### `/create-test-spec`

用途：

- 在开发前定义测试策略、验收标准和测试边界

输入：

- PRD
- UI Spec
- Tech Spec

输出：

- `.blueprint/Test_Spec.md`

建议模型：

- 优先使用逻辑严谨、覆盖意识强、擅长测试设计的模型
- 推荐模型 Opus

#### `/verify`

用途：

- 检查 PRD、Mockup、UI Spec、Tech Spec、Test Spec 是否彼此一致

输入：

- 以上所有 Blueprint 文档

输出：

- `reports/verify/`

建议模型：

- 优先使用长上下文、对照分析和矛盾发现能力强的模型
- 推荐模型 GPT 5.4

#### `/create-plan`

用途：

- 基于完整规格文档生成开发计划和实施顺序

输入：

- 已通过 verify 的 Blueprint 文档

输出：

- `plans/[feature].md`

建议模型：

- 优先使用擅长任务拆分、依赖排序和执行规划的模型
- 推荐模型 Opus

#### `/execute`

用途：

- 按 Plan 和 Mission Briefing 进行真实编码实现

输入：

- Plan
- Tech Spec
- UI Spec
- Mockup
- Test Spec

输出：

- 代码实现

建议模型：

- 优先使用工程执行和精确改码能力强的模型
- 推荐模型 Sonnet 

特别注意：

- `/execute` 前必须先完成 Mission Briefing
- 如果实现过程中发现规格冲突，应该暂停并回到文档层解决，而不是自行猜测

#### `/review`

用途：

- 从代码质量和规格漂移两个维度审查实现结果

输入：

- 当前代码
- PRD
- UI Spec
- Tech Spec

输出：

- review 结论与修复建议

建议模型：

- 优先使用审查能力强、善于发现遗漏和风险的模型

#### `/test`

用途：

- 按 Test Spec 执行测试，并输出可核验结果

输入：

- Test Spec
- 当前实现

输出：

- `reports/test-runs/`

建议模型：

- 优先使用执行稳定、适合逐条校验和记录证据的模型

#### 工具型命令（统一建议 Composer，速度快，成本低）

`/explore`

- 用于编码前理解现有代码结构与影响面
- 适合在进入实现前快速摸清上下文

`/document`

- 用于代码或文档变更后同步更新说明材料

`/peer-review`

- 用于跨模型交叉审查，降低单模型偏差

`/issue`

- 用于快速记录 bug、需求、改造点或问题线索

`/learn`

- 用于把当前会话切换到解释和教学模式

### 2.5 推荐工作方式

以下是一套实践中最稳妥的工作方式：

1. 先读 `.blueprint/CONTEXT.md`，确认当前项目走到哪一步
2. 根据当前材料状态，选择最接近现状的起点命令
3. 完成每一步后，及时更新上下文和相关文档
4. 对设计类工作，优先先确认 Mockup，再沉淀 UI Spec
5. 对开发类工作，不要跳过 `Test_Spec` 和 `/verify`
6. 在 `/execute` 前，确保 Plan、Tech Spec、UI Spec、Mockup、Test Spec 已经对齐

---

## 3. 最佳实践与注意事项

### 3.1 不要默认每次都从第一步开始

Blueprint 的正确用法不是机械跑完整流水线，而是根据当前项目状态，选择最合适的切入点。已有材料越完整，越应该从更靠后的步骤开始。

### 3.2 先确认 Mockup，再沉淀 UI Spec

Blueprint 当前强调 Mockup-first。不要在没有确认视觉结果之前急着写 `UI_Spec.md`，否则很容易把猜测固化成规范。

### 3.3 `Test_Spec` 必须在开发前生成

`/create-test-spec` 不是开发后补文档，而是在编码前定义验收边界。这样测试标准才能成为实现约束，而不是事后检查。

### 3.4 `/verify` 不要跳过

跨文档矛盾越晚发现，代价越高。`/verify` 是最便宜的问题发现时机，尤其适合在进入 `/create-plan` 和 `/execute` 前做总检查。

### 3.5 `/execute` 发现冲突时不要硬写

如果实现时发现 PRD、Mockup、UI Spec、Tech Spec 或 Test Spec 之间有冲突，应暂停并回到文档层澄清，而不是让 Agent 自行做隐含假设。

### 3.6 让 `.blueprint/CONTEXT.md` 成为会话入口

当会话变长、上下文变复杂时，可以新开一个会话，只带 `.blueprint/CONTEXT.md` 进入，让 Agent 更快恢复当前项目状态。

---

## 4. 常见问题

### Q1：Blueprint 只能用于新项目吗？

不是。Blueprint 同样适用于已有项目的迭代。对老项目来说，最常见的起点是 `/issue`、`/create-prd` 的迭代模式，或者直接从 `/create-tech-spec` 开始补齐缺失规范。

### Q2：我已经有 PRD 了，还需要 `/create-prd` 吗？

不一定。如果现有 PRD 已经足够清晰，可以直接从 `/create-mockup` 开始。如果 PRD 质量一般，或者需要重组需求结构，可以先用 `/create-prd` 进行整理和版本化。

### Q3：是不是每次都必须跑完整 Define 阶段？

不一定。Blueprint 的原则是基于当前项目状态继续，而不是重复生成已经存在且已确认的材料。

### Q4：为什么不建议直接让 Agent 写代码？

因为没有统一上下文时，Agent 往往会在需求、设计、技术边界和验收标准上自行补全假设，最终导致频繁返工。Blueprint 的价值就在于先把定义统一，再推进实现。

### Q5：`/issue` 和 `create-issue` 是同一个东西吗？

以当前仓库公开命令为准，问题记录命令是 `/issue`。如果历史讨论或内部口头表达出现过 `create-issue`，在正式文档中建议统一写成 `/issue`，避免使用者混淆。

---

## 5. 建议阅读顺序

如果你是第一次使用 Blueprint，建议按以下顺序阅读：

1. `README.md`：理解 Blueprint 的定位与整体流程
2. `START_HERE.md`：快速建立基本使用认知
3. `QUICK_REFERENCE.md`：查看命令和路径速查表
4. `.cursor/commands/README.md`：查看命令详细说明
5. `Blueprint_playbook.md`：结合具体项目状态，决定你的起点和用法

---

## 6. 一句话总结

Blueprint 的目标不是“让 Agent 更快生成代码”，而是“让 Agent 在更稳定、更一致、更可验证的上下文里工作”。

当你不确定从哪里开始时，先看 `.blueprint/CONTEXT.md`，再问自己一句：

**我现在已经有什么材料，下一步最合理的命令是什么？**
