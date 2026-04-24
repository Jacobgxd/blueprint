# UI Specification: Nuvante Clearing Platform

## 1. 元信息

| 项目 | 内容 |
|------|------|
| 产品名称 | Nuvante Clearing Platform |
| 基于 PRD | `PRD_Nuvante_Clearing_Platform.md` |
| 基于 Mockup | `.blueprint/mockup/index_ex.html` |
| 设计备注 | `.blueprint/mockup/design-notes.md` |
| 创建日期 | 2026-04-23 |
| 主题模式 | Light（浅色模式，桌面优先） |
| 风格关键词 | Clean Operational Dashboard · Light Gray Canvas · Professional · Data-Dense · Scannable |
| 产品定位 | 金融结算平台运营后台，面向 Member / Issuer / Admin 三种角色 |

---

## 2. 设计系统

### 2.1 Colors（色彩系统）

#### CSS 变量定义

```css
:root {
  /* 背景层 */
  --bg:           #F0F2F5;   /* 全局页面背景 - 浅灰 */
  --surface:      #FFFFFF;   /* 卡片/面板/侧边栏背景 - 纯白 */
  --border:       #E4E7EE;   /* 边框 / 分隔线 */

  /* 品牌主色 - Teal */
  --teal:         #0BBFB2;   /* 主色，按钮/激活状态/强调 */
  --teal-light:   #E6FAF8;   /* 主色浅色背景，激活导航 / Badge 背景 */
  --teal-dark:    #089C91;   /* 主色深色，Hover / ID文字 */

  /* 语义色 */
  --amber:        #F59E0B;   /* 警告 - 处理中 */
  --amber-light:  #FEF3C7;   /* 警告背景 */
  --red:          #EF4444;   /* 错误 - 失败 / 危险操作 */
  --red-light:    #FEE2E2;   /* 错误背景 */
  --green:        #10B981;   /* 成功 - 已完成 */
  --green-light:  #D1FAE5;   /* 成功背景 */
  --blue:         #3B82F6;   /* 信息 - 中性蓝 */
  --blue-light:   #DBEAFE;   /* 信息背景 */
  --purple:       #8B5CF6;   /* 辅助 - 紫色标签 */
  --purple-light: #EDE9FE;   /* 紫色背景 */

  /* 文字层级 */
  --text-primary:   #111827;  /* 主文字，标题/正文 */
  --text-secondary: #6B7280;  /* 次要文字，说明/标签 */
  --text-muted:     #9CA3AF;  /* 辅助文字，时间/元信息 */
}
```

#### 色彩用途速查

| Token | 颜色值 | 用途 |
|-------|--------|------|
| `--bg` | `#F0F2F5` | 全局背景、表格 TH 背景 |
| `--surface` | `#FFFFFF` | 卡片、侧边栏、顶栏、弹出层 |
| `--border` | `#E4E7EE` | 所有分隔线、边框线 |
| `--teal` | `#0BBFB2` | 主按钮、激活 Tab、Logo Icon、选中状态 |
| `--teal-dark` | `#089C91` | Hover 状态、ID 代码文字颜色 |
| `--teal-light` | `#E6FAF8` | 激活导航背景、Teal Badge 背景、角色标签背景 |
| `--text-primary` | `#111827` | 标题、正文、数值 |
| `--text-secondary` | `#6B7280` | 次要描述、表格列名 |
| `--text-muted` | `#9CA3AF` | 时间戳、元信息、占位文字 |
| `--green` | `#10B981` | 成功状态、正向增量 |
| `--red` | `#EF4444` | 失败/错误、负向增量、危险按钮 |
| `--amber` | `#F59E0B` | 处理中、警告 |
| `--blue` | `#3B82F6` | 信息提示、中性操作 |
| `--purple` | `#8B5CF6` | 辅助标签分类 |

---

### 2.2 Typography（字体系统）

#### 字体家族

```css
font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
/* ID / 代码字段使用 monospace */
font-family: 'Fira Code', monospace;
```

- **Inter**：全站主字体，适用于所有界面文字
- **Fira Code**：仅用于交易 ID、指令 ID 等代码类字段（提升可读性）

#### 字体层级

| 层级 | 元素 | 字号 | 字重 | 行高 | 颜色 |
|------|------|------|------|------|------|
| Page Title | 顶栏页面标题 | 16px | 700 | 1.5 | `--text-primary` |
| Card Title | 卡片标题 | 14px | 700 | 1.5 | `--text-primary` |
| Stat Value | 数据指标数字 | 28px | 700 | 1.0 | `--text-primary` |
| Body | 正文/列表内容 | 13px | 400–500 | 1.5 | `--text-primary` |
| Label / Meta | 次要说明/时间 | 11–12px | 400–500 | 1.5 | `--text-muted` |
| Section Header | 区块小标题 | 10–12px | 600 | 1.5 | `--text-muted` |
| Badge | 状态标签文字 | 11px | 600 | 1.6 | 各状态色 |
| Nav Item | 侧边导航文字 | 13px | 500 | 1.5 | `--text-secondary` |
| TH (表头) | 表格列名 | 11px | 600 | 1.5 | `--text-secondary` |
| Code | ID / 哈希值 | 12px | 400 | 1.5 | `--teal-dark` |

#### 字重使用规范

| 字重 | 用途 |
|------|------|
| 300 | 暂未使用 |
| 400 | 普通正文、描述文字 |
| 500 | Nav 菜单、Form Label、Transaction 对名称 |
| 600 | Badge、Section Title、表格字段、强调说明 |
| 700 | 页面标题、卡片标题、数据指标值、Logo |

---

### 2.3 Spacing（间距系统）

#### 基础单位

以 **4px** 为基本单位，通用间距序列：4 / 8 / 12 / 16 / 20 / 24 / 32

#### 页面级间距

| 区域 | 数值 |
|------|------|
| 侧边栏宽度 | 220px（折叠后 60px） |
| 顶栏高度 | 56px |
| 页面内容区 padding | 24px（四边） |
| 卡片间 Gap | 16px |
| 区块间 Gap | 20px |

#### 组件内间距

| 组件 | 内边距 |
|------|--------|
| Card Header | 16px 20px |
| Card Body | 16px 20px |
| Stat Card | 18px 20px |
| Table TH | 10px 16px |
| Table TD | 11px 16px |
| Button (默认) | 8px 16px |
| Button (sm) | 5px 12px |
| Form Control | 8px 12px |
| Nav Item | 9px 16px |
| Badge | 3px 10px |
| Alert | 10px 16px |
| Detail Panel | 20px 24px |

#### 间距 Token（CSS Utility）

```css
.mb-1 { margin-bottom: 4px; }
.mb-2 { margin-bottom: 8px; }
.mb-3 { margin-bottom: 12px; }
.mb-4 { margin-bottom: 16px; }
.mb-5 { margin-bottom: 20px; }
.gap-2 { gap: 8px; }
.gap-3 { gap: 12px; }
```

---

### 2.4 Radius（圆角系统）

```css
--radius-sm: 8px;   /* 按钮、输入框、图标按钮、小卡片 */
--radius-md: 12px;  /* 普通卡片、Stat Card */
--radius-lg: 16px;  /* 暂定大圆角场景 */
```

| 场景 | 值 |
|------|-----|
| 按钮 | `--radius-sm` (8px) |
| 输入框 / Select | `--radius-sm` (8px) |
| 图标按钮 | `--radius-sm` (8px) |
| 卡片 | `--radius-md` (12px) |
| Stat Card | `--radius-md` (12px) |
| Badge / Tab | `20px`（全圆角 pill 形） |
| Stat Icon | `10px` |
| Logo Icon | `8px` |
| User Avatar | `50%`（圆形） |
| Timeline Dot | `50%`（圆形） |
| Sidebar Role Tag | `--radius-sm` (8px) |

---

### 2.5 Shadows（阴影系统）

```css
--shadow-sm: 0 1px 3px rgba(0,0,0,.08), 0 1px 2px rgba(0,0,0,.05);
--shadow-md: 0 4px 12px rgba(0,0,0,.08);
```

| 场景 | 阴影 |
|------|------|
| 普通卡片 | `--shadow-sm` |
| 浮层 / Detail Panel | `-8px 0 32px rgba(0,0,0,.12)` |
| 弹窗遮罩背景 | `rgba(0,0,0,.35)` |
| Timeline Active Dot | `0 0 0 4px var(--teal-light)` |

---

### 2.6 Borders（边框规范）

- **全局统一**：`1px solid var(--border)`（`#E4E7EE`）
- **激活导航**：`border-left: 3px solid var(--teal)`
- **Alert 边框**：各状态色系（amber / red / blue）
- **Danger Button**：`1px solid #FCA5A5`
- **Sidebar / Topbar**：`1px solid var(--border)`（与 surface 的分隔）

---

### 2.7 Effects（视觉效果）

- **过渡动画**：全站统一使用 `transition: all 0.15s`（150ms），感知流畅
- **Hover 背景**：常用 `var(--bg)` 或 `var(--border)` 轻微填色
- **Pulse 动效**：`animation: pulse 2s infinite`，用于实时数据/活跃状态指示
- **Overlay 背景**：`rgba(0,0,0,.35)` 遮罩
- **不使用**：毛玻璃（backdrop-filter）、大型阴影、渐变背景 —— 本产品为运营后台，保持克制

---

## 3. 页面规范

### 3.1 全局布局（Shell）

```
┌─────────────────────────────────────────────────────────┐
│ Sidebar (220px fixed)  │  Topbar (56px sticky)          │
│                        ├─────────────────────────────────┤
│  Logo                  │  Content Area (padding: 24px)   │
│  Role Badge            │                                 │
│  Nav Items             │  页面具体内容                    │
│  ────                  │                                 │
│  User Footer           │                                 │
└────────────────────────┴─────────────────────────────────┘
```

- **Sidebar**：固定宽 220px，背景 `--surface`，右侧 1px 边框
- **Topbar**：高 56px，粘性顶部，包含页面标题 + 搜索框 + 操作区
- **Content**：`margin-left: 220px`，内边距 24px

---

### 3.2 Member 看板（`/member`）

**目标**：成员发起 Mint/Redeem 指令，查看历史交易状态

**布局结构**：
1. 顶部：4 列统计卡片（Stats Grid）
2. 主区：2 列（左 1fr 右 1fr），左为指令发起表单卡 + 交易列表，右为 RTGS 账户 + 活动流
3. 关键交互：新指令弹出面板（右侧 Drawer）、状态轮询更新

**首屏重点**：
- 显示当前余额 / 已完成 / 处理中数量
- 指令发起按钮（主 CTA）在卡片头部

**视觉特征**：
- Stats 数字大而清晰（28px 700）
- 交易列表行 Hover 背景延伸 + 圆角
- Teal Badge 标识 Mint，Amber Badge 标识处理中

---

### 3.3 Transaction 详情页（`/member/transactions/:id`）

**目标**：展示单笔交易完整流程与元信息，支持取消操作

**布局结构**：
1. 顶部：状态大 Badge + 交易 ID（monospace）
2. 左侧主栏：元信息表（Meta Row 列表）
3. 右侧侧栏：Timeline 交易流程步骤
4. 底部：取消按钮（按状态启用/禁用）

**Timeline 状态**：
- Done：绿色圆点 + 绿色背景
- Active：Teal 圆点 + 发光 ring
- Pending：灰色虚线圆点
- Failed：红色圆点

---

### 3.4 Issuer 看板（`/issuer`）

**目标**：发行方查看供应量、储备、交易活动，处理 Model 2 待处理操作

**布局结构**：
1. 顶部：Stats Grid（供应量、储备、待处理指令等）
2. 中部：1.5fr + 1fr 两列（左为交易活动图表/列表，右为待处理动作面板）
3. 右侧面板：Model 2 批准/拒绝操作列表

**特殊要求**：
- 储备充足率使用绿色显示，低于阈值用红/橙
- 待处理动作需明确数量 Badge（红色 Notification）

---

### 3.5 Admin 控制台（`/admin`）

**目标**：全局运营视图，展示系统指标、队列状态、暂停控制、趋势图

**布局结构**：
1. Stats Grid：全局指标总览（6 指标）
2. 队列表格：支持多列排序与状态过滤
3. 右侧控制面板：Pause/Resume 系统级操作（危险操作用 `btn-danger`）
4. 趋势图区域：折线图或柱状图（SVG 内联）

**注意**：
- Pause 操作写入 Audit Log
- 系统暂停状态用 Amber Alert Banner 全局展示

---

### 3.6 Audit Log 页面（`/admin/audit-log`）

**目标**：支持过滤与检索的完整审计记录，用于合规与排查

**布局结构**：
1. 顶部过滤栏：Actor / Event Type / Reference / 时间范围（form-row 水平排列）
2. 主体：表格（带排序、分页）
3. 行内：Actor Avatar（圆形）、Event 类型 Badge、Reference ID（monospace）

**扫描性要求**：
- 表头大写 + 字间距
- 行 Hover 高亮
- ID 字段 monospace Teal 色

---

## 4. 组件规范

### 4.1 Button

| 变体 | 背景 | 文字 | Hover |
|------|------|------|-------|
| `btn-primary` | `--teal` | `#fff` | `--teal-dark` |
| `btn-secondary` | `--bg` | `--text-primary` | `--border` |
| `btn-danger` | `--red-light` | `--red` | `#FECACA` 加深 |
| `btn-ghost` | 透明 | `--text-secondary` | `--bg` |
| `btn-sm` | 同上 | 同上，font-size 12px | 同上 |

**通用规则**：
- `padding: 8px 16px`，`font-size: 13px`，`font-weight: 600`
- `border-radius: --radius-sm`（8px）
- `transition: all 0.15s`
- `cursor: pointer`
- 图标与文字 `gap: 6px`，图标建议 14×14

---

### 4.2 Card

```css
.card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);    /* 12px */
  box-shadow: var(--shadow-sm);
}
```

- **Card Header**：`padding: 16px 20px 12px`，下方 1px 分隔线，flex 两端对齐
- **Card Body**：`padding: 16px 20px`
- **Card Title**：14px / 700，与左侧图标 `gap: 8px`

---

### 4.3 Stat Card

- 背景 `--surface`，圆角 `--radius-md`，阴影 `--shadow-sm`
- `padding: 18px 20px`
- **指标值**：28px / 700 / `--text-primary`（大而克制）
- **指标标签**：12px / 500 / `--text-secondary`
- **子文字**：11px / `--text-muted`
- **增减量**：11px / 600，正增长 `--green`，负增长 `--red`
- **图标区域**：40×40px，`border-radius: 10px`，各色系背景（teal/amber/blue/green）

---

### 4.4 Badge（状态标签）

```css
.badge {
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: .3px;
  text-transform: uppercase;
}
```

| 变体 | 背景 | 文字颜色 | 语义 |
|------|------|----------|------|
| `badge-teal` | `--teal-light` | `--teal-dark` | Mint / 活跃 |
| `badge-green` | `--green-light` | `#065F46` | 完成 / 成功 |
| `badge-amber` | `--amber-light` | `#92400E` | 处理中 / 待处理 |
| `badge-red` | `--red-light` | `#991B1B` | 失败 / 错误 |
| `badge-blue` | `--blue-light` | `#1E40AF` | 信息 / 中性 |
| `badge-purple` | `--purple-light` | `#5B21B6` | 辅助分类 |
| `badge-gray` | `#F3F4F6` | `#374151` | 禁用 / 中性 |

**带圆点变体**：`.badge-dot::before` 插入与文字同色的 6px 圆点，用于状态可扫描性

---

### 4.5 Tabs

- 容器：`display: flex; gap: 4px`
- Tab 项：`padding: 5px 14px`，`border-radius: 20px`（Pill 形），`font-size: 12px / 500`
- **默认**：文字 `--text-secondary`，透明背景
- **Hover**：背景 `--bg`
- **Active**：背景 `--teal`，文字 `#fff`，边框 `--teal`

---

### 4.6 Input / Select

```css
.form-control {
  padding: 8px 12px;
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  font-size: 13px;
  background: var(--surface);
  transition: border-color .15s;
}
.form-control:focus { border-color: var(--teal); }
```

- **Form Label**：11px / 600 / `--text-secondary`，uppercase，`letter-spacing: .4px`
- **Form Row**：水平 flex，`gap: 12px`，`flex-wrap: wrap`
- **Focus**：边框变 `--teal`，无 outline
- **Placeholder**：`--text-muted`

---

### 4.7 Table

```css
th {
  padding: 10px 16px;
  font-size: 11px; font-weight: 600;
  color: var(--text-secondary);
  text-transform: uppercase; letter-spacing: .5px;
  background: var(--bg);
  border-bottom: 1px solid var(--border);
}
td {
  padding: 11px 16px;
  font-size: 13px;
  border-bottom: 1px solid var(--border);
}
tr:hover td { background: #FAFAFA; cursor: pointer; }
```

- ID 列使用 `.id-code`（Fira Code，12px，`--teal-dark`）
- 最后一行无下边框
- 必须用 `overflow-x: auto` 包裹防溢出

---

### 4.8 Sidebar（导航侧边栏）

- **宽度**：220px（折叠态 60px）
- **背景**：`--surface`
- **区块**：Logo 区、角色 Badge 区、Nav Group、User Footer
- **Nav Item 激活**：`border-left: 3px solid --teal`，背景 `--teal-light`，文字 `--teal-dark`
- **Nav Item Hover**：背景 `--bg`，文字 `--text-primary`
- **角色标签**：`--teal-light` 背景，`--teal-dark` 文字，`--radius-sm` 圆角
- **Nav Badge（通知红点）**：红色 Pill，`font-size: 10px`，`margin-left: auto`

---

### 4.9 Topbar

- 高度：56px，sticky top:0，z-index:50
- 背景：`--surface`，底部 `1px solid --border`
- 内边距：`0 24px`
- 包含：左侧页面标题（16px/700）、右侧搜索框 + 图标按钮
- **搜索框**：宽 220px，背景 `--bg`，边框 `--border`，`--radius-sm`
- **图标按钮**：36×36px，背景 `--bg`，边框 `--border`，Hover 背景 `--border`
- **通知红点**：相对定位，7px 红色圆，带白色 1px 描边

---

### 4.10 Timeline

| 状态 | 圆点样式 |
|------|---------|
| Done | `--green-light` 背景 + `--green` 图标 |
| Active | `--teal-light` 背景 + `--teal` 图标 + `0 0 0 4px --teal-light` ring |
| Pending | `--bg` 背景 + `--text-muted` + `2px --border` 描边 |
| Failed | `--red-light` 背景 + `--red` 图标 |

- 圆点尺寸：28×28px，圆形
- 连接线：2px 宽，`--border` 色，`min-height: 24px`
- Title：13px / 600 / `--text-primary`
- Description：12px / `--text-secondary`
- Time：11px / `--text-muted`

---

### 4.11 Alert Banner

| 变体 | 背景 | 文字 | 边框 |
|------|------|------|------|
| `alert-warning` | `--amber-light` | `#92400E` | `#FCD34D` |
| `alert-error` | `--red-light` | `#991B1B` | `#FCA5A5` |
| `alert-info` | `--blue-light` | `#1E40AF` | `#93C5FD` |

- `padding: 10px 16px`，`border-radius: --radius-sm`，`margin-bottom: 16px`

---

### 4.12 Detail Panel（Drawer）

- **宽度**：480px，右侧弹出
- **背景**：`--surface`
- **遮罩**：`rgba(0,0,0,.35)`
- **阴影**：`-8px 0 32px rgba(0,0,0,.12)`
- **Header**：sticky top:0，24px 内边距，底部边框
- **Close Button**：32×32px，`--radius-sm`，`--bg` 背景
- **Meta Row**：`justify-content: space-between`，`padding: 8px 0`，底部边框

---

### 4.13 Transaction List Item

- `padding: 12px 0`，底部边框
- **Hover**：背景 `--bg`，左右各 -20px 延伸 + `padding-left/right: 20px`，`border-radius: 4px`
- 图标区：36×36px，`border-radius: 10px`，各语义色背景
- 主信息：13px / 600
- 元信息：11px / `--text-muted`

---

### 4.14 Empty State

- 垂直居中，文字/图标居中对齐
- `padding: 40px 20px`
- SVG 图标：`opacity: .4`
- 文字：13px / `--text-muted`

---

## 5. 交互规则

### 5.1 Hover 规范

| 场景 | 效果 |
|------|------|
| 导航 Item | 背景变 `--bg`，文字变 `--text-primary` |
| 按钮 Primary | 背景变 `--teal-dark` |
| 按钮 Secondary | 背景变 `--border` |
| 图标按钮 | 背景变 `--border` |
| 表格行 | 背景变 `#FAFAFA`，`cursor: pointer` |
| 交易列表行 | 背景延伸（负 margin），圆角 4px |
| Close Button | 背景变 `--border` |

### 5.2 Focus 规范

- Form Input Focus：`border-color: var(--teal)`，无 outline（保留视觉焦点）
- 按钮等可聚焦元素：应补充 `:focus-visible` 样式（补充规则，Mockup 未明确）
- Focus 颜色需使用 `--teal`，与品牌主色一致

### 5.3 Active / Selected 状态

- Nav Item：左侧 3px `--teal` 描边 + `--teal-light` 背景
- Tab：`--teal` 背景 + 白色文字
- Role Button：`--teal` 背景 + 白色文字

### 5.4 Disabled 状态

- 按钮：透明度降低，`cursor: not-allowed`（补充规则）
- 取消按钮：Settlement 边界后禁用（业务规则，参见 PRD）

### 5.5 Loading 状态

- 系统等待超过 300ms：展示 Spinner 或 Skeleton
- 提交成功/失败：Toast 反馈（补充规则）

### 5.6 动效节奏

- **统一**：`transition: all 0.15s`（150ms）
- **进入动画**：`ease-out`；退出动画：`ease-in`
- **Pulse**：`pulse 2s infinite`，仅用于数据刷新/实时状态指示
- **Reduced Motion**：需添加 `@media (prefers-reduced-motion: reduce)` 禁用动效（补充规则）

---

## 6. 响应式规则

### 6.1 断点

| 断点 | 宽度 | 行为 |
|------|------|------|
| Desktop（默认） | > 1200px | 全功能展示，4 列 Stats Grid |
| Tablet | 900px–1200px | Stats Grid 变 2 列，部分双栏变单列 |
| Collapsed Sidebar | < 900px | 侧边栏折叠为 60px，隐藏文字/标签 |
| Stack Layout | < 900px | `grid-3-2` / `grid-2-3` 变单列 |
| Mobile | < 600px | 隐藏侧边栏，`main margin-left: 0`，Stats 变单列 |

### 6.2 响应式行为细节

| 组件 | < 900px | < 600px |
|------|---------|---------|
| Sidebar | 折叠为 60px，隐藏文字 | 完全隐藏 |
| Stats Grid | 2 列 | 1 列 |
| `grid-3-2` / `grid-2-3` | 单列 | 单列 |
| 表格 | `overflow-x: auto` | `overflow-x: auto` |
| Topbar | 保持不变 | 建议隐藏搜索框（补充规则） |

### 6.3 移动端设计原则（补充规则）

> 当前 Mockup 为桌面优先，以下为基于最佳实践的补充建议：

- 移动端导航使用底部 Tab Bar 或 Hamburger 菜单
- 数据密集型页面（表格、Timeline）优先展示核心字段，次要信息折叠
- 触摸目标最小 44×44px

---

## 7. 可访问性要求

### 7.1 对比度

| 组合 | 对比度 | 是否达标 |
|------|--------|---------|
| `--text-primary` (#111827) on `--surface` (#FFF) | ≈ 16:1 | ✅ |
| `--text-secondary` (#6B7280) on `--surface` (#FFF) | ≈ 5.7:1 | ✅ |
| `--teal-dark` (#089C91) on `--teal-light` (#E6FAF8) | ≈ 3.9:1 | ⚠ 仅用于非正文（Badge） |
| Badge 文字颜色均在浅色背景上 | 需逐一验证 | 建议验证 |

### 7.2 键盘可达性

- 所有交互元素（按钮、链接、Nav Item）需可 Tab 聚焦
- Focus 样式需可见（补充 `:focus-visible` outline）
- Detail Panel 打开时需 Focus Trap

### 7.3 语义化 HTML

- 使用语义标签：`<nav>`、`<main>`、`<header>`、`<table>`（`<thead>/<tbody>`）
- 表单字段必须有对应 `<label>`
- 图标（SVG）如有含义需加 `aria-label`；纯装饰 SVG 加 `aria-hidden="true"`

### 7.4 ARIA 最低要求

- 弹出 Drawer：`role="dialog"`, `aria-modal="true"`, `aria-label`
- Alert Banner：`role="alert"`
- 加载状态：`aria-busy="true"`
- Badge / Status：`aria-label` 补充（屏幕阅读器友好）

---

## 8. 开发指导

### 8.1 必须忠实还原的视觉

- 色彩变量体系（所有颜色必须使用 CSS 变量）
- Badge 的颜色与语义对应关系
- Timeline 各状态的视觉表现
- Stat Card 的数字大小与信息层级
- 侧边栏激活状态（左侧边框 + 背景色）
- 表格 TH 的样式（大写 + 字间距 + 浅灰背景）

### 8.2 可合理抽象的部分

- 组件可按工程需要封装为 React/Vue 组件
- CSS 变量可迁移为 Tailwind 主题配置或 CSS-in-JS token
- Grid 布局可用 Tailwind Grid 类替代
- Icon 统一使用 Heroicons 或 Lucide（不使用 emoji）

### 8.3 Mock 数据说明

Mockup 中以下内容为示意性 Mock 数据，实际实现中需替换为 API 数据：
- 所有金额、数量、指标数值
- Transaction ID、Instruction ID 等 ID 字段
- 用户名、角色信息
- 时间戳

### 8.4 优先抽象为复用组件

- `StatCard` — 高频使用，4 变体（teal/amber/blue/green）
- `Badge` — 覆盖 7 种状态颜色
- `Card` / `CardHeader` / `CardBody` — 全站容器
- `Timeline` — 交易流程通用
- `DetailPanel` (Drawer) — 通用右侧弹出面板
- `MetaRow` — 详情页键值对行
- `AlertBanner` — 3 种语义
- `DataTable` — 带排序/过滤的通用表格

### 8.5 设计 Token 映射（迁移至 React/Tailwind）

```js
// tailwind.config.js 示例
theme: {
  colors: {
    bg: '#F0F2F5',
    surface: '#FFFFFF',
    border: '#E4E7EE',
    teal: { DEFAULT: '#0BBFB2', light: '#E6FAF8', dark: '#089C91' },
    amber: { DEFAULT: '#F59E0B', light: '#FEF3C7' },
    red: { DEFAULT: '#EF4444', light: '#FEE2E2' },
    green: { DEFAULT: '#10B981', light: '#D1FAE5' },
    blue: { DEFAULT: '#3B82F6', light: '#DBEAFE' },
    purple: { DEFAULT: '#8B5CF6', light: '#EDE9FE' },
    text: { primary: '#111827', secondary: '#6B7280', muted: '#9CA3AF' }
  },
  borderRadius: {
    sm: '8px', md: '12px', lg: '16px'
  },
  boxShadow: {
    sm: '0 1px 3px rgba(0,0,0,.08), 0 1px 2px rgba(0,0,0,.05)',
    md: '0 4px 12px rgba(0,0,0,.08)'
  }
}
```

---

## 9. 附录

### 9.1 Mockup 路径

- 确认版 Mockup：`.blueprint/mockup/index_ex.html`
- 参考 Mockup：`.blueprint/mockup/index.html`
- 设计备注：`.blueprint/mockup/design-notes.md`

### 9.2 设计关键词

`Clean Operational Dashboard` · `Light Gray Canvas` · `Teal Accent` · `Data-Dense` · `Scannable` · `Professional Fintech` · `Low Decoration` · `Status-Driven UI`

### 9.3 ui-ux-pro-max 检索摘要

| 检索 | 结论 |
|------|------|
| `fintech clearing platform dashboard professional` | 匹配 Glassmorphism + Fira Code 字体 + 专业蓝色系，但本产品已使用 Inter + Teal 系，以 Mockup 为准 |
| `data table status badge filter dashboard` | 确认表格需 `overflow-x: auto`，状态提交需有加载/成功反馈 |
| `animation accessibility` | 需添加 `prefers-reduced-motion`，Pulse 动效仅用于加载指示 |

---

> **最后更新**：2026-04-23  
> **基于**：已确认 Mockup `index_ex.html`（Nuvante Clearing Platform v0.2）
