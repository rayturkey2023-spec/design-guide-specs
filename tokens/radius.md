# 圆角 Token

## 尺寸梯度


| 档位     | 值     |
| ------ | ----- |
| mini   | 0px   |
| small  | 2px   |
| normal | 4px   |
| medium | 6px   |
| big    | 8px   |
| larger | 12px  |
| max    | 999px |

---

## 容器圆角（radius_container）

|   |   |   |
|---|---|---|
|Token|值|适用场景|
|radius_container_mini|0px|—|
|radius_container_small|2px|购物车气泡、偏全局按钮|
|radius_container_normal|4px|Toast、商卡一行一、一行二|
|radius_container_medium|6px|一般卡片、分类卡片、频道卡片tab、列表搜索|
|radius_container_big|8px|弹层、顶部push、半浮层、拉通式大卡片|
|radius_container_larger|12px|大小腰带并存时大腰带（特殊）|
|radius_container_max|999px|超大圆角容器（全圆角）|

---

## 控件圆角（radius_control）

|   |   |   |   |
|---|---|---|---|
|Token|值|适用场景|设计意图|
|radius_control_mini|0px|—|—|
|radius_control_small|2px|按钮、小标签、长条形横幅|保证边角细节精致|
|radius_control_max|999px|选项、勾选框、数量编辑器、开关、商卡加车btn、Tab|提升识别度与友好性（全圆角）|

---

## 图片圆角（radius_picture）

|   |   |   |
|---|---|---|
|Token|值|适用场景|
|radius_picture_mini|0px|图标笔画连接处，保证品牌方正感|
|radius_picture_small|2px|一排N（N＞4）商品图、购物车商品图、下单商卡、订单照片墙、首页图片坑、一行三商卡、红人图|
|radius_picture_normal|4px|大卡片、双列流、一行一、buybox商卡（仅商详）|

---

## 圆角使用约束

- 同一组件内不混用不同圆角 Token
    
- 底部浮层：仅顶部两角使用 radius_container_big(8px)，底部无圆角
    
- 卡片内嵌图片：图片圆角与卡片圆角保持一致或略小
    

---