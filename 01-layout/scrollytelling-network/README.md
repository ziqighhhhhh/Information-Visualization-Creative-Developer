# scrollytelling-network — 滚动叙事 · 网络图

可复用布局：左侧 sticky 网络图 + 右侧滚动步骤，步骤驱动图谱状态切换。单文件演示见 `index.html`（**需联网**加载依赖）。

## 身份

scrollytelling 框架的**网络图媒介**实例。 sticky 媒介是 Cytoscape.js 图谱，滚动步骤切换图布局/高亮。

## 共享骨架（五个 scrollytelling 资产通用）

- CSS `position:sticky` 固定视觉层，`.steps > .step[data-step]` 滚动文本列
- GSAP ScrollTrigger 负责滚动数学（进入/离开步骤 → 触发视觉状态）
- `.step.is-active` 控制当前步骤高亮；`ScrollTrigger.refresh()` 在内容/字体加载后调用
- 依赖 GSAP 3.13 + ScrollTrigger（CDN）

## 本资产特有

- 媒介引擎：**Cytoscape.js 3.34.3**（图谱布局与样式由引擎负责，滚动只切换其公开状态）
- 步骤语义示例：01 Ecosystem 总览 → 逐步聚焦子网络

## 依赖

cytoscape@3.34.3 · gsap@3.13 + ScrollTrigger（CDN）

## 相关资产

`../scrollytelling-chart/` · `../scrollytelling-map/` · `../scrollytelling-comparison/` · `../scrollytelling-pinned/`

## 来源

自研资产（原 `preview.html`，Scroll Story — Scrollytelling Network），2026-09 归档入 `01-layout/`。
