---

参考：[https://juejin.cn/post/6971426277261574152](https://juejin.cn/post/6971426277261574152)

功能：可以用代码生成任意你想要的**流程图**、**状态图**、**甘特图**、**时序图**、 **饼图**、**类图**、**关系图**、**旅程图**

## 流程图

---

### 基本结构

1. 圆角矩形 表示“开始”与“结束”
1. 矩形表示行动方案、普通工作环节用
1. 菱形表示问题判断或判定（审核/审批/评审）环节
1. 用平行四边形表示输入输出
1. 箭头代表工作流方向

### 节点：graph

---

![](https://cdn.nlark.com/yuque/__mermaid_v3/4268f447dae27c6902a7ff62672953b2.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuU1vlo7DmmI7kuIDkuKrmtYHnqIvlm75dLS0-XG5cbnMoXCLlvIDlp4vvvIhzdGFydO-8iVwiKVxuIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My80MjY4ZjQ0N2RhZTI3YzY5MDJhN2ZmNjI2NzI5NTNiMi5zdmciLCJpZCI6ImFPbXRwIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)
### 流程方向

---

自上而下 graph TB
自下而上 graph BT
自左而右 graph LR
自右而左 graph RL
![](https://cdn.nlark.com/yuque/__mermaid_v3/f0263801e09533845593657da8d44e63.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBMUlxuczFb5byA5aeLXVxuLS0-XG5zMlvnu5PmnZ9dIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My9mMDI2MzgwMWUwOTUzMzg0NTU5MzY1N2RhOGQ0NGU2My5zdmciLCJpZCI6ImZwS1lzIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)
### 节点形状

---

矩形：中括号[]
![](https://cdn.nlark.com/yuque/__mermaid_v3/1600b764a3f87b25b2dfe556ef6f0591.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBMUlxuczFb55-p5b2iXVxuIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My8xNjAwYjc2NGEzZjg3YjI1YjJkZmU1NTZlZjZmMDU5MS5zdmciLCJpZCI6ImV3NVhWIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)圆角矩形：小括号()
![](https://cdn.nlark.com/yuque/__mermaid_v3/4b044f736818595e7ad7cd7c750f7767.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBMUlxuczEo5ZyG6KeS55-p5b2iKSIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvNGIwNDRmNzM2ODE4NTk1ZTdhZDdjZDdjNzUwZjc3Njcuc3ZnIiwiaWQiOiJhQWk1VCIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)体育场形状：小括号中括号([])
![](https://cdn.nlark.com/yuque/__mermaid_v3/9a850a87c639937ccfc3023c72fbf160.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnMxKFvkvZPogrLlnLrlvaLnirZdKVxuLS0-XG5zMihb5L2T6IKy5Zy65b2i54q2Ml0pIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My85YTg1MGE4N2M2Mzk5MzdjY2ZjMzAyM2M3MmZiZjE2MC5zdmciLCJpZCI6ImJ3b1diIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)圆柱形：中括号小括号[()]
![](https://cdn.nlark.com/yuque/__mermaid_v3/7a9e3540babb9a7a6cb5e4684195c91a.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnMxWyjlnIbmn7HlvaIpXVxuLS0-XG5zMihb5L2T6IKy5Zy65b2i54q2Ml0pIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My83YTllMzU0MGJhYmI5YTdhNmNiNWU0Njg0MTk1YzkxYS5zdmciLCJpZCI6IkhtaFVYIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiaGVpZ2h0IjoyMzYuNzk5OTg3NzkyOTY4NzUsImNhcmQiOiJkaWFncmFtIn0=)圆形：小括号小括号(())
![](https://cdn.nlark.com/yuque/__mermaid_v3/c0425553d6dac5b0ca0d2f0fa7d8d011.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnMxKCjlnIblvaIpKVxuLS0-XG5zMihb5L2T6IKy5Zy65b2i54q2Ml0pIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My9jMDQyNTU1M2Q2ZGFjNWIwY2EwZDJmMGZhN2Q4ZDAxMS5zdmciLCJpZCI6InZrRVdGIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)菱形：大括号{}
![](https://cdn.nlark.com/yuque/__mermaid_v3/acfb51de383f2c0a1e5931d9537a6d79.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnMxe-iPseW9on1cbi0tPlxuczIoW-S9k-iCsuWcuuW9oueKtjJdKSIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvYWNmYjUxZGUzODNmMmMwYTFlNTkzMWQ5NTM3YTZkNzkuc3ZnIiwiaWQiOiJPVTJuOSIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)六边形：大括号大括号{{}}
![](https://cdn.nlark.com/yuque/__mermaid_v3/c42a2b4fe716ec16574b9130f3e78344.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnMxe3vlha3ovrnlvaJ9fVxuLS0-XG5zMihb5L2T6IKy5Zy65b2i54q2Ml0pIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My9jNDJhMmI0ZmU3MTZlYzE2NTc0YjkxMzBmM2U3ODM0NC5zdmciLCJpZCI6IlRSSjVVIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)
非对称图：id>内容]
![](https://cdn.nlark.com/yuque/__mermaid_v3/dc16eac8fca6328e5137288c2845b360.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnMxPumdnuWvueensOWbvuW9ol1cbi0tPlxuczIoW-S9k-iCsuWcuuW9oueKtjJdKSIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvZGMxNmVhYzhmY2E2MzI4ZTUxMzcyODhjMjg0NWIzNjAuc3ZnIiwiaWQiOiJRaE9KQSIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)
平行四边形
![](https://cdn.nlark.com/yuque/__mermaid_v3/28aa89d273447a27504f0eb9b278c037.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnNbXFzlvIDlp4tcXF0gLS0-IEVbL-e7k-adny9dIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My8yOGFhODlkMjczNDQ3YTI3NTA0ZjBlYjliMjc4YzAzNy5zdmciLCJpZCI6IndiTzNqIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)梯形
![](https://cdn.nlark.com/yuque/__mermaid_v3/9ad374d82261ec3c93760e9a322c32f2.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBcbnNbL-W8gOWni1xcXSAtLT4gRVsv57uT5p2fXFxdIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My85YWQzNzRkODIyNjFlYzNjOTM3NjBlOWEzMjJjMzJmMi5zdmciLCJpZCI6IlNXTUU1IiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)
### 节点间的连接

---

实线：---
![](https://cdn.nlark.com/yuque/__mermaid_v3/83aa253d87fe9cc8779893666ed5dfe0.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdIC0tLSBlW-e7k-adn10iLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzgzYWEyNTNkODdmZTljYzg3Nzk4OTM2NjZlZDVkZmUwLnN2ZyIsImlkIjoiU2U3dzciLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)虚线:-.-
![](https://cdn.nlark.com/yuque/__mermaid_v3/4d96a496ccf34dfe6fb73f75a7794680.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdIC0uLSBlW-e7k-adn10iLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzRkOTZhNDk2Y2NmMzRkZmU2ZmI3M2Y3NWE3Nzk0NjgwLnN2ZyIsImlkIjoiSmtaWW4iLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)粗连接线: ===
![](https://cdn.nlark.com/yuque/__mermaid_v3/5ea4b4ea0fb90474173b6155ca976006.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdID09PSBlW-e7k-adn10iLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzVlYTRiNGVhMGZiOTA0NzQxNzNiNjE1NWNhOTc2MDA2LnN2ZyIsImlkIjoiVGtXUkEiLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)实线箭头： -->
![](https://cdn.nlark.com/yuque/__mermaid_v3/242872241ee8e149bc90c0bed43658f6.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdIC0tPiBlW-e7k-adn10iLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzI0Mjg3MjI0MWVlOGUxNDliYzkwYzBiZWQ0MzY1OGY2LnN2ZyIsImlkIjoiZG0xQTMiLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)虚线箭头： -.->
![](https://cdn.nlark.com/yuque/__mermaid_v3/68e265a5554e72c43b0a5a0e141148ad.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdIC0uLT4gZVvnu5PmnZ9dIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My82OGUyNjVhNTU1NGU3MmM0M2IwYTVhMGUxNDExNDhhZC5zdmciLCJpZCI6ImJ6ZmU5IiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)粗线箭头：==>
![](https://cdn.nlark.com/yuque/__mermaid_v3/9549cae519db2c6198fe3ffc0bf5da4d.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdID09PiBlW-e7k-adn10iLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzk1NDljYWU1MTlkYjJjNjE5OGZlM2ZmYzBiZjVkYTRkLnN2ZyIsImlkIjoiR2lveGoiLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)带文字连接线（实线）: --内容--->
![](https://cdn.nlark.com/yuque/__mermaid_v3/73a736640de7ef8f22dd4623c5884503.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdIC0t6L-H56iLLS0-IGVb57uT5p2fXSIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvNzNhNzM2NjQwZGU3ZWY4ZjIyZGQ0NjIzYzU4ODQ1MDMuc3ZnIiwiaWQiOiJVM1NSUiIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)带文字连接线（虚线）: -.内容.-->
![](https://cdn.nlark.com/yuque/__mermaid_v3/581dddd850e0f0d829770003a024eb42.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuc1vlvIDlp4tdIC0u6L-H56iLLi0-IGVb57uT5p2fXSIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvNTgxZGRkZDg1MGUwZjBkODI5NzcwMDAzYTAyNGViNDIuc3ZnIiwiaWQiOiJqb2k3UiIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)

### 关系链

---

单行
![](https://cdn.nlark.com/yuque/__mermaid_v3/370378ee13ef30dc2d632bbdeacc4eb4.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBMUlxuc1vlvIDlp4tdIC0t6LWw6LevLS0-IFBb6I-c5biC5Zy6XS0tPiBlW-e7k-adn10iLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzM3MDM3OGVlMTNlZjMwZGMyZDYzMmJiZGVhY2M0ZWI0LnN2ZyIsImlkIjoiZ3d3M1oiLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)多行
![](https://cdn.nlark.com/yuque/__mermaid_v3/944ff0c07c6c90d9db24d1a29fe28f7e.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBMUlxuc1vlvIDlp4tdIC0t6LWw6LevLS0-IFBb6I-c5biC5Zy6XS0tPiBlW-e7k-adn11cbnMgLS3otbDot68tLT4gb1vmsLjovonotoXluIJdIC0tPiBlIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My85NDRmZjBjMDdjNmM5MGQ5ZGIyNGQxYTI5ZmUyOGY3ZS5zdmciLCJpZCI6Ik1oQWNBIiwibWFyZ2luIjp7InRvcCI6dHJ1ZSwiYm90dG9tIjp0cnVlfSwiY2FyZCI6ImRpYWdyYW0ifQ==)
单循环
![](https://cdn.nlark.com/yuque/__mermaid_v3/a36a71e4d119d2a739317d424c9e202f.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBMUlxuc1vlvIDlp4tdIC0t6LWw6LevLS0-IFBb6I-c5biC5Zy6XS0tPiBlW-e7k-adn10gLS0-IHMiLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzL2EzNmE3MWU0ZDExOWQyYTczOTMxN2Q0MjRjOWUyMDJmLnN2ZyIsImlkIjoiSzJDdXIiLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)

## 子图标

---

```java
graph
    节点关系
    subgraph title //子图表的名称
    子图表的节点关系
    end //子图标结束标志

```

![](https://cdn.nlark.com/yuque/__mermaid_v3/5e5c6c3ce755c3ab2a405ad3f73045e5.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaFxuXHRcdHN1YmdyYXBoIHRpdGxlMlxuICAgIGMxIC0tPiBjMlxuXHRcdGVuZFxuICAgIHN1YmdyYXBoIHRpdGxlIFxuICAgIGIxIC0tPiBiMlxuICAgIGVuZCAiLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzVlNWM2YzNjZTc1NWMzYWIyYTQwNWFkM2Y3MzA0NWU1LnN2ZyIsImlkIjoiSllSTm8iLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)
其他模板
![](https://cdn.nlark.com/yuque/__mermaid_v3/dc919ee8b0c856324cac5b8ab3bd986b.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJncmFwaCBURFxuICAgIEFbU3RhcnRdIC0tPiBCe0lzIGl0P307XG4gICAgQiAtLT58WWVzfCBDW09LXTtcbiAgICBDIC0tPiBEW1JldGhpbmtdO1xuICAgIEQgLS0-IEI7XG4gICAgQiAtLS0tPnxOb3wgRVtFbmRdOyIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvZGM5MTllZThiMGM4NTYzMjRjYWM1YjhhYjNiZDk4NmIuc3ZnIiwiaWQiOiJFWXdDUSIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)

![](https://cdn.nlark.com/yuque/__mermaid_v3/743010bfb6962498a4b9a485b60a8305.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJzZXF1ZW5jZURpYWdyYW1cbiAgICBwYXJ0aWNpcGFudCBKb2huXG4gICAgcGFydGljaXBhbnQgQWxpY2VcbiAgICBBbGljZS0-PkpvaG46IEhlbGxvIEpvaG4sIGhvdyBhcmUgeW91P1xuICAgIEpvaG4tLT4-QWxpY2U6IEdyZWF0ISIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvNzQzMDEwYmZiNjk2MjQ5OGE0YjlhNDg1YjYwYTgzMDUuc3ZnIiwiaWQiOiJNaGJqYSIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)
![](https://cdn.nlark.com/yuque/__mermaid_v3/c0bfd0479dcf29d7cc961774486a0da6.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJjbGFzc0RpYWdyYW1cbiAgICBBbmltYWwgPHwtLSBEdWNrXG4gICAgQW5pbWFsIDx8LS0gRmlzaFxuICAgIEFuaW1hbCA8fC0tIFplYnJhXG4gICAgQW5pbWFsIDogK2ludCBhZ2VcbiAgICBBbmltYWwgOiArU3RyaW5nIGdlbmRlclxuICAgIEFuaW1hbDogK2lzTWFtbWFsKClcbiAgICBBbmltYWw6ICttYXRlKClcbiAgICBjbGFzcyBEdWNre1xuICAgICAgICArU3RyaW5nIGJlYWtDb2xvclxuICAgICAgICArc3dpbSgpXG4gICAgICAgICtxdWFjaygpXG4gICAgfVxuICAgIGNsYXNzIEZpc2h7XG4gICAgICAgIC1pbnQgc2l6ZUluRmVldFxuICAgICAgICAtY2FuRWF0KClcbiAgICB9XG4gICAgY2xhc3MgWmVicmF7XG4gICAgICAgICtib29sIGlzX3dpbGRcbiAgICAgICAgK3J1bigpXG4gICAgfSIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvYzBiZmQwNDc5ZGNmMjlkN2NjOTYxNzc0NDg2YTBkYTYuc3ZnIiwiaWQiOiJLbkVYVyIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)

![](https://cdn.nlark.com/yuque/__mermaid_v3/f348e709ebd1ad4959576048d9fafb8d.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJzdGF0ZURpYWdyYW0tdjJcbiAgICBbKl0gLS0-IFN0aWxsXG4gICAgU3RpbGwgLS0-IFsqXVxuXG4gICAgU3RpbGwgLS0-IE1vdmluZ1xuICAgIE1vdmluZyAtLT4gU3RpbGxcbiAgICBNb3ZpbmcgLS0-IENyYXNoXG4gICAgQ3Jhc2ggLS0-IFsqXSIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvZjM0OGU3MDllYmQxYWQ0OTU5NTc2MDQ4ZDlmYWZiOGQuc3ZnIiwiaWQiOiJlY01BeSIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)
![](https://cdn.nlark.com/yuque/__mermaid_v3/e16f7cd64364da8b0dc630b57b403e0d.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJlckRpYWdyYW1cbiAgICBDVVNUT01FUiB8fC0tb3sgT1JERVIgOiBwbGFjZXNcbiAgICBPUkRFUiB8fC0tfHsgTElORS1JVEVNIDogY29udGFpbnNcbiAgICBDVVNUT01FUiB9fC4ufHsgREVMSVZFUlktQUREUkVTUyA6IHVzZXMiLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzL2UxNmY3Y2Q2NDM2NGRhOGIwZGM2MzBiNTdiNDAzZTBkLnN2ZyIsImlkIjoia0FFUWMiLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)
![](https://cdn.nlark.com/yuque/__mermaid_v3/dabe2a36c04e6d879b54592f5a800443.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJnYW50dFxuICAgIHRpdGxlIEEgR2FudHQgRGlhZ3JhbVxuICAgIGRhdGVGb3JtYXQgIFlZWVktTU0tRERcbiAgICBzZWN0aW9uIFNlY3Rpb25cbiAgICBBIHRhc2sgICAgICAgICAgIDphMSwgMjAxNC0wMS0wMSwgMzBkXG4gICAgQW5vdGhlciB0YXNrICAgICA6YWZ0ZXIgYTEgICwgMjBkXG4gICAgc2VjdGlvbiBBbm90aGVyXG4gICAgVGFzayBpbiBzZWMgICAgICA6MjAxNC0wMS0xMiAgLCAxMmRcbiAgICBhbm90aGVyIHRhc2sgICAgICA6IDI0ZCIsInVybCI6Imh0dHBzOi8vY2RuLm5sYXJrLmNvbS95dXF1ZS9fX21lcm1haWRfdjMvZGFiZTJhMzZjMDRlNmQ4NzliNTQ1OTJmNWE4MDA0NDMuc3ZnIiwiaWQiOiJMQm5UMSIsIm1hcmdpbiI6eyJ0b3AiOnRydWUsImJvdHRvbSI6dHJ1ZX0sImNhcmQiOiJkaWFncmFtIn0=)

![](https://cdn.nlark.com/yuque/__mermaid_v3/20ac314e39a514b80c69bd7e1abdf7f9.svg#lake_card_v2=eyJ0eXBlIjoibWVybWFpZCIsImNvZGUiOiJwaWVcbiAgICB0aXRsZSBLZXkgZWxlbWVudHMgaW4gUHJvZHVjdCBYXG4gICAgXCJDYWxjaXVtXCIgOiA0Mi45NlxuICAgIFwiUG90YXNzaXVtXCIgOiA1MC4wNVxuICAgIFwiTWFnbmVzaXVtXCIgOiAxMC4wMVxuICAgIFwiSXJvblwiIDogIDUiLCJ1cmwiOiJodHRwczovL2Nkbi5ubGFyay5jb20veXVxdWUvX19tZXJtYWlkX3YzLzIwYWMzMTRlMzlhNTE0YjgwYzY5YmQ3ZTFhYmRmN2Y5LnN2ZyIsImlkIjoiR2pMR3kiLCJtYXJnaW4iOnsidG9wIjp0cnVlLCJib3R0b20iOnRydWV9LCJjYXJkIjoiZGlhZ3JhbSJ9)


