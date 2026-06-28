# Toast 轻提示组件规范

## 使用场景

- 操作成功的即时反馈（提交成功、复制成功）
- 非关键性错误提示（网络不稳定、操作失败）
- 系统状态通知（不需要用户响应）

## 禁止场景

- 禁止用于需要用户确认的操作（用 Modal 替代）
- 禁止用于表单校验错误（用行内错误提示）
- 禁止同时出现 2 个 Toast
- 禁止 Toast 停留超过 5 秒（用户需要的信息应该放在页面上）

## 类型与图标

| 类型 | 图标 | 背景色 |
|------|------|-------|
| Success | ✓ | color-success |
| Error | ✗ | color-danger |
| Warning | ! | color-warning |
| Info | i | color-text-secondary |
| Loading | 转圈 | color-text-secondary |

## 位置与时长

- 移动端：屏幕顶部居中（导航栏下方）或底部居中（操作区上方）
- PC 端：右上角
- 自动消失时长：Success / Info → 2s；Warning / Error → 3s；Loading → 手动控制

## 尺寸约束

- 最大宽度：屏幕宽 - spacing-32
- 文字不超过 2 行，超出截断并补充说明入口

---

## 组件 Schema（AI 调用参考）

```json
{
  "componentName": "Toast",
  "figmaComponentKey": "【填入 Figma 组件 Key】",
  "description": "非阻断式的轻量操作反馈，自动消失，不需要用户主动关闭。仅用于告知用户操作结果，不用于需要响应的场景。",
  "properties": {
    "type": {
      "type": "string",
      "enum": ["success", "error", "warning", "info", "loading"],
      "description": "success=操作成功；error=操作失败；warning=风险提示；info=普通通知；loading=异步进行中（手动控制消失）"
    },
    "message": {
      "type": "string",
      "description": "提示文案，不超过 2 行，简洁描述结果而非原因"
    },
    "duration": {
      "type": "number",
      "description": "自动消失时长（ms）：success/info 默认 2000；warning/error 默认 3000；loading 传 0 表示手动控制"
    },
    "position": {
      "type": "string",
      "enum": ["top", "bottom"],
      "default": "top",
      "description": "移动端显示位置：top=导航栏下方；bottom=底部操作区上方。PC 端固定右上角，此属性无效"
    }
  },
  "slots": {},
  "usageRules": [
    "同一时刻屏幕上只能存在一个 Toast，新 Toast 出现时自动替换旧的",
    "表单校验错误禁止用 Toast，须使用字段行内错误提示",
    "需要用户确认或响应的信息禁止用 Toast，改用 Modal",
    "type=loading 时须在异步操作完成后手动关闭，不可无限展示",
    "文案须描述结果（'提交成功'），不描述过程（'正在提交中'配合 loading 类型使用）"
  ]
}
```
