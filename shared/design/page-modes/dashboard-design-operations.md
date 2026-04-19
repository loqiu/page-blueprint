# Dashboard 设计 — Operations / Workflow Mode

## 1. Purpose

本文档定义 operations 风格 dashboard 的设计规则。

当页面主要用于以下场景时，使用此模式：
- queue handling
- execution management
- candidate review
- proposal review
- workflow progression
- task-based operations
- table-first operational decision making

此模式不主要用于：
- executive KPI storytelling
- real-time health walls
- browse/discovery experiences

---

## 2. Core Intent

页面应按以下顺序回答问题：
1. 哪些项目需要操作？
2. 哪些项目最重要？
3. 每个项目当前处于什么状态？
4. 我下一步能做什么？
5. 我怎样在不丢失上下文的情况下查看详情？

此模式优先考虑：
- task completion
- list clarity
- state visibility
- bulk efficiency
- detail-on-demand

---

## 3. Visual Tone

operations dashboards 应给人这样的感受：
- structured
- efficient
- controllable
- less decorative
- table-capable
- action-oriented

与 overview mode 相比：
- 更高密度
- 更受 grid 驱动
- 更少强调 large charts
- 更强调 status、rows 和 actions

---

## 4. Page Anatomy

推荐的自上而下顺序：
1. page title + scope
2. primary filters + search + quick actions
3. summary counts / pipeline strip
4. main table or list
5. side detail / drawer / expandable row / lower detail region
6. history / audit / related records

main working surface 通常是 table/list，而不是 KPI row。

---

## 5. Filter and Toolbar Rules

operations pages 需要强 control surfaces。

推荐 toolbar elements：
- search
- status filter
- owner / assignee filter
- type/category filter
- date range when relevant
- saved views
- bulk actions when allowed

规则：
- primary controls 保持可见
- advanced controls 可收进 secondary filter panel
- 避免在视觉上埋没 search 或 status controls

---

## 6. Summary Strip

在 table 上方使用 compact summary strip 展示：
- total items
- pending items
- blocked items
- failed items
- completed items
- SLA / freshness / workload stats（在有帮助时）

这条 summary strip 应服务于 orientation，而不是替代表格工作区。

---

## 7. Table / List Rules

table 是主要 operating surface。

每一行都应让人容易理解：
- identity
- state
- priority
- owner
- time/freshness
- next action 或 action entry point

规则：
- row hierarchy 必须清晰
- critical columns 保持可见
- status columns 必须易于扫描
- numeric 和 time columns 保持一致对齐
- row actions 不应在视觉上压过 row identity

在有帮助时使用 sticky headers。

---

## 8. Detail-on-Demand

operations pages 应避免每次 inspection 都强制 full page navigation。

推荐的 detail patterns：
- side drawer
- split view
- expandable row
- lower detail panel
- detail page link（当 investigation 很深时）

目标：
- 在不丢失 queue context 的前提下查看某个 item

---

## 9. Action Rules

操作应清晰且安全。

主要 action types：
- review
- approve / reject
- retry
- assign
- pause / resume
- archive / dismiss
- open detail

规则：
- destructive actions 必须清晰区分
- dangerous actions 需要确认
- bulk actions 必须显示 affected count
- disabled actions 应解释为什么 unavailable

---

## 10. Status System

operations pages 需要强 state language。

常见 states 可包括：
- draft
- pending
- ready
- in_progress
- blocked
- failed
- completed
- cancelled
- stale

每个 state 都应具备：
- visual treatment
- readable label
- optional icon
- 在 workflow 语境中的清晰含义

---

## 11. Density Rules

此模式是三种 dashboard 模式中允许最高密度的。

推荐：
- compact vertical rhythm
- reduced card emphasis
- 更紧的 panel padding：12px 到 16px
- table row heights 保持可读但高效
- minimal decorative shadowing

优先使用结构和 separators，而不是柔软的视觉花哨感。

---

## 12. Chart Usage

charts 可以使用，但属于次要载体。

只有当 charts 支持以下任务时才使用：
- backlog trend
- completion rate
- failure trend
- throughput
- state distribution

没有强理由时，不要让 charts 把 operational table 挤到首屏以下。

---

## 13. States

### Empty
- 告诉用户是真的没有 items，还是只是没有 matching results
- 保留 filter context

### Loading
- 保持 table skeleton 结构可见
- 保持 column rhythm 稳定

### Error
- failed row actions 尽可能局部处理
- global errors 除非必要，不应抹掉整个 working surface

---

## 14. Responsive Rules

Desktop:
- table-first 布局
- 优先使用 side detail 或 split view

Tablet:
- 减少可见 columns
- 将 secondary information 移入 row expansion

Mobile:
- 将 rows 转换为 stacked cards 或 compact grouped lists
- 保持 search、status filter 和 primary action 可见
- 避免在小屏幕上保留完整 desktop table behavior
