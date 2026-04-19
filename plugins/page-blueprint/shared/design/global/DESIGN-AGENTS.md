# DESIGN-AGENTS.md

## Role

你正在为本仓库设计并实现前端 UI。

你必须按以下顺序遵循设计文档：

1. `global-design.md`
2. 页面模式设计文档：
   - `dashboard-design-overview.md`
   - `dashboard-design-monitoring.md`
   - `dashboard-design-operations.md`
   - `detail-design.md`
   - `browse-design.md`
   - `settings-admin-design.md`
3. `../../guides/professional-page-generation.md`

如果规则发生冲突：
- 页面模式规则可以细化布局和密度
- 全局规则仍然主导 tokens、typography、semantic colors、spacing philosophy 和 accessibility minimums

不要随意创造新的视觉语言。

---

## Mandatory Workflow

在生成 UI 之前，先明确以下内容：

1. 这是什么页面模式？
   - overview dashboard
   - monitoring dashboard
   - operations dashboard
   - detail page
   - browse/discovery page
   - admin/workflow page

2. 主要用户意图是什么？
   - scan
   - monitor
   - compare
   - review
   - act
   - investigate
   - browse

3. 主导界面载体是什么？
   - KPI cards
   - charts
   - table/list
   - detail sections
   - media/cards
   - settings sections / policy groups

在编码前简要说明这些判断。

---

## Design Priority Order

做设计决策时，按以下优先级排序：

1. user task clarity
2. information hierarchy
3. page-mode fit
4. consistency with global tokens
5. visual polish

不要为了好看牺牲任务清晰度。

---

## Global Rules

以下内容必须始终遵循 `global-design.md`：
- color tokens
- semantic state colors
- typography roles
- spacing system
- radius system
- shadow system
- component baselines
- accessibility rules
- state handling

如果已有对应 token，绝不要硬编码随意的颜色、间距或圆角。

---

## Page Mode Selection Rules

### Overview Dashboard
当页面主要用于以下场景时，使用 `dashboard-design-overview.md`：
- KPI summary
- top-level analysis
- trend review
- business overview

### Monitoring Dashboard
当页面主要用于以下场景时，使用 `dashboard-design-monitoring.md`：
- runtime state
- health monitoring
- alert handling
- recency and status visibility

### Operations Dashboard
当页面主要用于以下场景时，使用 `dashboard-design-operations.md`：
- queue handling
- proposal/execution/candidate lists
- workflow progression
- action-heavy table/list surfaces

### Detail Page
当页面主要用于以下场景时，使用 `detail-design.md`：
- one object
- one proposal
- one execution
- one candidate
- one order / trade / task
- one task/entity under investigation

### Browse / Discovery Page
当页面主要用于以下场景时，使用 `browse-design.md`：
- object browsing
- discovery
- lightweight comparison
- narrowing a result set

### Settings / Admin Page
当页面主要用于以下场景时，使用 `settings-admin-design.md`：
- preferences
- admin configuration
- permission management
- policy editing

如果页面混合多种模式，先识别主导模式，其他模式只作为辅助模式使用。

---

## Layout Rules

不要把每个页面都设计成：
- a marketing landing page
- a loose card grid
- a giant dashboard with equal-weight widgets
- a dense spreadsheet

布局应由页面模式决定。

规则：
- overview dashboards 是 summary-first
- monitoring dashboards 是 status-first
- operations dashboards 是 table/list-first
- detail pages 是 identity-and-context-first
- browse/discovery pages 是 results-first
- settings/admin pages 是 scope-and-section-first

---

## Chart Rules

只有当图表能回答真实问题时才添加图表：
- trend
- comparison
- composition
- threshold breach
- throughput
- change over time

不要添加图表：
- 作为装饰
- 仅仅因为页面有空白
- 当 table 或 metric 更直接时

一张图表只传达一个主要观点。

---

## Table Rules

tables 在 operations pages 中是一等界面载体，在其他页面中则是次要载体。

在以下情况下使用 tables：
- 用户需要跨行比较
- 用户需要扫描和排序
- 操作是逐项或批量发生的

如果用户任务是 row comparison，不要用 cards 替代 table。

---

## Detail Rules

在 detail pages 中：
- object identity 必须清晰
- current status 必须明显
- primary action 必须容易找到
- supporting evidence 应在完成定向之后再出现
- history 和 related records 不能压过 main object

不要用巨大的装饰性 banners 或空洞的 hero space 来开头 detail pages。

---

## State Rules

每个页面和每个主要模块都必须考虑：
- loading
- empty
- error
- disabled
- stale / outdated（如适用）
- permission-restricted（如适用）

绝不能只交付 “happy path” 状态。

---

## Density Rules

根据页面模式选择密度：

- overview dashboard: medium
- monitoring dashboard: medium-high
- operations dashboard: high
- detail page: medium
- browse/discovery: low-medium

不要无缘无故把面向操作的工具做成消费级的松散间距。

---

## Action Rules

操作必须是：
- visible
- scoped
- safe
- understandable

主要操作应位于以下位置附近：
- the top toolbar
- the summary header
- the active row/detail context

危险操作必须被清晰区分，并要求确认。

---

## Accessibility Rules

始终确保：
- visible keyboard focus
- readable contrast
- sufficiently large interactive targets
- charts are not color-only
- icon-only buttons have accessible labels

accessibility 不是可选项。

---

## Engineering Rules

实现时：
- 先把样式映射到 tokens
- 在创建新组件之前先复用现有组件
- 除非必要，不要写一次性的视觉 hack
- 优先组合，而不是复制
- 让 responsive behavior 是有意设计的

引入新组件时，说明：
- 为什么现有组件不够用
- 它属于哪个页面模式
- 它使用了哪些 global tokens

---

## Output Format for UI Tasks

编码前说明：
1. page mode
2. dominant user task
3. layout strategy
4. key modules
5. density choice

编码后说明：
1. applied 了哪些 design docs
2. used 了哪些 global tokens
3. 如何处理 loading/empty/error states
4. 做了哪些 tradeoffs

---

## Forbidden Patterns

除非明确要求，否则不要：
- 把 dashboards 做成 consumer landing pages 风格
- 在关键 operational content 上方放 giant hero banners
- 把每个 section 都做成同样的 generic card
- 在 data-heavy pages 中过度使用 bright brand color
- 当任务是 scan/compare 时，用 cards 替代表格
- 无缘无故把 key actions 藏进 overflow menus
- 只交付 static mockup states 而没有真实 state handling
- 在 token system 之外发明新的 colors 或 radii

---

## Decision Heuristic

如果不确定，就问：
- 用户在前 10 秒想完成什么？
- 他们首先必须看到的最重要信息是什么？
- 对这个任务来说，最合适的载体是什么：metric、chart、table 还是 detail section？

然后围绕这个答案来设计。
