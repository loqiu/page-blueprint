# 全局设计系统

## 1. Purpose

本文档定义整个产品共享的全局视觉与交互基础。

它的存在是为了让产品保持：
- 一致
- 专业
- 可扩展
- 便于工程师和 AI agents 实现

本文档规范以下内容：
- tokens
- typography
- color semantics
- spacing
- radius
- shadows
- motion
- component baselines
- shared state patterns
- accessibility minimums

本文档不定义以下页面的页面级布局模式：
- dashboards
- detail pages
- browse/discovery pages
- admin workflows

这些内容应由页面模式文档定义。

---

## 2. Product Tone

产品应给人这样的感受：

- 精准
- 可信
- 现代
- 冷静
- 高效
- 视觉整洁
- 具备数据能力但不显得冰冷

视觉语言原则：
- 克制地使用颜色
- 层级优先于装饰
- 有意识地使用留白
- 清晰优先于新奇
- 在所有业务关键视图中保持专业感

---

## 3. Design Tokens

### 3.1 Color Tokens

#### Neutral
- `--color-bg-page`: `#ffffff`
- `--color-bg-subtle`: `#f7f7f8`
- `--color-bg-muted`: `#f2f3f5`
- `--color-surface`: `#ffffff`
- `--color-surface-hover`: `#fafafa`
- `--color-border-default`: `#e6e8ec`
- `--color-border-strong`: `#d0d5dd`

#### Text
- `--color-text-primary`: `#1f2328`
- `--color-text-secondary`: `#667085`
- `--color-text-tertiary`: `#98a2b3`
- `--color-text-disabled`: `#b3b8c2`
- `--color-text-inverse`: `#ffffff`

#### Brand
- `--color-brand-primary`: `#ff385c`
- `--color-brand-primary-hover`: `#e31c5f`
- `--color-brand-primary-soft`: `#fff1f4`

#### Semantic
- `--color-success`: `#16a34a`
- `--color-success-soft`: `#ecfdf3`
- `--color-warning`: `#d97706`
- `--color-warning-soft`: `#fffbeb`
- `--color-danger`: `#dc2626`
- `--color-danger-soft`: `#fef2f2`
- `--color-info`: `#2563eb`
- `--color-info-soft`: `#eff6ff`

#### Data / Delta
- `--color-positive`: `#16a34a`
- `--color-negative`: `#dc2626`
- `--color-neutral-change`: `#64748b`

#### Focus
- `--color-focus-ring`: `rgba(37, 99, 235, 0.35)`

---

### 3.2 Typography Tokens

#### Font Families
- `--font-sans`: `Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`
- `--font-mono`: `"JetBrains Mono", "SFMono-Regular", Consolas, monospace`

#### Type Scale
- `--text-display-lg`: 32px / 40px / 700
- `--text-display-md`: 28px / 36px / 700
- `--text-title-lg`: 24px / 32px / 700
- `--text-title-md`: 20px / 28px / 600
- `--text-title-sm`: 18px / 26px / 600
- `--text-body-lg`: 16px / 24px / 400
- `--text-body-md`: 14px / 22px / 400
- `--text-body-sm`: 13px / 20px / 400
- `--text-label-md`: 14px / 20px / 500
- `--text-label-sm`: 12px / 18px / 500
- `--text-caption`: 12px / 16px / 400
- `--text-micro`: 11px / 14px / 500

#### Numeric Rules
- 重要指标在可能时应使用等宽数字
- 价格、数量、百分比、时间戳和类似 PnL 的数值在视觉上应对齐
- 在密集数据表中，必要时应使用等宽字体或等宽数字样式

---

### 3.3 Spacing Tokens

基础单位：4px

- `--space-1`: 4px
- `--space-2`: 8px
- `--space-3`: 12px
- `--space-4`: 16px
- `--space-5`: 20px
- `--space-6`: 24px
- `--space-8`: 32px
- `--space-10`: 40px
- `--space-12`: 48px
- `--space-16`: 64px

用法：
- 默认 UI 节奏使用 8px 和 16px
- 区块分隔使用 24px 和 32px
- 除非布局有明确理由，否则避免任意设置间距值

---

### 3.4 Radius Tokens

- `--radius-xs`: 4px
- `--radius-sm`: 8px
- `--radius-md`: 12px
- `--radius-lg`: 16px
- `--radius-xl`: 20px
- `--radius-pill`: 999px

用法：
- 表单控件：8px
- 卡片/面板：12px 到 16px
- 大型功能容器：16px 到 20px
- pills/badges：pill 或 999px

---

### 3.5 Shadow Tokens

- `--shadow-0`: none
- `--shadow-1`: `0 1px 2px rgba(16, 24, 40, 0.06)`
- `--shadow-2`: `0 4px 12px rgba(16, 24, 40, 0.08)`
- `--shadow-3`: `0 8px 24px rgba(16, 24, 40, 0.12)`

用法：
- 卡片和面板默认使用 shadow-1，或无阴影加边框
- 模态框/抽屉可使用 shadow-2
- 在数据密集视图中避免使用强装饰性阴影

---

### 3.6 Border Tokens

- `--border-default`: `1px solid var(--color-border-default)`
- `--border-strong`: `1px solid var(--color-border-strong)`

在增加更强阴影之前，优先用边框建立结构。

---

### 3.7 Motion Tokens

- `--motion-fast`: `120ms`
- `--motion-base`: `180ms`
- `--motion-slow`: `240ms`

规则：
- 过渡应让人感觉响应迅速，而不是轻佻
- 动效应服务于清晰性，而不是装饰
- 在 dashboards 和高密度业务工具中避免大幅运动

---

### 3.8 Layer Tokens

- `--z-base`: 0
- `--z-dropdown`: 100
- `--z-sticky`: 200
- `--z-overlay`: 400
- `--z-modal`: 500
- `--z-toast`: 700
- `--z-tooltip`: 800

---

## 4. Semantic Rules

### Status Color Usage
- success：完成、健康、正向结果
- warning：延迟、部分完成、有风险、警示状态
- danger：失败、严重、破坏性、不健康
- info：中性的系统引导、信息提示状态
- brand：仅用于主要 CTA 和选中的产品强调

不要用品牌色替代语义状态色。

---

## 5. Layout Foundations

### Content Width
- 标准内容最大宽度：1440px
- 高密度企业界面在合适时可使用更宽布局

### Grid
- 使用 12-column 布局作为默认桌面栅格
- tablet/mobile 可收缩为 8-column 和 4-column 的布局心智模型

### Section Rhythm
- 页面区块间距：24px 到 32px
- 面板内部间距：16px 到 24px
- 紧凑布局可将内部间距缩小到 12px

---

## 6. Component Baselines

### Buttons
- primary button 根据上下文使用品牌色或接近深色的强调样式
- 默认高度：36px 到 40px
- 默认圆角：8px
- labels 使用 label-md token
- focus 必须显示可见 ring
- 破坏性操作使用 danger 语义样式

### Inputs
- 默认高度：36px 到 40px
- 优先使用边框优先的样式
- 使用清晰的 hover/focus 过渡
- focus 必须使用可见 ring
- invalid state 必须使用 danger 语义样式

### Cards / Panels
- 默认背景：surface
- 默认边框：border-default
- 圆角：12px 到 16px
- 只有在需要增强分隔感时才使用轻阴影
- 在数据密集页面中，优先使用边框加轻微填充，而不是强烈悬浮感

### Badges / Tags
- 使用语义化背景和文字
- 紧凑且易读
- 除非设计上就是可交互元素，否则不要变成迷你按钮

### Tabs
- 应传达结构，而不是装饰
- 激活状态必须明显
- 没有明确目的时，不要混用 tabs 和 pills

### Tables
- 必须使用清晰的行分隔，或轻度 zebra 结构
- 数值列在适当时右对齐
- 表头层级必须始终强于表体层级

---

## 7. Shared State Patterns

每个重要流程都必须定义：
- loading
- skeleton
- empty
- error
- success
- stale/outdated
- disabled
- permission-restricted

### Loading
- 内容较重的区域使用 skeleton
- spinner 只用于小范围或不确定时长的等待

### Empty
- 解释为什么当前状态为空
- 在可能时提供下一步动作

### Error
- 说明失败了什么
- 提供恢复建议
- 避免脱离上下文地使用笼统的“something went wrong”

### Disabled
- 禁用控件仍须保持可读
- 禁用状态不应成为表达无权限或缺少前置条件的唯一方式

---

## 8. Accessibility Rules

- 文字对比度必须满足可访问性的对比要求
- 焦点状态必须始终可见
- 可点击目标应足够大，便于舒适操作
- 图表不能只依赖颜色表达
- 所有关键图标都应有文字标签或可访问名称
- 主要工作流必须支持键盘交互

---

## 9. Responsive Principles

- 有意识地分别设计 mobile、tablet 和 desktop
- 不要只是简单缩小 desktop 布局
- 逐步折叠复杂度
- 在小屏幕上保持核心操作可见
- 高密度数据在完整 tables 之前，可先转为堆叠摘要

---

## 10. Engineering Contract

- 在可能时使用 tokens，而不是硬编码值
- 新组件应优先映射到 token 名称，而不是临时写 CSS 值
- 语义状态色必须来自 semantic tokens
- 页面级文档可以细化布局，但不能随意重定义 global tokens
- 如果页面需要新增 token，必须说明为什么不能复用已有 token

---

## 11. Page Mode References

本文档由以下页面模式文档扩展：
- `dashboard-design-overview.md`
- `dashboard-design-monitoring.md`
- `dashboard-design-operations.md`
- `detail-design.md`
- `browse-design.md`
