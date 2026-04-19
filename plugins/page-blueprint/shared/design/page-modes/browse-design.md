# Browse / Discovery 设计

## 1. Purpose

本文档定义 browse / discovery 风格页面的设计规则。

当页面主要用于以下场景时，使用此模式：
- object browsing
- catalog or result discovery
- lightweight comparison
- narrowing a result set
- exploring entities before deeper inspection

此模式不适用于：
- KPI-first dashboards
- action-heavy queue handling
- one-object detail investigation

---

## 2. Core Intent

页面应按以下顺序回答问题：
1. 我正在浏览什么？
2. 结果范围是什么？
3. 如何缩小或排序？
4. 哪些对象值得进一步打开？

布局应优先考虑：
- scanability
- stable result comparison
- clear filtering
- obvious object identity

---

## 3. Page Anatomy

推荐的自上而下顺序：
1. page title + scope
2. filter / search bar
3. result summary
4. result surface
5. optional lightweight detail or supporting metadata

不要把 browse page 做成 dashboard。结果面必须是主角。

---

## 4. Layout Rules

### Result Surface
- 可使用 list、table、或 object-first card grid
- 哪种载体应由任务决定：
  - row comparison 强时用 list/table
  - object identity 与 visual grouping 更重要时用 cards

### Filters
- search、sort、category、status 等主筛选应靠近结果面
- advanced filters 应使用 progressive disclosure

### Supporting Panels
- supporting metadata 不应压过 result surface
- drawer / split view 适合轻量 inspection

---

## 5. Information Density

此模式应给人这样的感受：
- browseable
- readable
- not noisy
- not decorative

密度规则：
- 默认 low-medium
- 比 marketing page 更实用
- 比 operations console 更宽松

---

## 6. Result Rules

每个结果单元应优先表达：
1. identity
2. status or type
3. one or two comparison fields
4. next-step affordance

不要让结果单元过载：
- long descriptions
- too many badges
- too many equal-weight actions

---

## 7. Interaction Rules

- search, filter, sort 应明显
- object open action 应清楚
- lightweight inspection 优先于强制整页跳转
- selection context 和 filter context 在 drill-down 返回时应尽量保留

---

## 8. States

### Empty
- 说明是没有对象，还是当前筛选没有命中
- 保留 filter structure

### Error
- 不要让 result failure 抹掉整个页面 hierarchy

### Loading
- 保留 result skeleton 和 filter bar
- 不要在 loading 时打断用户对结果结构的预期

---

## 9. Responsive Rules

Desktop:
- result surface 保持主角
- filters 和 summary 靠近结果

Tablet:
- filters 更积极地折行
- supporting detail 可下移

Mobile:
- results 改为更紧凑的 list 或单列 cards
- 先保留筛选和结果，再考虑 supporting content
