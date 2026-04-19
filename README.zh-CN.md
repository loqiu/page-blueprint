# 中文 | [English](README.md)

# Page Blueprint

> 面向 Codex 的前端页面蓝图与实现双 Skill 仓库。

![Codex](https://img.shields.io/badge/Codex-Skills-111827?style=flat-square)
![Workflow](https://img.shields.io/badge/Workflow-Blueprint%20%E2%86%92%20Builder-2563eb?style=flat-square)
![Shell](https://img.shields.io/badge/Shell%20Mode-Workspace%20%7C%20Centered-0f766e?style=flat-square)
![Figma](https://img.shields.io/badge/Figma-MCP%20Ready-f97316?style=flat-square)
![License](https://img.shields.io/badge/License-GPL--2.0-16a34a?style=flat-square)
![Release](https://img.shields.io/badge/Release-v0.1.0-7c3aed?style=flat-square)

Page Blueprint 由两个核心 Skill 组成：

- `page-blueprint`：把产品目标、设计规则、截图和仓库上下文收敛成一份可评审的页面蓝图文档。
- `page-builder`：基于批准版蓝图落代码，不偏离路由、层级、状态、文案和页面壳结构。

这个仓库不是为了生成“像 UI 截图的页面”，而是为了让 Codex 更稳定地生成：

- 像真实产品一部分的页面
- 有明确主任务的工具型页面
- 有稳定信息层级的工作台页面
- 有真实状态处理的页面
- 能接进现有系统的页面

## `v0.1.0` 当前包含什么

- 双 Skill 工作流：
  - `skills/page-blueprint`
  - `skills/page-builder`
- 共享设计智能层：
  - 全局设计规则
  - page-mode 设计源
  - 专业页面生成规范
  - `workspace shell / centered page` 判定规则
- Builder 交接结构：
  - 实现附录
  - pre-code summary
  - verification contract
- 示例产物：
  - `shared/examples/moneykeeper-vue-statistics-blueprint.md`
- 可接 Figma MCP 的蓝图转结构稿流程

## 这个仓库解决什么问题

典型 AI 生成后台页的问题几乎都一样：

- 看起来像居中的设计稿画布，不像真实应用壳
- KPI、图表、表格、侧栏平均用力，主次不清
- 过度使用 hero、渐变、浮卡和通用 dashboard 模板
- 还没判断 page mode、dominant surface、route/context/state 就开始写代码

这个仓库的目的，就是强制 Codex 先走一条更严谨的路径：

1. 先理解页面目标
2. 先判断页面类型
3. 先决定页面壳模式
4. 先写页面蓝图
5. 可选生成 Figma / mock 结构
6. 再根据蓝图落代码

## 仓库结构

```text
skills/
  page-blueprint/
  page-builder/
shared/
  design/
    global/
    page-modes/
  examples/
  guides/
output/
  imagegen/
```

## 核心概念

### 1. 蓝图不是可选项

`page-builder` 不应该只看截图开工。  
批准版蓝图才是逻辑真源。

### 2. 页面壳模式是结构决策，不是装饰决策

- `workspace shell`
  - 系统中的持续工作节点
  - 左侧导航 / 顶部工具栏 / 主区流动展开
  - 信息密度中高到高
  - 适合控制台、工作台、后台、分析页
- `centered page`
  - 有边界的页面画布
  - 更偏单页任务
  - 信息密度低到中
  - 适合登录、引导、支付、设置表单、单对象详情

### 3. 大改造不是换皮

当蓝图标记为 `visual-redesign` 时，结果必须在这些层面发生明显改变：

- 页面壳策略
- 首屏顺序
- dominant surface
- 模块层级

只改间距和样式，不算真正的大改造。

## 如何在 Codex 中安装

当前这个仓库是一个 **skills 仓库**，不是一个完整的 Codex plugin 包。

这意味着：

- `v0.1.0` 可以作为有版本的 skills 安装
- `v0.1.0` 还不能当成“一键插件包”直接安装

### 推荐安装方式

直接让 Codex 使用内置的 `$skill-installer`，从这个仓库的 `v0.1.0` tag 安装：

- repo：`loqiu/page-blueprint`
- ref：`v0.1.0`
- paths：
  - `skills/page-blueprint`
  - `skills/page-builder`

### 脚本安装

Windows：

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.0
```

macOS / Linux：

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo loqiu/page-blueprint \
  --path skills/page-blueprint skills/page-builder \
  --ref v0.1.0
```

安装后：

1. 重启 Codex。
2. 先用 `page-blueprint` 生成页面蓝图。
3. 再用 `page-builder` 基于批准版蓝图落代码。

## 这个 release 能直接当 plugin 吗

不能直接当。

`v0.1.0` 目前是一个 **skills repo 的发布版本**，不是 Codex 插件包。  
如果后续要变成真正的 plugin release，还需要补：

- `.codex-plugin/plugin.json`
- 插件级元数据与打包结构
- 面向 plugin 的安装路径

这可以在后续版本加上，但不影响当前 skill 工作流。

## 首次使用建议流程

### 已经有 UI 仓库

1. 把仓库路径交给 Codex。
2. 先让 `page-blueprint` 做项目 intake。
3. 确认：
   - 目标页
   - page mode
   - shell mode
   - `safe-refactor` 或 `visual-redesign`
4. 批准蓝图。
5. 可选：把蓝图推到 Figma 里继续改。
6. 再运行 `page-builder`。

### 还没有 UI 仓库

1. 先走 `page-blueprint` 的 greenfield 模式。
2. 明确：
   - 目标页
   - 主要用户
   - 主任务
   - page mode
   - shell mode
3. 先产出页面蓝图。
4. 可选生成 Figma 结构稿。
5. 只有当真实代码仓库存在时，再进入 `page-builder`。

## 版本策略

这个仓库会通过 tag / release 持续迭代。

- `v0.1.0`：首个公开的双 Skill 版本

具体变化见 [CHANGELOG.md](CHANGELOG.md)。

## License

本仓库采用 GNU GPL-2.0 协议，详见 [LICENSE](LICENSE)。
