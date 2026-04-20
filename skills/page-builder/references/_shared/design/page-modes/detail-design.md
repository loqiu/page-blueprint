# 详情页设计系统

## 1. Purpose

本文档定义详情页的设计规则。

当页面主要用于以下场景时，使用此模式：
- proposal detail
- execution detail
- candidate detail
- order / trade / task detail
- entity profile
- single-object investigation
- object-centric review and action

此模式不主要用于：
- top-level KPI dashboards
- real-time monitoring walls
- browse/discovery experiences

---

## 2. Core Intent

页面应按以下顺序回答问题：
1. 这是什么对象？
2. 它当前处于什么状态？
3. 现在最重要的是什么？
4. 有哪些可用操作？
5. 哪些证据、历史和关联数据支撑当前决策？

此模式优先考虑：
- 快速定向
- 清晰状态
- 渐进披露
- 稳定层级
- 在不过载的前提下高效检查

---

## 3. Visual Tone

详情页应给人这样的感受：
- 聚焦
- 可信
- 结构化
- 易读
- 比 operations tables 更不拥挤
- 比 landing pages 信息更丰富

它们不应给人这样的感觉：
- 装饰化
- card 过载
- tab 混乱
- 没有层级却交互过重

---

## 4. Page Anatomy

推荐的自上而下结构：

1. page title + identifier + current status
2. summary header
3. key metadata / attributes
4. primary content sections
5. timeline / history / logs / related records
6. lower-priority supporting content

可选 right rail：
- quick actions
- current state summary
- risk markers
- owner / assignee / freshness
- shortcuts to related views

---

## 5. Summary Header

summary header 是页面的定向区块。

它通常应包含：
- object title
- object ID 或 external reference
- current status
- priority/severity（如适用）
- short description 或 context
- last updated time
- owner / source / scope（在有帮助时）

规则：
- status 必须立刻可见
- object identity 必须主导 header
- metadata 应服务于 identity，而不是与之竞争
- 不要把每个字段都堆进 header

---

## 6. Metadata Block

对稳定事实使用 metadata grid：
- type
- source
- owner
- created time
- updated time
- environment
- tags
- category
- version
- scope

规则：
- 使用简洁标签
- 保持值易于扫描
- 结构对齐保持一致
- 避免深层嵌套的 card-in-card metadata 布局

推荐模式：
- desktop 上使用 2-column 到 4-column metadata grid
- 在较小屏幕上使用堆叠的 key-value groups

---

## 7. Primary Sections

典型的 primary sections 可包括：
- summary / rationale
- decision context
- key metrics
- execution snapshot
- candidate attributes
- evidence / supporting signals
- linked entities

规则：
- 每个 section 都必须有清晰标题
- section 顺序应反映其决策相关性
- 不要让每个 section 在视觉上完全等权
- 最与决策相关的内容应放在 historical detail 之前

---

## 8. Action Placement

操作应明显但受控。

主要操作可能包括：
- approve / reject
- execute / retry
- assign
- pause / resume
- archive
- open full workflow
- compare
- escalate

推荐放置位置：
- primary actions 放在 header 或 sticky action rail
- secondary actions 放在 overflow menu
- destructive actions 清晰分离

规则：
- main action 必须在视觉上毫不含糊
- dangerous actions 需要确认
- disabled actions 应解释为什么 unavailable

---

## 9. Tabs vs Sections

只有当内容确实属于清晰不同的模式时才使用 tabs。

好的 tab 示例：
- Overview
- History
- Logs
- Related Items
- Audit

在以下情况下使用堆叠 sections：
- 用户受益于连续阅读
- 内容支持叙事式检查流程
- 切换 tabs 会隐藏必要上下文

规则：
- 不要只为了浅层分组就使用 tabs
- 不要默认把关键信息藏进 secondary tabs
- 除非绝对必要，不要嵌套多套 tab systems

---

## 10. Timeline / History / Audit

在以下场景中使用 timeline-like components：
- status transitions
- execution events
- review activity
- state changes
- retries / approvals / failures
- audit logs

规则：
- timestamps 必须高度可读
- 用于 operational review 时优先 newest-first
- 如果因果关系比时间先后更重要，也可以按时间顺序
- entries 应简洁且结构化
- 如有需要，应支持 drill-down 到 full event detail

理想情况下，每一项都应传达：
- 发生了什么
- 何时发生
- 由谁或哪个系统触发
- 结果状态
- 如有需要，附上 evidence 或 related object link

---

## 11. Related Records

related records 是辅助上下文，不是页面主体身份。

示例：
- related executions
- sibling candidates
- linked tasks
- previous versions
- attached documents
- upstream/downstream objects

规则：
- related records 通常应位于 primary detail 下方
- 使用 compact tables 或 grouped lists
- 不要让 related data 压过 main entity

---

## 12. Density Rules

详情页应使用中等密度。

推荐：
- section spacing: 24px to 32px
- panel padding: 16px to 24px
- metadata spacing: 12px to 16px
- 在 logs/tables 内部使用更紧凑的节奏

与 dashboards 相比：
- 比 operations mode 更不压缩
- 比 browse mode 更有结构
- 比 monitoring mode 更易读

---

## 13. Chart Usage

图表是可选的，且具有上下文依赖。

只有当图表能帮助回答以下问题时才使用：
- 这个对象随时间如何变化
- 它与同类相比如何
- 什么趋势支撑当前决策
- 哪种 execution 或 signal pattern 更关键

规则：
- 图表必须服务于 object story
- 不要放置没有决策目的的泛化图表
- one chart = one message
- 图表说明保持简洁

---

## 14. Table Usage

在以下场景中使用表格：
- related records
- evidence rows
- parameter lists
- fill / order / execution breakdown
- change history

规则：
- tables 应服务于 investigation，而不是替代页面层级
- 默认使用紧凑且可读的 table density
- 对深层 rows 支持 open-in-detail
- 在 drill-in 过程中保持上下文

---

## 15. States

### Loading
- 保留页面 skeleton
- 显示 header 和 section placeholders
- 避免大幅 layout shifts

### Empty
- 解释缺少了什么
- 区分 “no data yet” 和 “not applicable”

### Error
- 尽可能将 failure 隔离在 section level
- 不要因为一个 supporting section 失败就让整个 detail page 坍塌

### Stale
- 如果 freshness 很重要，stale state 必须在 header 附近可见

### Restricted
- 清楚解释 permission boundaries
- 不要无说明地静默隐藏 critical sections

---

## 16. Responsive Rules

Desktop:
- summary header + optional right rail
- metadata grid 可使用多列
- related tables 可保持 inline

Tablet:
- right rail 可移到 header 下方
- metadata grid 减少列数
- timeline 和 supporting sections 纵向堆叠

Mobile:
- actions 收起为一个 primary action + overflow
- metadata 改为堆叠布局
- tabs 应简化
- tables 在需要时转成 grouped lists 或 compact cards

---

## 17. Anti-Patterns

不要：
- 把 identity 和 status 藏到首屏以下
- 埋没 primary action
- 让每个 section 都长成一样的 card
- 做出噪音很大的 header，堆太多 chips 和 tags
- 每次查看 related inspection 都强迫跳转离开当前页
- 把 tabs 当成糟糕层级结构的垃圾场
