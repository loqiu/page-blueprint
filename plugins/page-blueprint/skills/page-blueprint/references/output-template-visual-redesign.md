# Visual Redesign Blueprint Template

Always emit the page blueprint in this section order when `改造级别 = visual-redesign`.

```md
# <页面名称> 改造蓝图

## 1. 页面定位
- 页面目标：
- page mode：
- 核心对象：
- 主要用户：
- 首要任务：
- 成功判定：

## 2. 依据与假设
- 改造级别：visual-redesign
- 已确认事实：
- 关键假设：
- 明确不做：

## 3. 旧结构骨架
- 当前页面壳模式：
- 当前主路由 / 页面归属：
- 当前共享壳 / 页面骨架：
- 当前首屏顺序：
- 当前主导载体：
- 当前一级模块顺序：
- 当前结构最关键的问题：

## 4. 重构目标与硬约束
- 首屏必须先回答什么：
- 页面主舞台是什么：
- 这次必须打掉的旧结构：
- 允许保留的少数资产：
- 不得牺牲什么：
- 为什么需要大改造：

## 5. 新结构骨架
- 新页面壳模式：
- 主路由：
- 路由归属理由：
- 共享壳决策：
- 新的首屏顺序：
- 主导载体：
- 一级模块顺序：

## 6. 新信息架构与阅读路径
- 首屏必须先看到：
- 10 秒阅读路径：
- 页面层级顺序：
- 主区 / 次区 / 支撑区：
- drill-down / 返回路径：
- 被降级 / 合并 / 移除的旧模块：

## 7. 页面模块拆解
### M1. <模块名>
- 目标：
- 关键内容：
- 为什么它现在在这里：
- 组件结构：
- 交互：
- 状态：

### M2. <模块名>
- 目标：
- 关键内容：
- 为什么它现在在这里：
- 组件结构：
- 交互：
- 状态：

## 8. 组件规范
### 8.1 继续复用的组件
- 组件名：
- 为什么还能保留：
- 责任：
- 允许保留到什么程度：
- 状态 / 变体：

### 8.2 新增组件
- 组件名：
- 为什么旧组件不够：
- 责任：
- 组合关系：
- 必要状态 / 变体：
- 依赖的全局规则：

## 9. 状态矩阵
- loading：
- empty：
- error：
- disabled：
- stale / outdated：
- permission-restricted：

## 10. 关键交互路径
- 筛选 / 搜索：
- 排序 / 比较：
- drill-down / 返回：
- 危险操作保护：
- 审计 / 历史查看：

## 11. 关键命名与动作
- 页面标题：
- 主操作文案：
- 空状态文案：
- 错误文案：
- 权限 / 限制文案：

## 12. 响应式策略
- Desktop：
- Tablet：
- Mobile：

## 13. 待确认项
- Q1：
- Q2：

## 14. 实现附录
### 14.1 实现落点
- 页面壳模式：
- 共享壳决策：
- 目标页面文件：
- 需要新增的 page-local 组件：
- 直接复用的共享组件：
- 需要接入或确认的路由 / 壳组件：

### 14.2 数据与状态归属
- 页面内状态：
- store / composable 归属：
- API / data access 归属：
- 派生状态：

### 14.3 组件树
- 页面根：
- 一级模块树：
- 新增组件边界：

### 14.4 接口与字段依赖
- 直接依赖接口：
- 关键字段：
- 错误与空状态依赖：

### 14.5 Builder 验收点
- 必须完成：
- 必须验证：
- 不得偏离：
```

## Template Rules

- This template is for structure-first redesign. The blueprint must explain what is being replaced, not just what is being added.
- `旧结构骨架` is mandatory. If you cannot state the current shell, dominant surface, and first-screen order, the task is not ready for a redesign.
- `重构目标与硬约束` is mandatory. If you cannot state what must change and what must survive, the redesign direction is not ready.
- `新结构骨架` and `新信息架构与阅读路径` must define a new reading path and module hierarchy. Enlarging the old layout is not enough.
- The new structure must be explainable without visual adjectives. If deleting words about style or tone collapses the redesign argument, the blueprint is aesthetic drift.
- `共享壳决策` may be `reuse`, `variant`, or `bypass`, but if the redesign still keeps the old shell, the blueprint must explain why the shell is not preventing the new structure.
- If the document mostly preserves the old layout and only tunes modules, stop and switch to `output-template-safe-refactor.md`.
