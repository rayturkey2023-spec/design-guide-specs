# 间距 Token

|   |   |   |
|---|---|---|
|维度|可选值|说明|
|层级（Type）|page / module / section / floor / element|页面 → 模块 → 分区 → 楼层 → 元素|
|尺寸（Variant）|bitty / mini / small / normal / big / larger / max|2 / 4 / 6 / 8 / 10 / 12 / 16 px|

> 方向（水平/垂直）不编码到 Token 名称中，由 CSS 属性本身决定。

---

## Token 全表

### Page 级（页面/栅格）

|   |   |   |
|---|---|---|
|Token|值|使用场景|
|`spacing_page_small`|6px|卡片横向间距（非通栏：购物车/首页/列表）|
|`spacing_page_normal`|8px|栅格基础间距|
|`spacing_page_larger`|12px|通栏间距|
|`spacing_page_max`|16px|页面左右安全边距（移动端）|

### Module 级（模块）

|   |   |   |
|---|---|---|
|Token|值|使用场景|
|`spacing_module_small`|6px|首页/列表：模块内间距|
|`spacing_module_normal`|8px|模块之间间距（首页/列表/商详）；首页/列表模块内间距|
|`spacing_module_big`|10px|商详交易：模块内间距|
|`spacing_module_larger`|12px|模块之间间距（首页/列表）；商详交易模块内间距|

**约束**：同页面内模块之间间距只允许使用一种值。

### Section 级（分区/区块）

|   |   |   |
|---|---|---|
|Token|值|使用场景|
|`spacing_section_normal`|8px|首页/列表：模块内间距|
|`spacing_section_big`|10px|商详交易：模块内间距|
|`spacing_section_larger`|12px|商详交易：区块之间间距|

**约束**：区块内间距为 0px（商详交易场景）。

### Floor 级（楼层/卡片）

|   |   |   |
|---|---|---|
|Token|值|使用场景|
|`spacing_floor_small`|6px|首页/列表：楼层/卡片之间间距|
|`spacing_floor_normal`|8px|首页/列表：楼层/卡片之间间距；卡片内间距|
|`spacing_floor_big`|10px|商详交易：楼层/卡片之间间距|
|`spacing_floor_larger`|12px|商详交易：楼层/卡片之间间距|
|`spacing_floor_max`|16px|卡片内边距（较大卡片）|

**约束**：同卡片内楼层之间间距只允许使用一种值。

### Element 级（元素）

|   |   |   |
|---|---|---|
|Token|值|使用场景|
|`spacing_element_bitty`|2px|图标与文字间距、极小内间距|
|`spacing_element_mini`|4px|标签内间距、图标对齐微调|
|`spacing_element_small`|6px|元素之间间距（商详交易）|
|`spacing_element_normal`|8px|组件内元素间距、行内元素间距|
|`spacing_element_big`|10px|元素之间间距（商详交易）|
|`spacing_element_larger`|12px|元素之间间距|

---

## 场景 → Token 速查表

### 首页 / 列表

|   |   |   |
|---|---|---|
|使用场景|Token|值|
|通栏横向间距|`spacing_page_larger`|12px|
|卡片横向间距（非通栏）|`spacing_page_small`|6px|
|页面左右安全边距|`spacing_page_max`|16px|
|模块之间|`spacing_module_normal` 或 `spacing_module_larger`|8px 或 12px|
|模块内间距|`spacing_module_small` 或 `spacing_module_normal`|6px 或 8px|
|楼层/卡片之间|`spacing_floor_small` 或 `spacing_floor_normal`|6px 或 8px|
|卡片内间距|`spacing_floor_normal`|8px|
|元素之间|`spacing_element_bitty` ~ `spacing_element_larger`|2/4/8/12px|

### 商详交易

|   |   |   |
|---|---|---|
|使用场景|Token|值|
|模块之间|`spacing_module_normal`|8px|
|模块内间距|`spacing_module_big` 或 `spacing_module_larger`|10px 或 12px|
|区块之间|`spacing_section_larger`|12px|
|区块内|—|0px|
|楼层/卡片之间|`spacing_floor_normal` / `big` / `larger`|8/10/12px|
|元素之间|`spacing_element_bitty` ~ `spacing_element_larger`|2/4/6/8/10/12px|

---

## 使用约束

- 禁止使用 Token 以外的值（如 3px、5px、7px、15px）
    
- 间距基数梯度：2 / 4 / 6 / 8 / 10 / 12 / 16（px）
    
- 同页面内，同层级间距只允许使用一种值（保持一致性）
    
- 页面层级关系：Page → Module → Section → Floor → Element
    
- 方向由 CSS 属性决定（margin-top、padding-left、gap 等），Token 只定义数值大小