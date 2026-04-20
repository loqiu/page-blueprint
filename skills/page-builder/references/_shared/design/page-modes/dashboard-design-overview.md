# Dashboard 设计 — Overview / Analytics Mode

## 1. Purpose

本文档定义 overview 风格 dashboard 的设计规则。

当页面主要用于以下场景时，使用此模式：
- KPI summary
- trend review
- top-level health check
- business analysis
- executive or analyst overview

此模式不适用于：
- real-time monitoring walls
- heavy queue handling
- row-by-row operations workflow

---

## 2. Core Intent

页面应按以下顺序回答问题：
1. 正在发生什么？
2. 这是好还是坏？
3. 有什么变化？
4. 用户应该往哪里 drill down？

布局应优先考虑：
- scanability
- summary-first hierarchy
- visual calm
- obvious drill-down paths

---

## 3. Page Anatomy

推荐的自上而下顺序：
1. page title + date range / scope
2. filter bar
3. KPI summary row
4. trend and comparison region
5. secondary insight modules
6. detailed table / lower-priority breakdowns

除非页面明确是 table-first，否则不要把 raw tables 放在 summary region 之上。

---

## 4. Layout Rules

### KPI Row
- desktop 上每行放 3 到 6 个 KPI cards
- 每个 KPI card 应显示：
  - label
  - current value
  - delta
  - optional sparkline or context
- KPI cards 不应变成 mini dashboards

### Trend Region
- 最重要的 trend chart 应直接放在 KPI cards 下方
- 先使用一个 dominant chart，再放 secondary charts
- 避免让每个模块拥有相同的视觉权重

### Secondary Modules
典型的 secondary modules：
- segment breakdown
- funnel snapshot
- category comparison
- recent anomalies
- top movers

在需要时使用 2-column 或 asymmetric grid。

---

## 5. Information Density

此模式应给人这样的感受：
- efficient
- readable
- not cramped
- not decorative

密度规则：
- 默认中等密度
- 比 marketing page 更紧凑
- 比 operations console 更宽松

建议使用：
- 16px 到 24px 的 panel padding
- 20px 到 24px 的 major sections 间距
- moderate chart height
- concise labels

---

## 6. KPI Card Rules

每个 KPI card 只应包含：
- metric name
- current value
- comparison value or delta
- optional short context

不要让 KPI cards 过载以下内容：
- too many submetrics
- multiple chart types
- long paragraphs
- multiple competing actions

视觉优先级：
1. value
2. delta
3. label
4. context

---

## 7. Chart Rules

用 charts 展示：
- trend
- composition
- ranking
- change over time
- comparison across categories

规则：
- 每张图表只表达一个信息重点
- 标题必须解释清楚图中展示的内容
- legends 应简化
- 正负意义使用 semantic colors
- 每页避免出现多个 dominant chart color theme

不要使用：
- 没有决策价值的装饰性图表
- 在同一视图中使用过多 chart types
- 3D 或 novelty styling

---

## 8. Table Rules

overview 模式中的 tables 是次要载体。
它们应当：
- support drill-down
- confirm detail after summary
- show top entities, not everything at once

推荐用途：
- top 10 / top 20 lists
- latest issues
- biggest movers
- breakdown details after charts

---

## 9. Filters

overview dashboards 应使用克制的 filtering。

推荐 filters：
- time range
- business scope
- category / strategy / region / portfolio
- status when truly needed

不要：
- 用 advanced controls 塞满 top bar
- 把所有 possible filters 永久放在屏幕上

advanced filters 应使用 progressive disclosure。

---

## 10. States

### Empty
- 说明是没有数据，还是没有 matching data
- 保留页面 skeleton 和 hierarchy

### Error
- 尽可能隔离 failed modules
- 不要因为一个 chart failed 就让整个页面 collapse

### Loading
- 使用 skeleton cards 和 chart placeholders
- 在 loading 时保持 layout 稳定，避免 jumpiness

---

## 11. Interaction Rules

- cards 可以支持 click-through 到 detail views
- charts 应支持 hover details，但核心理解不能依赖 hover
- drill-down actions 必须明显
- 避免在 overview pages 内部做深层 nested tabs

---

## 12. Responsive Rules

Desktop:
- KPI row 应在首屏可见
- 一个 dominant chart region

Tablet:
- KPI cards 自动换行
- secondary modules 更积极地堆叠

Mobile:
- KPI cards 改为纵向列表或 compact carousel
- 在过度压缩之前先减少 charts 数量
- tables 转为 summarized lists
