# Dashboard 设计 — Monitoring / Runtime Mode

## 1. Purpose

本文档定义 monitoring 风格 dashboard 的设计规则。

当页面主要用于以下场景时，使用此模式：
- runtime state
- health monitoring
- alert handling
- execution visibility
- operational supervision
- near-real-time system awareness

此模式不主要用于：
- executive KPI review
- marketing overview
- browse/discovery experiences

---

## 2. Core Intent

页面应按以下顺序回答问题：
1. 系统现在健康吗？
2. 什么正在失败或降级？
3. 什么最需要优先关注？
4. 最近发生了什么变化？
5. 我还能去哪里进一步调查？

此模式必须优先考虑：
- rapid scan
- status clarity
- alert visibility
- recency
- escalation paths

---

## 3. Visual Tone

monitoring dashboards 应给人这样的感受：
- focused
- structured
- low-friction
- highly legible
- 比 overview dashboards 略高密度

避免：
- large decorative whitespace
- oversized cards with weak information density
- overly soft consumer styling

---

## 4. Page Anatomy

推荐结构：
1. page title + last refresh time + environment/scope
2. critical status strip
3. summary health cards
4. live or recent trend region
5. alert / issue panel
6. timeline / event stream / execution list
7. detailed drill-down modules

critical issues 应位于 general analytics 之上。

---

## 5. Status Strip

顶部 status strip 用于展示：
- overall status
- critical alert count
- degraded subsystem count
- stale data indicator
- last refresh / source freshness

这条状态带应在视觉上立即可见，不能被埋没。

---

## 6. Health Cards

health cards 应展示：
- subsystem name
- current state
- key metric
- trend or freshness
- drill-down path

清晰使用 semantic states：
- healthy
- degraded
- failed
- paused
- stale
- unknown

不要让单张 card 承载过多 metrics。

---

## 7. Alert Rules

alerts 在此模式中是一等对象。

每个 alert item 应传达：
- severity
- title
- affected object/system
- time
- current status
- owner 或 action path（如适用）

severity levels 在视觉上应有明显区分：
- critical
- high
- medium
- low
- informational

不要只依赖颜色；同时使用 iconography 和 labels。

---

## 8. Timeline / Event Stream

在以下场景中使用 timeline 或 event streams：
- latest incidents
- job events
- execution transitions
- retries / failures / recoveries

规则：
- 除非 process timeline 要求按时间顺序，否则默认 newest first
- timestamps 必须高度可读
- 使用简洁的 event language
- 支持 drill-in 到 full event detail

---

## 9. Chart Rules

monitoring charts 应强调：
- trend changes
- spikes
- drops
- thresholds
- freshness

使用：
- line charts
- area charts
- status history bars
- threshold-aware visualizations

避免：
- 用于 critical runtime state 的 decorative pie charts
- 隐藏 recency 或 threshold breach 信息的图表

在相关情况下，thresholds 和 alert boundaries 应可见。

---

## 10. Density Rules

此模式允许比 overview mode 更高的密度。

推荐：
- panel padding: 12px to 16px
- tighter row spacing
- clear separators
- 比 browse-style UI 使用更低的 radius 和更弱的 shadow

panels 应有 operational 感，而不是 lounge-like。

---

## 11. Interaction Rules

- critical modules 应支持快速 drill-down
- 按 severity、subsystem、environment、time 进行 bulk filtering 应足够容易
- 不要无必要地把 active incidents 藏在 tabs 后面
- refresh behavior 必须明确
- stale-data state 必须明确

---

## 12. States

### Loading
- 如果安全且标识明确，可显示 last known data
- 清楚标明 refresh in progress

### Error
- 保持 unaffected modules 可见
- 在可能时显示 module-level errors

### Empty
- 如果没有 alerts，应将其表达为 healthy state，而不是 blank panel

### Stale
- stale data 是一等状态，不是 footnote

---

## 13. Responsive Rules

Desktop:
- critical strip 和 alerts 应保持高度可见
- 可以使用 2 到 4-column 的 operational grid

Tablet:
- 优先堆叠 lower-priority modules
- 保持 alert 和 health modules 靠近顶部

Mobile:
- 优先展示 summary status 和 alert list
- 更积极地折叠 trend 和 history modules
- 少显示 charts，多显示 compact summaries
