# Settings / Admin 设计

## 1. Purpose

本文档定义 settings / admin 风格页面的设计规则。

当页面主要用于以下场景时，使用此模式：
- preferences
- account or workspace settings
- permission management
- policy or rule editing
- admin configuration

此模式不适用于：
- KPI summary dashboards
- browse/discovery surfaces
- queue handling consoles

---

## 2. Core Intent

页面应按以下顺序回答问题：
1. 我正在配置什么范围？
2. 当前状态是什么？
3. 可以改什么？
4. 改动的影响是什么？

布局应优先考虑：
- scope clarity
- safe editing
- stable section grouping
- consequence visibility

---

## 3. Page Anatomy

推荐的自上而下顺序：
1. page title + scope identity
2. critical notices or permission status
3. primary settings sections
4. supporting sections or audit/history

不要把 settings page 做成 dashboard。section grouping 比视觉刺激更重要。

---

## 4. Layout Rules

### Section Structure
- 使用明确的 section 分组
- 每组应围绕一个稳定主题：profile、preferences、roles、rules、billing 等

### Actions
- save / apply / reset 等主要动作应靠近所属 section 或页面顶层 summary
- destructive actions 必须与常规保存动作清晰分离

### Metadata
- role、scope、last updated、permission 等 supporting metadata 应清楚但不抢主位

---

## 5. Information Density

此模式应给人这样的感受：
- controlled
- trustworthy
- readable
- operational

密度规则：
- 默认 medium
- 比 marketing page 更紧凑
- 比 operations console 更从容

---

## 6. Form and Policy Rules

优先表达：
1. scope
2. current value
3. editable control
4. side effect or helper copy

不要：
- 把 helper copy 写成大段营销文案
- 让每个 setting 都像促销模块
- 让 destructive action 与 save action 同权重

---

## 7. Interaction Rules

- unsaved changes 应可见
- disabled controls 应解释原因
- role or permission restricted sections 应明确说明
- settings save 不应强依赖模糊的 global action placement

---

## 8. States

### Empty
- 说明当前没有可配置对象，还是没有权限查看

### Error
- section-level failure 优先，不要抹掉整页

### Loading
- 保留 section skeleton，避免整个页面闪烁

### Restricted
- 必须明确说明当前角色限制和可联系路径

---

## 9. Responsive Rules

Desktop:
- section grouping 清楚
- form labels 和 helper copy 不应挤压主控件

Tablet:
- 多列 section 适度回落为单列

Mobile:
- 以单列 section 为主
- 优先保留 scope、control、save path；历史和 supporting info 后移
