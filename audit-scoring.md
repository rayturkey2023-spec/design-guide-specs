# 设计审核评分规则

> 用途：审核 Agent 对照此文件输出结构化评分  
> 更新：2026-07-14  
> Webhook URL：https://script.google.com/macros/s/AKfycbwrysvjKlFNlmRPjQjNoCF3DW1g_u8cGIZvMPMO1ipVjKLRK9NieGKMernX7yjPwAMw/exec

---

## 评分维度

| 维度 | 权重 | 说明 |
|------|------|------|
| 合规得分 | 50% | 是否违反 EU/FR 合规规则（regulations/） |
| 规范得分 | 50% | 是否符合 Token / 组件 / 布局规范 |

**综合得分 = 合规得分 × 0.5 + 规范得分 × 0.5**

---

## 问题严重等级

| 等级 | 扣分 | 定义 | 示例 |
|------|------|------|------|
| Critical | -25分 | 违反合规红线，必须修改才能上线 | 展示了 EU-D-001 禁止的销量信息 |
| High | -15分 | 严重违反规范，影响用户体验或品牌一致性 | 同屏出现 2 个 Primary 按钮 |
| Medium | -8分 | 规范偏差，视觉或交互不一致 | 使用了非 Token 色值 |
| Low | -3分 | 轻微偏差，建议修改 | 间距值不在梯度内 |

---

## 综合评级标准

| 评级 | 分数范围 | 含义 | 能否上线 |
|------|---------|------|---------|
| Pass | 90–100 | 符合规范 | ✅ 可直接上线 |
| Review | 70–89 | 存在中低级问题 | ⚠️ 修改后复审 |
| Fail | 0–69 | 存在严重问题 | ❌ 必须返工 |

---

## 审核 Checklist 顺序

### 1. 合规检查（优先）
- [ ] 涉及 EU 市场 → 逐条对照 `regulations/合规知识库-欧盟通用EU.md`
- [ ] 涉及 FR 市场 → 追加对照 `regulations/合规知识库-法国站FR.md`
- [ ] 每个违规项标注规则编号（如 EU-D-001）

### 2. Token 检查
- [ ] 所有颜色值是否在 `tokens/colors.md` Token 范围内
- [ ] 所有间距值是否在 2/4/6/8/10/12/16px 梯度内
- [ ] 圆角值是否使用 Token
- [ ] 字号/字重是否使用 Token

### 3. 组件检查
- [ ] 是否使用了规范外的自绘元素
- [ ] Primary 按钮是否每屏唯一
- [ ] 浮层/弹窗是否由用户操作触发（非自动弹出）
- [ ] 列表页是否包含骨架屏/空态/错误态

### 4. 布局检查
- [ ] 页面左右边距是否为 16px
- [ ] 可点击元素触控区是否 ≥ 44×44px
- [ ] 移动端是否有底部安全区处理

---

## 输出格式（固定结构，用于写入 Google Sheets）

```json
{
  "timestamp": "YYYY-MM-DD HH:mm",
  "reviewer": "姓名",
  "figma_file": "文件名",
  "figma_url": "链接",
  "market": "DE/FR/EU/全站",
  "platform": "APP/PWA/PC",
  "compliance_score": 0-100,
  "spec_score": 0-100,
  "total_score": 0-100,
  "rating": "Pass/Review/Fail",
  "issues": [
    {
      "rule": "规则编号或分类",
      "severity": "Critical/High/Medium/Low",
      "location": "页面位置描述",
      "detail": "具体问题描述",
      "suggestion": "修改建议"
    }
  ],
  "issues_count": 数量,
  "status": "待修改/已修改/已上线"
}
```
