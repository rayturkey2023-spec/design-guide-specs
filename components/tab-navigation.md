# Tab 导航（Tab Navigation）组件规范

## 使用场景

- 同层级、并列内容之间的切换导航
- 页面内分类浏览、模块切换、内容筛选/分组展示
- 局部内容区域的锚点定位导航
- 多层级信息架构的层级入口

## 禁止场景

- 禁止将 Tab 用作操作按钮（如"提交""确认""下一步"等动作语义）
- 禁止一级 Tab 与二级 Tab 使用相同视觉样式（同宽同高同权重）
- 禁止同一层级堆叠过多 Tab（超出可视区域时需考虑横向滚动或折叠方案）
- 禁止 Tab 选中后无明显反馈（必须有清晰的选中态指示）
- 禁止在内容密度已很高的页面再叠加多级 Tab
- 禁止将 Tab 用作复杂多条件筛选系统（应改用筛选器/下拉/标签控件）
- 禁止 Tab 样式过于"按钮化"，削弱导航语义

---

## 一、定义（Definition）

Tab Navigation 是用于在**同层级、并列内容**之间进行切换的导航组件。

### 核心特征

- 同一页面中存在多个平级内容分组
- 用户通过切换 Tab 查看不同内容
- Tab 本身不改变页面的整体层级结构
- 属于轻量级、局部承载的导航方式

### 结构模型

```
Tab 导航结构
├── 同层并列型：Tab组签（A / B / C / D）→ 对应内容面板
└── 层级入口型：编选页（A-1 / A-2 / A-3 / A-4）→ 子级内容
```

---

## 二、交互分类（Classification）

### 1. 整体切换型（横向切换型）

| 属性 | 说明 |
|------|------|
| 含义 | 用户可通过点击或滑动在同一页面的多个内容区域间横向切换，常作为复杂页面的主要导航使用 |
| 典型场景 | 首页的品类（小首页）切换，信息流的横向切换，商详的纵向锚点快速定位 |
| 交互特征 | 选中态明显，内容区与 Tab 强绑定，切换后整体内容重绘 |
| 适用原则 | 适合少量明确分类，各 Tab 内容量逻辑并列 |

### 2. 局部锚定型（纵向锚定型）

| 属性 | 说明 |
|------|------|
| 含义 | 当同一层级的分组过多，无法通过横向切换来实现时，用户点击纵向 tab 来切换页面右侧的内容，同时用户也可以通过滑动右侧的内容来切换左侧的 tab 锚点 |
| 典型场景 | Category 快速定位品类目录 |
| 交互特征 | 不替换内容而是引导定位，与长内容页结合，需实时反馈当前区块 |
| 适用原则 | Tab 位置在滚动时需保持可见（吸顶），适合内容长且有明确锚点分区的页面 |

### 3. 图文导航型

| 属性 | 说明 |
|------|------|
| 含义 | 图文导航通过图片与文字的组合形式引导用户进入对应内容模块，点击横向切换分页或跳转页面 |
| 典型场景 | 搜索结果页 |
| 交互特征 | 图片提供视觉预览，引导用户进入更深层级 |
| 适用原则 | 适合频道/品类入口，可与文字型 Tab 组合使用 |

---

## 三、样式说明（Anatomy）

### 文字型一级 Tab（Sliding Tab）

#### 组件结构

```
一级 Tab 容器（横向排列）
├── Tab Item × N
│   ├── 内容行（内容行）
│   │   ├── icon（可选，面性/线性）
│   │   ├── 文本标题（选中态 Bold / 未选中态 Bold 但颜色弱化）
│   │   └── Badge（可选：数字提醒 / 小红点）
│   └── 选中态指示器（Rectangle，固定宽度）
└── 底部分割线（可选）
```

#### 尺寸规范

| 属性                  | 规格                      | 说明                     |
| ------------------- | ----------------------- | ---------------------- |
| Tab 容器 padding      | 0px 12px                | 容器左右内边距                |
| Tab 间水平间距           | 16px                    | 相邻 Tab 之间的间距（等距模式，固定值） |
| Tab Item 内部 padding | 12px 0px 6px            | 单个 Tab 项的上下内边距         |
| Tab Item 内部 gap     | 2px                     | 文字与指示器之间的间距            |
| 文字字号                | 14px                    | 一级 Tab 文字大小            |
| 文字字体                | SF Pro                  | 系统字体                   |
| 文字字重                | 700 (Bold)              | 选中/未选均为 Bold，通过颜色区分    |
| 行高                  | ≈16.7px (1.19em)        | 文字行高                   |
| icon/Badge 与文字间距    | 2px                     | 内容元素之间的固定间距            |
| 指示线宽度               | 20px                    | 固定宽度，不跟随文字             |
| 指示线高度               | 3px                     | 指示线粗细                  |
| 指示线圆角               | 全圆角 (2px)               | 圆角胶囊形态                 |
| 图标尺寸（可选）            | 16×16px（标准）/ 最大 32×32px | Tab 项内可选前置图标           |
| 选项宽度                | 建议最大不超过屏幕 50%           | 宽度跟随内容变化               |

#### 颜色规范

| 状态 | 文字色 | 指示线色 | 说明 |
|------|--------|----------|------|
| 选中 | `#000000`（color_brand_primary） | `#000000`（color_brand_primary） | 选中态文字 + 底部指示线 |
| 未选中 | `#767676`（color_neutrals_text_tertiary） | — | 次要文字色，无指示线（opacity: 0） |

#### 状态

- Default（未选中）/ Selected（选中）
- 选中指示器在未选态 opacity 为 0，选中态为 1

#### 应用规则

- **等距模式**：标签数量多且变化较大，每个 Tab 宽度跟随内容变化，选项和选项的间距固定为 16px
- Tab 数量超出显示范围时支持左右滑动查看
- Tab 数量较少时：居左对齐排列
- Tab 数量较多时：超出容器宽度后横向滚动

---

### 文字型二级 Tab（Text Tab Level 2）

#### 组件结构

```
二级 Tab 容器（横向排列，层级弱于一级）
├── Tab Item × N
│   └── 文本标题（字号更小，通过字重区分状态）
└── 底部分割线（可选）
```

#### 尺寸规范

| 属性 | 规格 | 说明 |
|------|------|------|
| Tab Item padding | 13px 0px | 二级 Tab 项的上下内边距 |
| Tab Item gap | 2px | 内部元素间距 |
| 文字字号 | 12px | 二级 Tab 文字大小，比一级小 |
| 文字字体 | SF Pro | 系统字体 |
| 文字字重 | 选中态 700 (Bold) / 未选中态 400 (Regular) | 通过字重区分选中状态 |
| 行高 | ≈14.3px (1.19em) | 文字行高 |
| icon/Badge 与文字间距 | 2px | 内部固定间距 |
| 选项宽度 | 建议最大不超过屏幕 50% | 可变上下 padding |

#### 颜色规范

| 状态 | 文字色 | 说明 |
|------|--------|------|
| 选中 | `#000000`（color_brand_primary） | 选中态 Bold |
| 未选中 | `#666666`（color_neutrals_text_secondary） | 常规态 Regular |

#### 状态

- Default（未选中）/ Selected（选中）

---

### 胶囊型 Tab（Capsule Tab）

#### 组件结构

```
胶囊型 Tab 容器（横向排列）
├── Tab Item × N（胶囊形态）
│   ├── icon（可选，14×14，面性/线性）
│   ├── 文本标签
│   └── Badge（可选：数字提醒/小红点，绝对定位右上角）
└── 底部分割线（可选）
```

#### 尺寸规范

| 属性 | 规格 | 说明 |
|------|------|------|
| Tab Item padding | 6px 8px | 默认内边距 |
| Tab Item gap | 2px | icon 与文字之间间距 |
| 左右 padding 可选 | 6 / 8 / 10 / 12... | 根据场景选择 |
| 选项高度 | 24px（高屏效）/ 26px（常规） | 高屏效如信息流，常规如店铺、关注页、商详 |
| 宽度最小值 | 48px | |
| 宽度最大值 | 不超过屏幕 50% | 根据实际场景判断 |
| 文字字号 | 12px | |
| 文字字体 | SF Pro | |
| 文字字重 | 510 (Medium) | |
| 行高 | ≈14.3px (1.19em) | |
| icon 尺寸 | 14×14px | 面性容器用面性 icon，线性容器用线性 icon |
| 形状 | 小圆角胶囊 (borderRadius: 2px) | |
| 数字 Badge 偏移 | 右上角重叠 6×10 | |
| 红点 Badge 偏移 | 右上角重叠 4×4 | |

#### 容器样式

| 样式 | 说明 |
|------|------|
| 面性（填充） | 选中态为纯色填充背景（#000000），文字反白 |
| 白色填充 + 线框 | 选中态为白色背景 + 边框 |

#### 颜色规范

| 场景 | 规则 |
|------|------|
| 常规功能场景 | 使用中性色 |
| 营销频道场域 | 可选择使用对应的业务色 |

#### icon 规则

- 面性容器建议使用面性 icon
- 线性容器建议使用线性 icon
- 同一组 tab 需使用风格一致的 icon
- 使用线性换肤或面性 icon 均需提供未选/选中两种状态

#### 状态

- Default（未选中）/ Selected（选中）
- 变体组合：选项高度（24px/26px）× 选项样式（面性/线性）× 选中状态（已选/未选）× icon（有/无）× Badge（无/数字/红点）

---

### 图文组合型 Tab（Image + Text Tab）

#### 组件结构

```
图文 Tab 容器（横向排列/横向滚动）
├── Tab Item × N
│   ├── 图片区域（超椭圆定制形状）
│   └── 文本标签（图片下方/右侧）
└── 底部分割线（可选）
```

#### 尺寸规范

| 属性 | 规格 | 说明 |
|------|------|------|
| 图片尺寸 | 32px / 56px / 64px | 三种可选尺寸 |
| 图片形状 | 超椭圆定制形状 | 非标准圆形/方形 |
| 整体选项宽度（32px 图片） | 88px | 横向排列（图片+文字） |
| 整体选项宽度（56px 图片） | 64px | 纵向排列（图片上文字下） |
| 整体选项宽度（64px 图片） | 78px | 纵向排列（图片上文字下） |
| 图片与文字间距 | 4px | |
| 文字字号 | 12px | |
| 文字字体 | SF Pro | |
| 文字字重 | 选中态 700 (Bold) / 未选态 400 (Regular) | |
| 行高 | ≈14.3px (1.19em) | |
| 文字行数 | 最多 2 行，超出省略 | 56px 和 64px 支持 3 行以上省略 |
#### 描边规范

| 状态 | 描边规则 |
|------|----------|
| 默认/未选中态 | 内描边 color_neutrals_overlay_dark_soft |
| 选中态 | 两层描边：第一层内描边 color_brand_primary（粗细 1px）+ 第二层内描边 color_brand_primary_contrast（粗细 3px） |

#### 颜色规范

| 状态 | 文字色 | 说明 |
|------|--------|------|
| 选中 | color_brand_primary_contrast | 选中态文字加深 + Bold |
| 未选中 | color_brand_primary_contrast | 未选态 Regular |

#### 应用规则

- **水平滚动**：主要用于首页/列表的相关页面，使用 32px 和 56px 的图片尺寸
- 选项的展示个数可根据业务需求自定义，最多支持展示两排图文 tab
- 支持点击后在当前页面刷新、也支持点击后直接跳转新页面
- 32px 尺寸适合横向排列（图片 + 文字并排）
- 56px/64px 尺寸适合纵向排列（图片上方，文字下方）
- 具体可根据实际应用场景判断调整选项宽度，建议最大不超过屏幕的 50%

#### 状态

- Default（未选中）/ Selected（选中）
- 变体组合：选项尺寸/状态（上滑态/32px/56px/64px）× 选中状态（已选/未选）× 文本行数（1行/2行/2行以上/3行以上）

---

## 四、多级 Tab 组合规范

当页面内容比较复杂时，可通过多级 Tab 导航构建页面信息层级，但需注意以下规则：

### 基本原则

1. **最多同时展示 3 级 Tab 导航**（包含 Tab 导航与筛选标签的组合），禁止超过 3 级
2. **出现多 Tab 时，需要通过样式进行层级梯度的差别设计**，视觉上必须有明确主从
3. **当导航 Tab 与其他可交互元素上下并排时，需保证其之间有足够空间**，每个可点击热区至少达到 44×44pt，避免误触
4. **先大类后小类**：先让用户选择大范围分类，再在大类下选择细分项

### ✅ 推荐组合方式

| 组合 | 结构 | 描述 |
|------|------|------|
| A | 一级 Tab + 二级 Tab | 页面主内容区上方放一级 Tab，下方承接二级 Tab，层级分层清晰 |
| B | 一级 Tab + 筛选标签云 | 一级 Tab 切换大类，下方筛选标签云做细分筛选（如 Local / Category / Material / Size / Color） |
| C | 一级 Tab + 二级 Tab + 筛选标签云 | 三层结构但各层样式有明显差异，功能分工明确 |

### ❌ 禁止组合方式

| 问题 | 描述 |
|------|------|
| 样式过重 | 样式过于重，层级不清晰，用户认知负担较大 |
| 超过三级 | 不建议叠加三级以上导航 Tab，用户认知负担较大 |
| 样式雷同 | 一级、二级样式太接近，无法判断当前导航深度 |
| 热区冲突 | 多层 Tab 上下过于紧密，可点击热区不足 44×44pt，易误触 |

### 组合间距规范

| 属性 | 规格 | 说明 |
|------|------|------|
| 一级与二级 Tab 间距 | 8-12pt | 两级 Tab 之间的垂直间距 |
| 二级 Tab 与内容区间距 | 16pt | 二级 Tab 下方到内容区的间距 |
| 可点击热区最小尺寸 | 44×44pt | 每个 Tab 项的最小触控面积 |

---

## 五、交互规范

### 切换行为

| 行为 | 说明 |
|------|------|
| 点击切换 | 点击目标 Tab 立即切换内容，无需二次确认 |
| 滑动切换 | 内容区支持左右滑动切换时，Tab 指示器同步滑动跟随 |
| 吸顶 | 长页面滚动时，Tab 栏可吸顶固定，保持可操作性 |

### 滚动规则（Tab 数量较多时）

| 规则 | 说明 |
|------|------|
| 横向滚动 | Tab 数量超出一屏时支持横向滚动 |
| 居中展示 | 选中 Tab 自动居中展示（如可滚动） |
| 渐隐提示 | 可滚动时边缘可增加渐隐遮罩，提示有更多内容 |

### 点击态

- 与全局组件一致：点击态统一为整体 60% 不透明度，提供按压反馈

---

## 六、Token 与颜色汇总

| Token 名 | 色值 | 用途 |
|-----------|------|------|
| `功能色/sui_color_brand` | `#000000` | 品牌主色，一级 Tab 选中文字/指示线 |
| `功能色/sui_color_main` | `#222222` | 主功能色 |
| `结构色/sui_color_gray_dark1` | `#000000` | 深色文字 |
| `结构色/sui_color_gray_dark2` | `#666666` | 二级 Tab 未选中文字 |
| `结构色/sui_color_gray_dark3` | `#767676` | 一级 Tab 未选中文字/注释文字 |
| `结构色/sui_color_gray_weak1` | `#E5E5E5` | 分割线 |
| `结构色/sui_color_gray_weak2a` | `#FAFAFA` | 浅灰背景 |
| `结构色/sui_color_white` | `#FFFFFF` | 白色背景/胶囊选中态反白文字 |
| `结构色/sui_color_black_alpha60` | `rgba(0,0,0,0.6)` | 60% 黑色透明 |
| `功能色/sui_color_guide` | `#FE3B30` | 红点/数字 Badge 背景 |

---

## 组件 Schema（AI 调用参考）

### 一级 Tab（Primary Tab Navigation / Sliding Tab）

```json
{
  "componentName": "TabNavigation",
  "figmaComponentKey": "1:333（已选）/ 1:337（未选）",
  "description": "用于同层级并列内容之间的切换导航，支持整体切换、局部锚定、图文导航三种交互模式。一级 Tab 用于页面主导航切换，视觉层级最高。",
  "properties": {
    "type": {
      "type": "string",
      "enum": ["switch", "anchor", "image-nav"],
      "default": "switch",
      "description": "交互类型：switch=横向切换型（内容全部替换）；anchor=纵向锚定型（滚动定位）；image-nav=图文导航型（跳转页面）"
    },
    "level": {
      "type": "string",
      "enum": ["primary", "secondary"],
      "default": "primary",
      "description": "Tab 层级：primary=一级（页面主导航）；secondary=二级（局部筛选）"
    },
    "items": {
      "type": "array",
      "minItems": 2,
      "description": "Tab 项列表，每项包含 label（文案）和可选 badge（角标）"
    },
    "activeIndex": {
      "type": "number",
      "default": 0,
      "description": "当前选中项索引"
    },
    "indicatorStyle": {
      "type": "string",
      "enum": ["underline"],
      "default": "underline",
      "description": "选中态指示形式：固定宽度 20px 底部短线，高 3px，全圆角"
    },
    "sticky": {
      "type": "boolean",
      "default": false,
      "description": "是否在滚动时吸顶固定，局部锚定型建议设为 true"
    },
    "scrollable": {
      "type": "boolean",
      "default": false,
      "description": "Tab 数量较多时是否支持横向滚动"
    },
    "swipeable": {
      "type": "boolean",
      "default": false,
      "description": "内容区是否支持左右滑动切换 Tab"
    },
    "icon": {
      "type": "string",
      "enum": ["none", "solid"],
      "default": "none",
      "description": "是否展示前置 icon：none=无；solid=面性 icon 16×16"
    },
    "badge": {
      "type": "string",
      "enum": ["none", "number", "dot"],
      "default": "none",
      "description": "角标类型：none=无；number=数字提醒；dot=小红点"
    }
  },
  "designTokens": {
    "containerPadding": "0px 12px",
    "itemGap": "16px",
    "itemPadding": "12px 0px 6px",
    "internalGap": "2px",
    "fontSize": "14px",
    "fontFamily": "SF Pro",
    "fontWeight": "700",
    "lineHeight": "1.19em",
    "indicatorWidth": "20px",
    "indicatorHeight": "3px",
    "indicatorRadius": "2px",
    "selectedColor": "#000000",
    "unselectedColor": "#767676",
    "iconSize": "16px"
  },
  "usageRules": [
    "一级 Tab 与二级 Tab 必须有明显视觉层级差异（字号 14 vs 12、指示线 vs 无、颜色对比）",
    "同一页面多级 Tab 组合时，先大类后小类，层级关系清晰",
    "Tab 不用于操作动作（提交/确认/下一步），仅用于内容导航切换",
    "等距模式下 Tab 间距固定 16px，宽度跟随内容自适应",
    "局部锚定型 Tab 栏须吸顶（sticky=true），保持可操作性",
    "多级 Tab 最多同时展示 3 级（含筛选标签组合），禁止超过 3 级",
    "Tab 数量超出一屏宽度时须启用横向滚动（scrollable=true）",
    "禁止一级二级使用相同字号+字重+指示线样式的组合",
    "多级 Tab 之间须有足够间距或分隔，每个可点击热区至少 44×44pt，避免误触",
    "同一组 tab 中 icon 风格须一致，提供选中/未选两种状态"
  ]
}
```

### 胶囊型 Tab（Capsule Tab）

```json
{
  "componentName": "CapsuleTabNavigation",
  "figmaComponentKey": "1:451（面性已选26px）/ 1:455（面性已选红点26px）",
  "description": "胶囊形态的 Tab 导航，适用于筛选型场景。小圆角胶囊容器，支持面性填充和线框两种样式，常用于信息流、店铺、商详等场景。",
  "properties": {
    "height": {
      "type": "string",
      "enum": ["24", "26"],
      "default": "26",
      "description": "选项高度：24=高屏效场景（信息流）；26=常规场景（店铺、关注页、商详）"
    },
    "style": {
      "type": "string",
      "enum": ["solid", "outline"],
      "default": "solid",
      "description": "选项样式：solid=面性填充；outline=白色填充+线框"
    },
    "items": {
      "type": "array",
      "minItems": 2,
      "description": "Tab 项列表"
    },
    "activeIndex": {
      "type": "number",
      "default": 0
    },
    "icon": {
      "type": "string",
      "enum": ["none", "solid", "outline"],
      "default": "none",
      "description": "icon 类型：none=无；solid=面性 14×14；outline=线性 14×14"
    },
    "badge": {
      "type": "string",
      "enum": ["none", "number", "dot"],
      "default": "none"
    }
  },
  "designTokens": {
    "itemPadding": "6px 8px",
    "itemGap": "2px",
    "borderRadius": "2px",
    "fontSize": "12px",
    "fontFamily": "SF Pro",
    "fontWeight": "510",
    "lineHeight": "1.19em",
    "iconSize": "14px",
    "minWidth": "48px",
    "selectedBg": "#000000",
    "selectedTextColor": "#FFFFFF",
    "colorScheme": "中性色（常规）/ 业务色（营销频道）"
  },
  "usageRules": [
    "面性容器使用面性 icon，线性容器使用线性 icon",
    "同一组 tab 需使用风格一致的 icon",
    "icon 均需提供未选/选中两种状态",
    "宽度最小 48px，最大不超过屏幕 50%",
    "常规功能场景使用中性色，营销频道可使用业务色"
  ]
}
```

### 图文组合型 Tab（Image Tab）

```json
{
  "componentName": "ImageTabNavigation",
  "figmaComponentKey": "1:1071（上滑态已选）/ 1:1104（56px已选）/ 1:1155（64px未选）",
  "description": "图片+文字组合的 Tab 导航，适用于频道入口、品类导航等需要视觉预览的场景。图片为超椭圆定制形状，选中态有双层描边强调。",
  "properties": {
    "imageSize": {
      "type": "string",
      "enum": ["32", "56", "64"],
      "default": "56",
      "description": "图片尺寸：32=小规格（横向排列，整体宽 88px）；56=中规格（纵向排列，整体宽 64px）；64=大规格（纵向排列，整体宽 78px）"
    },
    "imageShape": {
      "type": "string",
      "enum": ["squircle"],
      "default": "squircle",
      "description": "图片形状：超椭圆定制形状"
    },
    "items": {
      "type": "array",
      "minItems": 2,
      "description": "Tab 项列表，每项包含 image（图片）和 label（文案）"
    },
    "activeIndex": {
      "type": "number",
      "default": 0
    },
    "scrollable": {
      "type": "boolean",
      "default": true,
      "description": "通常支持横向滚动"
    },
    "textLines": {
      "type": "string",
      "enum": ["1", "2", "multiline"],
      "default": "2",
      "description": "文案行数：1=单行；2=双行；multiline=超出省略"
    }
  },
  "designTokens": {
    "imageTextGap": "4px",
    "fontSize": "12px",
    "fontFamily": "SF Pro",
    "fontWeightSelected": "700",
    "fontWeightDefault": "400",
    "lineHeight": "1.19em",
    "textColor": "color_brand_primary_contrast",
    "unselectedStroke": "color_neutrals_overlay_dark_soft（内描边）",
    "selectedStroke": "color_brand_primary 1px + color_brand_primary_contrast 3px（双层内描边）"
  },
  "usageRules": [
    "主要用于首页/列表的相关页面",
    "32px 尺寸适合横向排列（图片左+文字右），56px/64px 适合纵向排列（图片上+文字下）",
    "图片须保持一致的尺寸和形状，禁止同一行混用不同规格",
    "文字标签超出省略，不换行（32px 尺寸限 2 行，56px/64px 可多行）",
    "横向滚动时选中项自动居中展示",
    "最多支持展示两排图文 tab",
    "支持点击后在当前页面刷新或直接跳转新页面",
    "选项宽度建议最大不超过屏幕 50%"
  ]
}
```
