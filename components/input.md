# 输入框（Input / Form Control）组件规范

## 变体与使用场景

| 变体 | 使用场景 |
|------|---------|
| Text Input | 单行文字输入（姓名、手机号、搜索词）|
| Textarea | 多行文字输入（备注、描述，超过 1 行内容）|
| Password | 密码输入，带明文切换图标 |
| Search | 搜索框，含搜索图标 + 清除按鈕 |
| Number | 纯数字输入，可带步进器 |

## 状态

- Default / Focus / Filled / Error / Disabled / Read-only

## 结构规范

表单项
├── Label（必填项左侧标红色星号 *）
├── 输入框容器（radius-md，border color-border，padding spacing-12 水平）
│   ├── 前置图标（可选）
│   ├── 输入区域（text-body-md，color-text-primary）
│   ├── 占位文字（color-text-placeholder）
│   └── 后置图标/清除按鈕（可选）
└── 辅助文字 / 错误提示（text-body-sm，错误态用 color-danger）

## 尺寸约束

| 尺寸 | 高度 | 使用场景 |
|------|------|---------|
| Large | 【填入 px】 | 移动端主要表单 |
| Medium | 【填入 px】 | 常规表单 |
| Small | 【填入 px】 | 紧凑型筛选、内嵌表单 |

## 表单布局规范

- 标签与输入框：垂直排列（移动端）/ 水平排列（PC 端宽表单）
- 相邻表单项间距：spacing-16（移动端）/ spacing-20（PC 端）
- 表单分组：相关字段用 Card 包裹，组间距 spacing-24
- 必填字段全部填写后，提交按鈕才可点击

## 禁止事项

- 禁止 Error 状态通过弹窗提示，必须使用输入框下方行内错误文字
- 禁止 Label 省略（纯 placeholder 不可代替 Label，无障碍不合格）
- 禁止 Textarea 高度固定过小（最小显示 3 行）
- 禁止在移动端使用水平滚动的表单布局

---

## 组件 Schema（AI 调用参考）

{
  "componentName": "Input",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "description": "用于收集用户文字输入的基础表单控件。通过 type 区分输入类型，通过 state 反映当前状态。表单场景中须配合 Label 和错误提示使用。",
  "properties": {
    "type": { "type": "string", "enum": ["text", "password", "search", "number", "textarea"], "default": "text" },
    "size": { "type": "string", "enum": ["large", "medium", "small"], "default": "medium" },
    "state": { "type": "string", "enum": ["default", "focus", "filled", "error", "disabled", "readonly"], "default": "default" },
    "label": { "type": "string", "description": "表单项标签，不可省略" },
    "required": { "type": "boolean", "default": false },
    "placeholder": { "type": "string" },
    "errorMessage": { "type": "string", "description": "state=error 时显示在输入框下方" },
    "helperText": { "type": "string" },
    "showClear": { "type": "boolean", "default": false }
  },
  "slots": {
    "prefix": { "description": "前置区域", "acceptedComponents": ["Icon", "Text"] },
    "suffix": { "description": "后置区域", "acceptedComponents": ["Icon", "Button", "Text"] }
  },
  "usageRules": [
    "每个输入框必须配有 Label，禁止仅用 placeholder 替代 Label",
    "必填字段须设 required=true，显示星号标识",
    "错误提示必须使用行内方式，禁止使用弹窗",
    "表单提交前所有必填项未填时，提交按鈕须为 disabled 状态",
    "Textarea 最小显示高度不低于 3 行"
  ]
}
