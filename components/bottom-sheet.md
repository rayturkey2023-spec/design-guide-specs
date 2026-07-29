# 半浮层（Bottom Sheet / Action Sheet）组件规范

## 使用场景

- 提供多个操作选项（3 个以上操作时优于弹窗）
- 筛选面板、分享面板、更多操作菜单
- 需要展示中等量内容而不跳转页面

## 禁止场景

- 禁止用于复杂表单填写（改用全屏页面）
- 禁止与底部导航栏同时出现在同一操作流内（层级冲突）
- 内容高度超过屏幕 75% 时，改为全屏 Drawer
- 仅适用于移动端；PC 端使用 Dropdown 或侧边 Drawer 替代

## 结构规范

```
半浮层
├── 遮罩层（color-bg-overlay，点击遮罩关闭）
└── 浮层容器（顶部 radius-lg，底部无圆角，color-bg-card，shadow-lg）
    ├── 拖拽指示条（可选）：居中，宽 40px，高 4px，radius-full，color-border
    ├── 标题行（可选）：text-heading-md，左对齐 + 右上角关闭按钮
    ├── 内容区：padding spacing-16，内容超出高度时内部滚动
    └── 底部操作区（可选）：固定在底部，含系统安全区间距
```

## 高度规范

- 最小高度：自适应内容
- 最大高度：屏幕高度 × 75%
- 超出最大高度时，内容区开启滚动，标题行与操作区固定

## 动效规范

- 进入：从底部滑入，时长 250ms，缓动 ease-out
- 退出：向底部滑出，时长 200ms，缓动 ease-in
- 遮罩：透明度渐变，与浮层同步

---

## 组件 Schema（AI 调用参考）

```json
{
  "componentName": "BottomSheet",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "description": "移动端专用的从底部弹出的浮层容器，适合多选项操作、筛选面板、分享菜单等场景。比弹窗更轻量，不强制中断用户流程。仅限移动端使用。",
  "platform": "mobile-only",
  "properties": {
    "showDragIndicator": {
      "type": "boolean",
      "default": true,
      "description": "是否显示顶部拖拽指示条；内容较多可拖拽时建议开启"
    },
    "showTitle": {
      "type": "boolean",
      "default": false,
      "description": "是否显示标题行；纯操作列表类（如分享菜单）通常不需要标题"
    },
    "title": {
      "type": "string",
      "description": "标题文字，showTitle 为 true 时生效"
    },
    "showCloseButton": {
      "type": "boolean",
      "default": true,
      "description": "标题行右上角是否显示关闭按钮，showTitle 为 true 时有效"
    },
    "showFooter": {
      "type": "boolean",
      "default": false,
      "description": "是否显示底部固定操作区；筛选面板类场景需要'重置+应用'按钮时开启"
    },
    "maskClosable": {
      "type": "boolean",
      "default": true,
      "description": "点击遮罩是否关闭浮层；默认可关闭，强制选择场景可设为 false"
    }
  },
  "slots": {
    "content": {
      "description": "浮层主内容区，可注入操作列表、筛选条件、分享选项等任意内容",
      "acceptedComponents": ["ActionList", "FilterPanel", "ShareGrid", "Form", "List"],
      "scrollable": true,
      "maxHeightRule": "内容区最大高度为屏幕高度 75% 减去标题行和底部操作区高度"
    },
    "footer": {
      "description": "底部固定操作区，showFooter 为 true 时渲染，常用于筛选面板的'重置+应用'",
      "acceptedComponents": ["Button", "ButtonGroup"],
      "note": "底部操作区自动包含系统安全区间距，无需手动添加"
    }
  },
  "usageRules": [
    "仅限移动端使用，PC 端同类场景请改用 Dropdown 或 Drawer 组件",
    "内容高度超过屏幕 75% 时禁止使用，改为全屏页面或全屏 Drawer",
    "禁止与页面底部导航栏（Tab Bar）同时出现在同一操作流中",
    "操作列表类（如分享、更多操作）不需要标题行，设 showTitle: false",
    "筛选面板类必须开启 showFooter 提供'重置'和'应用'操作入口",
    "禁止在浮层内再嵌套 BottomSheet 或 Modal"
  ]
}
```
