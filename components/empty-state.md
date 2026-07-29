# 空态与异常态（Empty State / Error State）规范

## 使用场景

| 类型 | 触发条件 |
|------|---------|
| 空列表 | 搜索结果为空、列表无数据 |
| 无内容 | 用户未创建任何内容（新用户引导） |
| 网络错误 | 请求失败、超时 |
| 无权限 | 用户无访问权限 |
| 加载中 | 数据请求中，防止内容闪烁 |

## 结构规范

### 空态 / 错误态

空态容器（居中布局，垂直方向居中于内容区）
├── 插图（可选）：宽度 【填入 px，建议 160px】，统一使用规范插图资源
├── 主标题：text-heading-md，color-text-primary，居中
├── 描述文字（可选）：text-body-md，color-text-secondary，居中，最多 2 行
└── 操作按鈕（可选）：单个 Primary 或 Ghost 按鈕，居中

### 加载中（Skeleton）

- 使用骨架屏（Skeleton Screen）替代 Loading Spinner 全屏占位
- 骨架屏形状模拟真实内容布局（矩形条块替代文字，方块替代图片）
- 骨架屏颜色：color-bg-hover，动效：shimmer 横向扫光
- 禁止使用全屏旋转 Spinner 作为列表/页面加载状态

## 位置规范

- 整页空态：垂直居中于内容区（距顶部 NavBar 的 1/3 处）
- 局部空态（如卡片内）：居中于所在容器
- 最小高度：包含插图时不低于 【填入 px，建议 240px】

## 禁止事项

- 禁止空态页面无任何操作引导（至少提供一个操作出口）
- 禁止网络错误态不提供「重试」按鈕
- 禁止使用全屏 Loading Spinner 遗挡整个页面（改用骨架屏）
- 禁止空态文案使用技术性错误信息直接展示给用户

---

## 组件 Schema（AI 调用参考）

{
  "componentName": "EmptyState",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "description": "用于列表无数据、请求错误、无权限等异常场景的占位组件。须包含引导用户下一步操作的入口。",
  "properties": {
    "type": {
      "type": "string",
      "enum": ["empty-list", "no-content", "network-error", "no-permission", "loading"],
      "description": "empty-list=搜索/筛选无结果；no-content=用户尚未创建内容；network-error=请求失败；no-permission=无权限；loading=骨架屏加载态"
    },
    "illustration": {
      "type": "string",
      "description": "插图资源名称，使用规范插图库中的图片，留空则不显示插图"
    },
    "title": { "type": "string", "description": "主标题文字" },
    "description": { "type": "string", "description": "描述文字，最多 2 行" },
    "actionLabel": { "type": "string", "description": "操作按鈕文字，如「重试」「去创建」「返回」" },
    "actionVariant": {
      "type": "string",
      "enum": ["primary", "ghost"],
      "default": "primary"
    }
  },
  "slots": {
    "action": {
      "description": "自定义操作区，默认使用 actionLabel 渲染单个按鈕，复杂场景可自定义",
      "acceptedComponents": ["Button", "ButtonGroup"]
    }
  },
  "usageRules": [
    "所有列表页面必须设计 empty-list 和 network-error 两种状态",
    "network-error 必须提供重试操作按鈕",
    "加载中状态使用 type=loading 骨架屏，禁止全屏旋转 Spinner",
    "空态文案须使用用户可理解的语言，禁止展示技术性错误信息",
    "空态页面必须提供至少一个操作出口"
  ]
}
