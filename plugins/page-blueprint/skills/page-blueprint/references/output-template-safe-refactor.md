# Safe Refactor Blueprint Template

Always emit the page blueprint in this section order when `改造级别 = safe-refactor`.

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
- 改造级别：safe-refactor
- 已确认事实：
- 关键假设：
- 明确不做：

## 3. 继承边界
- 页面壳模式：
- 保留的主路由 / 导航关系：
- 保留的共享壳 / 页面骨架：
- 保留的核心模块：
- 不得破坏的用户路径：

## 4. 当前问题与改造目标
- 当前页面的主要问题：
- 这次只解决什么：
- 这次明确不重做什么：
- 为什么保持保守改造：

## 5. 信息架构微调
- 首屏必须先看到：
- 主导载体：
- 保留的阅读路径：
- 需要调整的层级：

## 6. 模块调整清单
### M1. <模块名>
- 当前职责：
- 保留内容：
- 需要调整：
- 组件结构：
- 交互：
- 状态：

### M2. <模块名>
- 当前职责：
- 保留内容：
- 需要调整：
- 组件结构：
- 交互：
- 状态：

## 7. 组件规范
### 7.1 继续复用的组件
- 组件名：
- 保留理由：
- 责任：
- 需要调整的点：
- 状态 / 变体：

### 7.2 新增或替换组件
- 组件名：
- 为什么需要新增或替换：
- 责任：
- 组合关系：
- 必要状态 / 变体：
- 依赖的全局规则：

## 8. 状态矩阵
- loading：
- empty：
- error：
- disabled：
- stale / outdated：
- permission-restricted：

## 9. 业务文案
- 页面标题：
- 页面副标题 / 定位文案：
- 主操作文案：
- 次操作文案：
- 空状态文案：
- 错误文案：
- 权限 / 限制文案：

## 10. 交互与规则
- 筛选 / 搜索：
- 排序 / 比较：
- drill-down / 返回：
- 危险操作保护：
- 审计 / 历史查看：

## 11. 响应式策略
- Desktop：
- Tablet：
- Mobile：

## 12. 待确认项
- Q1：
- Q2：

## 13. 实现附录
### 13.1 实现落点
- 页面壳模式：
- 共享壳决策：
- 目标页面文件：
- 需要新增的 page-local 组件：
- 直接复用的共享组件：
- 需要接入或确认的路由 / 壳组件：

### 13.2 数据与状态归属
- 页面内状态：
- store / composable 归属：
- API / data access 归属：
- 派生状态：

### 13.3 组件树
- 页面根：
- 一级模块树：
- 新增组件边界：

### 13.4 接口与字段依赖
- 直接依赖接口：
- 关键字段：
- 错误与空状态依赖：

### 13.5 Builder 验收点
- 必须完成：
- 必须验证：
- 不得偏离：
```

## Template Rules

- This template is for preservation-first work. The blueprint should state what stays before it states what changes.
- `继承边界` is mandatory. If you cannot say what must remain stable, the task is not ready for `safe-refactor`.
- `模块调整清单` must describe deltas, not a fully reimagined layout.
- Use `共享壳决策 = reuse` or `variant` by default. Use `bypass` only with explicit proof that the shared shell blocks the required change.
- If the document starts redefining the page from scratch, stop and switch to `output-template-visual-redesign.md`.
