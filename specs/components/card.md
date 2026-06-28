# 卡片（Card）组件规范

## 变体与使用场景

| 变体 | 使用场景 |
|------|---------|
| Basic Card | 通用信息展示容器，无固定内部结构 |
| List Item | 列表中的单行/多行条目，含图标或缩略图 |
| Product Card | 电商商品卡，含图片、标题、价格 |
| Info Card | 数据统计、关键指标展示 |

## 结构规范

### Basic Card

Card
├── 背景：color-bg-card，radius-md，shadow-sm（可选）
├── 内边距：spacing-16
├── 标题区（可选）：text-heading-md + 右侧操作（可选）
├── 内容区：可注入任意内容
└── 操作区（可选）：Button 组，右对齐或撑满

### List Item

List Item
├── 左侧：图标（24px）或 头像（32px）或 缩略图（48×48px）
├── 中间内容区（flex: 1）
│   ├── 主标题：text-body-md，color-text-primary
│   └── 副标题（可选）：text-body-sm，color-text-secondary
└── 右侧（可选）：文字说明 / 箭头图标 / 操作按鈕

## 尺寸约束

- 卡片内边距：spacing-16（标准）/ spacing-12（紧凑）
- 卡片圆角：radius-md
- 列表项最小高度：【填入 px，建议 56px（单行）/ 72px（双行）】
- 列表项左右内边距：spacing-16
- 相邻列表项分割线：1px，color-border（或用间距 spacing-1 替代）
- 相邻卡片间距：spacing-12

## 禁止事项

- 禁止卡片内直接嵌套同层级卡片（同级并列，不同层级用内容区块区分）
- 禁止列表项高度小于 44px（移动端触控最小区域）
- 禁止在卡片内放置超过 2 个操作按鈕（超出用更多菜单收纳）
- 禁止卡片不加任何背景/边框/阴影（必须有视觉区分）

---

## 组件 Schema（AI 调用参考）

{
  "componentName": "Card",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "description": "通用信息展示容器，通过 variant 区分使用场景。是页面内容的基本承载单元。",
  "properties": {
    "variant": {
      "type": "string",
      "enum": ["basic", "list-item", "product", "info"],
      "default": "basic"
    },
    "padding": {
      "type": "string",
      "enum": ["normal", "compact", "none"],
      "default": "normal",
      "description": "normal=spacing-16；compact=spacing-12；none=无内边距（内容自行控制）"
    },
    "showShadow": { "type": "boolean", "default": true },
    "showDivider": {
      "type": "boolean",
      "default": false,
      "description": "列表项底部是否显示分割线，list-item variant 常用"
    },
    "clickable": {
      "type": "boolean",
      "default": false,
      "description": "是否可点击；为 true 时显示 press 态背景色 color-bg-hover"
    }
  },
  "slots": {
    "header": {
      "description": "卡片头部，可放标题、副标题、右侧操作",
      "acceptedComponents": ["Text", "Icon", "Button"]
    },
    "content": {
      "description": "卡片主内容区，可注入任意内容组件",
      "acceptedComponents": ["*"]
    },
    "footer": {
      "description": "卡片底部操作区，最多 2 个操作按鈕",
      "acceptedComponents": ["Button", "ButtonGroup"]
    },
    "leading": {
      "description": "list-item 变体左侧区域，放图标、头像或缩略图",
      "acceptedComponents": ["Icon", "Avatar", "Image"]
    },
    "trailing": {
      "description": "list-item 变体右侧区域，放说明文字、箭头、操作按鈕",
      "acceptedComponents": ["Icon", "Text", "Button"]
    }
  },
  "usageRules": [
    "禁止卡片内直接嵌套同层级卡片",
    "列表项高度不低于 44px",
    "卡片内操作按鈕不超过 2 个",
    "可点击卡片须设 clickable=true 以显示交互反馈"
  ]
}
