# 搜索框（SearchBar）组件规范

## 使用场景

- 在已有的内容集合中进行精细化筛选，帮助用户缩小搜索范围，提高查找效率
- 页面顶部全局搜索入口
- 列表页、商品页等需要关键词检索的场景

## 禁止场景

- 禁止搜索框内同时展示过多功能图标（保持简洁）
- 禁止在无搜索推荐词时展示快捷搜索按钮（应置灰或隐藏）
- 禁止修改彩色备注标注以外的参数（间距、尺寸等不可自由调整）

---

## 一、元素拆解（Anatomy）

### 结构规范

```
搜索栏容器
├── ①搜索框底框（白色填充 + 黑色描边 + 全圆角）
│   ├── 搜索文字区（左侧）
│   │   ├── 搜索推荐底纹词 / 用户输入文字
│   │   └── 趋势箭头图标（可选，推荐词相关）
│   └── 功能区（右侧）
│       ├── 清除按钮（输入中/输入后出现）
│       ├── 图搜按钮（相机图标，可选）
│       └── ④快捷搜索按钮（圆形黑底，可选）
├── 左侧导航图标区（返回箭头等）
└── 右侧扩展功能区（切换视图、收藏、分享等）
```

### 元素说明

| 序号 | 元素 | 说明 |
|------|------|------|
| ① | 搜索框底框 | 填充颜色：#FFFFFF；描边颜色：#000000（1.5px）；圆角：6px |
| ② | 搜索推荐底纹词 | 平台推荐给用户的搜索词，可配置多个推荐词滚动轮播展示。文字颜色：#222222 / #666666（根据场景可选）|
| ③ | 搜索框扩充功能区 | 根据用户不同的使用场景配置不同的功能 |
| ④ | 快捷搜索按钮 | 与「②搜索推荐底纹词」配合出现，如默认态无推荐词则不展示此按钮或置灰。填充颜色：#000000 |

---

## 二、间距与尺寸

> 以下参数均来自 UI 组件库（componentSetId: 23:43274）实际数值，不可自行修改。

### 搜索框底框（白底状态）

| 参数 | 数值（多词条态） | 数值（未输入态） |
|------|----------------|----------------|
| 高度 | 35px | 35px |
| 描边 | 1.5px #000000 | 1.5px #000000 |
| 圆角 | 6px | 6px |
| padding | 2px 8px 2px 2px | 2px 4px 2px 12px |
| 内部元素 gap | 8px | 6px |

### 搜索栏容器（元素行）

| 参数 | 数值 |
|------|------|
| 搜索框与左右导航图标 gap | 12px |
| 搜索框与右侧功能区 gap | 10px（未输入态）/ 12px（多词条态）|

### 功能区（右侧图标组）

| 参数 | 数值 |
|------|------|
| 功能区内图标间 gap | 8px |
| 清除按钮尺寸 | 16×16px |
| 图搜按钮（相机）尺寸 | 24×24px |
| 图搜按钮描边 | 1.7px #959595 |

### 词条标签（多词条态）

| 参数 | 数值 |
|------|------|
| 标签高度 | 26px |
| 标签圆角 | 15px |
| 标签 padding | 6px 4px 6px 8px |
| 标签内 gap（文字与关闭图标）| 8px |
| 标签间 gap | 4px |
| 关闭图标尺寸 | 12×12px |
| 字号 | 11px SF Pro Regular |

### 快捷搜索按钮

| 参数 | 数值 |
|------|------|
| 圆角 | 4px |
| padding | 4px 12px |
| 内部 gap | 8px |
| 填充颜色 | #000000 |

---

## 三、交互事件

### 状态流转

| 状态 | 说明 |
|------|------|
| 搜索框正常状态 | 显示推荐底纹词，搜索图标在左侧或功能区 |
| 搜索框激活 | 点击搜索框后，光标出现，底纹词变为 placeholder，展示输入光标 |
| 搜索框输入中 | 用户正在输入，显示清除按钮（sui_icon_cleanall_xs）和搜索按钮 |
| 搜索框输入结束 | 用户已输入关键词并完成搜索，文字保留，可展示清除和图搜按钮 |

### 光标样式

- 光标颜色：`结构色/sui_color_gray_dark1`
- 光标圆角：2px

---

## 四、背景适配

### 浅色背景（样式①）

- 浅色背景可直接使用样式①
- 浅色背景非专指白色 #FFFFFF，带有色相的淡色背景也可直接使用，以使用场景效果为优先
- 除彩色备注参数外其他参数不可调整

### 有色/沉浸背景（样式②）

- 有色/沉浸背景可直接使用样式②
- 除彩色备注参数外其他参数不可调整

---

## 五、配色规范

| 序号 | 元素 | 颜色规则 |
|------|------|---------|
| ① | 搜索框底框 | 填充：#FFFFFF；描边：#000000（1.5px）|
| ② | 搜索推荐底纹词 | 文字颜色：#222222 / #666666（根据场景可选）|
| ③ | 搜索框功能区 | 图标颜色：#959595 |
| ④ | 快捷搜索按钮 | 填充颜色：#000000 |
| - | 输入中文字 | `结构色/sui_color_black` |
| - | Placeholder 文字 | `结构色/sui_color_gray_light1` |
| - | 清除按钮 | `结构色/sui_color_gray_light1` |
| - | 搜索结果文字 | `功能色/sui_color_brand`（品牌色高亮）|

---

## 组件 Schema（AI 调用参考）

```json
{
  "componentName": "SearchBar",
  "figmaComponentKey": "a511b53d7449f08ab694487fcd5d390f254aa97c",
  "componentSetId": "23:43274",
  "platformMapping": {
    "And": "component_system_search-bar",
    "iOS": "component_system_search-bar",
    "Web": "component_system_search-bar"
  },
  "description": "搜索框组件，用于在已有内容集合中进行精细化筛选，帮助用户缩小搜索范围，提高查找效率。支持推荐词轮播、图搜、快捷搜索等功能配置。",
  "properties": {
    "quickSearchButton": {
      "type": "boolean",
      "enum": ["on", "off"],
      "default": "off",
      "description": "是否展示快捷搜索按钮（圆形黑底），需与推荐底纹词配合出现"
    },
    "imageSearch": {
      "type": "boolean",
      "enum": ["on", "off"],
      "default": "on",
      "description": "是否展示图搜（相机）按钮"
    },
    "inputState": {
      "type": "string",
      "enum": ["未输入", "激活", "多词条"],
      "default": "未输入",
      "description": "输入状态：未输入=默认展示推荐词；激活=光标出现准备输入；多词条=已输入内容"
    },
    "immersiveBackground": {
      "type": "boolean",
      "enum": ["on", "off"],
      "default": "off",
      "description": "是否为沉浸式（有色/深色）背景模式"
    }
  },
  "designTokens": {
    "searchBoxHeight": "35px",
    "borderRadius": "6px",
    "borderWidth": "1.5px",
    "borderColor": "#000000",
    "backgroundColor": "#FFFFFF",
    "paddingDefault": "2px 4px 2px 12px（未输入态）",
    "paddingMultiTag": "2px 8px 2px 2px（多词条态）",
    "innerGapDefault": "6px（未输入态）",
    "innerGapMultiTag": "8px（多词条态）",
    "navToSearchGap": "12px",
    "searchToRightGap": "10px（未输入态）/ 12px（多词条态）",
    "functionIconGap": "8px",
    "clearIconSize": "16×16px",
    "cameraIconSize": "24×24px",
    "cameraIconStroke": "1.7px #959595",
    "tagHeight": "26px",
    "tagBorderRadius": "15px",
    "tagPadding": "6px 4px 6px 8px",
    "tagGap": "4px",
    "tagInnerGap": "8px",
    "tagCloseIconSize": "12×12px",
    "tagFontSize": "11px SF Pro Regular",
    "tagBackgroundColor": "#F6F6F6",
    "tagTextColor": "#000000",
    "quickSearchBtnPadding": "4px 12px",
    "quickSearchBtnRadius": "4px",
    "quickSearchBtnColor": "#000000",
    "placeholderColor": "#222222 / #666666",
    "inputTextColor": "#000000（sui_color_black）",
    "functionIconColor": "#959595",
    "clearIconColor": "#959595（sui_color_gray_light1）",
    "highlightColor": "sui_color_brand"
  },
  "usageRules": [
    "搜索框高度固定 35px，不可自定义",
    "圆角固定 6px，不可修改",
    "描边固定 1.5px #000000",
    "快捷搜索按钮须与推荐底纹词配合，无推荐词时不展示或置灰",
    "浅色背景使用样式①，有色/沉浸背景使用样式②",
    "除彩色备注参数外，间距和尺寸参数不可调整",
    "输入中状态须展示清除按钮（sui_icon_cleanall_xs，16×16px）",
    "推荐底纹词支持多词滚动轮播",
    "多词条态标签使用 #F6F6F6 背景、15px 圆角、高度 26px"
  ]
}
```
