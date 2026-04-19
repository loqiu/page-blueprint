# 统计分析页面 改造蓝图

## 1. 页面定位
- 页面目标：让已登录用户在 `/statistics` 首屏先完成本周期判断，再看变化来源，最后决定是否继续下钻。
- page mode：`overview dashboard`
- 核心对象：当前账本的统计窗口
- 主要用户：个人记账用户与共享账本的日常使用者
- 首要任务：切换统计周期与成员范围后，快速判断本周期是盈余还是失衡，以及变化主要发生在时间趋势还是分类结构
- 成功判定：用户在首屏完成一次整体判断，并在一屏半内看清主要波动与分类来源，不需要先扫页面壳或多个同权重模块

## 2. 依据与假设
- 改造级别：visual-redesign
- 已确认事实：项目使用 Vue 3 + vue-router + Pinia + Element Plus + Tailwind；`/statistics` 已存在且要求登录；可用数据包括总收入、总支出、结余、记录数、上一周期对比、bucket 列表、收入分类、支出分类、当前窗口与上一窗口范围
- 关键假设：统计页继续保持 overview dashboard；本轮不新增后端接口；本轮不强制接独立下钻详情页
- 明确不做：不改成录入工作台；不改成 table-first；不新增监控模块；不扩展多层 tabs；不新增蓝图外业务动作

## 3. 旧结构骨架
- 当前主路由 / 页面归属：`/statistics`，属于已登录后的账本分析入口
- 当前共享壳 / 页面骨架：`深色 hero + 白色工作区 + 右侧 sticky 信息栏`
- 当前首屏顺序：hero 标题说明 -> 大块摘要区 -> 右侧窗口信息栏 -> 趋势与分类内容卡
- 当前主导载体：页面壳和摘要容器，而不是趋势分析区
- 当前一级模块顺序：hero 区 -> 主工作区 -> 右侧信息栏 -> 趋势卡 -> 分类卡 -> 窗口说明卡
- 当前结构最关键的问题：用户先被页面壳定向，再被模块分散注意力，趋势区没有成为首屏主舞台

## 4. 重构目标与硬约束
- 首屏必须先回答什么：我在看哪个账本、哪个统计范围、这一周期整体是变好还是变差
- 页面主舞台是什么：趋势主舞台
- 这次必须打掉的旧结构：`hero + 白色工作区 + 右侧信息栏` 三段式；多个同权重白卡并列；独立的大块窗口说明区
- 允许保留的少数资产：`/statistics` 路由、账本上下文、现有统计接口、`TopNavBar`、`PlatformStateCard`、Element Plus 基础筛选控件、`StatisticsKpiCard`、`StatisticsCategorySection`
- 不得牺牲什么：账本上下文、筛选主流程、overview 的 summary-first 判断链、现有认证与数据接口边界
- 为什么需要大改造：如果首屏顺序、主舞台和模块权重不变，页面只会变成旧结构的换皮版本

## 5. 新结构骨架
- 主路由：`/statistics`
- 路由归属理由：该页服务于账本统计判断，不承担逐条记录操作
- 共享壳决策：`bypass`
- 新的首屏顺序：分析控制带 -> KPI 横向指标带 -> 趋势主舞台 -> 分类构成区 -> 上下文对照带
- 主导载体：趋势主舞台
- 一级模块顺序：`StatisticsCommandBar -> StatisticsKpiRail -> StatisticsTrendStage -> CompositionDeck -> StatisticsContextLedger`

## 6. 新信息架构与阅读路径
- 首屏必须先看到：当前账本、统计范围、筛选控件、四个关键指标、趋势主区域
- 10 秒阅读路径：先确认账本与范围，再扫四个关键指标，然后进入趋势主舞台判断波动，最后查看分类来源与边界信息
- 页面层级顺序：分析控制带 -> KPI 横向指标带 -> 趋势主舞台 -> 分类构成区 -> 上下文对照带
- 主区 / 次区 / 支撑区：主区是趋势主舞台；次区是 KPI 带和分类构成区；支撑区是上下文对照带
- drill-down / 返回路径：本轮以内联分析为主；若后续接 `/search`，仅从上下文对照带提供单一 drill-down 入口，并保留当前筛选上下文
- 被降级 / 合并 / 移除的旧模块：旧 hero 拆成控制带与 KPI 带；旧右侧信息栏并入上下文对照带；重复窗口说明压缩成一句边界提示；多个同权重大卡改成主区 + 次区

## 7. 页面模块拆解
### M1. 分析控制带
- 目标：先让用户确认自己正在看哪个账本、哪个周期、哪些筛选条件
- 关键内容：页面标题、当前账本标签、周期筛选、锚点日期、成员筛选、刷新统计、应用筛选
- 为什么它现在在这里：overview 页面顶部应该先给范围和控制，而不是先给装饰性页面壳
- 组件结构：`StatisticsCommandBar` + `el-select` + `el-date-picker` + `el-button`
- 交互：点击 `应用筛选` 更新结果；`刷新统计` 重新拉取当前条件；账本缺失时主流程禁用并给出去账本页入口
- 状态：default、loading、disabled-no-ledger

### M2. KPI 横向指标带
- 目标：用最少指标回答“当前结果是变好还是变差”
- 关键内容：收入、支出、结余、记录数，以及上一周期对比
- 为什么它现在在这里：KPI 应紧跟控制带，形成 overview 的第一层判断
- 组件结构：`StatisticsKpiRail` + `StatisticsKpiCard` x 4
- 交互：默认只读扫描；卡片不承担导航
- 状态：default、loading、no-baseline

### M3. 趋势主舞台
- 目标：让 bucket 趋势成为全页唯一主舞台
- 关键内容：bucket 标签、每个 bucket 的收入/支出对比、记录数、当前粒度、趋势说明
- 为什么它现在在这里：overview 模式里，KPI 之后应该直接进入主趋势判断区
- 组件结构：`StatisticsTrendStage` + `TrendHeader` + `BucketRail`
- 交互：默认直接可读，不依赖 hover；后续如需下钻，只在 bucket 行尾预留单一入口
- 状态：default、loading、empty-buckets、module-error

### M4. 分类构成区
- 目标：解释变化主要来自哪些分类
- 关键内容：支出分类列表、收入分类列表、金额、占比、分类数量
- 为什么它现在在这里：分类解释属于第二层结论，不应和趋势主舞台抢首屏主导权
- 组件结构：`CompositionDeck` + `StatisticsCategorySection` x 2
- 交互：默认只读扫描；本轮不扩成独立 drill-down 页
- 状态：default、expense-empty、income-empty、loading

### M5. 上下文对照带
- 目标：集中确认统计边界，而不是继续占据首屏主导位置
- 关键内容：当前时间范围、上一周期时间范围、锚点日期、粒度、总记录数、收入/支出记录数
- 为什么它现在在这里：这些信息用于确认边界，应作为支撑区存在
- 组件结构：`StatisticsContextLedger`
- 交互：只读展示；未来若接 `/search`，只在这里提供单一 drill-down 入口
- 状态：default、loading、empty

## 8. 组件规范
### 8.1 继续复用的组件
- 组件名：`TopNavBar`
- 为什么还能保留：只承担平台级导航，不决定统计页内部层级
- 责任：提供平台顶层导航与页外跳转
- 允许保留到什么程度：仅保留导航职责，不向内延伸页面壳
- 状态 / 变体：维持现有导航状态

- 组件名：`PlatformStateCard`
- 为什么还能保留：它是状态容器，不绑定旧页面结构
- 责任：承载 loading / empty / error / warning 等主状态
- 允许保留到什么程度：仅用于状态门控；正常数据态不能继续包装整页主体
- 状态 / 变体：`loading`、`empty`、`error`、`warning`、`info`

- 组件名：`StatisticsKpiCard`
- 为什么还能保留：指标卡的数据契约仍成立
- 责任：输出单个指标的 label、value、delta、短上下文
- 允许保留到什么程度：允许保留数据契约，不允许保留旧的大体量摘要样式
- 状态 / 变体：default、loading、no-baseline、records

- 组件名：`StatisticsCategorySection`
- 为什么还能保留：分类列表仍然是有效的次级模块
- 责任：输出单侧分类列表、金额、占比和 empty 处理
- 允许保留到什么程度：允许保留列表结构，不允许继续作为与趋势区同权重的大 panel
- 状态 / 变体：default、empty、loading

### 8.2 新增组件
- 组件名：`StatisticsCommandBar`
- 为什么旧组件不够：旧页面缺少把标题、账本上下文、筛选和主操作收束到一起的页首控制组件
- 责任：承接分析标题、账本标签、筛选控件和主操作
- 组合关系：`StatisticsPage -> StatisticsCommandBar`
- 必要状态 / 变体：default、loading、disabled-no-ledger
- 依赖的全局规则：overview 的 summary-first hierarchy、克制筛选、清晰操作优先级

- 组件名：`StatisticsTrendStage`
- 为什么旧组件不够：现有 bucket 内容只是一张普通内容卡，不能承担主舞台职责
- 责任：承接趋势标题、粒度说明、bucket 对比和主舞台布局
- 组合关系：`StatisticsPage -> StatisticsTrendStage`
- 必要状态 / 变体：default、loading、empty-buckets、module-error
- 依赖的全局规则：overview 的 dominant trend region、单一主舞台、稳定 loading 结构

- 组件名：`StatisticsContextLedger`
- 为什么旧组件不够：旧右栏信息块属于侧栏思路，不适合新的支撑区定位
- 责任：承接当前窗口、上一周期、锚点、记录数与未来单一 drill-down 入口
- 组合关系：`StatisticsPage -> StatisticsContextLedger`
- 必要状态 / 变体：default、loading、empty
- 依赖的全局规则：secondary hierarchy、低噪音支撑区、明确返回与下钻路径

## 9. 状态矩阵
- loading：保留控制带、KPI 带和趋势主舞台骨架，禁止整页塌缩成单一 loading 卡
- empty：区分“当前账本没有统计数据”和“当前筛选下没有匹配数据”；趋势主舞台和分类区都保留标题与层级
- error：优先隔离到具体模块；趋势区失败不能让 KPI 和控制带一起消失
- disabled：无账本上下文时禁用筛选与应用操作，并明确给出 `前往账本中心`
- stale / outdated：当前版本不做实时 freshness 模块；仅在手动刷新失败但仍展示旧结果时提示“当前结果可能不是最新”
- permission-restricted：不适用；当前页面只依赖登录态和账本上下文

## 10. 关键交互路径
- 筛选 / 搜索：顶部只保留周期、锚点日期、成员三类主筛选，不加入高级筛选抽屉或自由搜索
- 排序 / 比较：比较逻辑固定为当前周期对比上一周期，以及收入对比支出、分类对比分类；不新增独立排序系统
- drill-down / 返回：本轮仍以内联分析为主；若后续接 `/search`，只允许从 `StatisticsContextLedger` 提供单一 drill-down 入口
- 危险操作保护：本页没有 destructive action；刷新与应用筛选不需要确认弹窗
- 审计 / 历史查看：当前页只提供上一周期基线，不扩展独立审计时间线

## 11. 关键命名与动作
- 页面标题：`统计分析`
- 主操作文案：`刷新统计`、`应用筛选`
- 空状态文案：`当前窗口还没有统计数据。可以切换周期、调整锚点日期，或者先在当前账本补充记录后再回来查看。`
- 错误文案：`统计数据加载失败，请稍后重试。`
- 权限 / 限制文案：`请先选择账本。统计页完全基于当前账本上下文运行。`

## 12. 响应式策略
- Desktop：控制带、KPI 带、趋势主舞台首屏可见；分类构成区与上下文对照带作为后续区块
- Tablet：控制带拆成上下两层；KPI 带换行；趋势主舞台保留全宽；分类构成区改双段堆叠
- Mobile：控制带纵向排布；KPI 改紧凑纵向列表；趋势主舞台优先保留，分类区和上下文对照带顺序下移

## 13. 待确认项
- Q1：货币格式是否继续固定为 `GBP`，还是需要跟随账本币种或用户区域设置
- Q2：成员筛选在多人账本里是否保持默认 `全部成员`，还是需要按当前登录用户预选
- Q3：后续是否要把某个 bucket 或分类点击后导向 `/search` 作为下钻页

## 14. 实现附录
### 14.1 实现落点
- 共享壳决策：`bypass`，不再复用 `PlatformPageShell`，也不得重新造出等价的 hero 壳或右侧 sticky 信息栏
- 目标页面文件：`C:\WorkSpace\Vue\moneykeeper-vue\src\views\StatisticsPage.vue`
- 需要新增的 page-local 组件：`src\components\statistics\StatisticsCommandBar.vue`、`src\components\statistics\StatisticsTrendStage.vue`、`src\components\statistics\StatisticsContextLedger.vue`
- 直接复用的共享组件：`TopNavBar.vue`、`PlatformStateCard.vue`、Element Plus 表单控件、现有 `/statistics` 路由
- 需要接入或确认的路由 / 壳组件：继续挂在现有 `/statistics` 路由下，并保持 `requiresAuth: true`；页面壳由 `StatisticsPage.vue` 自己持有

### 14.2 数据与状态归属
- 页面内状态：`filters`、`isLoading`、`errorMessage`、`memberOptions`、`statistics`
- store / composable 归属：账本上下文继续来自 `C:\WorkSpace\Vue\moneykeeper-vue\src\stores\ledger.js` 的 `useLedgerStore`；当前页不新增全局 store
- API / data access 归属：统计数据继续来自 `C:\WorkSpace\Vue\moneykeeper-vue\src\api\modules\statistics.js` 的 `fetchLedgerStatistics`；成员筛选继续来自 `C:\WorkSpace\Vue\moneykeeper-vue\src\api\modules\ledgers.js` 的 `fetchLedgerMembers`
- 派生状态：`hasLedgerContext`、`currentLedgerName`、`selectedPeriodLabel`、`granularityLabel`、`hasStatisticsData`、`maxBucketAmount`、`recordCount`

### 14.3 组件树
- 页面根：`StatisticsPage -> TopNavBar + StatisticsCommandBar + StatisticsKpiRail + StatisticsTrendStage + CompositionDeck + StatisticsContextLedger`
- 一级模块树：`StatisticsKpiRail -> StatisticsKpiCard x 4`；`CompositionDeck -> StatisticsCategorySection(expense) + StatisticsCategorySection(income)`
- 新增组件边界：`StatisticsCommandBar` 只持有页首控制与主操作；`StatisticsTrendStage` 只持有趋势主舞台；`StatisticsContextLedger` 只持有边界确认与未来 drill-down 槽位；数据请求和主状态门控仍由 `StatisticsPage` 持有

### 14.4 接口与字段依赖
- 直接依赖接口：`GET /ledgers/{ledgerId}/statistics`、`GET /ledgers/{ledgerId}/members`
- 关键字段：`totalIncome`、`totalExpense`、`balance`、`recordCount`、`incomeRecordCount`、`expenseRecordCount`、`incomeChangePercentage`、`expenseChangePercentage`、`balanceChangePercentage`、`startDate`、`endDate`、`previousStartDate`、`previousEndDate`、`anchorDate`、`bucketGranularity`、`buckets[]`、`expenseCategories[]`、`incomeCategories[]`
- 错误与空状态依赖：`currentLedgerId` 缺失时进入账本必选 warning；统计接口异常时进入 error；`recordCount`、`buckets`、`expenseCategories`、`incomeCategories` 同时为空时进入 empty；变化百分比为 `null` 时显示无基线文案

### 14.5 Builder 验收点
- 必须完成：把 `/statistics` 改成 `分析控制带 -> KPI 横向指标带 -> 趋势主舞台 -> 分类构成区 -> 上下文对照带` 的新结构；去掉巨型 hero 和独立右侧 sticky 信息栏；让趋势区成为页面唯一主舞台；把旧的 `StatisticsKpiCard` / `StatisticsCategorySection` 收进新层级而不是沿用旧体量
- 必须验证：运行 `npm run lint` 与 `npm run build`；确认登录后能正常进入 `/statistics`；确认无账本、loading、error、empty、正常数据五种主状态都可渲染；确认 `刷新统计` 与 `应用筛选` 在当前账本上下文下正常工作
- 不得偏离：不得保留 `hero + 白色工作区 + 右侧信息栏` 的旧阅读路径；不得把趋势区再次做成普通次级卡片；不得引入蓝图外的图表类型、额外筛选器或新的业务动作；不得改动现有认证守卫语义
