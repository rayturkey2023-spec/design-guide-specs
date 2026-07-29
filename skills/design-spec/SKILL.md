---
name: design-spec
description: 设计规范按需检索工具。根据用户描述的设计任务，智能选取相关规范模块，输出精简的 Figma Make Context。避免每次注入全量规范文档。
---

# 设计规范按需加载 Skill

## 触发条件

以下任何情况都应激活此 skill：

- 用户要生成 Figma 设计方案、UI 稿、交互稿
- 用户说"帮我设计 XX 页面"、"生成 XX 组件"、"Figma Make 用什么规范"
- 用户需要为 Figma Make 准备设计规范 Context
- 用户询问某个组件/Token 的使用规范

## 执行步骤

### Step 1：理解任务

分析用户描述的设计任务，识别以下维度：
- **平台**：移动端 / PC 端 / 不明确（需追问）
- **涉及组件**：从用户描述中提取（弹窗、按钮、半浮层、Toast 等）
- **内容类型**：列表、表单、详情页、操作面板等

如果平台不明确，先追问：「这是移动端还是 PC 端页面？」再继续。

### Step 2：读取模块索引

```
读取文件：~/tasks/ai-workflow/specs/index.md
```

根据 Step 1 的分析结果，从索引中选出本次需要加载的模块。

**选取逻辑：**
- Token 模块：几乎所有任务都需要 colors + spacing；有浮层/卡片加 radius + shadow；有文字展示加 typography
- Component 模块：仅加载任务中明确涉及的组件，不预加载
- Layout 模块：根据平台加载 mobile.md 或 pc.md
- constraints.md：始终加载

### Step 3：读取选中的规范文件

逐一读取 Step 2 选出的文件：
- `~/tasks/ai-workflow/specs/tokens/colors.md`
- `~/tasks/ai-workflow/specs/tokens/spacing.md`
- `~/tasks/ai-workflow/specs/tokens/typography.md`（按需）
- `~/tasks/ai-workflow/specs/tokens/radius.md`（按需）
- `~/tasks/ai-workflow/specs/tokens/shadow.md`（按需）
- `~/tasks/ai-workflow/specs/components/[组件名].md`（按需）
- `~/tasks/ai-workflow/specs/layout/mobile.md` 或 `pc.md`
- `~/tasks/ai-workflow/specs/constraints.md`

### Step 4：整合输出

将读取的规范内容整合为一份格式化的 Context，输出格式如下：

---

## 设计规范 Context

> 已加载模块：[列出加载的文件名]

[整合后的规范内容，按 Token → 组件 → 布局 → 全局约束 顺序排列]

---

## 下一步

将以上 Context 粘贴到 Figma Make，追加你的设计任务描述：

```
[粘贴上方 Context]

---

## 当前任务
[描述你要设计的页面/组件]

请严格基于以上设计规范生成 UI 方案。遇到规范未覆盖的场景，先说明设计决策依据再生成。
```

---

## 注意事项

- 规范文件中标注 `【填入 xxx】` 的占位符表示该团队尚未填写真实值，输出时原样保留并提示用户补充
- 如果用户询问的组件在规范文件中不存在，告知用户该组件规范尚未建立，并建议参考哪个最相近的规范
