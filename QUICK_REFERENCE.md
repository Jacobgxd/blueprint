# Blueprint — Quick Reference

## 🔄 标准流水线

```
DEFINE 阶段
  /create-prd          →  .blueprint/PRD_V{N}.md      （如当前没有 PRD）
  /create-mockup       →  .blueprint/mockup/index.html
  /review-mockup       →  reports/mockup-reviews/     ⟲ 不满足则返回修改
  /create-ui-spec      →  .blueprint/UI_Spec.md
                         + .blueprint/mockup/design-system.html
  /create-tech-spec    →  .blueprint/Tech_Spec.md      （资深工程师 Review）
  /create-test-spec    →  .blueprint/Test_Spec.md      （测试工程师 Review）⚠️ 开发前
  /verify              →  reports/verify/              （无阻塞项才能继续）

IMPLEMENT 阶段
  /create-plan         →  plans/[feature].md           （资深工程师 Review）
  /execute             →  source code                  （先读 Mission Briefing）
  /review              →  代码质量 + 漂移检测
  /test                →  reports/test-runs/
```

---

## 📋 命令速查

### Define 阶段（生成规格文档）

| 命令 | Agent | 输入 | 输出 |
|-----|-------|-----|------|
| `/create-prd` | PM Agent | 想法/需求 | `.blueprint/PRD_V{N}.md` |
| `/create-mockup` | Mockup Agent | 当前生效 PRD | `.blueprint/mockup/index.html` |
| `/review-mockup` | Review Agent | mockup（必要时结合 UI Spec） | `reports/mockup-reviews/` |
| `/create-ui-spec` | Design Agent | 已确认 mockup + PRD | `.blueprint/UI_Spec.md` + `.blueprint/mockup/design-system.html` |
| `/create-tech-spec` | Dev Agent | PRD + UI Spec + mockup | `.blueprint/Tech_Spec.md` |
| `/create-test-spec` | QA Agent | PRD + UI Spec + Tech Spec | `.blueprint/Test_Spec.md` |
| `/verify` | Global Verifier | 所有上述文档 | `reports/verify/` |

### Implement 阶段（编码执行）

| 命令 | 作用 | 关键约束 |
|-----|-----|---------|
| `/create-plan` | 生成开发计划 | 需 verify 无阻塞项 |
| `/execute` | 编码实现 | 先读 Mission Briefing（Tech Spec + mockup + Test Spec） |
| `/review` | 代码审查 + 漂移检测 | 两个维度都无阻塞才能进入 /test |
| `/test` | 执行测试计划 | 按 Test Spec，有证据才可判通过 |

### 工具命令

| 命令 | 用途 |
|-----|-----|
| `/explore` | 编码前影响面分析 |
| `/document` | 代码变更后更新文档 |
| `/peer-review` | 跨模型代码审查 |
| `/issue` | 快速捕获 bug/需求 → `issues/` |
| `/learn` | 遇到不熟悉概念时切换教学模式 |

---

## 📂 文件路径速查

| 内容 | 路径 |
|-----|-----|
| AI 入口文件 | `.blueprint/CONTEXT.md` |
| 当前生效 PRD | `.blueprint/PRD.md` / `.blueprint/PRD_V{N}.md` |
| UI 规范 | `.blueprint/UI_Spec.md` |
| 可运行 Mockup | `.blueprint/mockup/` |
| 设计系统预览 | `.blueprint/mockup/design-system.html` |
| 技术方案 | `.blueprint/Tech_Spec.md` |
| 测试方案 | `.blueprint/Test_Spec.md` |
| Mockup Review 报告 | `reports/mockup-reviews/` |
| Global Verify 报告 | `reports/verify/` |
| 测试运行报告 | `reports/test-runs/` |
| 开发计划 | `plans/[feature].md` |
| 问题追踪 | `issues/` |

---

## ⚠️ 最容易犯的错误

| 错误 | 正确做法 |
|-----|---------|
| 先写 UI Spec 再做 Mockup | 先基于 PRD 生成并确认 Mockup，再提炼 UI Spec |
| `/create-test-spec` 放到开发后运行 | Test Spec 必须在 `/execute` 之前 |
| 跳过 `/verify` 直接 `/create-plan` | verify 有阻塞项时代价最低，之后代价成倍增加 |
| `/execute` 只看 Plan，不读 Tech Spec | Mission Briefing 不可跳过，否则必然漂移 |
| PRD 迭代时直接覆盖文件 | 保留迭代历史，记录变更原因 |
| Mockup Review 报告只保留 LATEST | 每次生成带时间戳的版本，LATEST 只是索引 |

---

## 💡 上下文管理

- **开始任何命令前**：先读 `.blueprint/CONTEXT.md` 确认当前状态
- **完成任何命令后**：更新 `CONTEXT.md` 的流水线执行记录
- **做视觉探索时**：优先在 `/create-mockup` 和 `/create-ui-spec` 中使用 `ui-ux-pro-max`
- **上下文窗口过长时**：新开会话，只带 `.blueprint/CONTEXT.md` 入口文件
- **AI 偏离规格时**：指出具体偏差，引用文档章节，而不是重新描述需求

---

完整文档：`.cursor/commands/README.md`
