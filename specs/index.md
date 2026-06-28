# 设计规范模块索引

> 供 design-spec Skill 读取，用于判断按需加载哪些规范模块。

## Tokens（原子级）

| 文件 | 内容 | 典型关联场景 |
|------|------|------------|
| tokens/colors.md | 品牌色、功能色、中性色、背景色 | 几乎所有场景 |
| tokens/typography.md | 字号、行高、字重 | 文字展示、列表、表单 |
| tokens/spacing.md | 间距系统（内外边距） | 几乎所有场景 |
| tokens/radius.md | 圆角系统 | 卡片、按钮、浮层 |
| tokens/shadow.md | 阴影系统 | 浮层、弹窗、卡片 |
| tokens/mask.md | 蒙层透明度系统（黑/白色系，30%～90%）| 弹窗、半浮层、促销层 |

## Components（组件级）

| 文件 | 内容 | 典型关联场景 |
|------|------|------------|
| components/button.md | 按钮变体、使用规则 | 操作类页面 |
| components/modal.md | 弹窗规范 | 确认操作、临时输入 |
| components/bottom-sheet.md | 半浮层规范 | 移动端多选项操作、筛选面板 |
| components/toast.md | 轻提示规范 | 操作反馈 |
| components/input.md | 输入框、表单控件 | 表单页面 |
| components/navigation.md | 导航栏、底部 Tab | 页面级框架 |
| components/card.md | 卡片、列表项 | 内容列表、信息展示 |
| components/empty-state.md | 空态、错误态 | 列表页、加载态 |
| components/reminder-label.md | 提醒标签（红点/数量徽标）| 消息、订单、通知、筛选入口提醒 |

## Layout（布局规范）

| 文件 | 内容 | 典型关联场景 |
|------|------|------------|
| layout/mobile.md | 移动端页面结构、安全区 | 移动端页面 |
| layout/pc.md | PC 端页面结构、栅格 | PC 端页面 |

## 始终加载

| 文件 | 内容 |
|------|------|
| constraints.md | 全局禁止事项（每次必须加载）|
