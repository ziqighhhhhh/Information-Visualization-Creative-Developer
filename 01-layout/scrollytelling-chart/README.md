# scrollytelling-chart — 滚动叙事 · 图表

可复用布局：sticky D3 图表 + 滚动步骤，步骤驱动图表状态机（总览 → 聚焦 → 对比……）。单文件演示见 `index.html`（**需联网**加载依赖）。

## 身份

scrollytelling 框架的**图表媒介**实例——信息可视化最经典的叙事结构："section trigger + stateful visualization"。

## 共享骨架

同 `../scrollytelling-network/`：sticky 视觉 + `.step[data-step]` + ScrollTrigger。

## 本资产特有

- 媒介引擎：**D3 v7**，图表是有状态的（stateful）：每个步骤对应一个图表状态，滚动即状态切换
- 叙事设计示例：01 Overview（先给全量分布，建立基线）→ 02 Focus（收窄注意力）——先整体后局部的信息纪律

## 依赖

d3@7 · gsap@3.13 + ScrollTrigger（CDN）

## 相关资产

`../scrollytelling-network/` · `../scrollytelling-map/` · `../scrollytelling-comparison/` · `../scrollytelling-pinned/`

## 来源

自研资产（原 `scroll-story-scrollytelling-data-fixed.html`），2026-09 归档入 `01-layout/`。
