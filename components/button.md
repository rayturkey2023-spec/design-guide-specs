# 按钮（Button）组件规范

## 使用场景

- 触发操作、提交表单、页面跳转等交互行为
- 区分主次操作优先级，引导用户完成核心流程
- 活动类场景使用活动主题色按钮提升转化

## 禁止场景

- 禁止同屏出现 2 个 Primary 按钮
- 禁止 Danger 按钮无二次确认直接触发破坏性操作
- 禁止按钮文字超过 2 行（文字过长时截断或缩短文案）
- 禁止弹窗/基础场景中按钮宽度完全自由伸缩（须使用固定宽度）

---

## 一、全局操控按钮（Global Control Button）

### 简述

主要用于对页面内容进行全局操控，可以和底部栏组合使用固定于页面底部，也可以跟随内容一起上下滚动。

### 变体与使用场景

| 变体 | 使用场景 | 每屏限制 |
|------|---------|---------|
| 深色背景（Primary） | 唯一主操作（提交、确认、下一步）| 每屏最多 1 个 |
| 线框背景（Outline） | 次要操作（取消、返回、重置）| 不限 |
| 白色背景 | 低优先级操作、多选项并列 | 不限 |
| 反白样式 | 深色背景页面上的操作 | 不限 |

### 尺寸规范

| 尺寸 | 高度 | 字号 | 内边距 (padding) | 使用场景 |
|------|------|------|-----------------|---------|
| 44pt | 44pt | 16px Bold | 10px 12px | 主操作+icon 强化场景 |
| 40pt | 40pt | 16px Bold | 8px 12px（纯文字）/ 6px 12px（有辅助信息） | 页面底部标准全局按钮 |

> 图标尺寸：20×20pt，icon 和文字间距固定为 **8pt**
> 辅助信息模式下 icon 和文字间距固定为 **2pt**

### 布局约束

- 标准全局按钮高度 40pt 或 44pt，宽度根据页面宽度自适应
- 移动端底部主操作按钮：宽度撑满（减去左右边距），高度使用 40pt
- 并列按钮（如取消+确认）：等宽排列，间距固定
- 空间不足时，横排改为竖排，主按钮在上，次按钮在下
- 弹窗内按钮须使用固定宽度，不随文案自由拉伸
- 默认只展示按钮的主标题
- 可展示主标题+辅助引导决策信息，但辅助引导信息仅展示1个，超出上下轮播展示
- 若需进一步强化主操作，可以在按钮主标题前加单色图标（icon 20×20pt）
- 文字左右内边距固定为 **12pt**
- 圆角固定 **2px**

### 本土化适配（溢出规则）

| 场景 | 处理方式 |
|------|---------|
| 纯文字按钮 | 1) 字号默认16号加粗，保持左右内边距12；2) 展示不下时优先缩小字号，最小字号为12；3) 依旧不够则换行展示，换行后仍不下打点省略 |
| 主标题+辅助信息 | 1) 主标题展示不下时优先缩小字号，最小字号为11，依然不下打点省略；2) 副标题展示不下时直接打点省略 |

### 颜色规范

#### 基础色

| 色值 | Token | 用途 |
|------|-------|------|
| `#000000` | `功能色/sui_color_brand` | 深色按钮正常态背景色；浅色按钮正常态文字色 |
| `#BBBBBB` | `结构色/sui_color_gray_light2` | 深色按钮置灰态背景色；线框按钮描边色；浅色按钮置灰态文字色 |
| `#FFFFFF` | `结构色/sui_color_white` | 白色和描边按钮背景色；深色按钮文字色 |
| `#E5E5E5` | `结构色/sui_color_gray_weak1` | 深色按钮置灰态文字色 |

#### 促销色（按业务场景控制）

| 色值 | Token | 适用场景 |
|------|-------|---------|
| `#FA6338` | `功能色/sui_color_discount` | 新人活动、促销相关场景 |
| `#FA6338` | `功能色/sui_color_promo` | 促销信息辅助图标 |

> 活动色允许根据业务需要替换整套界面主题色，不属于默认主色

#### 按钮样式状态配色

| 按钮样式 | 正常态 | 置灰态（Disabled） | 点击态 |
|---------|--------|-------------------|--------|
| 深色背景 | 背景 `#000000` + 文字 `#FFFFFF` | 背景 `#BBBBBB` + 文字 `#E5E5E5` | 背景 `#000000` + 内容 60% 不透明度 |
| 线框背景 | 背景 `#FFFFFF` + 描边 `#BBBBBB`(0.5px) + 文字 `#000000` | 背景 `#FFFFFF` + 描边 `#BBBBBB` + 文字 `#BBBBBB` | 背景 `#FFFFFF` + 内容 60% 不透明度 |
| 白色背景 | 背景 `#FFFFFF` + 文字 `#000000` | 背景 `#FFFFFF` + 文字 `#BBBBBB` | 背景 `#FFFFFF` + 内容 60% 不透明度 |
| 反白样式 | 背景深色 + 文字 `#FFFFFF` | 同上 + 文字弱化 | 内容 60% 不透明度 |

### 状态

- Default / Active（点击态）/ Disabled / Loading

### 交互规范

#### 点击态

- 点击态统一处理：**按钮整体不透明度降低至 60%**
- 适用于所有背景样式下的按钮，提供一致的按压反馈
- 点击前后需有明显可感知的状态变化

---

## 二、局部操控按钮（Section Control Buttons）

### 简述

通常用于对页面内子模块交互，或弹窗等二级页面的操控。

### 尺寸规范

| 规格 | 高度 | 内边距 (padding) | 最小宽度 | 字号 | 字重 | 字体 | 图标尺寸 |
|------|------|-----------------|---------|------|------|------|---------|
| 极小号 | 20pt | 5px 6px | 40pt | 12px | Regular(400) | SF Pro | 12×12pt |
| 小号 | 24pt | 5px 6px | 40pt | 12px | Regular(400) | SF Pro | 12×12pt |
| 中小号 | 26pt | 5px 8px | 56pt | 14px | Regular(400) | SF Pro | 12×12pt |
| 中号 | 28pt | 5px 8px | 56pt | 14px | Regular(400) | SF Pro | 12×12pt |
| 中大号 | 30pt | 5px 12px | 90pt | 14px | Bold(700) | SF Pro | 12×12pt |
| 大号 | 36pt | 9px 12px | 90pt | 14px | Bold(700) | SF UI Text | 12×12pt |

> icon 与文字之间间距固定为 **2px**
> 圆角固定 **2px**（允许自定义导角，导角度数必须为双数）
> 内部元素间距 gap: **8px**（icon 与文字之间除外）

### 文案截断规则

- 按钮内文本过长时，优先显示文案前部，末尾截断显示省略号（`…`）
- 不破坏按钮整体高度和对齐

### 可行性（Accessibility）布局场景

| 布局方式 | 使用场景 |
|---------|---------|
| 单按钮 | 单个主操作，居中或靠近主内容区 |
| 双按钮横排 | 空间充足时，主按钮在右，次按钮在左，视觉等重 |
| 双按钮竖排 | 空间不足时，主按钮在上，次按钮在下 |
| 弹窗内按钮 | 固定宽度，不自由拉伸，主次按钮有明显视觉区分 |
### 布局约束

- 常规样式：允许使用导角，导角度数根据实际需求自定义，但必须为双数
- 特殊样式包含：文案+图标样式、纯文字样式、纯图标样式
- 用在多个子模块的局部操作，或者信息层级比较复杂的页面的局部操作，需要通过差异化样式来起到层级差异的作用
- 间距为最小间距，具体可根据实际场景自定义，但必须为双数
- 文案+图标样式中 icon 尺寸为 12×12pt

### 颜色规范

同全局操控按钮（深色背景/线框背景/白色背景/反白样式四种）

### 交互规范

同全局操控按钮（点击态整体 60% 不透明度）


## 三、悬浮按钮（Floating Button / FAB）

### 简述

悬浮按钮（FAB）是一个独立的悬浮按钮，可让用户在应用中快速执行操作。通常位于屏幕的右下角，不支持手动关闭。

### 结构规范

```
页面（全高）
└── 悬浮按钮（右下角固定定位）
    ├── 圆形按钮：44×44px（仅图标）
    └── 竖版按钮：44×54px（图标 + 文案）
        ├── 图标区（圆形，44×44px）
        └── 文案区（图标下方，最多 60 字符，超出省略）
```

### 尺寸规范

| 形态 | 尺寸 | 说明 |
|------|------|------|
| 圆形（常规尺寸）| 44×44px | 纯图标，无文案 |
| 竖版（按钮+文案）| 44×54px | 图标 + 下方文案 |

### 位置规范

- **默认位置**：页面右下角，固定定位，不允许拖动（区别于悬浮球）
- 一级页面（有底部导航栏）：悬浮按钮距离侧边 & 下边间距均为 **12pt**
- 非一级页面（无底部导航栏）：悬浮按钮距离下边间距为 **32pt**
- 存在多个悬浮按钮时，悬浮按钮之间间距 **14pt**

### 颜色规范

#### 背景色

| 用途 | 色值 | 透明度 |
|------|------|--------|
| 悬浮按钮背景 | `#FFFFFF` | 90% |

#### 图标颜色（按业务状态）

| 状态 | 色值 | 适用场景 |
|------|------|---------|
| 常规色 | `#767676` | 默认状态，0 件加购时 |
| 黑色 | `#000000` | 已加购商品，强调状态 |
| 绿色（免邮色）| `#198055` | 购物车商品满足免邮条件 |
| 折扣色 | `#FA6338` | 购物车商品存在促销折扣 |

### 场景状态

| 场景 | 图标颜色 | 说明 |
|------|---------|------|
| 0 加车 | `#767676` | 用户未加购任何商品 |
| 1 件商品加车 | `#000000` | 用户已加购商品 |
| 购物车商品免邮 | `#198055` | 已满足免邮门槛 |
| 购物车商品有促销折扣 | `#FA6338` | 购物车有可用促销 |

### 交互规范

#### 展示规则

| 展示规则 | 说明 |
|---------|------|
| 默认展示 | 模块适用于该页面组合时，默认展示 |
| 单按钮展示 | 页面只有一个悬浮按钮时，直接展示 |
| 数量限制 | 超过 3 个时需折叠/合并，避免遮挡页面内容 |

- 当页面不适用独立悬浮按钮时，改为页面内固定按钮
- **同一页面悬浮按钮数量不超过 3 个**

### 禁止事项

- 禁止悬浮按钮支持手动关闭
- 禁止悬浮按钮支持拖动改变位置
- 禁止同一页面超过 3 个悬浮按钮同时展示
- 禁止悬浮按钮文案超过 60 字符

---

## 交易链路场景示意

| 页面 | 按钮类型 | 典型文案 |
|------|---------|---------|
| 列表页 | 商品卡片内 CTA | `Add`、进入商详 |
| 商详页 | 底部全宽主按钮 | `Add to Cart` |
| 购物车 | 底部结算按钮 + 卡片内操作 | `Checkout`、`View More`、`Go to shop` |
| 下单页 | 底部主操作 | `Place Order`、`Continue` |
| 订单详情 | 操作性按钮 | `To Pay`、`View` |
| 活动/礼品卡 | 活动色 CTA | `Grab Now`、`Check Balance`、`Link Card` |

---

## 组件 Schema（AI 调用参考）

### 全局操控按钮（Global Control Button）

```json
{
  "componentName": "GlobalControlButton",
  "figmaComponentKey": "1:7043（按钮h44）",
  "description": "主要用于对页面内容进行全局操控，可以和底部栏组合使用固定于页面底部，也可以跟随内容一起上下滚动。通过按钮样式区分视觉层级。支持主标题+辅助引导信息组合展示。",
  "properties": {
    "buttonStyle": {
      "type": "string",
      "enum": ["深色背景", "线框背景", "白色背景", "反白样式"],
      "default": "深色背景",
      "description": "按钮样式变体：深色背景=唯一主操作(#000000背景白字)；线框背景=次要操作(白底黑字#BBBBBB描边)；白色背景=低优先级；反白样式=深色页面上的操作"
    },
    "buttonState": {
      "type": "string",
      "enum": ["正常", "禁用", "点击"],
      "default": "正常",
      "description": "正常=默认状态；禁用=置灰态(背景#BBBBBB)；点击=点击态(内容60%不透明度)"
    },
    "size": {
      "type": "string",
      "enum": ["44", "40"],
      "default": "40",
      "description": "按钮高度（pt）：44=有icon强化场景(padding:10px 12px)；40=标准全局按钮(padding:8px 12px)"
    },
    "icon": {
      "type": "boolean",
      "default": false,
      "description": "是否在主标题前展示单色图标(20×20pt)，icon与文字间距8pt"
    },
    "fullWidth": {
      "type": "boolean",
      "default": true,
      "description": "宽度根据页面宽度自适应，移动端底部主操作按钮须设为 true"
    },
    "label": {
      "type": "string",
      "description": "按钮主标题文案，字号16px Bold，展示不下时先缩小至12px，再换行，仍不下打点省略"
    },
    "subLabel": {
      "type": "string",
      "description": "辅助引导决策信息（可选），字号11px Regular，仅展示1条；多条时上下轮播展示"
    }
  },
  "designTokens": {
    "borderRadius": "2px",
    "paddingH44": "10px 12px",
    "paddingH40": "8px 12px",
    "paddingH40WithSub": "6px 12px",
    "contentGap": "8px",
    "subContentGap": "2px",
    "textPaddingHorizontal": "12px",
    "fontSize": "16px",
    "fontWeight": "700",
    "fontFamily": "SF UI Text / SF Pro",
    "subFontSize": "11px",
    "subFontWeight": "400",
    "minFontSize": "12px",
    "minFontSizeWithSub": "11px",
    "iconSize": "20px"
  },
  "usageRules": [
    "同一屏幕内深色背景按钮最多出现 1 个",
    "点击态统一为内容元素 60% 不透明度，不单独设计每个变体的点击色",
    "表单提交前未满足必填条件时须设为禁用态",
    "移动端底部主操作按钮须设 size=40 且 fullWidth=true",
    "弹窗内按钮须使用固定宽度，不随文案自由拉伸",
    "并列按钮组（如取消+确认）须等宽排列",
    "subLabel 最多同时展示 1 条，多条须轮播，不可堆叠显示",
    "icon=true 时图标须为单色 20×20pt，不可使用多色图标",
    "线框按钮描边粗细 0.5px，颜色 #BBBBBB"
  ]
}
```

### 局部操控按钮（Section Control Button）

```json
{
  "componentName": "SectionControlButton",
  "figmaComponentKey": "1:8780（按钮H28）/ 1:8839（按钮H24）",
  "description": "通常用于对页面内子模块交互，或弹窗等二级页面的操控。支持文案+图标、纯文字、纯图标三种内容样式，允许自定义导角（必须双数）。",
  "properties": {
    "size": {
      "type": "string",
      "enum": ["36", "30", "28", "26", "24", "20"],
      "default": "28",
      "description": "按钮高度（pt）：36=大号(14px Bold, padding:9px 12px, 最小宽度90pt)；30=中大号(14px Bold, padding:5px 12px, 最小宽度90pt)；28=中号(14px Regular, padding:5px 8px, 最小宽度56pt)；26=中小号(14px Regular, padding:5px 8px, 最小宽度56pt)；24=小号(12px Regular, padding:5px 6px, 最小宽度40pt)；20=极小号(12px Regular, padding:5px 6px, 最小宽度40pt)"
    },
    "contentType": {
      "type": "string",
      "enum": ["label-icon", "label", "icon"],
      "default": "label",
      "description": "内容样式：label-icon=文案+图标（icon 12×12pt，间距2px）；label=纯文字；icon=纯图标"
    },
    "buttonStyle": {
      "type": "string",
      "enum": ["深色背景", "线框背景", "白色背景", "反白样式"],
      "default": "深色背景",
      "description": "按钮样式变体，与全局操控按钮规范一致"
    },
    "buttonState": {
      "type": "string",
      "enum": ["正常", "禁用", "点击"],
      "default": "正常",
      "description": "正常=默认；禁用=置灰；点击=内容60%不透明度"
    },
    "cornerRadius": {
      "type": "number",
      "default": 2,
      "description": "导角半径（px），允许自定义，但必须为双数（如 2、4、6、8…）"
    },
    "label": {
      "type": "string",
      "description": "按钮文案，长文案末尾省略"
    }
  },
  "designTokens": {
    "borderRadius": "2px（默认，允许自定义双数值）",
    "iconSize": "12px",
    "iconTextGap": "2px",
    "fontFamily": "SF Pro",
    "sizeSpecs": {
      "20": {"padding": "5px 6px", "minWidth": "40px", "fontSize": "12px", "fontWeight": "400"},
      "24": {"padding": "5px 6px", "minWidth": "40px", "fontSize": "12px", "fontWeight": "400"},
      "26": {"padding": "5px 8px", "minWidth": "56px", "fontSize": "14px", "fontWeight": "400"},
      "28": {"padding": "5px 8px", "minWidth": "56px", "fontSize": "14px", "fontWeight": "400"},
      "30": {"padding": "5px 12px", "minWidth": "90px", "fontSize": "14px", "fontWeight": "700"},
      "36": {"padding": "9px 12px", "minWidth": "90px", "fontSize": "14px", "fontWeight": "700"}
    }
  },
  "usageRules": [
    "局部操控按钮不承担全局主操作，禁止替代全局操控按钮使用",
    "点击态统一为内容 60% 不透明度",
    "cornerRadius 必须为双数，禁止使用奇数圆角值",
    "间距为最小间距基准，可根据场景自定义但必须为双数",
    "contentType=label-icon 适用于多子模块或信息层级复杂页面，需通过差异化样式体现层级",
    "文案过长时末尾省略，不换行，不破坏按钮高度",
    "icon 与文字间距固定 2px，所有尺寸规格统一"
  ]
}
```

### 悬浮按钮（FAB）

```json
{
  "componentName": "FloatingButton",
  "figmaComponentKey": "【待确认具体 componentId】",
  "description": "悬浮操作按钮(FAB)是一种功能型按钮，可让用户在应用中便捷执行操作。固定在页面右下角，不支持手动关闭，不允许拖动（区别于悬浮球）。",
  "platform": "mobile-only",
  "properties": {
    "shape": {
      "type": "string",
      "enum": ["circle", "vertical"],
      "default": "circle",
      "description": "circle=纯图标圆形（44×44px）；vertical=图标+文案竖版（44×54px）"
    },
    "iconColor": {
      "type": "string",
      "enum": ["#767676", "#000000", "#198055", "#FA6338"],
      "default": "#767676",
      "description": "#767676=常规/0加购；#000000=已加购；#198055=免邮；#FA6338=有促销折扣"
    },
    "label": {
      "type": "string",
      "description": "shape=vertical 时的文案，最多 60 字符，超出省略"
    },
    "position": {
      "type": "string",
      "enum": ["primary-page", "secondary-page"],
      "default": "secondary-page",
      "description": "primary-page=一级页面(距侧边&下边均12pt)；secondary-page=非一级页面(距下边32pt)"
    }
  },
  "designTokens": {
    "size": "44×44px（圆形）/ 44×54px（竖版）",
    "backgroundColor": "#FFFFFF 90% 透明度 + 投影",
    "marginPrimaryPage": "12pt（侧边和下边）",
    "marginSecondaryPage": "32pt（下边）",
    "multiButtonGap": "14pt"
  },
  "usageRules": [
    "固定于屏幕右下角，不支持拖动",
    "不支持手动关闭",
    "同一页面悬浮按钮数量不超过 3 个",
    "超过 3 个时需折叠合并展示",
    "vertical 文案最多 60 字符，超出省略",
    "一级页面距侧边&下边间距均12pt",
    "非一级页面距下边间距32pt",
    "多个悬浮按钮之间间距14pt"
  ]
}
```
