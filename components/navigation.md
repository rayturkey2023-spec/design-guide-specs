# 导航（Navigation）组件规范

## 组件类型

| 类型 | 平台 | 使用场景 |
|------|------|---------|
| TopBar / NavBar | 移动端 | 页面顶部导航，含返回、标题、右侧操作 |
| Tab Bar | 移动端 | 底部一级导航，2-5 个 Tab |
| Header | PC 端 | 顶部全局导航，含 Logo、主导航菜单 |
| Breadcrumb | PC 端 | 多层级页面的路径导航 |
| Side Nav | PC 端 | 侧边导航菜单 |

## TopBar / NavBar 规范（移动端）

### 结构规范

NavBar
├── 左侧区域：返回按鈕（图标，44×44px 触控区）
├── 标题区域：text-heading-md，居中或左对齐统一选一种
└── 右侧区域：操作图标，最多 2 个，间距 spacing-8

### 尺寸约束

- 高度：【填入 px，建议 44px】
- 背景：color-bg-card
- 底部分割线：1px，color-border（视设计风格可选）
- 右侧操作图标尺寸：24×24px，触控区 44×44px

### 禁止事项

- 禁止右侧操作超过 2 个图标（超出用「…更多」收纳）
- 禁止标题文字超过 1 行（过长时截断加「…」）
- 禁止在 NavBar 内放置 Primary 按鈕

## Tab Bar 规范（移动端）

### 结构规范

Tab Bar
├── 背景：color-bg-card，顶部分割线 color-border
├── 每个 Tab：图标（选中/未选中态）+ 文字标签
│   ├── 选中态：color-primary + text-caption
│   └── 未选中态：color-text-secondary + text-caption
└── 底部：系统安全区自动填充

### 尺寸约束

- 高度（不含安全区）：【填入 px，建议 50px】
- Tab 数量：2-5 个，超过 5 个改用侧边导航
- 图标尺寸：24×24px
- 图标与文字间距：spacing-2

### 禁止事项

- 禁止 Tab 数量超过 5 个
- 禁止 Tab 标签文字超过 4 个字
- 禁止在 Tab Bar 上方弹出 Bottom Sheet 时不隐藏 Tab Bar（层级冲突）

---

## 组件 Schema（AI 调用参考）

NavBar:
{
  "componentName": "NavBar",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "platform": "mobile-only",
  "description": "移动端页面顶部导航栏，提供返回导航、页面标题展示和右侧操作入口。",
  "properties": {
    "title": { "type": "string" },
    "showBack": { "type": "boolean", "default": true },
    "titleAlign": { "type": "string", "enum": ["center", "left"], "default": "center" },
    "rightActions": { "type": "array", "maxItems": 2, "description": "右侧操作图标，最多 2 个" }
  },
  "usageRules": [
    "右侧操作最多 2 个图标，超出用更多菜单收纳",
    "标题超出一行时截断，不换行",
    "NavBar 内禁止放置 Primary Button"
  ]
}

TabBar:
{
  "componentName": "TabBar",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "platform": "mobile-only",
  "description": "移动端底部一级导航，用于应用的顶层模块切换。",
  "properties": {
    "items": { "type": "array", "minItems": 2, "maxItems": 5 },
    "activeIndex": { "type": "number" }
  },
  "usageRules": [
    "Tab 数量限制 2-5 个",
    "Tab 文字不超过 4 个字",
    "底部包含系统安全区，不可手动添加额外间距"
  ]
}
