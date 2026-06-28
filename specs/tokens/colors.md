# 颜色 Token

## 品牌色

| Token | 色值 | 使用场景 | 禁止场景 |
|-------|------|---------|---------|
| color-primary | 【填入 #HEX】 | 主操作按钮、选中态、关键链接、进度条 | 不用于大面积背景；不与警告红并列 |
| color-primary-light | 【填入 #HEX】 | 选中态背景、Tag 背景 | 不单独用于文字 |
| color-primary-dark | 【填入 #HEX】 | 按下态、hover 态 | 仅用于交互反馈，不用于静态展示 |

## 功能色

| Token | 色值 | 使用场景 |
|-------|------|---------|
| color-success | 【填入 #HEX】 | 成功提示、完成状态、正向数据 |
| color-warning | 【填入 #HEX】 | 警告提示、待处理状态 |
| color-danger | 【填入 #HEX】 | 错误提示、删除操作、危险警示 |
| color-info | 【填入 #HEX】 | 普通提示、说明信息 |

## 中性色（文字）

| Token | 色值 | 使用场景 |
|-------|------|---------|
| color-text-primary | 【填入 #HEX】 | 标题、正文主要内容 |
| color-text-secondary | 【填入 #HEX】 | 辅助说明、标签、次要信息 |
| color-text-placeholder | 【填入 #HEX】 | 输入框占位文字 |
| color-text-disabled | 【填入 #HEX】 | 禁用控件的文字 |
| color-text-inverse | 【填入 #HEX】 | 深色背景上的文字（如 Primary 按钮内文字）|

## 边框色

| Token | 色值 | 使用场景 |
|-------|------|---------|
| color-border | 【填入 #HEX】 | 分割线、输入框默认边框 |
| color-border-strong | 【填入 #HEX】 | 选中边框、强调边框 |

## 背景色层级

| Token | 色值 | 使用场景 |
|-------|------|---------|
| color-bg-page | 【填入 #HEX】 | 整体页面背景（最底层）|
| color-bg-card | 【填入 #HEX】 | 卡片、表单区块背景 |
| color-bg-hover | 【填入 #HEX】 | 列表项 hover / 按下态背景 |
| color-bg-overlay | 【填入 #HEX，含透明度，如 rgba(0,0,0,0.5)】 | 遮罩层背景 |

## 颜色使用约束

- 同一屏内主色系与功能色不超过 3 种
- 文字与背景对比度必须达到 AA 级（4.5:1 以上）
- 禁止使用规范 Token 以外的自定义色值
