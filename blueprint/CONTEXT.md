# Blueprint Context Index

> 这是 AI Agent 的入口文件。每次运行任何命令前，先读这个文件确认当前状态。
> 每个 Agent 命令完成后必须更新对应的状态和时间戳。

---

## 当前项目信息

**项目名称**: [项目名称]
**当前活跃大版本**: [待设置]
**PDLC 当前阶段**: [待设置]

---

## 文档状态

| 文档 | 文件路径 | 当前版本 | 状态 | 最后更新 | 负责人 |
|-----|---------|---------|------|---------|------|
| PRD | `.blueprint/PRD.md` / `.blueprint/PRD_V1.md` | 1.0 | ⚪ 待生成 | - | - |
| Mockup | `.blueprint/mockup/` | - | ⚪ 待生成 | - | - |
| Mockup Review | `reports/mockup-reviews/LATEST.md` | - | ⚪ 待生成 | - | - |
| UI Spec | `.blueprint/UI_Spec.md` | 1.0 | ⚪ 待生成 | - | - |
| Design System Preview | `.blueprint/mockup/design-system.html` | 1.0 | ⚪ 待生成 | - | - |
| Tech Spec | `.blueprint/Tech_Spec.md` | 1.0 | ⚪ 待生成 | - | - |
| Test Spec | `.blueprint/Test_Spec.md` | 1.0 | ⚪ 待生成 | - | - |
| Global Verify | `reports/verify/LATEST.md` | - | ⚪ 待运行 | - | - |
| Plan | `plans/[feature].md` | - | ⚪ 待生成 | - | - |

**状态说明**：⚪ 待生成 → 🟡 进行中 → 👀 待 Review → ✅ 已确认 → 📦 Archived


---

## AI 实现代码时，必读文件（按顺序）

1. **当前生效 PRD**（如 `.blueprint/PRD.md` 或 `.blueprint/PRD_V1.md`）— 读"📌 当前需求全貌"部分
2. **`.blueprint/AGENT_RUNTIME_PROTOCOL_V1.md`** — 统一 Runtime 协议、相位语义与结构化 `runtime` 契约
3. **`.blueprint/mockup/`** — 视觉基准（优先读 `index.html` 与 `design-system.html`）
4. **`.blueprint/UI_Spec.md`** — UI 规范（由确认版 Mockup 提炼）
5. **`.blueprint/Tech_Spec.md`** — 架构、数据模型、API 设计、src 结构
6. **`.blueprint/Test_Spec.md`** — 验收标准（编码时的完成边界）

---

## 流水线执行记录

| 步骤 | 命令 | 状态 | 完成时间 | 备注 |
|-----|-----|------|---------|------|
| 1. PM Agent（如需） | `/create-prd` | ⚪ | - | 若已有 PRD 可跳过 |
| 2. Mockup Agent | `/create-mockup` | ⚪ | - | 基于 PRD 直接生成 |
| 2a. Mockup Review + 人工确认 | `/review-mockup` | ⚪ | - | 迭代次数：0 |
| 3. UI Design Agent | `/create-ui-spec` | ⚪ | - | 同时生成 `design-system.html` |
| 4. Dev Agent | `/create-tech-spec` | ⚪ | - | - |
| 5. QA Agent | `/create-test-spec` | ⚪ | - | - |
| 6. Global Verifier | `/verify` | ⚪ | - | - |
| 7. Plan Agent | `/create-plan` | ⚪ | - | - |
| 8. Exe Agent | `/execute` | ⚪ | - | - |
| 9. Implementation Review | `/review` | ⚪ | - | - |
| 10. Test Exe | `/test` | ⚪ | - | - |

---

## 最近更新日志

```
YYYY-MM-DD  [步骤] [命令] — [做了什么，为什么]
```

---

## 历史版本

| 版本 | PRD | 状态 | 归档时间 |
|-----|-----|------|---------|
| V1 | `.blueprint/PRD_V1.md` | ⚪ Pending | - |
