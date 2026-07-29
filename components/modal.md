# 模态弹窗（Modal / Dialog）组件规范

## 使用场景

- 需要用户明确确认的操作（删除、提交、风险提示）
- 需要临时输入少量信息（单字段填写、单项选择）
- 内容层级需与当前页面明显区分
- 承载表单、纯阅读字段、业务交互等暂态容器，相比半浮层更具备阻断性

## 禁止场景

- 禁止弹窗内嵌套弹窗
- 禁止用于非关键提示（用 Toast 替代）
- 禁止自动弹出（必须由用户操作触发）
- 禁止底部按钮区为空（底部按钮必须配置）
- 禁止内容区域未撑满最大高度时出现滚动条

---

## 一、对话框弹窗（Dialog）

### 简述

弹窗是一种暂态容器，承载表单、纯阅读字段、业务交互等，该容器相比半浮层更具备阻断性。

### 结构规范

```
页面
├── 背景遮罩（#000000，60% 不透明度）
└── 弹窗容器（圆角 8px，白色背景 sui_color_white）
    ├── 顶部栏（可配置：纯色 / 图片背景 / 不配置关闭按钮）
    │   └── 关闭按钮（右上角 x 图标，可选隐藏）
    ├── 内容区（自定义内容：主文字 / 次文字 / 图片等）
    └── 底部按钮区（必选：单按钮 / 双按钮水平 / 双按钮垂直）
```

### 尺寸约束

| 维度 | 规则 |
|------|------|
| 宽度 | 固定宽度，安卓左右两边与屏幕保留 10% 间距 |
| 最小高度 | 150px |
| 最大高度 | 498px（屏幕高度的 60%） |
| 圆角 | 8px（可自定义） |

### 间距规范

| 位置 | 数值 |
|------|------|
| 内容区左右边距 | 16px |
| 底部边距 | 20px |

### 可配置项

#### 顶部栏

| 配置 | 说明 |
|------|------|
| 纯色 | 白色背景 + 关闭按钮，圆角 8px 8px 0 0 |
| 图片 | 图片背景 + 关闭按钮，圆角 8px 8px 0 0 |
| 不配置关闭按钮 | 隐藏 x，强制用户通过底部按钮操作 |

#### 底部按钮区

| 样式 | 说明 |
|------|------|
| 单按钮（按钮×1）| 一个深色背景主按钮，高度 36pt，圆角 2px |
| 双按钮水平（按钮×2_水平）| 左侧线框按钮(次操作) + 右侧深色按钮(主操作) |
| 双按钮垂直（按钮×2_垂直）| 上方深色按钮(主操作) + 下方线框按钮(次操作) |
| 按钮&文字 | 按钮 + 链接文字（功能色 sui_color_link）|

#### 内容区变体

| 变体属性 | 可选值 |
|---------|--------|
| 主标题 | yes / no |
| 副文案 | yes / no |
| 图片 | yes / no |
| 图片位置 | 无 / 顶部沉浸式 / 上图下文 / 上文下图 |
| 最大高度 | yes（限制高度，内滚动） / no |
| 自定弹窗 | yes（完全自定义内容） / no |

### 特殊情况：隐藏关闭按钮

对话框弹窗需要点击"关闭"按钮才能对弹窗进行关闭（点击弹窗之外区域不关闭），以下三种情况需要隐藏弹窗右上角"关闭"图标：

| 场景 | 规则 |
|------|------|
| 二次确认 | 当弹窗内容表达某种询问，且需要进行类似"是否""确定取消"这种对立操作时，须隐藏顶部栏关闭按钮 |
| 强制操作 | 当弹窗内容需要强制操作时（如强制升级弹窗），须隐藏顶部栏关闭按钮 |
| 单一路径 | 用户只有一个操作选择时 |

### 交互规范

#### 点击事件

| 操作 | 行为 |
|------|------|
| 点击行动点（底部按钮）| 执行操作，关闭弹窗 |
| 点击 x（关闭按钮）| 关闭弹窗 |
| 点击遮罩区域 | 不关闭弹窗（对话框强制用户通过按钮操作）|

#### 滑动事件

| 操作 | 行为 |
|------|------|
| 内容溢出最大高度 | 支持用户内部滚轴查看，滚动时展示滚动条 |

### 错误用法（禁止事项）

- 错误点1：二次确认弹窗不应展示 x 按钮
- 错误点2：内容区域未撑到最大高度，就出现滚动条
- 错误点3：底部按钮未配置（底部按钮必须配）

---

## 二、营销弹窗（黄流场域）

### 简述

用于黄流场域的营销弹窗，承载新人返券、促销活动等营销内容。

### 尺寸约束

| 区域 | 规则 |
|------|------|
| 弹窗主体内容区域 | 最大宽度为屏幕的 80%（375pt 宽度下为 300pt），最大高度为屏幕的 65%（812pt 高度下为 527pt）|
| 氛围营造区域 | 最大宽度/高度为整个屏幕（避免裁切，但设计中须避免过度设计）|
| 背景遮罩 | 不透明度 80%（#000000） |
| 关闭按钮 | 尺寸 30×30pt，位置为右上角，与屏幕右侧距离 26pt，与主体内容间距 16pt |

### 输出规则

- 输出宽度为屏幕 100%
- 输出高度为弹窗实际内容高度（不超过最大高度限制）
- 主体内容区域限制是为了让用户感知当前所在页面，提供安全感和方向感

### 关闭按钮

- 线形 icon 风格
- 支持倒计时自动关闭
- 如有倒计时，在关闭按钮左侧展示，字号 16px，Regular，与关闭 icon 间距 8pt

---

## 颜色规范

| 用途 | Token / 色值 |
|------|-------------|
| 弹窗背景 | `结构色/sui_color_white` |
| 遮罩背景（对话框）| `#000000` 60% 不透明度 |
| 遮罩背景（营销弹窗）| `#000000` 80% 不透明度 |
| 主标题文字 | `结构色/sui_color_gray_dark1` |
| 副文案文字 | `结构色/sui_color_gray_dark3` |
| 链接文字 | `功能色/sui_color_link` |
| 主按钮背景 | `结构色/sui_color_gray_dark1`（深色）|
| 主按钮文字 | `结构色/sui_color_white` |
| 次按钮背景 | `结构色/sui_color_white` |
| 次按钮描边 | `结构色/sui_color_gray_light2`（0.5px）|
| 次按钮文字 | `结构色/sui_color_gray_dark1` |

---

## 组件 Schema（AI 调用参考）

### 对话框弹窗（Dialog）

```json
{
  "componentName": "Dialog",
  "figmaComponentKey": "7e764a22dde06f43902d2aac62375cd71f10a98d",
  "componentSetId": "10:56180",
  "platformMapping": {
    "And": "component_system_modal / SuiAlertDialog",
    "iOS": "component_system_modal / SHAlertController",
    "Web": "component_system_modal / s-dialog"
  },
  "description": "对话框弹窗，一种暂态容器，承载表单、纯阅读字段、业务交互等，相比半浮层更具备阻断性。点击弹窗之外区域不关闭，必须通过关闭按钮或底部行动按钮关闭。",
  "properties": {
    "title": {
      "type": "boolean",
      "default": true,
      "description": "是否展示主标题"
    },
    "subtitle": {
      "type": "boolean",
      "default": false,
      "description": "是否展示副文案"
    },
    "image": {
      "type": "boolean",
      "default": false,
      "description": "是否展示图片"
    },
    "imagePosition": {
      "type": "string",
      "enum": ["无", "顶部沉浸式", "上图下文", "上文下图"],
      "default": "无",
      "description": "图片位置：顶部沉浸式=图片作为顶部背景；上图下文=图片在文字上方；上文下图=图片在文字下方"
    },
    "maxHeight": {
      "type": "boolean",
      "default": false,
      "description": "是否启用最大高度限制（启用时内容超出可滚动）"
    },
    "customContent": {
      "type": "boolean",
      "default": false,
      "description": "是否使用完全自定义内容区"
    },
    "showCloseButton": {
      "type": "boolean",
      "default": true,
      "description": "是否显示右上角关闭图标；二次确认和强制操作场景须设为 false"
    },
    "headerStyle": {
      "type": "string",
      "enum": ["plain", "image", "none"],
      "default": "plain",
      "description": "顶部栏样式：plain=纯色白底；image=图片背景；none=无顶部栏"
    },
    "footerLayout": {
      "type": "string",
      "enum": ["single", "horizontal", "vertical", "button-text"],
      "default": "single",
      "description": "底部按钮区布局：single=单按钮；horizontal=双按钮水平(左次右主)；vertical=双按钮垂直(上主下次)；button-text=按钮+链接文字"
    }
  },
  "slots": {
    "header": {
      "description": "顶部栏区域，可配置关闭按钮、纯色或图片背景",
      "componentKey": "7c8f4ae2df09cf94305c448a121012a792b1cd69"
    },
    "body": {
      "description": "内容区，可注入主文字、次文字、图片或完全自定义内容",
      "componentKey": "7847fac4478bd03f795b4dad49dca4711eac47cb",
      "maxHeightRule": "最大高度 498px（屏幕高度的 60%），超出时内部滚动"
    },
    "footer": {
      "description": "底部按钮区，必须配置，支持多种布局",
      "componentKey": "c3d5f5529beda9df092e199b592a3f6c7d069d7a"
    }
  },
  "designTokens": {
    "borderRadius": "8px（可自定义）",
    "minHeight": "150px",
    "maxHeight": "498px（屏幕高度的 60%）",
    "width": "屏幕宽度 - 左右各 10%（安卓）",
    "paddingHorizontal": "16px",
    "paddingBottom": "20px",
    "maskColor": "#000000 60% 不透明度",
    "backgroundColor": "sui_color_white",
    "buttonHeight": "36pt",
    "buttonRadius": "2px",
    "buttonStrokeWidth": "0.5px"
  },
  "usageRules": [
    "同一页面同时只能存在一个弹窗，禁止嵌套",
    "底部按钮区必须配置，禁止为空",
    "点击弹窗之外区域不关闭弹窗（必须通过按钮或关闭图标关闭）",
    "二次确认场景（'是否'/'确定取消'对立操作）须隐藏关闭按钮",
    "强制操作场景（如强制升级）须隐藏关闭按钮",
    "内容区域未撑满最大高度时，禁止出现滚动条",
    "弹窗必须由用户主动操作触发，禁止自动弹出",
    "footerLayout=horizontal 时，左侧为线框按钮（次操作），右侧为深色按钮（主操作）",
    "footerLayout=vertical 时，上方为深色按钮（主操作），下方为线框按钮（次操作）"
  ]
}
```

### 营销弹窗（Marketing Modal）

```json
{
  "componentName": "MarketingModal",
  "figmaComponentKey": "7e764a22dde06f43902d2aac62375cd71f10a98d",
  "description": "黄流场域营销弹窗，用于新人返券、促销活动等营销场景。限制主体尺寸以保证用户感知当前页面，支持氛围营造区域和倒计时关闭。",
  "platform": "mobile",
  "properties": {
    "contentWidth": {
      "type": "string",
      "default": "80%",
      "description": "主体内容区域最大宽度为屏幕的 80%（375pt 下为 300pt）"
    },
    "contentMaxHeight": {
      "type": "string",
      "default": "65%",
      "description": "主体内容区域最大高度为屏幕的 65%（812pt 下为 527pt）"
    },
    "hasAtmosphere": {
      "type": "boolean",
      "default": true,
      "description": "是否有氛围营造区域（礼花/飘带/眩光等），最大可全屏但须避免过度设计"
    },
    "hasCountdown": {
      "type": "boolean",
      "default": false,
      "description": "是否有倒计时自动关闭，展示在关闭按钮左侧"
    }
  },
  "designTokens": {
    "maskColor": "#000000 80% 不透明度",
    "contentMaxWidth": "屏幕宽度的 80%（375pt 下 = 300pt）",
    "contentMaxHeight": "屏幕高度的 65%（812pt 下 = 527pt）",
    "outputWidth": "屏幕 100%",
    "outputHeight": "实际内容高度（不超过最大高度）",
    "closeButtonSize": "30×30pt",
    "closeButtonPosition": "右上角，距屏幕右侧 26pt",
    "closeButtonGap": "与主体内容间距 16pt",
    "countdownFontSize": "16px",
    "countdownFontWeight": "Regular",
    "countdownGap": "与关闭 icon 间距 8pt"
  },
  "usageRules": [
    "主体内容区域尺寸限制：宽度不超过屏幕 80%，高度不超过屏幕 65%",
    "输出尺寸：宽度按屏幕 100%，高度按实际内容自适应",
    "背景遮罩统一 80% 不透明度，突出弹窗内容降低背景干扰",
    "氛围营造区域不做严格尺寸限制，但须避免全屏和过度设计",
    "关闭按钮为线形风格，固定右上角位置",
    "支持倒计时自动关闭功能"
  ]
}
```
