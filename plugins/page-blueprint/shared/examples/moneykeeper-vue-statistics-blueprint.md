# 统计分析页面 改造蓝图

## 1. 页面定位
- 页面目标：让已登录用户在一个分析工作台里快速判断当前账本周期表现，先看整体波动，再看变化来源，最后决定是否需要继续下钻。
- page mode：`overview dashboard`
- 核心对象：当前账本的统计窗口
- 主要用户：个人记账用户与共享账本的日常使用者
- 首要任务：切换统计周期与成员范围，快速判断本周期是盈余还是失衡，变化来自时间趋势还是分类结构
- 成功判定：用户在首屏即可完成一次整体判断，并在一屏半内看清主要波动与分类来源，而不需要先阅读大段说明或扫多个同权重卡片。

## 2. 依据与假设
- 改造级别：`visual-redesign`
- 已确认事实：项目使用 Vue 3 + vue-router + Pinia + Element Plus + Tailwind；`/statistics` 已存在且要求登录；可用数据包括总收入、总支出、结余、记录数、上一周期对比、bucket 列表、收入分类、支出分类、当前窗口与上一窗口范围。
- 关键假设：统计页仍保持 overview 模式，不改造成录入工作台或操作控制台；本轮不新增新的后端接口；下钻入口可以保留为预留位，不强制接独立详情页。
- 明确不做：不新增实时监控模块；不改成 table-first；不引入复杂图表库；不扩展多层 tabs；不发明新的业务动作。

## 3. 旧结构骨架
- 当前主路由 / 页面归属：`/statistics`，属于已登录后的账本分析入口。
- 当前共享壳 / 页面骨架：`深色 hero + 白色工作区 + 右侧 sticky 信息栏` 的后台模板骨架。
- 当前首屏顺序：hero 标题说明 -> 大块摘要区 -> 右侧窗口信息栏 -> 趋势与分类内容卡。
- 当前主导载体：页面壳和摘要容器，而不是趋势分析区。
- 当前一级模块顺序：hero 区 -> 主工作区 -> 右侧信息栏 -> 趋势卡 -> 分类卡 -> 窗口说明卡。
- 当前结构最关键的问题：旧页把分析内容塞进“深色 hero + 白色工作区 + 右侧信息栏”的常规后台模板里，用户先看到的是页面壳，而不是分析关系。

## 4. 重构目标与硬约束
- 首屏必须先回答什么：我在看哪个账本、哪个统计范围、这一周期整体是变好还是变差。
- 页面主舞台是什么：趋势主舞台。用户必须先看到波动发生在哪些时间段，而不是先读说明文字或边界信息。
- 这次必须打掉的旧结构：`hero + 白色工作区 + 右侧信息栏` 的旧三段式；多个同权重白卡并列；把分析窗口说明做成独立大块。
- 允许保留的少数资产：继续保留 `/statistics` 路由、账本上下文、现有统计接口、`TopNavBar`、`PlatformStateCard`、Element Plus 基础筛选控件，以及已有的 `StatisticsKpiCard` / `StatisticsCategorySection` 作为可重塑原语。
- 不得牺牲什么：现有账本上下文、筛选主流程、overview 模式下的 summary-first 判断链，以及现有认证与数据接口边界。
- 为什么需要大改造：用户要的是“改头换面”，而不是原结构放大。只要主舞台、阅读路径和模块权重不变，视觉再换也仍然像旧页。

## 5. 新结构骨架
- 主路由：`/statistics`
- 路由归属理由：此页承接已登录后的账本分析入口，核心是周期总览、变化判断和轻量下钻提示，而不是逐条记录操作。
- 共享壳决策：`bypass`，不再复用旧 hero 壳和右侧 sticky 信息栏。
- 新的首屏顺序：分析控制带 -> KPI 横向指标带 -> 趋势主舞台 -> 分类构成区 -> 上下文账本对照带。
- 主导载体：`trend board + compact KPI rail + composition panels`
- 一级模块顺序：`StatisticsCommandBar -> StatisticsKpiRail -> StatisticsTrendStage -> CompositionDeck -> StatisticsContextLedger`

## 6. 新信息架构与阅读路径
- 首屏必须先看到：当前账本、分析范围、筛选控件、四个关键指标、一个主趋势区域。
- 10 秒阅读路径：先确认账本与筛选范围，再扫四个关键指标，随后进入趋势主舞台判断波动，最后查看分类来源与上下文边界。
- 页面层级顺序：分析控制带 -> KPI 横向指标带 -> 趋势主舞台 -> 分类构成区 -> 上下文对照带。
- 主区 / 次区 / 支撑区：主区是趋势主舞台；次区是 KPI 带与分类构成区；支撑区是上下文对照带。
- drill-down / 返回路径：本轮以内联分析为主，不强制整页跳转；未来若接 `/search`，只从上下文对照带提供单一 drill-down 入口，并保留当前筛选上下文。
- 被降级 / 合并 / 移除的旧模块：旧 hero 被拆成控制带与 KPI 带；旧右侧分析窗口栏被合并进底部对照带；重复性的窗口说明文案被压缩到一句上下文提示；多张同层级大白卡被改成“主舞台 + 次级模块”。

## 7. 页面模块拆解
### M1. 分析控制带
- 目标：让用户先确认“我在看哪个账本、哪个时间范围、当前筛选是什么”，并立即可以刷新或改筛选。
- 关键内容：页面标题、当前账本标签、周期筛选、锚点日期、成员筛选、刷新统计、应用筛选。
- 为什么它现在在这里：overview 页的顶部应该先给范围与控制，而不是先给装饰性 hero。
- 组件结构：`StatisticsCommandBar` + `el-select` + `el-date-picker` + `el-button`
- 交互：显式点击 `应用筛选` 更新结果；`刷新统计` 重拉当前条件；账本缺失时主流程禁用并给出去账本页的入口。
- 状态：default、loading、disabled-no-ledger

### M2. KPI 横向指标带
- 目标：用最少的指标回答“这是好还是坏”，并提供上一周期对比。
- 关键内容：收入、支出、结余、记录数。
- 为什么它现在在这里：KPI 应紧跟控制带，形成 overview 页的第一层判断，而不是嵌进 hero 里做装饰。
- 组件结构：`StatisticsKpiRail` + `StatisticsKpiCard` x 4
- 交互：默认只读扫描；卡片不承担页面导航。
- 状态：default、loading、no-baseline

### M3. 趋势主舞台
- 目标：把 bucket 趋势变成全页唯一主舞台，让用户一眼看到波动发生在哪些时间段。
- 关键内容：bucket 标签、每个 bucket 的收入/支出对比、记录数、当前粒度、主趋势说明。
- 为什么它现在在这里：overview 模式要求 KPI 后面直接出现 dominant trend chart / region，这里不再让趋势区退居为一张普通内容卡。
- 组件结构：`StatisticsTrendStage` + `TrendHeader` + `BucketRail`
- 交互：默认以直接可读为主，不依赖 hover；后续若接下钻，统一从 bucket 行尾预留 affordance，而不是在本轮引入复杂跳转。
- 状态：default、loading、empty-buckets、module-error

### M4. 分类构成区
- 目标：解释“变化来自哪里”，分别给出支出分类和收入分类结构。
- 关键内容：支出分类列表、收入分类列表、金额、占比、分类数量。
- 为什么它现在在这里：分类解释应跟在趋势判断后面，是第二层结论，不该与主趋势区争夺首屏中心。
- 组件结构：`CompositionDeck` + `StatisticsCategorySection` x 2
- 交互：默认只读扫描；不在本轮扩成独立 drill-down 列表页。
- 状态：default、expense-empty、income-empty、loading

### M5. 上下文对照带
- 目标：把当前窗口、上一周期、统计锚点和记录数压成一个低噪音的确认区，替代旧版右侧信息栏。
- 关键内容：当前时间范围、上一周期时间范围、锚点日期、粒度、总记录数、收入/支出记录数。
- 为什么它现在在这里：这些信息是确认边界，不该在页面上获得与主趋势区同等的视觉权重。
- 组件结构：`StatisticsContextLedger`
- 交互：只读展示；若后续接入 `/search`，在这里预留单一的 drill-down 入口。
- 状态：default、loading、empty

## 8. 组件规范
### 8.1 继续复用的组件
- 组件名：`TopNavBar`
- 为什么还能保留：它只承担平台级导航，不会决定统计页的内部结构。
- 责任：提供平台顶层导航与页外跳转。
- 允许保留到什么程度：仅保留全局导航职责，不向内延伸页面壳。
- 状态 / 变体：维持现有导航状态

- 组件名：`PlatformStateCard`
- 为什么还能保留：它是状态容器，不会绑死视觉骨架。
- 责任：统一承载 loading / empty / error / warning 等主状态。
- 允许保留到什么程度：只用于状态门控；正常数据态不能继续用它包装整块内容。
- 状态 / 变体：`loading`、`empty`、`error`、`warning`、`info`

- 组件名：`StatisticsKpiCard`
- 为什么还能保留：已有指标卡逻辑可复用，但必须从“大块 hero 卡”改成“紧凑横向指标卡”。
- 责任：输出单个指标的 label、current value、delta、短上下文。
- 允许保留到什么程度：允许保留数据契约，不允许保留旧的 hero-size 视觉体量。
- 状态 / 变体：default、loading、no-baseline、records

- 组件名：`StatisticsCategorySection`
- 为什么还能保留：分类列表契约本身成立，只需要从独立大卡调整为次级模块内容。
- 责任：输出单侧分类列表、金额、占比和 empty 处理。
- 允许保留到什么程度：允许保留列表结构，不允许继续作为与趋势区同权重的大型 panel。
- 状态 / 变体：default、empty、loading

### 8.2 新增组件
- 组件名：`StatisticsCommandBar`
- 为什么旧组件不够：旧页面没有一个把标题、账本上下文、筛选和主操作压成同一分析入口的组件。
- 责任：承接分析标题、账本标签、筛选控件和主操作。
- 组合关系：`StatisticsPage -> StatisticsCommandBar`
- 必要状态 / 变体：default、loading、disabled-no-ledger
- 依赖的全局规则：overview 模式的 summary-first hierarchy、克制 filtering、视觉 calm

- 组件名：`StatisticsTrendStage`
- 为什么旧组件不够：现有实现把 bucket 列表当普通内容卡，不足以承担 dominant trend region。
- 责任：承接主趋势标题、粒度说明、bucket 对比、趋势主舞台布局。
- 组合关系：`StatisticsPage -> StatisticsTrendStage`
- 必要状态 / 变体：default、loading、empty-buckets、module-error
- 依赖的全局规则：overview 模式的 dominant chart region、单一信息重点、稳定 loading layout

- 组件名：`StatisticsContextLedger`
- 为什么旧组件不够：旧右栏信息块是独立侧栏思路，不适合新的低噪音边界确认区。
- 责任：承接当前窗口、上一周期、锚点、记录数与后续单一 drill-down affordance。
- 组合关系：`StatisticsPage -> StatisticsContextLedger`
- 必要状态 / 变体：default、loading、empty
- 依赖的全局规则：secondary module hierarchy、低视觉噪音、obvious drill-down path

## 9. 状态矩阵
- loading：保留控制带、KPI 带和趋势主舞台骨架，禁止整页塌缩成单一 loading 卡。
- empty：区分“当前账本没有任何统计数据”和“当前筛选下没有匹配数据”；趋势主舞台和分类区都保留标题与层级。
- error：优先隔离到具体模块；趋势区失败不能让 KPI 和控制带一起消失。
- disabled：无账本上下文时禁用筛选与应用操作，并明确给出 `前往账本中心`。
- stale / outdated：当前版本不做实时 freshness 设计；仅在手动刷新失败但仍展示旧结果时提示“当前结果可能不是最新”。
- permission-restricted：不适用；当前页面只依赖登录态和账本上下文。

## 10. 关键交互路径
- 筛选 / 搜索：顶部只保留周期、锚点日期、成员三类主筛选；不加入高级筛选抽屉或自由搜索。
- 排序 / 比较：比较逻辑固定为当前周期对比上一周期，以及收入对比支出、分类对比分类；不新增独立排序系统。
- drill-down / 返回：本轮仍以内联分析为主；若后续接入 `/search`，只允许从 `StatisticsContextLedger` 提供单一 drill-down 入口。
- 危险操作保护：本页没有 destructive action；刷新与应用筛选不需要确认弹窗。
- 审计 / 历史查看：当前页只提供上一周期基线，不扩展独立审计时间线。

## 11. 关键命名与动作
- 页面标题：`统计分析`
- 主操作文案：`刷新统计`、`应用筛选`
- 空状态文案：`当前窗口还没有统计数据。可以切换周期、调整锚点日期，或者先在当前账本补充记录后再回来查看。`
- 错误文案：`统计数据加载失败，请稍后重试。`
- 权限 / 限制文案：`请先选择账本。统计页完全基于当前账本上下文运行。`

## 12. 响应式策略
- Desktop：控制带、KPI 带、趋势主舞台首屏可见；分类构成区与上下文对照带作为后续区块。
- Tablet：控制带拆成上下两层；KPI 带换行；趋势主舞台保留全宽；分类构成区改双段堆叠。
- Mobile：控制带纵向排布；KPI 改紧凑纵向列表；趋势主舞台优先保留，分类区和上下文对照带顺序下移。

## 13. 待确认项
- Q1：货币格式是否继续固定为 `GBP`，还是需要跟随账本币种或用户区域设置？
- Q2：成员筛选在多人账本里是否保持默认 `全部成员`，还是需要按当前登录用户预选？
- Q3：后续是否要把某个 bucket 或分类点击后导向 `/search` 作为下钻页？

## 14. 实现附录
### 14.1 实现落点
- 共享壳决策：`bypass`，不再复用 `PlatformPageShell`，也不得重新造出一个等价的 hero 壳或右侧 sticky 信息栏。
- 目标页面文件：`C:\WorkSpace\Vue\moneykeeper-vue\src\views\StatisticsPage.vue`
- 需要新增的 page-local 组件：`src\components\statistics\StatisticsCommandBar.vue`、`src\components\statistics\StatisticsTrendStage.vue`、`src\components\statistics\StatisticsContextLedger.vue`
- 直接复用的共享组件：`TopNavBar.vue`、`PlatformStateCard.vue`、Element Plus 表单控件、现有 `/statistics` 路由
- 需要接入或确认的路由 / 壳组件：继续挂在现有 `/statistics` 路由下，并保持 `requiresAuth: true`；页面壳由 `StatisticsPage.vue` 自己持有

### 14.2 数据与状态归属
- 页面内状态：`filters`、`isLoading`、`errorMessage`、`memberOptions`、`statistics`
- store / composable 归属：账本上下文继续来自 `C:\WorkSpace\Vue\moneykeeper-vue\src\stores\ledger.js` 的 `useLedgerStore`；当前页先不新增全局 store
- API / data access 归属：统计数据继续来自 `C:\WorkSpace\Vue\moneykeeper-vue\src\api\modules\statistics.js` 的 `fetchLedgerStatistics`；成员筛选继续来自 `C:\WorkSpace\Vue\moneykeeper-vue\src\api\modules\ledgers.js` 的 `fetchLedgerMembers`
- 派生状态：`hasLedgerContext`、`currentLedgerName`、`selectedPeriodLabel`、`granularityLabel`、`hasStatisticsData`、`maxBucketAmount`、`recordCount`

### 14.3 组件树
- 页面根：`StatisticsPage -> TopNavBar + StatisticsCommandBar + StatisticsKpiRail + StatisticsTrendStage + CompositionDeck + StatisticsContextLedger`
- 一级模块树：`StatisticsKpiRail -> StatisticsKpiCard x 4`；`CompositionDeck -> StatisticsCategorySection(expense) + StatisticsCategorySection(income)`
- 新增组件边界：`StatisticsCommandBar` 只持有页首控制与主操作；`StatisticsTrendStage` 只持有主趋势舞台；`StatisticsContextLedger` 只持有边界确认与未来 drill-down 槽位；数据请求和主状态门控仍由 `StatisticsPage` 持有

### 14.4 接口与字段依赖
- 直接依赖接口：`GET /ledgers/{ledgerId}/statistics`、`GET /ledgers/{ledgerId}/members`
- 关键字段：统计接口至少依赖 `totalIncome`、`totalExpense`、`balance`、`recordCount`、`incomeRecordCount`、`expenseRecordCount`、`incomeChangePercentage`、`expenseChangePercentage`、`balanceChangePercentage`、`startDate`、`endDate`、`previousStartDate`、`previousEndDate`、`anchorDate`、`bucketGranularity`、`buckets[]`、`expenseCategories[]`、`incomeCategories[]`
- 错误与空状态依赖：`currentLedgerId` 缺失时进入账本必选 warning；统计接口异常时进入 error；`recordCount`、`buckets`、`expenseCategories`、`incomeCategories` 同时为空时进入 empty；变化百分比为 `null` 时显示无基线文案

### 14.5 Builder 验收点
- 必须完成：把 `/statistics` 改成 `分析控制带 -> KPI 横向指标带 -> 趋势主舞台 -> 分类构成区 -> 上下文对照带` 的新结构；去掉巨型 hero 和独立右侧 sticky 信息栏；让趋势区成为页面唯一主舞台；把旧的 `StatisticsKpiCard` / `StatisticsCategorySection` 收进新层级而不是沿用旧体量
- 必须验证：运行 `npm run lint` 与 `npm run build`；确认登录后能正常进入 `/statistics`；确认无账本、loading、error、empty、正常数据五种主状态都可渲染；确认 `刷新统计` 与 `应用筛选` 在当前账本上下文下正常工作
- 不得偏离：不得保留 `hero + 白色工作区 + 右侧信息栏` 的旧阅读路径；不得把趋势区再次做成普通次级卡片；不得引入蓝图外的图表类型、额外筛选器或新的业务动作；不得改动现有认证守卫语义
