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
| components/tab-navigation.md | Tab 内容切换导航（一级/二级/多级组合） | 内容分类切换、页面内局部导航、多层级信息架构 |
| components/card.md | 卡片、列表项 | 内容列表、信息展示 |
| components/empty-state.md | 空态、错误态 | 列表页、加载态 |
| components/reminder-label.md | 提醒标签（红点/数量徽标）| 消息、订单、通知、筛选入口提醒 |

## Layout（布局规范）

| 文件 | 内容 | 典型关联场景 |
|------|------|------------|
| layout/mobile.md | 移动端页面结构、安全区 | 移动端页面 |
| layout/pc.md | PC 端页面结构、栅格 | PC 端页面 |

## Regulations（合规规范）

| 文件 | 内容 | 典型关联场景 |
|------|------|------------|
| regulations/合规知识库-欧盟通用EU.md | 欧盟通用合规规则（暗黑模式 EU-D / 信息披露 EU-I） | 欧盟所有站点设计方案 |
| regulations/合规知识库-法国站FR.md | 法国站专项合规规则（价格展示 FR-P / 暗黑模式 FR-D） | 法国站设计方案 |

## 流程规则（Process）

| 文件 | 内容 | 典型关联场景 |
|------|------|------------|
| prd-intake-rules.md | 提需阶段准入规则，Agent 1 必填字段校验 + 追问话术 + 合规触发规则 | 产品提需、需求接收 |
| audit-scoring.md | 审核评分规则，评分维度/严重等级/评级标准/输出 JSON 格式 | 审核 Agent 评分、结果写入 Google Sheets |

## 始终加载

| 文件 | 内容 |
|------|------|
| constraints.md | 全局禁止事项（每次必须加载）|
