# 弹窗（Modal / Dialog）组件规范

## 使用场景

- 需要用户明确确认的操作（删除、提交、风险提示）
- 需要临时输入少量信息（单字段填写、单项选择）
- 内容层级需与当前页面明显区分

## 禁止场景

- 禁止展示大量内容（内容超过屏幕高度 70% 时，改用全屏页面）
- 禁止弹窗内嵌套弹窗
- 禁止用于非关键提示（用 Toast 替代）
- 禁止自动弹出（必须由用户操作触发）

## 结构规范

```
弹窗
├── 遮罩层（color-bg-overlay，点击遮罩是否可关闭视业务决定）
└── 弹窗容器（radius-lg，color-bg-card，shadow-lg）
    ├── 标题区（可选）：text-heading-md，对齐方式统一（居中或左对齐选一种）
    ├── 内容区：text-body-md，padding spacing-16 或 spacing-20
    └── 操作区
         ├── 确认 + 取消：左取消右确认，或上下排列（确认在上）
         └── 仅确认：居中
```

## 尺寸约束

- 移动端：宽度 = 屏幕宽 - spacing-32×2，高度自适应内容
- PC 端：宽度固定 【填入 px，建议 400–480px】
- 操作区按钮间距 spacing-8

## 动效规范

- 进入：从中心缩放 + 透明度渐入，时长 200ms
- 退出：透明度渐出，时长 150ms
- 遮罩：透明度渐入渐出，与弹窗同步

---

## 组件 Schema（AI 调用参考）

```json
{
  "componentName": "Modal",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "description": "用于需要用户明确响应的中断性操作，如确认、警示、简单表单输入。触发后打断当前页面流程，要求用户完成操作后才能继续。",
  "properties": {
    "title": {
      "type": "string",
      "description": "弹窗标题文字，为空时不渲染标题区"
    },
    "titleAlign": {
      "type": "string",
      "enum": ["left", "center"],
      "default": "center",
      "description": "标题对齐方式，同一产品线须统一选择一种，不可混用"
    },
    "showCloseButton": {
      "type": "boolean",
      "default": true,
      "description": "是否显示右上角关闭图标；确认类弹窗建议关闭以强制用户选择"
    },
    "maskClosable": {
      "type": "boolean",
      "default": false,
      "description": "点击遮罩是否关闭弹窗；破坏性操作（删除/提交）须设为 false"
    },
    "footerLayout": {
      "type": "string",
      "enum": ["horizontal", "vertical", "single"],
      "default": "horizontal",
      "description": "操作区布局：horizontal=左取消右确认，vertical=上确认下取消，single=仅一个居中按钮"
    },
    "size": {
      "type": "string",
      "enum": ["sm", "md", "lg"],
      "default": "md",
      "description": "sm 用于纯文字确认提示；md 用于含简单表单；lg 用于内容较多的展示场景"
    }
  },
  "slots": {
    "body": {
      "description": "弹窗内容区，可注入任意内容组件（表单、列表、图文等）",
      "acceptedComponents": ["Form", "List", "Image", "Text"],
      "maxHeightRule": "内容区最大高度为屏幕高度 70%，超出时内部滚动"
    },
    "footer": {
      "description": "操作按钮区，默认渲染确认+取消，可替换为自定义按钮组",
      "acceptedComponents": ["Button", "ButtonGroup"]
    }
  },
  "usageRules": [
    "同一页面同时只能存在一个 Modal，禁止嵌套",
    "破坏性操作（删除、清空）的确认按钮必须使用 Button/Danger 变体",
    "内容超过屏幕高度 70% 时禁止使用此组件，改用全屏页面",
    "弹窗必须由用户主动操作触发，禁止页面加载时自动弹出",
    "footerLayout 为 single 时，按钮文案须明确动作（如'知道了'，而非'确定'）"
  ]
}
```
